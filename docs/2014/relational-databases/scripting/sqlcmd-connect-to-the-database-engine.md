---
title: Conectarse al motor de base de datos con sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd utility, Database Engine connections
- Named Pipes [SQL Server], sqlcmd utility
- TCP/IP [SQL Server], client protocols
- network protocols [SQL Server], sqlcmd utility
- protocols [SQL Server], sqlcmd utility
- VIA
- client protocols [SQL Server]
ms.assetid: 74b0fb71-7f8e-4171-9431-d07528532524
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 441a2ebc1f147e71a0bfa3bce20daf9fd67d09f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090099"
---
# <a name="connect-to-the-database-engine-with-sqlcmd"></a>Conectarse al motor de base de datos con sqlcmd
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite las comunicaciones de clientes con el protocolo de red TCP/IP (valor predeterminado) y el protocolo de canalizaciones con nombre. El protocolo de memoria compartida también está disponible si el cliente se está conectando a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en el mismo equipo. Hay varios métodos habituales para seleccionar el protocolo. El protocolo que la utilidad **sqlcmd** utiliza se determina en el siguiente orden:  
  
-   **sqlcmd** usa el protocolo especificado como parte de la cadena de conexión, como se describe a continuación.  
  
-   Si no se especifica ningún protocolo como parte de la cadena de conexión, **sqlcmd** usará el protocolo definido como parte del alias al que se está conectando. Para configurar **sqlcmd** para usar un protocolo de red específico al crear un alias, vea [Crear o eliminar un alias de servidor para que lo use un cliente &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
-   Si el protocolo no se especifica de otra forma, **sqlcmd** usará el protocolo de red determinado por el orden de protocolos en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 En los siguientes ejemplos se muestran diversas formas de conectarse a la instancia predeterminada de [!INCLUDE[ssDE](../../includes/ssde-md.md)] en el puerto 1433, mientras que se supone que las instancias con nombre de [!INCLUDE[ssDE](../../includes/ssde-md.md)] están escuchando en el puerto 1691. En algunos de estos ejemplos se utiliza la dirección IP del adaptador de bucle invertido (127.0.0.1). Pruebe el uso de la dirección IP de la tarjeta de interfaz de red del equipo.  
  
 Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)] especificando el nombre de la instancia:  
  
```  
sqlcmd -S ComputerA  
sqlcmd -S ComputerA\instanceB  
```  
  
 Conéctese a [!INCLUDE[ssDE](../../includes/ssde-md.md)] especificando la dirección IP:  
  
```  
sqlcmd -S 127.0.0.1  
sqlcmd -S 127.0.0.1\instanceB  
```  
  
 Conéctese a [!INCLUDE[ssDE](../../includes/ssde-md.md)] especificando el número de puerto TCP\IP:  
  
```  
sqlcmd -S ComputerA,1433  
sqlcmd -S ComputerA,1691  
sqlcmd -S 127.0.0.1,1433  
sqlcmd -S 127.0.0.1,1691  
```  
  
### <a name="to-connect-using-tcpip"></a>Para conectarse utilizando TCP/IP  
  
-   Conéctese mediante la siguiente sintaxis:  
  
    ```  
    sqlcmd -S tcp:<computer name>,<port number>  
    ```  
  
-   Conéctese a la instancia predeterminada:  
  
    ```  
    sqlcmd -S tcp:ComputerA,1433  
    sqlcmd -S tcp:127.0.0.1,1433  
    ```  
  
-   Conéctese a una instancia con nombre:  
  
    ```  
    sqlcmd -S tcp:ComputerA,1691  
    sqlcmd -S tcp:127.0.0.1,1691  
    ```  
  
### <a name="to-connect-using-named-pipes"></a>Para conectarse mediante canalizaciones con nombre  
  
-   Conéctese utilizando una de las sintaxis generales siguientes:  
  
    ```  
    sqlcmd -S np:\\<computer name>\<pipe name>  
    ```  
  
-   Conéctese a la instancia predeterminada:  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\sql\query  
    ```  
  
-   Conéctese a una instancia con nombre:  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\MSSQL$<instancename>\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\MSSQL$<instancename>\sql\query  
    ```  
  
### <a name="to-connect-using-shared-memory-a-local-procedure-call-from-a-client-on-the-server"></a>Para conectarse mediante la memoria compartida (una llamada a un procedimiento local) desde un cliente en el servidor  
  
-   Conéctese utilizando una de las sintaxis generales siguientes:  
  
    ```  
    sqlcmd -S lpc:<computer name>  
    ```  
  
-   Conéctese a la instancia predeterminada:  
  
    ```  
    sqlcmd -S lpc:ComputerA  
    ```  
  
-   Conéctese a una instancia con nombre:  
  
    ```  
    sqlcmd -S lpc:ComputerA\<instancename>  
    ```  
  
  
