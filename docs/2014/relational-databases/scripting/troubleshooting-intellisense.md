---
title: Solución de problemas IntelliSense (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- unavailable options [IntelliSense]
- IntelliSense [SQL Server], troubleshooting
- IntelliSense [SQL Server], unavailable options
- troubleshooting [IntelliSense]
ms.assetid: 4b72ffc6-aea2-4e11-ab36-fa2de4d7bcc5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a642fbe7dbd866baa01fe9db7163292bfda6db30
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063260"
---
# <a name="troubleshooting-intellisense-sql-server-management-studio"></a>Solución de problemas IntelliSense (SQL Server Management Studio)
  Hay algunos casos en que es posible que las opciones de IntelliSense no funcionen como se espera.  
  
## <a name="conditions-that-affect-intellisense"></a>Condiciones que afectan a IntelliSense  
 Las condiciones siguientes pueden afectar al comportamiento de IntelliSense:  
  
-   Hay un error de código encima del cursor.  
  
     Si hay una instrucción incompleta u otro error de código encima de la ubicación del punto de inserción, es posible que IntelliSense no pueda analizar los elementos del código y que, por lo tanto, no funcione. Para volver a habilitar IntelliSense, puede marcar con comentarios el código aplicable.  
  
-   El punto de inserción está dentro de un comentario de código.  
  
     Las opciones de IntelliSense no están disponibles cuando el punto de inserción está dentro de un comentario del archivo de origen.  
  
-   El punto de inserción está dentro de un literal de cadena.  
  
     Las opciones de IntelliSense no están disponibles cuando el punto de inserción está dentro de las comillas de un literal de cadena; por ejemplo:  
  
     `WHERE FirstName LIKE 'Patri%|'`  
  
-   Las opciones automáticas están desactivadas.  
  
     La mayoría de las características de IntelliSense funcionan automáticamente de forma predeterminada. No obstante, se pueden deshabilitar todas.  
  
     Es posible usar las características de IntelliSense aunque la finalización de instrucciones automática esté deshabilitada. Para obtener más información, vea [Configurar IntelliSense &#40;SQL Server Management Studio&#41;](configure-intellisense-sql-server-management-studio.md).  
  
## <a name="database-engine-query-intellisense"></a>IntelliSense en las consultas de Database Engine  
 Los problemas siguientes se aplican al Editor de consultas de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] :  
  
-   La funcionalidad IntelliSense del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no es compatible con todos los elementos de sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] . La ayuda sobre parámetros no es compatible con los parámetros de algunos objetos, como los procedimientos almacenados extendidos. Para obtener más información, vea [Sintaxis de Transact-SQL compatible con IntelliSense](transact-sql-syntax-supported-by-intellisense.md).  
  
-   IntelliSense solamente está disponible cuando el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] está conectado a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posterior. IntelliSense no está disponible cuando el Editor de consultas está conectado a versiones anteriores del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   IntelliSense se desactiva en el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] cuando está activado el modo SQLCMD.  
  
-   La funcionalidad de IntelliSense no abarca a los objetos de base de datos creados por otra conexión después de que la ventana del editor se conecte a la base de datos. Si faltan objetos de las características de IntelliSense tales como las listas de finalización, puede elegir uno de estos tres mecanismos si desea actualizar la memoria caché de objetos para la ventana del editor:  
  
    -   Seleccione el menú **Edición** , seleccione **IntelliSense**y, a continuación, seleccione **Actualizar caché local**.  
  
    -   Utilice el método abreviado de teclado CTRL+Mayús+R.  
  
    -   Desconecte la ventana del editor de la instancia [!INCLUDE[ssDE](../../includes/ssde-md.md)] y vuelva a conectarla.  
  
-   Las listas de finalización no incluyen los objetos de base de datos para los que no tiene permisos. IntelliSense marca las referencias a los objetos para los que tiene permisos. Por ejemplo, si abre un script que ha escrito otra persona, cualquier referencia a los objetos para los que esa persona tenga permisos y usted no se marca como incorrecta.  
  
-   Las listas de finalización podrían dejar de funcionar si pierde la conexión a la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Vuelva a conectarse a la instancia.  
  
  
