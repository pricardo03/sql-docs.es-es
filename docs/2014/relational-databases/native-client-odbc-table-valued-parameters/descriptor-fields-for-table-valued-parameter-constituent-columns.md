---
title: Campos de descriptor para columnas de parámetros con valores de tabla | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a31491b56e5b5cd700e744be2b7a84f10f1e0121
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199938"
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>Campos de descriptor para columnas de parámetros con valores de tabla
  Los campos de descriptor de parámetro con valores de tabla se describe en esta sección se manipulan mediante [SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md) y [SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md) con el identificador para el descriptor de parámetro de implementación () IPD).  
  
## <a name="remarks"></a>Comentarios  
 SQL_DESC_AUTO_UNIQUE_VALUE se usa para los parámetros con valores de tabla así como otras características.  
  
|Nombre del atributo|Tipo|Descripción|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE indica que esta columna es una columna de identidad.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Puede usar esta información para optimizar el rendimiento, pero no tienen las aplicaciones lo establezcan para las columnas de identidad.|  
  
 Los atributos siguientes se agregan a todos los tipos de parámetro en los campos descriptor de parámetros de la aplicación (APD) y descriptor de parámetro de implementación (IPD):  
  
|Nombre del atributo|Tipo|Descripción|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE indica que esta columna está calculada.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Puede usar esta información para optimizar el rendimiento, pero no tienen las aplicaciones lo establezcan para las columnas calculadas.<br /><br /> Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE indica que una columna de parámetro con valores de tabla participa en una clave única. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|Indica el criterio de ordenación de una columna de parámetro con valores de tabla. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla. Los valores posibles son los siguientes:<br /><br /> -SQL_SS_ASCENDING_ORDER<br />-   SQL_SS_DESCENDING_ORDER<br />-   SQL_SS_ORDER_UNSPECIFIED<br /><br /> Los valores distintos de SQL_SS_ASCENDING_ORDER y SQL_SS_DESCENDING_ORDER generan un error con SQLSTATE HY024 y el mensaje 'Valor de atributo no válido', y se tratan como SQL_SS_ORDER_UNSPECIFIED, que es el valor predeterminado para este atributo.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|Indica el ordinal de una columna de parámetro con valores de tabla en el conjunto de columnas que definen la clasificación total para un parámetro con valores de tabla. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla. La ordenación de los ordinales se inicia en 1. Un valor de 0, el valor predeterminado, indica que una columna de parámetro con valores de tabla no tiene ordenación de columnas.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|Indica si todas las filas en el parámetro con valores de tabla tendrán el valor predeterminado para esta columna. Para los parámetros con valores de tabla, no es posible seleccionar el valor predeterminado fila a fila. Un valor de SQL_FALSE indica que las filas tendrán valores no predeterminados. Ésta es la opción predeterminada. Un valor de SQL_TRUE indica que esta columna tendrá los valores predeterminados para todas las filas.<br /><br /> Si está establecido en SQL_TRUE, no se enviará al servidor ningún dato.<br /><br /> Este campo también se puede usar con columnas de identidad o calculadas si los valores de columna no son necesarios en el procesamiento del servidor.|  
  
 Estos atributos únicamente son válidos en columnas de parámetro con valores de tabla. Se pasan por alto para otros parámetros.  
  
 Si SQL_CA_SS_COL_HAS_DEFAULT_VALUE está establecido para una columna de parámetro con valores de tabla, SQL_DESC_DATA_PTR para esa columna debe ser un puntero NULL. En caso contrario, SQLExecute o SQLExecDirect devolverá SQL_ERROR. Se generará un registro de diagnóstico con SQLSTATE = 07S01 y el mensaje "uso no válido de parámetro predeterminado para el parámetro \<p >, columna \<c >", donde \<p > es el parámetro ordinal y \<c > es el ordinal de columna.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
