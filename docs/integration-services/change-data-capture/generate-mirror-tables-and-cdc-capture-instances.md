---
title: Generar tablas reflejadas e instancias de captura CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- mirTab
ms.assetid: 260c1617-eecc-4007-a84d-3c5778ce46b6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: dbefe9209072ec6e68e393bcef6f56360e6afe58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011379"
---
# <a name="generate-mirror-tables-and-cdc-capture-instances"></a>Generar tablas reflejadas e instancias de captura CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use la página Generar tablas reflejadas para generar las tablas reflejadas para las tablas que se incluyeron en la instancia CDC.  
  
 Haga clic en **Ejecutar** para crear las tablas reflejadas. Se mostrará el progreso de la creación de cada tabla y aparecerá un mensaje para que sepa si cada tabla reflejada se completó correctamente o con errores. Si se produce algún error, haga clic en **Detalles** para ver un cuadro de diálogo con una explicación del error.  
  
 Si alguna de las tablas no se puede crear, puede elegir entre continuar o eliminar las tablas que produjeron errores antes de continuar. Cuando termine de ejecutar el asistente, puede decidir si desea corregir la tabla de la base de datos de origen de Oracle o no usarla en la instancia CDC. Si corrige la tabla, puede agregarla al [Edit Tables](../../integration-services/change-data-capture/edit-tables.md).  
  
 Haga clic en **Siguiente** para abrir la página [Finish](../../integration-services/change-data-capture/finish.md) .  
  
## <a name="see-also"></a>Consulte también  
 [Cómo crear la instancia de base de datos de cambios de SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)  
  
  
