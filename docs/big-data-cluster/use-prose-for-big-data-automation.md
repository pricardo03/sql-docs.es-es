---
title: Generación de código para tareas de limpieza y transformación de datos
titleSuffix: Azure Data Studio
description: En este artículo se describe cómo usar el acelerador de código PROSE en Azure Data Studio para generar automáticamente código destinado a tareas comunes de limpieza y transformación de datos.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e21c172bf886695a3d424d25907a0c36e4b22f20
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67957685"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>Limpieza y transformación de datos mediante el acelerador de código PROSE

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El acelerador de código PROSE genera código Python legible para las tareas de limpieza y transformación de datos. El código generado se puede combinar con el código escrito a mano de una manera fluida mientras se trabaja en un cuaderno dentro de Azure Data Studio. En este artículo se proporciona información general sobre cómo se puede usar el acelerador de código.

 > [!NOTE]
 > Program Synthesis using Examples, también conocido como PROSE, es una tecnología de Microsoft que genera código legible para personas mediante IA. Para ello, analiza la intención del usuario, así como de los datos, genera varios programas candidatos y selecciona el mejor programa mediante algoritmos de clasificación. Para obtener más información sobre la tecnología PROSE, visite [la página principal de PROSE](https://microsoft.github.io/prose/).

El acelerador de código viene preinstalado con Azure Data Studio. Puede importarlo como cualquier otro paquete de Python en el cuaderno. Por convención, lo importamos como cx para abreviar.

```python
import prose.codeaccelerator as cx
```

En la versión actual, el acelerador de código puede generar código Python de forma inteligente para las tareas siguientes:

- Lectura de archivos de datos en un dataframe de Pandas o Pyspark
- Corrección de tipos de datos en un dataframe
- Búsqueda de expresiones regulares que representan patrones en una lista de cadenas

Para obtener información general sobre los métodos del acelerador de código, consulte la [documentación](https://aka.ms/prose-codeaccelerator-overview).

## <a name="reading-data-from-a-file-to-a-dataframe"></a>Lectura de datos de un archivo en un dataframe

A menudo, la lectura de archivos en un dataframe implica el examen del contenido del archivo y la determinación de los parámetros correctos para pasarlos a una biblioteca de carga de datos. En función de la complejidad del archivo, la identificación de los parámetros correctos puede requerir varias iteraciones.

El acelerador de código PROSE resuelve este problema mediante el análisis de la estructura del archivo de datos y la generación automática de código para cargar el archivo. En la mayoría de los casos, el código generado analiza los datos correctamente. En algunas ocasiones, es posible que deba ajustar el código para satisfacer sus necesidades.

Considere el ejemplo siguiente:

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

El bloque de código anterior imprime el siguiente código de Python para leer un archivo delimitado. Observe cómo PROSE calcula automáticamente el número de líneas que se van a omitir, los encabezados, los caracteres de citas, los delimitadores, etc.

 ```python
import pandas as pd

def read_file(file):
    names = ["lat",
             "lng",
             "desc",
             "zip",
             "title"]

    df = pd.read_csv(file,
        skiprows = 11,
        header = None,
        names = names,
        quotechar = "\"",
        delimiter = "|",
        index_col = False,
        dtype = str,
        na_values = [],
        keep_default_na = False,
        skipinitialspace = True)
    return df
 ```

El acelerador de código puede generar código para cargar archivos delimitados, JSON y de ancho fijo en un dataframe. Para leer archivos de ancho fijo, `ReadFwfBuilder` toma opcionalmente un archivo de esquema legible que puede analizar para obtener la posición de las columnas. Para obtener más información, consulte la [documentación](https://aka.ms/prose-codeaccelerator-docs).

## <a name="fixing-data-types-in-a-dataframe"></a>Corrección de tipos de datos en un dataframe

Es habitual tener un dataframe de Pandas o Pyspark con tipos de datos incorrectos. A menudo, esto sucede debido a la existencia de valores no conformes en una columna. Como resultado, los enteros se leen como valores float o cadenas, y las fechas se leen como cadenas. El esfuerzo necesario para corregir manualmente los tipos de datos es proporcional al número de columnas.

En estas situaciones, puede utilizar `DetectTypesBuilder`. Analiza los datos y, en lugar de corregir los tipos de datos en forma de "caja negra", genera código para corregirlos. El código sirve como punto de partida. Puede revisarlos, utilizarlos o modificarlos según sea necesario.

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

Para obtener más información, consulte la [documentación](https://aka.ms/prose-codeaccelerator-fixtypes).

## <a name="identifying-patterns-in-strings"></a>Identificación de patrones en cadenas

Otro escenario común es detectar patrones en una columna de cadena con el fin de limpiar o agrupar los valores. Por ejemplo, puede tener una columna de fecha con fechas en varios formatos distintos. Para normalizar los valores, quizá desee escribir instrucciones condicionales mediante expresiones regulares.


|   |Nombre                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Desconocido        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-abr-67      |
| 4 |Maya de Villiers          |19-mar-60      |

Dependiendo del volumen y la diversidad de los datos, la escritura de expresiones regulares para distintos patrones en la columna puede ser una tarea que consume mucho tiempo. `FindPatternsBuilder` es una eficaz herramienta de aceleración de código que resuelve el problema anterior con la generación de expresiones regulares para una lista de cadenas.

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

Estas son las expresiones regulares generadas por `FindPatternsBuilder` para los datos anteriores.

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

Además de generar expresiones regulares, `FindPatternsBuilder` también puede generar código para la agrupación en clústeres de los valores basados en regex generadas. También puede afirmar que todos los valores de una columna se ajustan a las expresiones regulares generadas. Para obtener más información y ver otros escenarios prácticos, consulte la [documentación](https://aka.ms/prose-codeaccelerator-findpatterns).
