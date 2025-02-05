---
title: Función SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65683174ee5b48a8f7b861f3ba838334d70025ae
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345436"
---
# <a name="sqlrowcount-function"></a>Función SQLRowCount
**Conformidad**  
 Versión introducida: Compatibilidad con los estándares de ODBC 1,0: ISO 92  
  
 **Resumen**  
 **SQLRowCount** devuelve el número de filas afectadas por una instrucción **Update**, **Insert**o **Delete** . una operación SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK en **SQLBulkOperations**; o una operación SQL_UPDATE o SQL_DELETE en **SQLSetPos**.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entradas Identificador de instrucción.  
  
 *RowCountPtr*  
 Genere Señala a un búfer en el que se va a devolver un recuento de filas. Para las instrucciones **Update**, **Insert**y **Delete** , para las operaciones SQL_ADD, SQL_UPDATE_BY_BOOKMARK y SQL_DELETE_BY_BOOKMARK en **SQLBulkOperations**, y para las operaciones SQL_UPDATE o SQL_DELETE en **SQLSetPos** , el valor devuelto en **RowCountPtr* es el número de filas afectadas por la solicitud o-1 si el número de filas afectadas no está disponible.  
  
 Cuando se llama a **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos o SQLMoreResults** , el campo SQL_DIAG_ROW_COUNT de la estructura de datos de diagnóstico se establece en el recuento de filas y el recuento de filas se almacena en caché en un manera dependiente de la implementación. **SQLRowCount** devuelve el valor de recuento de filas almacenadas en caché. El valor de recuento de filas almacenadas en caché es válido hasta que el identificador de instrucción se vuelve a establecer en el estado preparado o asignado, la instrucción se vuelve a ejecutar o se llama a **SQLCloseCursor** . Tenga en cuenta que si se ha llamado a una función desde que se estableció el campo SQL_DIAG_ROW_COUNT, el valor devuelto por **SQLRowCount** podría ser diferente del valor del campo SQL_DIAG_ROW_COUNT porque el campo SQL_DIAG_ROW_COUNT se restablece en 0 mediante cualquier llamada de función.  
  
 Para otras instrucciones y funciones, el controlador puede definir el valor devuelto \*en *RowCountPtr*. Por ejemplo, algunos orígenes de datos pueden devolver el número de filas devueltas por una instrucción **Select** o una función de catálogo antes de capturar las filas.  
  
> [!NOTE]  
>  Muchos orígenes de datos no pueden devolver el número de filas de un conjunto de resultados antes de capturarlas; para obtener la máxima interoperabilidad, las aplicaciones no deben basarse en este comportamiento.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLRowCount** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *identificador* de *StatementHandle*. En la tabla siguiente se enumeran los valores de SQLSTATE que devuelve normalmente **SQLRowCount** y se explica cada uno de ellos en el contexto de esta función. la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|ADVERTENCIA general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para el que no había ningún SQLSTATE específico y para el que no se definió ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*búfer MessageText* describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLRowCount** .<br /><br /> Se llamó a **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** para *StatementHandle* y se devolvió SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos de todos los parámetros transmitidos por secuencias.<br /><br /> (DM) se llamó a la función antes de llamar a **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** para *StatementHandle*.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para *StatementHandle* y que todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> Se llamó a **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSETPOS** para *StatementHandle* y se devolvió SQL_NEED_DATA. Se llamó a esta función antes de enviar los datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de memoria insuficientes.|  
|HY117|La conexión se suspendió debido a un estado de transacción desconocido. Solo se permiten las funciones de desconexión y de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Expiró el tiempo de espera de conexión antes de que el origen de datos respondiera a la solicitud. El tiempo de espera de la conexión se establece mediante **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) el controlador asociado a *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Si la última instrucción SQL ejecutada en el identificador de instrucción no era una instrucción **Update**, **Insert**o **Delete** , o si el argumento *Operation* de la llamada anterior a **SQLBulkOperations** no era SQL_ADD, SQL_UPDATE_BY_ MARCADOR, o SQL_DELETE_BY_BOOKMARK, o si el argumento de la *operación* de la llamada anterior a **SQLSETPOS** no era SQL_UPDATE o SQL_DELETE, el valor de **RowCountPtr* es definido por el controlador. Para obtener más información, vea [determinar el número de filas afectadas](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
