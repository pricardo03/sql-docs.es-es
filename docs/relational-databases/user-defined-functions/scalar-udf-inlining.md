---
title: Inserción de UDF escalares en bases de datos de Microsoft SQL | Microsoft Docs
description: Característica Inserción de UDF escalar para mejorar el rendimiento de las consultas que llaman a UDF escalares en SQL Server (2018 y versiones posteriores) y Azure SQL Database.
ms.custom: ''
ms.date: 02/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: s-r-k
ms.author: karam
monikerRange: = azuresqldb-current || >= sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: fc60a102a56aa5cb8c749db93290d20ec4b7f30e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126247"
---
# <a name="scalar-udf-inlining"></a>Inserción de UDF escalares

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

En este artículo se presenta Inserción de UDF escalar, una característica del conjunto de características de procesamiento de consultas inteligentes. Esta característica mejora el rendimiento de las consultas que llaman a UDF escalares en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQLv15](../../includes/sssqlv15-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

## <a name="t-sql-scalar-user-defined-functions"></a>Funciones escalares definidas por el usuario de T-SQL

Las funciones definidas por el usuario que se implementan en Transact-SQL y que devuelven un único valor de datos se conocen como Funciones escalares definidas por el usuario de T-SQL. Las UDF de T-SQL son una forma elegante de lograr la reutilización y modularidad del código en todas las consultas de SQL. Algunos cálculos (como las reglas de negocios complejas) son más fáciles de expresar en forma de UDF imperativa. Las UDF ayudan a crear una lógica compleja, sin necesidad de tener experiencia en escribir consultas de SQL complejas.

## <a name="performance-of-scalar-udfs"></a>Rendimiento de las UDF escalares

Las UDF escalares suelen tener un rendimiento deficiente debido a las razones siguientes.

- **Invocación iterativa:** las UDF se invocan de forma iterativa, una vez por cada tupla certificada. Esto supone costos adicionales de cambio de contexto repetido debido a la invocación de funciones. En concreto, las UDF que ejecutan consultas SQL en su definición se ven gravemente afectadas.
- **Falta de costos:** durante la optimización, solo se calcula el costo de los operadores relacionales, mientras que el de los operadores escalares no. Antes de la introducción de las UDF escalares, otros operadores escalares eran normalmente baratos y no requerían una estimación de los costos. Un pequeño costo de CPU agregado para una operación escalar era suficiente. Hay escenarios donde el costo real es significativo y, aun así, se sigue representando de forma insuficiente.
- **Ejecución interpretada:** las UDF se evalúan como un lote de instrucciones, y se ejecutan instrucción por instrucción. Se compila cada instrucción y el plan compilado se almacena en caché. Aunque esta estrategia de almacenamiento en caché ahorra algo de tiempo porque evita las recompilaciones, cada instrucción se ejecuta de forma aislada. No se realizan optimizaciones entre instrucciones.
- **Ejecución en serie:** SQL Server no admite el paralelismo entre consultas en las consultas que invocan las UDF. 

## <a name="automatic-inlining-of-scalar-udfs"></a>Inserción automática de UDF escalares

El objetivo de la característica Inserción de UDF escalar es mejorar el rendimiento de las consultas que llaman a UDF escalares de T-SQL, donde la ejecución de la UDF es el principal cuello de botella.

Con esta nueva característica, las UDF escalares se transforman automáticamente en expresiones o subconsultas escalares que se sustituyen en la consulta que realiza la llamada en lugar del operador de UDF. Después, estas expresiones y subconsultas se optimizan. Como resultado, el plan de consulta dejará de tener un operador de función definida por el usuario, pero sus efectos se tendrán en cuenta en el plan, como las vistas o las funciones con valores de tabla insertadas.

### <a name="example-1---single-statement-scalar-udf"></a>Ejemplo 1: UDF escalar con una instrucción

Considere la consulta siguiente.

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (L_EXTENDEDPRICE *(1 - L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE;
```

Esta consulta calcula la suma de los precios con descuento para los artículos de línea y presenta los resultados agrupados por fecha de envío y prioridad de envío. La expresión `L_EXTENDEDPRICE *(1 - L_DISCOUNT)` es la fórmula para el precio con descuento para un determinado artículo de línea. Estas fórmulas se pueden extraer en funciones para el beneficio de la modularidad y la reutilización.

```sql
CREATE FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2)) 
RETURNS DECIMAL (12,2) AS
BEGIN
  RETURN @price * (1 - @discount);
END

```

Ahora se puede modificar la consulta para invocar esta UDF.

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (dbo.discount_price(L_EXTENDEDPRICE, L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE
```

Debido a las razones descritas anteriormente, la consulta con la UDF tiene un rendimiento bajo. Ahora, con la inserción de UDF escalar, la expresión escalar en el cuerpo de la UDF se sustituye directamente en la consulta. Los resultados de ejecutar esta consulta se muestran en la tabla siguiente:

| Consulta: | Consulta sin UDF | Consulta con UDF (sin inserción) | Consulta con inserción de UDF escalar | 
| --- | --- | --- | --- |
| Tiempo de ejecución: | 1,6 segundos | 29 minutos 11 segundos | 1,6 segundos |

Estos números se basan en una base de datos de CCI de 10 GB (con el esquema de TPC-H), que se ejecuta en un equipo con procesador dual (12 núcleos), 96 GB de RAM, respaldado por SSD. Los números incluyen el tiempo de compilación y ejecución con un procedimiento pasivo de almacenamiento en caché y un grupo de búferes. Se ha usado la configuración predeterminada y no se han creado otros índices.

### <a name="example-2---multi-statement-scalar-udf"></a>Ejemplo 2: UDF escalar con varias instrucciones

Las UDF escalares que se implementan mediante varias instrucciones de T-SQL, como las asignaciones de variables y las bifurcaciones condicionales, también se pueden insertar. Observe la siguiente UDF escalar que, dada una clave de cliente, determina la categoría de servicio para ese cliente. Para llegar a la categoría, primero calcula el precio total de todos los pedidos realizados por el cliente mediante una consulta SQL. Después, usa una instrucción `IF-ELSE` lógica para decidir la categoría en función del precio total.

```sql
CREATE OR ALTER FUNCTION dbo.customer_category(@ckey INT) 
RETURNS CHAR(10) AS
BEGIN
  DECLARE @total_price DECIMAL(18,2);
  DECLARE @category CHAR(10);

  SELECT @total_price = SUM(O_TOTALPRICE) FROM ORDERS WHERE O_CUSTKEY = @ckey;

  IF @total_price < 500000
    SET @category = 'REGULAR';
  ELSE IF @total_price < 1000000
    SET @category = 'GOLD';
  ELSE 
    SET @category = 'PLATINUM';

  RETURN @category;
END

```

Ahora, considere la posibilidad de una consulta que invoca esta UDF.

```sql
SELECT C_NAME, dbo.customer_category(C_CUSTKEY) FROM CUSTOMER;
```

El plan de ejecución para esta consulta en SQL Server 2017 (nivel de compatibilidad 140 y versiones anteriores) es el siguiente:

![Plan de consulta sin inserción](./media/query-plan-without-udf-inlining.png)

Como se muestra en el plan, SQL Server adopta aquí una estrategia sencilla: para cada tupla de la tabla `CUSTOMER`, se invoca la UDF y se muestran los resultados. Esta estrategia es ingenua e ineficaz. Con la inserción, esas UDF se transforman en subconsultas escalares equivalentes, que se sustituyen en la consulta que realiza la llamada en lugar de la UDF.

Para la misma consulta, el plan con la UDF insertada tiene este aspecto.

![Plan de consulta con inserción](./media/query-plan-with-udf-inlining.png)

Como se ha mencionado antes, el plan de consulta ya no tiene un operador de función definida por el usuario, pero sus efectos se tienen en cuenta en el plan, como las vistas o las funciones con valores de tabla insertadas. Estas son algunas observaciones clave del plan anterior:

1. SQL Server ha inferido la combinación implícita entre `CUSTOMER` y `ORDERS`, y la ha convertido en explícita a través de un operador de combinación.
2. SQL Server también ha inferido la cláusula `GROUP BY O_CUSTKEY on ORDERS` implícita y ha usado IndexSpool y StreamAggregate para implementarla.
3. Ahora SQL Server usa el paralelismo de todos los operadores.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

Según la complejidad de la lógica de la UDF, es posible que el plan de consulta resultante también aumente de tamaño y complejidad. Como se puede ver, las operaciones dentro de la UDF ahora ya no son una caja negra y, por tanto, el optimizador de consultas es capaz de calcular los costos de esas operaciones y optimizarlas. Además, como la UDF ya no está en el plan, la invocación iterativa de UDF se sustituye por un plan que evita totalmente la sobrecarga de la llamada de función.

## <a name="inlineable-scalar-udfs-requirements"></a>Requisitos de las UDF escalares que se pueden insertar

Una UDF escalar de T-SQL se puede insertar si se cumplen todas las condiciones siguientes:

- La UDF se escribe con las construcciones siguientes:
    - `DECLARE`, `SET`: declaración de variables y asignaciones.
    - `SELECT`: consulta SQL con asignaciones de una o múltiples variables<sup>1</sup>.
    - `IF`/`ELSE`: bifurcación con niveles de anidamiento arbitrarios.
    - `RETURN`: una o varias instrucciones RETURN.
    - `UDF`: llamadas de función anidadas o recursivas<sup>2</sup>.
    - Otros: operaciones relacionales como `EXISTS`, `ISNULL`.
- La UDF no invoca ninguna función intrínseca que dependa de la hora (como `GETDATE()`) o que tenga efectos secundarios<sup>3</sup> (como `NEWSEQUENTIALID()`).
- La UDF usa la cláusula `EXECUTE AS CALLER` (el comportamiento predeterminado si no se especifica la cláusula `EXECUTE AS`).
- La UDF no hace referencia a variables de tabla ni a parámetros con valores de tabla.
- La consulta que invoca una UDF escalar no hace referencia a una llamada a la UDF escalar en su cláusula `GROUP BY`.
- La consulta que invoca una UDF escalar en su lista de selección con la cláusula `DISTINCT` no hace referencia a una llamada a la UDF escalar en su cláusula `ORDER BY`.
- La UDF no se compila de forma nativa (se admite la interoperabilidad).
- La UDF no se usa en una columna calculada ni en una definición de restricción CHECK.
- La UDF no hace referencia a tipos definidos por el usuario.
- No se agrega ninguna firma a la UDF.
- La UDF no es una función de partición.

<sup>1</sup> `SELECT` con acumulación o agregación de variables (por ejemplo, `SELECT @val += col1 FROM table1`) no se admite para la inserción.

<sup>2</sup> Las UDF recursivas solo se insertan hasta una profundidad concreta.

<sup>3</sup> Las funciones intrínsecas cuyos resultados dependen de la hora actual del sistema son dependientes de la hora. Una función intrínseca que puede actualizar algún estado global interno es un ejemplo de una función con efectos secundarios. Estas funciones devuelven resultados diferentes cada vez que se llaman, según el estado interno.

### <a name="checking-whether-or-not-a-udf-can-be-inlined"></a>Comprobación de si una UDF se puede insertar o no

Para todas las UDF escalares de T-SQL, la vista de catálogo [sys.sql_modules](../system-catalog-views/sys-sql-modules-transact-sql.md) incluye una propiedad denominada `is_inlineable`, que indica si una UDF se puede insertar o no. Un valor de 1 indica que se puede insertar y 0 indica lo contrario. Esta propiedad también tendrá un valor de 1 para todas las funciones con valores de tabla insertadas. Para todos los demás módulos, el valor será 0.

>[!NOTE]
>Si una UDF escalar se puede insertar, no implica que siempre se inserte. SQL Server decidirá (por cada consulta y UDF), si una UDF se inserta o no. Por ejemplo, si la definición de UDF se ejecuta en miles de líneas de código, es posible que SQL Server decida no insertarla. Otro ejemplo es una UDF en una cláusula `GROUP BY`: no se insertará. Esta decisión se toma cuando se compila la consulta que hace referencia a una UDF escalar.

### <a name="checking-whether-inlining-has-happened-or-not"></a>Comprobación de si la inserción se ha realizado o no

Si se cumplen todas las condiciones previas y SQL Server decide realizar la inserción, transforma la UDF en una expresión relacional. A partir del plan de consulta, es fácil averiguar si la inserción se ha realizado o no:

- El código XML del plan no tendrá un nodo `<UserDefinedFunction>` de XML para una UDF que se ha insertado correctamente. 
- Se emiten determinados XEvents.

## <a name="enabling-scalar-udf-inlining"></a>Habilitación de la inserción de UDF escalar

Puede hacer que las cargas de trabajo sean aptas automáticamente para la inserción de UDF escalar si habilita el nivel de compatibilidad 150 para la base de datos.? Puede establecerlo con Transact-SQL.?Por ejemplo:  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 150;
```

Aparte de esto, no hay que realizar ningún otro cambio en las UDF o las consultas para aprovechar esta característica.

## <a name="disabling-scalar-udf-inlining-without-changing-the-compatibility-level"></a>Deshabilitación de la inserción de UDF escalares sin cambiar el nivel de compatibilidad

La inserción de UDF escalares se puede deshabilitar en el ámbito de la base de datos, la instrucción o la UDF mientras se mantiene el nivel de compatibilidad de base de datos 150 o superior. Para deshabilitar la inserción de UDF escalares en el ámbito de la base de datos, ejecute la instrucción siguiente en el contexto de la base de datos aplicable: 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF;
```

Para volver a habilitar la inserción de UDF escalares para la base de datos, ejecute la instrucción siguiente en el contexto de la base de datos aplicable:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = ON;
```

Cuando es ON, esta opción aparece como habilitada en [`sys.database_scoped_configurations`](../system-catalog-views/sys-database-scoped-configurations-transact-sql.md). También puede deshabilitar la inserción de UDF escalares para una consulta específica mediante la designación de `DISABLE_TSQL_SCALAR_UDF_INLINING` como una sugerencia de consulta `USE HINT`. Por ejemplo:

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (dbo.discount_price(L_EXTENDEDPRICE, L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE
OPTION (USE HINT('DISABLE_TSQL_SCALAR_UDF_INLINING'));
```

Una sugerencia de consulta `USE HINT` tiene prioridad sobre una configuración de ámbito de base de datos o una opción de nivel de compatibilidad.

La inserción de UDF escalares también se puede deshabilitar para una UDF específica mediante la cláusula INLINE en la instrucción `CREATE FUNCTION` o `ALTER FUNCTION`.
Por ejemplo:

```sql
CREATE OR ALTER FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2))
RETURNS DECIMAL (12,2)
WITH INLINE = OFF
AS
BEGIN
    RETURN @price * (1 - @discount);
END
```

Una vez que se ejecuta la instrucción anterior, esta UDF nunca se insertará en ninguna consulta que la invoca. Para volver a habilitar la inserción para esta UDF, ejecute la instrucción siguiente:

```sql
CREATE OR ALTER FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2))
RETURNS DECIMAL (12,2)
WITH INLINE = ON
AS
BEGIN
    RETURN @price * (1 - @discount);
END
```

>[!NOTE]
>La cláusula `INLINE` no es obligatoria. Si no se especifica la cláusula `INLINE`, se establece automáticamente en `ON`/`OFF` en función de si la UDF es insertable. Si se especifica `INLINE=ON` pero se detecta que la UDF no es insertable, se producirá un error.

## <a name="important-notes"></a>Notas importantes

Como se describe en este artículo, la inserción de UDF escalar transforma una consulta con UDF escalares en una consulta con una subconsulta escalar equivalente. Debido a esta transformación, es posible que los usuarios observen algunas diferencias de comportamiento en los escenarios siguientes:

1. La inserción dará como resultado otro valor de hash de consulta para el mismo texto de consulta.
1. Es posible que, debido a la inserción, aparezcan algunas advertencias en las instrucciones dentro de la UDF (como la división por cero, etc.) que antes podrían estar ocultas.
1. Es posible que las sugerencias de combinación de nivel de consulta ya no sean válidas, ya que la inserción puede introducir nuevas combinaciones. En su lugar será necesario usar sugerencias de combinación locales.
1. Las vistas que hacen referencia a UDF escalares insertadas no se pueden indexar. Si tiene que crear un índice en esas vistas, deshabilite la inserción para las UDF a las que se hace referencia.
1. Puede haber algunas diferencias en el comportamiento del [enmascaramiento dinámico de datos](../security/dynamic-data-masking.md) con la inserción de UDF. En determinadas situaciones (en función de la lógica de la UDF), es posible que la inserción sea más conservadora que el enmascaramiento de las columnas de salida. En escenarios donde las columnas a las que se hace referencia en una UDF no son columnas de salida, no se enmascararán. 
1. Si una UDF hace referencia a funciones integradas como `SCOPE_IDENTITY()`, con la inserción se cambiará el valor devuelto por la función integrada. Este cambio de comportamiento se debe a que la inserción modifica el ámbito de las instrucciones dentro de la UDF.

## <a name="see-also"></a>Consulte también

[Centro de rendimiento para el motor de base de datos SQL Server y Azure SQL Database](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)

[Guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md)

[Referencia de operadores lógicos y físicos del plan de presentación](../../relational-databases/showplan-logical-and-physical-operators-reference.md)

[Combinaciones](../../relational-databases/performance/joins.md)

[Demostración del procesamiento de consultas adaptable](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)
