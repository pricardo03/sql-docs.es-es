---
title: Sys. resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f151d62a03cebf931c58f37b1e126a7331cefae9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68418870"
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve datos de almacenamiento y uso de CPU para una base de datos de Azure SQL. Los datos se recopilan y agregan en intervalos de cinco minutos. Para cada base de datos de usuario, hay una fila por cada ventana de informes de cinco minutos en la que hay un cambio en el consumo de recursos. Los datos devueltos incluyen el uso de CPU, el cambio de tamaño de almacenamiento y la modificación de la SKU de base de datos. Las bases de datos inactivas sin cambios no pueden tener filas por cada intervalo de cinco minutos. Los datos históricos se conservan durante 14 días aproximadamente.  
  
 La vista **Sys. resource_stats** tiene definiciones diferentes en función de la versión del servidor de Azure SQL Database al que está asociada la base de datos. Tenga en cuenta estas diferencias y cualquier modificación que requiera la aplicación al actualizar a una nueva versión de servidor.  
  
 En la tabla siguiente se describen las columnas disponibles en un servidor v12:  
  
|Columnas|Tipo de datos|Descripción|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|Hora UTC que indica el inicio del intervalo de informes de cinco minutos.|  
|end_time|**datetime**|Hora UTC que indica el final del intervalo de informes de cinco minutos.|  
|database_name|**nvarchar(128)**|Nombre de la base de datos del usuario.|  
|sku|**nvarchar(128)**|Nivel de servicio de la base de datos. Los posibles valores son los siguientes:<br /><br /> Básica<br /><br /> Estándar<br /><br /> Premium<br /><br />Uso general<br /><br />Crítico para la empresa|  
|storage_in_megabytes|**float**|Tamaño de almacenamiento máximo en megabytes para el período de tiempo, incluidos los datos de base de datos, los índices, los procedimientos almacenados y los metadatos.|  
|avg_cpu_percent|**decimal(5,2)**|Uso de proceso promedio como porcentaje del límite del nivel de servicio.|  
|avg_data_io_percent|**decimal(5,2)**|Uso de E/S promedio como porcentaje según el límite del nivel de servicio.|  
|avg_log_write_percent|**decimal(5,2)**|Uso de recursos de escritura promedio como porcentaje del límite del nivel de servicio.|  
|max_worker_percent|**decimal(5,2)**|Número máximo de trabajos simultáneos (solicitudes) en porcentaje según el límite del nivel de servicio de la base de datos.<br /><br /> El máximo se calcula actualmente para el intervalo de cinco minutos basado en las muestras de 15 segundos de los recuentos de trabajo simultáneos.|  
|max_session_percent|**decimal(5,2)**|Número máximo de sesiones simultáneas en porcentaje según el límite del nivel de servicio de la base de datos.<br /><br /> El valor máximo se calcula actualmente para el intervalo de cinco minutos basado en las muestras de 15 segundos de los recuentos de sesiones simultáneas.|  
|dtu_limit|**int**|Valor actual máximo de DTU de base de datos para esta base de datos durante este intervalo. |   
|allocated_storage_in_megabytes|**float**|La cantidad de espacio de archivo con formato en MB disponible para almacenar los datos de la base de datos. El espacio de archivo con formato también se conoce como espacio de datos asignado.  Para obtener más información, vea: [Administración del espacio de archivo en SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|
  
> [!TIP]  
>  Para más información sobre estos límites y los niveles de servicio, consulte los temas sobre los [niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/).  
    
## <a name="permissions"></a>Permisos  
 Esta vista está disponible para todos los roles de usuario con permisos para conectarse a la base de datos **maestra** virtual.  
  
## <a name="remarks"></a>Comentarios  
 Los datos devueltos por **Sys. resource_stats** se expresan como un porcentaje de los límites máximos permitidos para el nivel de servicio/nivel de rendimiento que se está ejecutando.  
  
 Cuando una base de datos es miembro de un grupo elástico, las estadísticas de recursos que se presentan como valores porcentuales se expresan como el porcentaje del límite máximo de las bases de datos establecidas en la configuración del grupo elástico.  
  
 Para obtener una vista más detallada de estos datos, use la vista de administración dinámica **Sys. DM _ _db_resource_stats** en una base de datos de usuario. Esta vista captura datos cada 15 segundos u mantiene datos históricos durante 1 hora.  Para obtener más información, vea [Sys. DM &#40;_&#41;_db_resource_stats Azure SQL Database](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todas las bases de datos cuyo promedio de uso de proceso fue al menos del 80 % durante la semana pasada.  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>Vea también  
 [Niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Capacidades y límites del nivel de servicio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
