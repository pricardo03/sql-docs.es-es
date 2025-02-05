---
title: Método rowUpdated (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9eb0f1bf73f719550ce0a00b3b7f96fab9c2af38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975663"
---
# <a name="rowupdated-method-sqlserverresultset"></a>Método rowUpdated (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si se ha actualizado la fila actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si el propietario u otro usuario han actualizado la fila visiblemente y si se detectan actualizaciones. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método RowUpdated especifica este método rowUpdated en la interfaz java. SQL. ResultSet.  
  
 El valor que se devuelve depende de si el conjunto de resultados puede detectar las actualizaciones o no.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]no detecta filas actualizadas para ningún tipo de cursor.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
