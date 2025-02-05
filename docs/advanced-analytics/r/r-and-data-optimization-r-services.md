---
title: Optimización del rendimiento para la optimización de datos
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a65afba9455fb475b760439e92ad8d4d38a70be8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715655"
---
# <a name="performance-for-r-services---data-optimization"></a>Rendimiento de R Services: optimización de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo es el tercero de una serie que describe la optimización del rendimiento de R Services en función de dos casos prácticos. En este artículo se describen las optimizaciones de rendimiento para scripts de R o Python que se ejecutan en SQL Server. También se describen los métodos que puede usar para actualizar el código de R, tanto para mejorar el rendimiento como para evitar problemas conocidos.

## <a name="choosing-a-compute-context"></a>Elección de un contexto de cálculo

En SQL Server 2016 y 2017, puede usar el contexto de proceso **local** o **SQL** al ejecutar un script de R o Python.

Cuando se usa el contexto de proceso **local** , el análisis se realiza en el equipo y no en el servidor. Por lo tanto, si está obteniendo datos de SQL Server usar en el código, se deben capturar los datos a través de la red. El impacto en el rendimiento en el que se incurre para esta transferencia de red depende del tamaño de los datos transferidos, la velocidad de la red y otras transferencias de red que se producen al mismo tiempo.

Cuando se usa el **contexto de cálculo de SQL Server**, el código se ejecuta en el servidor. Si está obteniendo datos de SQL Server, los datos deben ser locales en el servidor que ejecuta el análisis y, por lo tanto, no se introduce ninguna sobrecarga de la red. Si necesita importar datos de otros orígenes, considere la posibilidad de organizar los ETL de antemano.

Cuando se trabaja con grandes conjuntos de datos, se debe usar siempre el contexto de cálculo SQL.

## <a name="factors"></a>Factores

El lenguaje R tiene el concepto de *factores*, que son una variable especial para los datos de categorías. Los científicos de datos suelen usar variables de factor en su fórmula, porque el control de las variables de categorías como factores garantiza que los datos se procesan correctamente mediante las funciones de aprendizaje automático. Para obtener más información, [vea R para Dummies: Variables](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)de factor.

Por diseño, las variables de factor se pueden convertir de cadenas a enteros y viceversa para el almacenamiento o el procesamiento. La función `data.frame` de R controla todas las cadenas como variables de factor, a menos que el argumento *stringsAsFactors* se establezca en **false**. Esto significa que las cadenas se convierten automáticamente en un entero para su procesamiento y, a continuación, se asignan de nuevo a la cadena original.

Si los datos de origen de los factores se almacenan como un entero, el rendimiento puede verse afectado porque R convierte los enteros de factor en cadenas en tiempo de ejecución y, a continuación, realiza su propia conversión de cadena a entero interna.

Para evitar estas conversiones en tiempo de ejecución, considere la posibilidad de almacenar los valores como enteros en la tabla de SQL Server y el uso del argumento _colInfo_ para especificar los niveles de la columna que se usa como factor. La mayoría de los objetos de origen de datos de RevoScaleR toman el parámetro _colInfo_. Use este parámetro para asignar un nombre a las variables utilizadas por el origen de datos, especificar su tipo y definir los niveles de variables o las transformaciones en los valores de columna.

Por ejemplo, la siguiente llamada de función de R obtiene los enteros 1, 2 y 3 de una tabla, pero asigna los valores a un factor con los niveles "Apple", "Orange" y "banana".

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Cuando la columna de origen contiene cadenas, siempre es más eficaz especificar los niveles con anterioridad mediante el parámetro _colInfo_ . Por ejemplo, el siguiente código R trata las cadenas como factores a medida que se leen.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Si no hay ninguna diferencia semántica en la generación del modelo, el último enfoque puede dar lugar a un mejor rendimiento.

## <a name="data-transformations"></a>Transformaciones de datos

Los científicos de datos suelen emplear funciones de transformación escritas en R como parte del análisis. La función de transformación se aplica a cada fila recuperada de la tabla. En SQL Server, estas transformaciones se aplican a todas las filas recuperadas en un lote, lo que requiere comunicación entre el intérprete de R y el motor de análisis. Para realizar la transformación, se mueven los datos de SQL al motor de análisis y, después, al proceso del intérprete de R y viceversa.

Por esta razón, el uso de transformaciones como parte del código de R puede tener un efecto adverso significativo en el rendimiento del algoritmo, en función de la cantidad de datos implicados.

Es más eficaz tener todas las columnas necesarias en la tabla o vista antes de realizar el análisis y evitar las transformaciones durante el cálculo. Si no es posible agregar más columnas a las tablas existentes, considere la posibilidad de crear otra tabla o vista con las columnas transformadas y usar una consulta adecuada para recuperar los datos.

## <a name="batch-row-reads"></a>Lecturas de filas por lotes

Si usa un origen de datos de SQL Server`RxSqlServerData`() en el código, se recomienda que intente usar el parámetro _rowsPerRead_ para especificar el tamaño del lote. Este parámetro define el número de filas que se consultan y, a continuación, se envían al script externo para su procesamiento. En tiempo de ejecución, el algoritmo solo ve el número especificado de filas en cada lote.

La capacidad de controlar la cantidad de datos que se procesan a la vez puede ayudarle a resolver o evitar problemas. Por ejemplo, si el conjunto de datos de entrada es muy amplio (tiene muchas columnas) o si el conjunto de datos tiene algunas columnas de gran tamaño (por ejemplo, texto libre), puede reducir el tamaño del lote para evitar la paginación de los datos sin memoria.

De forma predeterminada, el valor de este parámetro se establece en 50000, para garantizar un rendimiento aceptable, incluso en equipos con poca memoria. Si el servidor tiene suficiente memoria disponible, el aumento de este valor a 500.000 o incluso un millón puede mejorar el rendimiento, especialmente en el caso de las tablas grandes.

Las ventajas del aumento del tamaño del lote se vuelven evidentes en un conjunto de datos grande y en una tarea que se puede ejecutar en varios procesos. Sin embargo, el aumento de este valor no siempre produce los mejores resultados. Se recomienda experimentar con los datos y el algoritmo para determinar el valor óptimo.

## <a name="parallel-processing"></a>Procesamiento paralelo

Para mejorar el rendimiento de las funciones analíticas de **RX** , puede aprovechar la capacidad de SQL Server para ejecutar tareas en paralelo mediante núcleos disponibles en el equipo servidor.

Hay dos maneras de lograr la paralelización con R en SQL Server:

-   **Usar \@Parallel.** Cuando se usa el procedimiento almacenado `sp_execute_external_script` para ejecutar un script de R, se establece el parámetro `@parallel` en `1`. Este es el mejor método si el script de R **no** usa las funciones de RevoScaleR, que tienen otros mecanismos para el procesamiento. Si el script usa funciones RevoScaleR (generalmente con el prefijo "RX"), el procesamiento en paralelo se realiza automáticamente y no es necesario establecer `@parallel` explícitamente en `1`.

    Si el script de R se puede ejecutar en paralelo, y si la consulta SQL se puede ejecutar en paralelo, el motor de base de datos crea varios procesos paralelos. El número máximo de procesos que se pueden crear es igual al valor **de grado máximo de paralelismo** (MAXDOP) de la instancia. A continuación, todos los procesos ejecutan el mismo script, pero reciben solo una parte de los datos.
    
    Por lo tanto, este método no es útil con los scripts que deben ver todos los datos, como al entrenar un modelo. Pero resulta útil al realizar tareas como la predicción por lotes en paralelo. Para obtener más información sobre el uso del `sp_execute_external_script`paralelismo con, vea la sección **sugerencias avanzadas: procesamiento en paralelo** del [uso de código de R en Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

-   **Use numTasks = 1.** Al usar funciones **RX** en un contexto de cálculo de SQL Server, establezca el valor del parámetro _numTasks_ en el número de procesos que desea crear. El número de procesos creados nunca puede ser superior a **MAXDOP**; sin embargo, el número real de procesos creados viene determinado por el motor de base de datos y puede ser menor que el solicitado.

    Si el script de R se puede ejecutar en paralelo, y si la consulta SQL se puede paralelizar, SQL Server crea varios procesos paralelos al ejecutar las funciones RX. El número real de procesos que se crean depende de diversos factores, como la regulación de recursos, el uso actual de los recursos, otras sesiones y el plan de ejecución de consultas para la consulta utilizada con el script de R.

## <a name="query-parallelization"></a>Paralelización de consultas

En Microsoft R, puede trabajar con orígenes de datos de SQL Server definiendo los datos como un objeto de origen de datos RxSqlServerData.

Crea un origen de datos basado en una tabla o vista completa:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

Crea un origen de datos basado en una consulta SQL:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> Si se especifica una tabla en el origen de datos en lugar de una consulta, R Services usa la heurística interna para determinar las columnas necesarias para la captura de la tabla; sin embargo, es poco probable que este método resulte en ejecución en paralelo.

Para asegurarse de que los datos se pueden analizar en paralelo, la consulta utilizada para recuperar los datos debe estar tramada de forma que el motor de base de datos pueda crear un plan de consulta paralelo. Si el código o el algoritmo usan grandes volúmenes de datos, asegúrese de que la consulta dada `RxSqlServerData` está optimizada para la ejecución en paralelo. Una consulta que no da como resultado un plan de ejecución en paralelo puede producir un único proceso para el cálculo.

Si necesita trabajar con grandes conjuntos de recursos, use Management Studio u otro analizador de consultas de SQL antes de ejecutar el código de R para analizar el plan de ejecución. A continuación, realice los pasos recomendados para mejorar el rendimiento de la consulta. Por ejemplo, un índice que falta en una tabla puede afectar al tiempo necesario para ejecutar una consulta. Para obtener más información, consulte [supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Otro error común que puede afectar al rendimiento es que una consulta recupera más columnas de las necesarias. Por ejemplo, si una fórmula se basa solo en tres columnas, pero la tabla de origen tiene 30 columnas, el traslado de los datos no es necesario.

 + Evite usar `SELECT *`.
 + Tómese un tiempo para revisar las columnas del conjunto de registros e identificar solo las necesarias para el análisis
 + Quitar de las consultas las columnas que contienen tipos de datos que no son compatibles con código de R, como GUID y ROWGUID
 + Comprobar los formatos de fecha y hora no admitidos
 + En lugar de cargar una tabla, cree una vista que seleccione determinados valores o convierta columnas para evitar errores de conversión.

## <a name="optimizing-the-machine-learning-algorithm"></a>Optimización del algoritmo de aprendizaje automático

En esta sección se proporcionan varias sugerencias y recursos específicos de RevoScaleR y otras opciones de Microsoft R.

> [!TIP]
> Un análisis general de la optimización de R está fuera del ámbito de este artículo. Sin embargo, si necesita que el código sea más rápido, se recomienda el artículo popular, [el Inferno de R](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Trata las construcciones de programación en R y los errores comunes en un lenguaje y detalle intensos, y proporciona muchos ejemplos específicos de técnicas de programación de R.

### <a name="optimizations-for-revoscaler"></a>Optimizaciones para RevoScaleR

Muchos algoritmos de RevoScaleR admiten parámetros para controlar cómo se genera el modelo entrenado. Aunque la precisión y la exactitud del modelo son importantes, el rendimiento del algoritmo puede ser igualmente importante. Para obtener el equilibrio adecuado entre la precisión y el tiempo de entrenamiento, puede modificar los parámetros para aumentar la velocidad del cálculo y, en muchos casos, mejorar el rendimiento sin reducir la precisión o la corrección.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree`admite el `maxDepth` parámetro, que controla la profundidad del árbol de decisión. Como `maxDepth` aumenta, el rendimiento puede reducirse, por lo que es importante analizar las ventajas de aumentar la profundidad frente a la inestabilidad del rendimiento.

    También puede controlar el equilibrio entre la complejidad temporal y la precisión de la predicción mediante el `maxNumBins`ajuste `maxDepth`de `maxComplete`parámetros como `maxSurrogate`,, y. Aumentar la profundidad por encima de 10 o 15 puede hacer que el cálculo sea muy costoso.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Intente usar el `cube` argumento si la primera variable dependiente de la fórmula es una variable de factor.
    
    Cuando `cube` se establece en `TRUE`, la regresión se realiza mediante un inverso con particiones, que podría ser más rápido y utilizar menos memoria que el cálculo de regresión estándar. Si la fórmula tiene un gran número de variables, la ganancia de rendimiento puede ser significativa.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Use el `cube` argumento si la primera variable dependiente es una variable de factor.
    
    Cuando `cube` se establece en `TRUE`, el algoritmo utiliza un inverso con particiones, que podría ser más rápido y utilizar menos memoria. Si la fórmula tiene un gran número de variables, la ganancia de rendimiento puede ser significativa.

Para obtener instrucciones adicionales sobre la optimización de RevoScaleR, consulte estos artículos:

+ Artículo de soporte: [Opciones de optimización del rendimiento para rxDForest y rxDTree](https://support.microsoft.com/kb/3104235)

+ Los métodos para controlar el modelo se ajustan a un modelo de árbol mejorado: [Calcular modelos mediante la potenciación del gradiente de estocástico](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Información general sobre cómo RevoScaleR mueve y procesa los datos: [Escribir algoritmos de fragmentación personalizados en ScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Modelo de programación para RevoScaleR: [Administración de subprocesos en RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Referencia de función para [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Referencia de función para [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Usar MicrosoftML

También se recomienda que examine el nuevo paquete **MicrosoftML** , que proporciona algoritmos de aprendizaje automático escalables que pueden usar los contextos de cálculo y las transformaciones proporcionadas por RevoScaleR.

+ [Introducción a MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Cómo elegir un algoritmo de MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Poner en funcionamiento una solución mediante Microsoft R Server

Si el escenario implica una predicción rápida con un modelo almacenado o la integración de machine learning en una aplicación, puede usar las características de [operacionalización](https://docs.microsoft.com/r-server/what-is-operationalization) de Microsoft R Server (anteriormente conocido como implementador).

+ Como **científico de datos**, use el [paquete mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) para compartir código r con otros equipos e integre R Analytics en aplicaciones Web, de escritorio, móviles y de panel: [Cómo publicar y administrar servicios Web de R en R Server](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Como **Administrador**, obtenga información sobre cómo administrar paquetes, supervisar nodos web y nodos de proceso, y controlar la seguridad en trabajos de R: [Interacción y uso de servicios web en R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Artículos de esta serie

[Optimización del rendimiento para R: introducción](sql-server-r-services-performance-tuning.md)

[Ajuste del rendimiento para la configuración de R-SQL Server](sql-server-configuration-r-services.md)

[Optimización del rendimiento de código R-R y optimización de datos](r-and-data-optimization-r-services.md)

[Optimización del rendimiento: resultados de los casos prácticos](performance-case-study-r-services.md)
