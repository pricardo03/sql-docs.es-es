---
title: Función SQLStatistics | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef0f25660a0faa0747752a8ca15c207c1e939669
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039550"
---
# <a name="sqlstatistics-function"></a>Función SQLStatistics
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLStatistics** recupera una lista de las estadísticas sobre una sola tabla y los índices asociados con la tabla. El controlador devuelve la información como un conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *CatalogName*  
 [Entrada] Nombre del catálogo. Si un controlador es compatible con los catálogos para algunas tablas pero no para otros factores, como cuando el controlador recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tengan los catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente y su caso es significativo. Para obtener más información, consulte [argumentos en funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nombre del esquema. Si un controlador es compatible con los esquemas para algunas tablas pero no para otros factores, como cuando el controlador recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tiene esquemas. *SchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *SchemaName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Nombre de tabla. Este argumento no puede ser un puntero nulo. *SchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *TableName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
 *Único*  
 [Entrada] Tipo de índice: SQL_INDEX_UNIQUE o SQL_INDEX_ALL.  
  
 *Reserved*  
 [Entrada] Indica la importancia de las columnas de la CARDINALIDAD y las páginas del conjunto de resultados. Las opciones siguientes afectan a la devolución de la CARDINALIDAD y las páginas solo las columnas; incluso si no se devuelven las páginas y CARDINALIDAD, se devuelve información de índice.  
  
 SQL_ENSURE solicita que el controlador incondicionalmente recuperar las estadísticas. (Los controladores que solo cumplen el estándar Open Group y no admiten extensiones de ODBC no será capaz de admitir SQL_ENSURE.)  
  
 SQL_QUICK solicita que el controlador de recuperar la CARDINALIDAD y las páginas solo si están disponibles desde el servidor. En este caso, el controlador no garantiza que los valores sean actuales. (Las aplicaciones que se escriben en el estándar Open Group siempre obtendrá el comportamiento SQL_QUICK de ODBC *3.x*-controladores compatibles.)  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLStatistics** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLStatistics** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** hubiera llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*, y, a continuación, se llamó a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero nulo|El *TableName* argumento era un puntero nulo.<br /><br /> El atributo de instrucción SQL_ATTR_METADATA_ID estuviera establecido en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y la SQL_CATALOG_NAME *InfoType* devuelve que los nombres de catálogo es compatibles.<br /><br /> (DM) se estableció el atributo de instrucción SQL_ATTR_METADATA_ID en SQL_TRUE y el *SchemaName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLStatistics** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de uno de los argumentos de longitud de nombre era menor que 0 pero no es igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud del nombre supera el valor de longitud máxima para el nombre correspondiente.|  
|HY100|Tipo de opción de unicidad fuera del intervalo|(DM) no es válido *Unique* se especificó un valor.|  
|HY101|Tipo de opción de precisión fuera del intervalo|(DM) no es válido *reservado* se especificó un valor.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo, y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema y el controlador o el origen de datos no admite esquemas.<br /><br /> La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y se ha establecido el atributo de instrucción SQL_ATTR_CURSOR_TYPE a un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes del origen de datos devuelve el conjunto de resultados solicitada. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLStatistics** devuelve información acerca de una sola tabla como un conjunto de resultados estándar, ordenado por NON_UNIQUE, TYPE, INDEX_QUALIFIER, INDEX_NAME y ORDINAL_POSITION. El conjunto de resultados combina información de estadísticas (en las columnas de CARDINALIDAD y las páginas del conjunto de resultados) para la tabla con información acerca de cada índice. Para obtener información acerca de cómo se podría utilizar esta información, consulte [usa de datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar las longitudes de las columnas TABLE_CAT, según TABLE_SCHEM, TABLE_NAME y COLUMN_NAME reales, una aplicación puede llamar a **SQLGetInfo** con el SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, y las opciones de SQL_MAX_COLUMN_NAME_LEN.  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Las columnas siguientes se han cambiado para ODBC *3.x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque el enlace de aplicaciones por número de columna.  
  
|Columna de ODBC 2.0|ODBC *3.x* columna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. El controlador se pueden definir columnas adicionales más allá de 13 (FILTER_CONDITION) de la columna. Una aplicación debe tener acceso a columnas específicas del controlador mediante la cuenta atrás desde el final del conjunto en lugar de especificar una posición ordinal explícita de resultados. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nombre de columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nombre del catálogo de la tabla a la que se aplica la estadística o índice; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con los catálogos para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tengan los catálogos.|  
|SEGÚN TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre del esquema de la tabla a la que se aplica la estadística o índice; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con los esquemas para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tiene esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar no es NULL|Nombre de la tabla a la que se aplica la estadística o índice.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|Indica si el índice no permite valores duplicados:<br /><br /> SQL_TRUE si los valores de índice pueden ser no únicos.<br /><br /> SQL_FALSE si los valores de índice deben ser únicos.<br /><br /> Se devuelve NULL si el tipo es SQL_TABLE_STAT.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|El identificador que se utiliza para calificar el índice nombre si lo hace un **DROP INDEX**; Se devuelve NULL si el calificador de un índice no es compatible con el origen de datos o si el tipo es SQL_TABLE_STAT. Si se devuelve un valor distinto de null en esta columna, debe usarse para calificar el nombre del índice en un **DROP INDEX** instrucción; de lo contrario, se debe usar el según TABLE_SCHEM para calificar el nombre del índice.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|Nombre del índice; Se devuelve NULL si el tipo es SQL_TABLE_STAT.|  
|TIPO DE (ODBC 1.0)|7|Smallint no NULL|Tipo de información que se devuelve:<br /><br /> SQL_TABLE_STAT indica una estadística para la tabla (en la columna de CARDINALIDAD o páginas).<br /><br /> SQL_INDEX_BTREE indica un índice de árbol B.<br /><br /> SQL_INDEX_CLUSTERED indica un índice agrupado.<br /><br /> SQL_INDEX_CONTENT indica un índice de contenido.<br /><br /> SQL_INDEX_HASHED indica un índice hash.<br /><br /> SQL_INDEX_OTHER indica de otro tipo de índice.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|Número de secuencia de la columna de índice (empezando por 1); Se devuelve NULL si el tipo es SQL_TABLE_STAT.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|Nombre de columna. Si la columna se basa en una expresión, como el salario + ventajas, se devuelve la expresión; Si la expresión no puede determinarse, se devuelve una cadena vacía. Se devuelve NULL si el tipo es SQL_TABLE_STAT.|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|Secuencia de ordenación para la columna: "A" ascendente; "D" para descendente; Se devuelve NULL si la secuencia de ordenación de columnas no es compatible con el origen de datos o si el tipo es SQL_TABLE_STAT.|  
|CARDINALIDAD (ODBC 1.0)|11|Entero|Cardinalidad de tabla o índice; número de filas de tabla si el tipo es SQL_TABLE_STAT; número de valores únicos del índice si el tipo no es SQL_TABLE_STAT; Se devuelve NULL si el valor no está disponible desde el origen de datos.|  
|PÁGINAS DE (ODBC 1.0)|12|Entero|Número de páginas utilizadas para almacenar el índice o tabla. número de páginas de la tabla si el tipo es SQL_TABLE_STAT; número de páginas de índice si el tipo no es SQL_TABLE_STAT; Se devuelve NULL si el valor no está disponible desde el origen de datos o si no es aplicable al origen de datos.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|Si el índice es un índice filtrado, se trata de la condición de filtro, como el salario > 30000; Si no se puede determinar la condición de filtro, esto es una cadena vacía.<br /><br /> NULL si el índice no es un índice filtrado, no se puede determinar si el índice es un índice filtrado o el tipo es SQL_TABLE_STAT.|  
  
 Si la fila del conjunto de resultados que se corresponde a una tabla, el controlador establece el tipo a SQL_TABLE_STAT y NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME y ASC_OR_DESC establece en NULL. Si la CARDINALIDAD o páginas no están disponibles en el origen de datos, el controlador los establece en NULL.  
  
## <a name="code-example"></a>Ejemplo de código  
 Para obtener un ejemplo de código de una función similar, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance.|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver las columnas de claves externas|[Función SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Devolver las columnas de una clave principal|[Función SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
