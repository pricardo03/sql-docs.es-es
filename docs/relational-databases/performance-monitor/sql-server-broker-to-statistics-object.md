---
title: Objeto SQL Server, Broker TO Statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker Transmission Object object
- 'SQL Server: Broker Transmission Object'
ms.assetid: b5bc5dde-e540-4848-8aa3-5735c51df2fb
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 6485a99d759d4c4b09ec2b78946f7e1aecd46204
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986976"
---
# <a name="sql-server-broker-to-statistics-object"></a>Objeto SQL Server, Broker TO Statistics
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto de rendimiento SQLServer:Broker To Statistics informa del número de veces que los cuadros de diálogo de [!INCLUDE[ssSB](../../includes/sssb-md.md)] solicitan objetos de transmisión y con qué frecuencia se escriben los objetos de transmisión en **tempdb**.  
  
 Los objetos de transmisión registran el estado de las transmisiones de mensajes para un diálogo de [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Están almacenados en la memoria. Para liberar memoria, [!INCLUDE[ssSB](../../includes/sssb-md.md)] escribe periódicamente lotes de objetos de transmisión inactivos en las tablas de trabajo de **tempdb**.  
  
 En la tabla siguiente se muestran los contadores incluidos en este objeto.  
  
|Contadores de SQL Server Broker TO Statistics|Descripción|  
|----------------------------------------------|-----------------|  
|**Avg. longitud de escrituras por lotes**|Promedio de objetos de transmisión guardados en un lote.|  
|**Avg. tiempo para escribir un lote (ms)**|Promedio de milisegundos necesarios para guardar un lote de objetos de transmisión.|  
|**Avg. tiempo para escribir una base de lote**|Exclusivamente para uso interno.|
|**Avg. tiempo entre lotes (ms)**|Promedio de milisegundos entre las escrituras de lotes de objetos de transmisión.|  
|**Avg. tiempo entre base de lotes**|Exclusivamente para uso interno.| 
|**Obtenciones de objeto de transmisión/s**|Número de veces por segundo en que los diálogos solicitaron objetos de transmisión.|  
|**Número de objetos de transmisión marcados con errores/s**|Número de veces por segundo en que se han marcado con errores los objetos de transmisión. Los objetos de transmisión se marcan con errores al producirse la primera modificación que hace que la copia en memoria difiera de la copia almacenada en **tempdb**. Los objetos de transmisión se modifican cuando [!INCLUDE[ssSB](../../includes/sssb-md.md)] tiene que registrar un cambio en el estado de las transmisiones de mensajes para el diálogo.|  
|**Escrituras de objeto de transmisión/s**|El número de veces por segundo en que un lote de objetos de transmisión se escribió en las tablas de trabajo de **tempdb** . Si se produce un gran número escrituras, podría deberse a que la memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está siendo a sometida una gran demanda.|  
  
## <a name="see-also"></a>Consulte también  
 [Access Methods (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-access-methods-object.md)   
 [Memory Manager (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-memory-manager-object.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
