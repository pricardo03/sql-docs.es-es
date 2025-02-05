---
title: Método prepareStatement (java.lang.String, int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b78d2192-f315-4c45-9051-c77059e2c3f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a47ac1202ec73c15198b9b6f3c87ee53e027c83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976183"
---
# <a name="preparestatement-method-javalangstring-int-int-int"></a>Método prepareStatement (java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) que genera objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) con el tipo, simultaneidad y capacidad de alojamiento especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   int nType,  
                                                   int nConcur,  
                                                   int nHold)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sql*  
  
 Un valor **String** que contiene la instrucción SQL.  
  
 *nType*  
  
 Un valor **int** que indica el tipo de conjunto de resultados.  
  
 *nConcur*  
  
 Un valor **int** que indica el tipo de simultaneidad del conjunto de resultados.  
  
 *nHold*  
  
 Un valor **int** que indica la capacidad de alojamiento del conjunto de resultados.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto PreparedStatement.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método prepareStatement se especifica mediante el método prepareStatement en la interfaz java. SQL. Connection.  
  
## <a name="see-also"></a>Consulte también  
 [Método prepareStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
