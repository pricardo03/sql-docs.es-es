---
title: CAST y CONVERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CAST_TSQL
- CONVERT_TSQL
- CAST
- CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- automatic data type conversion
- varbinary data type
- CONVERT function
- data types [SQL Server], converting
- large value data types
- implicit data type conversions
- image data type, converting
- explicit data type conversions [SQL Server]
- binary [SQL Server], converting
- text data type, converting
- date and time [SQL Server], cast and convert
- truncating conversions
- converting data types [SQL Server], conversion functions
- time zones [SQL Server]
- roundtrip conversions
ms.assetid: a87d0850-c670-4720-9ad5-6f5a22343ea8
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: caba5466432356cf6997b26a0a3b8c732b3179ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040169"
---
# <a name="cast-and-convert-transact-sql"></a>CAST y CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Estas funciones convierten una expresión de un tipo de datos a otro.  

**Ejemplo:** Cambio del tipo de datos de entrada

**Cast**
```sql  
SELECT 9.5 AS Original,
       CAST(9.5 AS INT) AS [int],
       CAST(9.5 AS DECIMAL(6, 4)) AS [decimal];

```  
**Convertir**
```sql  
SELECT 9.5 AS Original,
       CONVERT(INT, 9.5) AS [int],
       CONVERT(DECIMAL(6, 4), 9.5) AS [decimal];
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|Original   |INT    |Decimal |  
|----|----|----|  
|9.5 |9 |9.5000 |  

**Vea los [ejemplos](#BKMK_examples)** que aparecen a continuación en este tema. 
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- CAST Syntax:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- CONVERT Syntax:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*expression*  
Cualquier [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida.
  
*data_type*  
El tipo de datos de destino. Esto engloba **xml**, **bigint** y **sql_variant**. No se pueden utilizar tipos de datos de alias.
  
*length*  
Un número entero opcional que especifica la longitud del tipo de datos de destino. El valor predeterminado es 30.
  
*style*  
Una expresión de tipo entero que especifica cómo traducirá la función CONVERT *expression*. Para un valor de estilo NULL, se devuelve NULL. *data_type* determina el intervalo. 
  
## <a name="return-types"></a>Tipos de valores devueltos
Devuelve *expression*, traducido a *data_type*.

## <a name="date-and-time-styles"></a>Estilos de fecha y hora  
Para una *expression* que tenga el tipo de datos de fecha u hora, *style* puede tener uno de los valores que se muestran en la siguiente tabla. Otros valores se procesan como 0. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los únicos estilos que se admiten al convertir de tipos de fecha y hora a **datetimeoffset** son 0 o 1. Todos los demás estilos de conversión devuelven el error 9809.
  
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el formato de fecha, en estilo árabe, con el algoritmo kuwaití.
  
|Sin el siglo (aa) (<sup>1</sup>)|Con el siglo (aaaa)|Estándar|Entrada/salida (<sup>3</sup>)|  
|---|---|--|---|
|-|**0** o **100** (<sup>1,</sup><sup>2</sup>)|Valor predeterminado para datetime y smalldatetime|mes dd aaaa hh:mia.m. (o p.m.)|  
|**1**|**101**|EE. UU.|  1 = mm/dd/aa<br /> 101 = mm/dd/aaaa|  
|**2**|**102**|ANSI|  2 = aa.mm.dd<br /> 102 = aaaa.mm.dd|  
|**3**|**103**|Británico/Francés|  3 = dd/mm/aa<br /> 103 = dd/mm/aaaa|  
|**4**|**104**|German|  4 = dd.mm.aa<br /> 104 = dd.mm.aaaa|  
|**5**|**105**|Italiano|  5 = dd-mm-aa<br /> 105 = dd-mm-aaaa|  
|**6**|**106** <sup>(1)</sup>|-|  6 = dd mes aa<br /> 106 = dd mes aaaa|  
|**7**|**107** <sup>(1)</sup>|-|  7 = Mes dd, aa<br /> 107 = Mes dd, aaaa|  
|**8**|**108**|-|hh:mi:ss|  
|-|**9** o **109** (<sup>1,</sup><sup>2</sup>)|Valor predeterminado + milisegundos|mes dd aaaa hh:mi:ss:mmma.m. (o p.m.)|  
|**10**|**110**|EE. UU.| 10 = mm-dd-aa<br /> 110 = mm-dd-aaaa|  
|**11**|**111**|JAPÓN| 11 = aa/mm/dd<br /> 111 = aaaa/mm/dd|  
|**12**|**112**|ISO| 12 = aammdd<br /> 112 = aaaammdd|  
|-|**13** o **113** (<sup>1,</sup><sup>2</sup>)|Europeo predeterminado + milisegundos|dd mes aaaa hh:mi:ss:mmm(24h)|  
|**14**|**114**|-|hh:mi:ss:mmm(24h)|  
|-|**20** o **120** (<sup>2</sup>)|ODBC canónico|aaaa-mm-dd hh:mi:ss(24h)|  
|-|**21** o **121** (<sup>2</sup>)|ODBC canónico (con milisegundos), valor predeterminado para time, date, datetime2 y datetimeoffset|aaaa-mm-dd hh:mi:ss.mmm(24h)|  
|-|**126** (<sup>4</sup>)|ISO8601|aaaa-mm-ddThh:mi:ss.mmm (sin espacios)<br /><br /> Nota: En el caso de un valor 0 en milisegundos (mmm), el valor de fracción decimal en milisegundos no se mostrará. Por ejemplo, el valor "2012-11-07T18:26:20.000" se muestra como "2012-11-07T18:26:20".|  
|-|**127**(<sup>6, 7</sup>)|ISO8601 con zona horaria Z.|aaaa-mm-ddThh:mi:ss.mmmZ (sin espacios)<br /><br /> Nota: En el caso de un valor 0 en milisegundos (mmm), el valor decimal en milisegundos no se mostrará. Por ejemplo, el valor "2012-11-07T18:26:20.000" se mostrará como "2012-11-07T18:26:20".|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|Hijri (<sup>5</sup>)|dd mes aaaa hh:mi:ss:mmma.m.<br /><br /> En este estilo, **mon** es una representación Unicode Hijri multitoken del nombre completo del mes. Este valor no se representa correctamente en una instalación estadounidense predeterminada de SSMS.|  
|-|**131** (<sup>2</sup>)|Hijri (<sup>5</sup>)|dd/mm/aaaa hh:mi:ss:mmma.m.|  
  
<sup>1</sup> Estos valores de estilo devuelven resultados no deterministas. Incluye todos los estilos (aa) (sin el siglo) y un subconjunto de estilos (aaaa) (con el siglo).
  
<sup>2</sup> Los valores predeterminados (**0** o **100**, **9** o **109**, **13** o **113**, **20** o **120** y **21** o **121**) siempre devuelven el siglo (aaaa).

<sup>3</sup> Entrada cuando se convierte en **datetime**; salida cuando se convierte en datos de caracteres.

<sup>4</sup> Diseñado para usarse con XML. Para convertir datos **datetime** o **smalldatetime** en datos de caracteres, consulte la tabla anterior para ver el formato de salida.

<sup>5</sup> Hijri es un sistema del calendario con varias variaciones. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el algoritmo kuwaití.

> [!IMPORTANT]
>  De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta los años de dos dígitos según el año límite 2049. Esto significa que SQL Server interpreta el año de dos dígitos 49 como 2049 y el año de dos dígitos 50 como 1950. Muchas aplicaciones cliente, como las que se basan en objetos de Automation, usan el año límite de 2030. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona la opción de configuración de año límite de dos dígitos para cambiar el año límite usado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto permite tratar las fechas de manera coherente. Se recomienda especificar años de cuatro dígitos.

<sup>6</sup> Solo se admite en la conversión de datos de caracteres a **datetime** o **smalldatetime**. Al convertir datos de caracteres que representan componentes de solo fecha o solo hora al tipo de datos **datetime** o **smalldatetime**, el componente de hora no especificado se establece en 00:00:00.000 y el componente de fecha no especificado se establece en 1900-01-01.
  
<sup>7</sup>Use el indicador opcional de zona horaria **Z** para facilitar la asignación de valores XML de tipo **datetime** que contienen información de zona horaria a valores de tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** que no tienen zona horaria. Z indica la zona horaria UTC-0. El desplazamiento HH:MM, en sentido + o -, indica otras zonas horarias. Por ejemplo: `2006-12-12T23:45:12-08:00`.
  
Al convertir datos **smalldatetime** en datos de caracteres, los estilos que incluyen segundos o milisegundos muestran ceros en dichas posiciones. Al convertir valores **datetime** o **smalldatetime**, use una longitud adecuada de valor de datos **char** o **varchar** para truncar las partes de la fecha que no quiera.
  
Al convertir datos de caracteres en datos **datetimeoffset** con un estilo que incluye una hora, se anexa un desplazamiento de zona horaria al resultado.
  
## <a name="float-and-real-styles"></a>Estilos float y real
En el caso de una *expression* **float** o **real**, *style* puede tener uno de los valores que se muestran en la siguiente tabla. Otros valores se procesan como 0.
  
|Valor|Salida|  
|---|---|
|**0** (valor predeterminado)|Un máximo de 6 dígitos. Utilícelo en notación científica cuando proceda.|  
|**1**|Siempre 8 dígitos. Utilícelo siempre en notación científica.|  
|**2**|Siempre 16 dígitos. Utilícelo siempre en notación científica.|  
|**3**|Siempre 17 dígitos. Se usa para la conversión sin pérdida de información. Con este estilo, se garantiza que cada valor de float o real distinto se va a convertir en una cadena de caracteres distinta.<br /><br /> **:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] y a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
|**126, 128, 129**|Se incluye por razones heredadas. Una versión futura podría dejar estos valores en desuso.|  
  
## <a name="money-and-smallmoney-styles"></a>Estilos money y smallmoney
En el caso de una *expression* **money** o **smallmoney**, *style* puede tener uno de los valores que se muestran en la siguiente tabla. Otros valores se procesan como 0.
  
|Valor|Salida|  
|---|---|
|**0** (valor predeterminado)|Sin separadores de millar cada tres dígitos a la izquierda del separador decimal y dos dígitos a la derecha del separador decimal<br /><br />Ejemplo: 4235,98.|  
|**1**|Separadores de millar cada tres dígitos a la izquierda del separador decimal y dos dígitos a la derecha del separador decimal<br /><br />Ejemplo: 3.510,92.|  
|**2**|Sin separadores de millar cada tres dígitos a la izquierda del separador decimal y cuatro dígitos a la derecha del separador decimal<br /><br />Ejemplo: 4235,9819.|  
|**126**|Equivalente al estilo 2 al convertir a char(n) o varchar(n)|  
  
## <a name="xml-styles"></a>Estilos xml
En el caso de una *expression* **xml**, *style* puede tener uno de los valores que se muestran en la siguiente tabla. Otros valores se procesan como 0.
  
|Valor|Salida|  
|---|---|
|**0** (valor predeterminado)|Usa el comportamiento de análisis predeterminado que descarta los espacios en blanco insignificantes y no permite un subconjunto DTD interno.<br /><br />**Nota:** Al convertir al tipo de datos **xml**, los espacios en blanco insignificantes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se controlan de forma distinta que en XML 1.0. Para más información, vea [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md).|  
|**1**|Conserva los espacios en blanco insignificantes. Esta configuración de estilo establece el control predeterminado de **xml:space** para emular el comportamiento de **xml:space="preserve"** .|  
|**2**|Habilita el procesamiento limitado de subconjuntos DTD internos.<br /><br /> Si está habilitado, el servidor puede usar la siguiente información proporcionada en un subconjunto DTD interno para realizar operaciones de análisis que no se validan.<br /><br />   - Se aplican los valores predeterminados de los atributos<br />   - Las referencias a entidades internas se resuelven y se amplían<br />   - Se comprueba la corrección sintáctica del modelo de contenido DTD<br /><br /> El analizador pasa por alto los subconjuntos DTD externos. Además, no evalúa la declaración XML para comprobar si el atributo **standalone** tiene el valor **yes** o **no**. En su lugar, analiza la instancia XML como documento independiente.|  
|**3**|Conserva los espacios en blanco insignificantes y habilita el procesamiento limitado de los subconjuntos DTD internos.|  
  
## <a name="binary-styles"></a>Estilos binarios
En el caso de una *expression* **binary(n)** , **char(n)** , **varbinary(n)** o **varchar(n)** , *style* puede tener uno de los valores que se muestran en la siguiente tabla. Los valores de estilo que no figuran en la tabla devolverán un error.
  
|Valor|Salida|  
|---|---|
|**0** (valor predeterminado)|Traduce caracteres ASCII a bytes binarios o bytes binarios a caracteres ASCII. Cada carácter o byte se convierte con una proporción 1:1.<br /><br /> En el caso de un *data_type* binario, los caracteres 0x se agregan a la izquierda del resultado.|  
|**1**, **2**|Para un *data_type* binario, la expresión debe ser de caracteres. *expression* debe tener un número **par** de dígitos hexadecimales (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, a, b, c, d, e, f). Si *style* se establece en 1, los dos primeros caracteres deben ser 0x. Si la expresión contiene un número impar de caracteres o si alguno de los caracteres no es válido, se producirá un error.<br /><br /> Si la longitud de la expresión convertida supera la longitud de *data_type*, el resultado se truncará a la derecha.<br /><br /> Los *data_type* de longitud fija que sean mayores que el resultado convertido tienen ceros agregados a la derecha del resultado.<br /><br /> Los *data_type* con el tipo carácter necesitan una expresión binaria. Cada carácter binario se convierte en dos caracteres hexadecimales. Si la longitud de la expresión convertida supera la longitud de *data_type*, se truncará a la derecha.<br /><br /> En el caso de que *data_type* sea un tipo de caracteres de tamaño fijo y de que la longitud del resultado convertido sea menor que la longitud de *data_type*, se agregan espacios a la derecha de la expresión convertida para mantener un número par de dígitos hexadecimales.<br /><br /> Los caracteres 0x se agregarán a la izquierda del resultado convertido para *style* 1.|  
  
## <a name="implicit-conversions"></a>Conversiones implícitas
Las conversiones implícitas no requieren la especificación de la función CAST ni de la función CONVERT. Las conversiones explícitas requieren la especificación de la función CAST o de la función CONVERT. En la siguiente ilustración se muestran todas las conversiones de tipos de datos explícitas e implícitas permitidas para los tipos de datos proporcionados por el sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Algunas de ellas son **bigint**, **sql_variant** y **xml**. No existe una conversión implícita en la asignación del tipo de datos **sql_variant**, pero sí hay una conversión implícita en **sql_variant**.
  
> [!TIP]  
>  En el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=35834) está disponible este gráfico como archivo PDF para su descarga.  
  
![Tabla de conversión de tipos de datos](../../t-sql/data-types/media/lrdatahd.png "Tabla de conversión de tipos de datos")
  
Al convertir entre **datetimeoffset** y los tipos de caracteres **char**, **nchar**, **nvarchar** y **varchar**, la parte del ajuste de zona horaria convertida siempre debe tener dígitos dobles para HH y MM. Por ejemplo: -08:00.
  
> [!NOTE]  
>  
>  Puesto que los datos Unicode siempre usan un número par de bytes, preste atención al convertir datos **binary** o **varbinary** en o desde tipos de datos compatibles con Unicode. Por ejemplo, la siguiente conversión no devuelve el valor hexadecimal 41. Devuelve un valor hexadecimal de 4100: `SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)`.  
  
## <a name="large-value-data-types"></a>Tipos de datos de valor grande
Los tipos de datos de valor grande tienen el mismo comportamiento de conversión implícita y explícita que sus equivalentes más pequeños, en concreto los tipos de datos **nvarchar**, **varbinary** y **varchar**. Aun así, tenga en cuenta las directrices siguientes:
-   La conversión de datos **image** a datos **varbinary(max)** y viceversa funciona como una conversión implícita, al igual que las conversiones entre **text** y **varchar(max)** y entre **ntext** y **nvarchar(max)** .  
-   La conversión de tipos de datos de valor grande, como **varchar(max)** , a un tipo de datos equivalente más pequeño, como **varchar**, es una conversión implícita, aunque se produce un truncamiento si el tamaño del valor grande supera la longitud especificada del tipo de datos más pequeño.  
-   La conversión de **nvarchar**, **varbinary** o **varchar** a sus tipos de datos correspondientes de valor grande tiene lugar de forma implícita.  
-   La conversión del tipo de datos **sql_variant** en los tipos de datos de valor grande es una conversión explícita.  
-   Los tipos de datos de valor grande no se pueden convertir en el tipo de datos **sql_variant**.  
  
Para más información sobre la conversión del tipo de datos **xml**, vea [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="xml-data-type"></a>tipo de datos xml
Cuando se convierte de forma explícita o implícita el tipo de datos **xml** en un tipo de datos de cadena o binario, el contenido del tipo de datos **xml** se serializa en función de un conjunto de reglas definido. Para más información sobre estas reglas, vea [Definir la serialización de datos XML](../../relational-databases/xml/define-the-serialization-of-xml-data.md). Para más información sobre la conversión de otros tipos de datos al tipo de datos **xml**, vea [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="text-and-image-data-types"></a>Tipos de datos text e image
Los tipos de datos **text** e **image** no admiten la conversión automática de tipos de datos. Puede convertir explícitamente datos **text** en datos de caracteres y datos **image** en **binary** o **varbinary**, pero la longitud máxima es de 8000 bytes. Si intenta una conversión incorrecta (por ejemplo, intentando convertir una expresión de caracteres que incluye letras) a un tipo **int**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devolverá un mensaje de error.
  
## <a name="output-collation"></a>Intercalación de salida  
Si las funciones CAST o CONVERT generan una cadena de caracteres y reciben una entrada de una cadena de caracteres, la salida tiene la misma intercalación y la misma etiqueta de intercalación que la entrada. Si la entrada no es una cadena de caracteres, la salida tiene la intercalación predeterminada de la base de datos y una etiqueta de intercalación coaccionable-predeterminada. Para más información, vea [Prioridad de intercalación &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md).
  
Para asignar otra intercalación a la salida, aplique la cláusula COLLATE a la expresión de resultado de las funciones CAST o CONVERT. Por ejemplo:
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>Truncar y redondear resultados
Al convertir expresiones binarias o de caracteres (**binary**, **char**, **nchar**, **nvarchar**, **varbinary** o **varchar**) en una expresión de otro tipo de datos, la operación de conversión podría truncar los datos de salida, mostrar solo parcialmente los datos de salida o devolver un error. Estos casos se producen si el resultado es demasiado corto para mostrarse. Las conversiones a **binary**, **char**, **nchar**, **nvarchar**, **varbinary** o **varchar** se truncan, excepto aquellas que se muestran en la siguiente tabla.
  
|De tipo de datos|En tipo de datos|Resultado|  
|---|---|---|
|**int**, **smallint** o **tinyint**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**money**, **smallmoney**, **numeric**, **decimal**, **float** o **real**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\* = Resultado demasiado corto para ser mostrado<br /><br />E = Error devuelto porque el resultado es demasiado corto para ser mostrado.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] garantiza que solo las conversiones circulares (dicho de otra manera, las conversiones que convierten un tipo de datos en otro y después vuelven a convertirlo en el tipo de datos original) devuelvan los mismos valores en versiones diferentes. En el siguiente ejemplo se muestra una conversión circular:
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!NOTE]  
>  No cree valores **binary**. Después, conviértalos a un tipo de datos de la categoría de datos numéricos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no garantiza que el resultado de una conversión de tipos de datos **decimal** o **numeric** a **binary** sea idéntica en las distintas versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
En el siguiente ejemplo se muestra una expresión resultante demasiado corta para ser mostrada.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, SUBSTRING(p.Title, 1, 25) AS Title,
    CAST(e.SickLeaveHours AS char(1)) AS [Sick Leave]  
FROM HumanResources.Employee e JOIN Person.Person p 
    ON e.BusinessEntityID = p.BusinessEntityID  
WHERE NOT e.BusinessEntityID >5;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```   
FirstName   LastName      Title   Sick Leave
---------   ------------- ------- --------`
Ken         Sanchez       NULL   *
Terri       Duffy         NULL   *
Roberto     Tamburello    NULL   *
Rob         Walters       NULL   *
Gail        Erickson      Ms.    *
(5 row(s) affected)  
```
  
Al convertir tipos de datos que difieren en los decimales, SQL Server devolverá a veces un valor de resultado truncado y otras veces devolverá un valor redondeado. En esta tabla se muestra el comportamiento.
  
|De|A|Comportamiento|  
|---|---|---|
|**numeric**|**numeric**|Redondear|  
|**numeric**|**int**|Truncamiento|  
|**numeric**|**money**|Redondear|  
|**money**|**int**|Redondear|  
|**money**|**numeric**|Redondear|  
|**float**|**int**|Truncamiento|  
|**float**|**numeric**|Redondear<br /><br /> La conversión de los valores **float** que usan la notación científica a **decimal** o **numeric** se restringe únicamente a los valores con una precisión de 17 dígitos. Cualquier valor con una precisión mayor de 17 se redondea a cero.|  
|**float**|**datetime**|Redondear|  
|**datetime**|**int**|Redondear|  
  
Por ejemplo, los valores 10,6496 y-10,6496 se pueden truncar o redondear durante la conversión a los tipos **int** o **numeric**:
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
Los resultados de la consulta se muestran en la siguiente tabla:
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
Al convertir tipos de datos donde el tipo de datos de destino tiene menos decimales que el tipo de datos de origen, el valor se redondea. Por ejemplo, esta conversión devuelve `$10.3497`:
  
`SELECT CAST(10.3496847 AS money);`
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un mensaje de error al convertir datos **char**, **nchar**, **nvarchar** o **varchar** no numéricos en datos **decimal**, **float**, **int** o **numeric**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también devuelve un error cuando se convierte una cadena vacía (" ") en los tipos de datos **numeric** o **decimal**.
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>Determinadas conversiones de fecha y hora son no deterministas
En la siguiente tabla se muestran los estilos para los que la conversión de cadena a fecha y hora es no determinista.
  
|||  
|-|-|  
|Todos los estilos por debajo de 100<sup>1</sup>|106|  
|107|109|  
|113|130|  
  
<sup>1</sup> Con la excepción de los estilos 20 y 21

Para obtener más información, vea [Conversión no determinista de las cadenas de fecha literales en valores DATE](../data-types/nondeterministic-convert-date-literals.md).

## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)
A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], si se usan intercalaciones de caracteres complementarios (SC), lasa operaciones CAST de **nchar** o **nvarchar** a un tipo **nchar** o **nvarchar** de menor longitud no se truncarán dentro de un par suplente, sino que lo hará antes del carácter suplementario. Por ejemplo, el fragmento de código siguiente deja `@x` con solo `'ab'`. No hay espacio suficiente para albergar el carácter suplementario.
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
Al usar intercalaciones de SC, el comportamiento de `CONVERT` es análogo al de `CAST`.
  
## <a name="compatibility-support"></a>Soporte de compatibilidad
En versiones anteriores a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el estilo predeterminado de las operaciones CAST y CONVERT en tipos de datos **time** y **datetime2** es 121, a menos que se use otro tipo en una expresión de columna calculada. Para las columnas calculadas, el estilo predeterminado es 0. Este comportamiento afecta a las columnas calculadas cuando se crean, cuando se utilizan en las consultas que implican parametrización automática o cuando se usan en definiciones de restricciones.
  
En el nivel de compatibilidad 110 y posteriores, las operaciones CAST y CONVERT en los tipos de datos **time** y **datetime2** siempre tienen el estilo predeterminado 121. Si una consulta se basa en el comportamiento anterior, use un nivel de compatibilidad menor de 110, o especifique explícitamente el estilo 0 en la consulta correspondiente.
  
Actualizar la base de datos al nivel de compatibilidad 110 y posteriores no cambiará los datos de usuario que se hayan almacenado en disco. Debe corregir manualmente estos datos según convenga. Por ejemplo, si usara SELECT INTO para crear una tabla de un origen que contuviera una expresión de columna calculada como la descrita anteriormente, se almacenarían los datos (si se usa el estilo 0) en lugar de la propia definición de columna calculada. Debe actualizar manualmente estos datos para que coincidan con el estilo 121.
  
## <a name="BKMK_examples"></a> Ejemplos  
  
### <a name="a-using-both-cast-and-convert"></a>A. Utilizar CAST y CONVERT  
En estos ejemplos se recupera el nombre de aquellos productos que tienen un `3` como primer dígito del precio y se convierte sus valores `ListPrice` en `int`.
  
```sql
-- Use CAST  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CAST(ListPrice AS int) LIKE '3%';  
GO  
  
-- Use CONVERT.  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
GO  
```  
  
### <a name="b-using-cast-with-arithmetic-operators"></a>B. Utilizar CAST con operadores aritméticos  
En este ejemplo se calcula una única columna (`Computed`) mediante la división de las ventas anuales hasta la fecha (`SalesYTD`) entre el porcentaje de la comisión (`CommissionPCT`). Este valor se redondea al número entero más cercano y luego se convierte (CAST) en un tipo de datos `int`.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT CAST(ROUND(SalesYTD/CommissionPCT, 0) AS int) AS Computed  
FROM Sales.SalesPerson   
WHERE CommissionPCT != 0;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```  
Computed
------
379753754
346698349
257144242
176493899
281101272
0  
301872549
212623750
298948202
250784119
239246890
101664220
124511336
97688107
(14 row(s) affected)  
```  
  
### <a name="c-using-cast-to-concatenate"></a>C. Utilizar CAST para concatenar  
En este ejemplo se concatenan expresiones que no son de caracteres usando CAST. Usa la base de datos AdventureWorksDW.
  
```sql
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice  
FROM dbo.DimProduct  
WHERE ListPrice BETWEEN 350.00 AND 400.00;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09  
```  
  
### <a name="d-using-cast-to-produce-more-readable-text"></a>D. Utilizar CAST para obtener texto más legible  
En este siguiente ejemplo se usa CAST en la lista SELECT para convertir la columna `Name` en una columna de tipo **char(10)** . Usa la base de datos AdventureWorksDW.
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        ListPrice
----------  ---------
Long-Sleev  31.2437
Long-Sleev  32.4935
Long-Sleev  49.99  
```  
  
### <a name="e-using-cast-with-the-like-clause"></a>E. Utilizar CAST con la cláusula LIKE  
En este ejemplo se convierten los valores `SalesYTD` de la columna `money` al tipo de datos `int` y, después, al tipo de datos `char(20)`, de modo que la cláusula `LIKE` pueda usarlo.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, s.SalesYTD, s.BusinessEntityID  
FROM Person.Person AS p   
JOIN Sales.SalesPerson AS s   
    ON p.BusinessEntityID = s.BusinessEntityID  
WHERE CAST(CAST(s.SalesYTD AS int) AS char(20)) LIKE '2%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
FirstName        LastName            SalesYTD         BusinessEntityID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289
(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>F. Utilizar CONVERT o CAST con XML con tipo  
En estos ejemplos se muestra el uso de CONVERT para convertir datos a XML con tipo mediante [Tipo de datos XML y columnas &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md).
  
En este ejemplo se convierte una cadena con espacios en blanco, texto y marcado en XML con tipo y se quitan todos los espacios en blanco insignificantes (espacios en blanco de límite entre los nodos):
  
```sql
SELECT CONVERT(XML, '<root><child/></root>')  
```  
  
En este ejemplo se convierte una cadena similar con espacios en blanco, texto y marcado en XML con tipo y se conservan los espacios en blanco insignificantes (espacios en blanco de límite entre los nodos):
  
```sql
SELECT CONVERT(XML, '<root>          <child/>         </root>', 1)  
```  
  
En este ejemplo se convierte una cadena con espacios en blanco, texto y marcado en XML con tipo:
  
```sql
SELECT CAST('<Name><FName>Carol</FName><LName>Elliot</LName></Name>'  AS XML)  
```  
  
Vea [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md) para ver más ejemplos.
  
### <a name="g-using-cast-and-convert-with-datetime-data"></a>G. Utilizar CAST y CONVERT con datos de fecha y hora  
A partir de los valores GETDATE(), en este ejemplo se muestran la fecha y la hora actuales, se usa `CAST` para cambiarlas a un tipo de datos de caracteres y, después, se usa `CONVERT` para mostrar la fecha y la hora en el formato `ISO 8601`.
  
```sql
SELECT   
   GETDATE() AS UnconvertedDateTime,  
   CAST(GETDATE() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), GETDATE(), 126) AS UsingConvertTo_ISO8601  ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast              UsingConvertTo_ISO8601
----------------------- ---------------------- ------------------------------
2006-04-18 09:58:04.570 Apr 18 2006  9:58AM    2006-04-18T09:58:04.570
(1 row(s) affected)  
```
  
Este ejemplo es lo opuesto, aproximadamente, al ejemplo anterior. En este ejemplo se muestra la fecha y la hora como datos de caracteres, se usa `CAST` para cambiar los datos de caracteres al tipo de datos `datetime` y, luego, se usa `CONVERT` para cambiar los datos de caracteres al tipo de datos `datetime`.
  
```sql
SELECT   
   '2006-04-25T15:50:59.997' AS UnconvertedText,  
   CAST('2006-04-25T15:50:59.997' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2006-04-25T15:50:59.997', 126) AS UsingConvertFrom_ISO8601 ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2006-04-25T15:50:59.997 2006-04-25 15:50:59.997 2006-04-25 15:50:59.997
(1 row(s) affected)  
```
  
### <a name="h-using-convert-with-binary-and-character-data"></a>H. Usar CONVERT con datos binarios y de caracteres  
En estos ejemplos se muestran los resultados de la conversión de datos binarios y de caracteres usando estilos diferentes.
  
```sql
--Convert the binary value 0x4E616d65 to a character value.  
SELECT CONVERT(char(8), 0x4E616d65, 0) AS [Style 0, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, binary to character
----------------------------
Name  
(1 row(s) affected)  
```
 
En este ejemplo se muestra que Style 1 puede forzar el truncamiento del resultado. Los caracteres 0x del conjunto de resultados fuerzan el truncamiento.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 1) AS [Style 1, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, binary to character
------------------------------
0x4E616D
(1 row(s) affected)  
```  
 
En este ejemplo se muestra que Style 2 no trunca el resultado, ya que este no incluye los caracteres 0x.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 2) AS [Style 2, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, binary to character
------------------------------
4E616D65
(1 row(s) affected)  
```
  
Convierta el valor del carácter 'Name' en un valor binario.  
```sql
SELECT CONVERT(binary(8), 'Name', 0) AS [Style 0, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, character to binary
----------------------------
0x4E616D6500000000
(1 row(s) affected)  
```
  
```sql
SELECT CONVERT(binary(4), '0x4E616D65', 1) AS [Style 1, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, character to binary
---------------------------- 
0x4E616D65
(1 row(s) affected)  
```  

```sql
SELECT CONVERT(binary(4), '4E616D65', 2) AS [Style 2, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, character to binary  
----------------------------------  
0x4E616D65
(1 row(s) affected)  
```  
  
### <a name="i-converting-date-and-time-data-types"></a>I. Convierte tipos de datos de fecha y hora  
En este ejemplo se muestra la conversión de los tipos de datos date, time y datetime.
  
```sql
DECLARE @d1 date, @t1 time, @dt1 datetime;  
SET @d1 = GETDATE();  
SET @t1 = GETDATE();  
SET @dt1 = GETDATE();  
SET @d1 = GETDATE();  
-- When converting date to datetime the minutes portion becomes zero.  
SELECT @d1 AS [date], CAST (@d1 AS datetime) AS [date as datetime];  
-- When converting time to datetime the date portion becomes zero   
-- which converts to January 1, 1900.  
SELECT @t1 AS [time], CAST (@t1 AS datetime) AS [time as datetime];  
-- When converting datetime to date or time non-applicable portion is dropped.  
SELECT @dt1 AS [datetime], CAST (@dt1 AS date) AS [datetime as date], 
   CAST (@dt1 AS time) AS [datetime as time];  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-using-cast-and-convert"></a>J. Usar CAST y CONVERT  
En este ejemplo se recupera el nombre de aquellos productos que tienen un `3` como primer dígito del precio y se convierte su `ListPrice` en **int**. Usa la base de datos AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
En este ejemplo se muestra la misma consulta, pero usando CONVERT en vez de CAST. Usa la base de datos AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="k-using-cast-with-arithmetic-operators"></a>K. Utilizar CAST con operadores aritméticos  
En este ejemplo se calcula un único valor de columna dividiendo el precio por unidad de producto (`UnitPrice`) entre el porcentaje de descuento (`UnitPriceDiscountPct`). Este resultado se redondea al número entero más cercano y, por último, se convierte al tipo de datos `int`. En este ejemplo se usa la base de datos AdventureWorksDW.
  
```sql
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,  
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice  
FROM dbo.FactResellerSales  
WHERE SalesOrderNumber = 'SO47355'   
      AND UnitPriceDiscountPct > .02;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1  
```  
  
### <a name="l-using-cast-with-the-like-clause"></a>L. Utilizar CAST con la cláusula LIKE  
En este ejemplo se convierte `ListPrice` de la columna **money** a un tipo **int** y, luego, a un tipo **char(20)** , de modo que la cláusula LIKE pueda usarla. En este ejemplo se usa la base de datos AdventureWorksDW.  
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="m-using-cast-and-convert-with-datetime-data"></a>M. Utilizar CAST y CONVERT con datos de fecha y hora  
En este ejemplo se muestra la fecha y la hora actuales, se usa CAST para cambiarlas a un tipo de datos de caracteres y, por último, se usa CONVERT para mostrar la fecha y la hora en el formato ISO 8601. En este ejemplo se usa la base de datos AdventureWorksDW.
  
```sql
SELECT TOP(1)  
   SYSDATETIME() AS UnconvertedDateTime,  
   CAST(SYSDATETIME() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), SYSDATETIME(), 126) AS UsingConvertTo_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast                     UsingConvertTo_ISO8601  
---------------------   ---------------------------   ---------------------------  
07/20/2010 1:44:31 PM   2010-07-20 13:44:31.5879025   2010-07-20T13:44:31.5879025  
```  
  
Este ejemplo es lo opuesto, aproximadamente, al ejemplo anterior. En este ejemplo se muestra la fecha y la hora como datos de caracteres, se usa CAST para cambiar los datos de caracteres al tipo de datos **datetime** y, luego, se usa CONVERT para cambiar los datos de caracteres al tipo de datos **datetime**. En este ejemplo se usa la base de datos AdventureWorksDW.
  
```sql
SELECT TOP(1)   
   '2010-07-25T13:50:38.544' AS UnconvertedText,  
CAST('2010-07-25T13:50:38.544' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2010-07-25T13:50:38.544', 126) AS UsingConvertFrom_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2010-07-25T13:50:38.544 07/25/2010 1:50:38 PM   07/25/2010 1:50:38 PM  
```  
  
## <a name="see-also"></a>Vea también
 [Conversiones de tipos de datos &#40;motor de base de datos&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
 [FORMAT &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
 [Escribir instrucciones Transact-SQL internacionales](../../relational-databases/collations/write-international-transact-sql-statements.md)
  
