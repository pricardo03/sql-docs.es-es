---
title: Método executeUpdate (java.lang.String) (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85e7c3a2-f2da-49bf-9d90-5fd246fd60e1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5adfcb9127e6bc073bda7385387edf0946a96021
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954714"
---
# <a name="executeupdate-method-javalangstring-sqlserverstatement"></a>Método executeUpdate (java.lang.String) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la instrucción SQL determinada, que puede ser una instrucción INSERT, UPDATE o DELETE; o una instrucción SQL que no devuelve nada, como una instrucción DDL de SQL. A partir del controlador JDBC 3.0 de [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], executeUpdate devolverá el número correcto de filas actualizado en una operación MERGE.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int executeUpdate(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sql*  
  
 Objeto **String** que contiene la instrucción SQL.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el número de filas afectadas o 0 si se usa una instrucción DDL.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método executeUpdate especifica este método executeUpdate en la interfaz java.sql.Statement.  
  
 Si la ejecución de un procedimiento almacenado produce un recuento de actualización mayor que uno o que genera más de un conjunto de resultados, use el método [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) para ejecutar el procedimiento almacenado.  
  
## <a name="see-also"></a>Consulte también  
 [Método executeUpdate &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
