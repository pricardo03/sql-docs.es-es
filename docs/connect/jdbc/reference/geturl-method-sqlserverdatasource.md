---
title: Método getURL (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dd0d5d2c-91fe-4b0f-a162-69d898ba176e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f3922e5cf97b6c7b5a795f295249950fd21a9f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978198"
---
# <a name="geturl-method-sqlserverdatasource"></a>Método getURL (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la dirección URL que se utiliza para la conexión al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto **String** que contiene la dirección URL.  
  
## <a name="remarks"></a>Notas  
 Por razones de seguridad, no debería incluir la contraseña en la dirección URL que se proporciona para el método [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md). Esto se debe a que los servidores de aplicación Java de otro fabricante muy a menudo muestran el conjunto de valores para la propiedad URL en la interfaz de usuario para la configuración del origen de datos. En su lugar, utilice el método [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) para establecer el valor de la contraseña. Los servidores de aplicación Java no mostrarán las contraseñas que se establezcan en su origen de datos de la interfaz de usuario para la configuración.  
  
> [!NOTE]  
>  Si no se llama al método setURL antes de llamar al método getURL, getURL devuelve el valor predeterminado de "jdbc:sqlserver://".  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
