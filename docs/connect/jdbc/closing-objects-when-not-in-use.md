---
title: Cerrar objetos cuando no están en uso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2a9539599848f86a84cd03838c1fa7412c24fb1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957304"
---
# <a name="closing-objects-when-not-in-use"></a>Cerrar los objetos cuando no se usan
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando trabaje con objetos del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], especialmente [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) o uno de los objetos Statement como [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), debe cerrarlos explícitamente usando sus métodos close cuando ya no sean necesarios. Esto mejora el rendimiento al liberar lo antes posible los recursos del servidor y el controlador, en lugar de esperar a que el recolector de elementos no utilizados de la máquina virtual Java lo haga en su lugar.  
  
 Cerrar los objetos es especialmente importante para mantener una buena simultaneidad en el servidor cuando se usan bloqueos de desplazamiento. Los bloqueos de desplazamiento del búfer de captura al que se tuvo acceso por última vez se mantienen hasta que se cierra el conjunto de resultados. De igual forma, los identificadores que configuraron las instrucciones se conservan hasta que éstas se cierran. Si está reutilizando una conexión para varias instrucciones y las cierra antes de permitirles salir del ámbito, el servidor podrá limpiar los identificadores preparados con anterioridad.  
  
## <a name="see-also"></a>Consulte también  
 [Mejorar el rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
