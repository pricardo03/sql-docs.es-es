---
title: Método deletesAreDetected (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.deletesAreDetected
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 73f3d994-bbd7-43d2-8b64-50057e278983
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aef2ebd78b1aed2d03ba56ef3371d7f0dbfade31
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955121"
---
# <a name="deletesaredetected-method-sqlserverdatabasemetadata"></a>Método deletesAreDetected (SQLServerDatabaseMetaData)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si se puede detectar una eliminación de filas visible mediante una llamada al método [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) de la clase [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
public boolean deletesAreDetected(int type)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Tipo*  
  
 Un valor **int** que indica el tipo de conjunto de resultados, que puede ser uno de los siguientes valores como queda definido en java.sql.ResultSet o SQLServerResultSet:  
  
## <a name="javasqlresultset-types"></a>Tipos java.sql.ResultSet  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>Tipos SQLServerResultSet  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si un hueco reemplaza a la fila eliminada. **false** si se quita la fila eliminada.  
  
 Cuando se usa el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este método devuelve **true** con los cursores TYPE_SS_SCROLL_KEYSET y **false** con todos los demás tipos de conjuntos de resultados.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método deletesAreDetected se especifica mediante el método deletesAreDetected en la interfaz java. SQL. DatabaseMetaData.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]detecta las filas eliminadas para todos los tipos de cursores actualizables, aunque la detección es transitoria para los cursores de avance y dinámicos.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
