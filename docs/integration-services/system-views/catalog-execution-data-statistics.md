---
title: catalog.execution_data_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6811363e2465d7de24e31e136920feba345a2706
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080766"
---
# <a name="catalogexecutiondatastatistics"></a>catalog.execution_data_statistics 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta vista muestra una fila cada vez que un componente de flujo de datos envía datos a un componente de nivel inferior para una ejecución del paquete determinada. La información de esta vista se puede usar para calcular el rendimiento de datos de un componente.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|Identificador (id.) único de los datos.|  
|execution_id|**bigint**|Identificador único de la instancia de ejecución.|  
|package_name|**nvarchar(260)**|Nombre del primer paquete que se inició durante la ejecución.|  
|task_name|**nvarchar(4000)**|Nombre de la tarea Flujo de datos.|  
|dataflow_path_id_string|**nvarchar(4000)**|Cadena de identificación de la ruta de flujo de datos.|  
|dataflow_path_name|**nvarchar(4000)**|Nombre de la ruta de flujo de datos.|  
|source_component_name|**nvarchar(4000)**|Nombre del componente de flujo de datos que envió los datos.|  
|destination_component_name|**nvarchar(4000)**|Nombre del componente de flujo de datos que recibió los datos.|  
|rows_sent|**bigint**|Número de filas enviadas desde el componente de origen.|  
|created_time|**datatimeoffset(7)**|Hora en que se obtuvieron los valores.|  
|execution_path|**nvarchar(max)**|Ruta de acceso de ejecución del componente.|  
  
## <a name="remarks"></a>Notas  
  
-   Cuando hay varios resultados del componente, se agrega una fila para cada uno de ellos.  
  
-   De forma predeterminada, cuando se inicia una ejecución, la información sobre el número de filas que se envían no se registra.  
  
-   Para ver los datos de una ejecución de paquetes determinada, establezca el nivel de registro en modo **Detallado**. Para más información, vea [Habilitar el registro para la ejecución de paquetes en el servidor SSIS](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de ejecución  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
