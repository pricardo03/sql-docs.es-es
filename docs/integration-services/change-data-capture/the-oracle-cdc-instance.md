---
title: Instancia Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ed71e8c4-e013-4bf2-8b6c-1e833ff2a41d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bc1307c49bca581c3ec036d28067dafa62b7a5b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049639"
---
# <a name="the-oracle-cdc-instance"></a>La instancia CDC de Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La instancia CDC de Oracle es un proceso creado por el servicio CDC de Oracle para procesar los cambios capturados a partir de una sola base de datos de origen de Oracle. La instancia CDC de Oracle recupera su configuración de la tabla **cdc.xdbcdc_config** y mantiene su estado en la tabla **cdc.xdbcdc_state** . Estas tablas forman parte de la base de datos CDC, que define la instancia CDC de Oracle. Para obtener más información acerca de la base de datos y las tablas xdbcdc, vea [The CDC Databases](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CDCdatabase).  
  
 A continuación se describen las tareas que realiza la instancia CDC de Oracle:  
  
-   **Gestionar la comprobación del inicio del servicio**: cuando se inicia, la instancia CDC carga su configuración desde la tabla **xdbcdc_config** y realiza una serie de comprobaciones de estado que garantizan que el estado almacenado de la instancia CDC es coherente y que puede comenzar a procesar cambios.  
  
-   **Prepararse para la captura de los cambios**: cuando la comprobación se realiza correctamente, la instancia CDC de Oracle examina todas las instancias de captura definidas actualmente y prepara las consultas de Oracle LogMiner y otras estructuras auxiliares necesarias para la captura de cambios. Además, la instancia de Oracle vuelve a cargar el estado interno de captura que se guardó la última vez que se ejecutó la instancia CDC de Oracle.  
  
-   **Capturar cambios de Oracle**: la instancia CDC de Oracle agrupa los cambios de Oracle mediante Oracle LogMiner, los ordena según la confirmación de la transacción y después cambia el tiempo en una transacción y los escribe en las tablas de cambios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos de CDC.  
  
-   **Gestión del cierre del servicio**: el servicio CDC de Oracle administra el ciclo de vida de la instancia CDC de Oracle. Cuando se solicita el cierre de la instancia CDC de Oracle, realiza las tareas siguientes:  
  
    -   Deja de leer desde el registro de transacciones de Oracle.  
  
    -   Deja de escribir las transacciones completadas de Oracle en la base de datos CDC.  
  
    -   Espera hasta 30 segundos (si es necesario) hasta que la transacción actual termina de escribir en la base de datos CDC. Si transcurren más de 30 segundos, se cancela la escritura y se revierte la transacción (se volverá a intentar cuando se reinicie la instancia CDC).  
  
    -   En un subproceso independiente, escribe en la tabla de transacciones de ensayo todos los registros almacenados en caché posibles durante un máximo de 30 segundos (de la transacción más antigua a la más reciente), actualiza la tabla **xdbcdc_state** y confirma todos los cambios.  
  
-   **Gestión de los cambios de configuración**: la instancia CDC de Oracle recibe una notificación de los cambios de configuración por parte del servicio CDC o mediante la detección de una nueva versión de la tabla **cdc.xdbcdc_config** . La mayoría de los cambios no necesitan que se reinicie la instancia CDC de Oracle (por ejemplo, agregar o quitar instancias de captura). Sin embargo, algunos cambios (como cambiar las credenciales de acceso o la cadena de conexión de Oracle) sí hacen necesario el reinicio de la instancia CDC.  
  
-   **Gestión de la recuperación**: cuando se inicia una instancia CDC de Oracle, su estado interno se restaura desde las tablas **xdbcdc_state** y **xdbcdc_staged_transactions**. Una vez restaurado el estado, la instancia CDC continúa de la forma habitual.  
  
## <a name="see-also"></a>Consulte también  
 [Tratamiento de errores](../../integration-services/change-data-capture/error-handling.md)  
  
  
