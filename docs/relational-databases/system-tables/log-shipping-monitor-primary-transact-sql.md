---
title: log_shipping_monitor_primary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_primary
- log_shipping_monitor_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_primary system table
ms.assetid: 5f629a29-1a62-40e6-ae33-6f6b7dd09a36
author: stevestein
ms.author: sstein
ms.openlocfilehash: d39ea859f1fd2cc3064d8d8c71c91ba6324f162c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989976"
---
# <a name="logshippingmonitorprimary-transact-sql"></a>log_shipping_monitor_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena un registro de supervisión por cada base de datos principal en cada configuración de trasvase de registros. Esta tabla se almacena en el **msdb** base de datos.  
  
 Las tablas relacionadas con el historial y la supervisión también se utilizan en el servidor principal y los servidores secundarios.   
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|Id. de la base de datos principal para la configuración del trasvase de registros.|  
|**primary_server**|**sysname**|El nombre de la instancia principal de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en la configuración de trasvase de registros.|  
|**primary_database**|**sysname**|Nombre de la base de datos principal en la configuración del trasvase de registros.|  
|**backup_threshold**|**int**|Número de minutos permitido entre las operaciones de copia de seguridad antes de que se genere una alerta.|  
|**threshold_alert**|**int**|Alerta que se generará cuando se sobrepase el umbral de copia de seguridad.|  
|**threshold_alert_enabled**|**bit**|Determina si las alertas de umbral de copia de seguridad están habilitadas. 1 = Habilitada.<br /><br /> 0 = Deshabilitada.|  
|**last_backup_file**|**nvarchar(500)**|Ruta de acceso absoluta de la copia de seguridad más reciente del registro de transacciones.|  
|**last_backup_date**|**datetime**|Fecha y hora de la última operación de copia de seguridad del registro de transacciones en la base de datos principal.|  
|**last_backup_date_utc**|**datetime**|Fecha y hora de la última operación de copia de seguridad del registro de transacciones en la base de datos principal, expresadas en UTC (hora universal coordinada).|  
|**history_retention_period**|**int**|Cantidad de tiempo, en minutos, durante la que los registros de historial del trasvase de registros se mantienen en una base de datos principal determinada antes de ser eliminados.|  
  
## <a name="remarks"></a>Comentarios  
 Además de almacenarse en el servidor de supervisión remota, la información relacionada con el servidor principal se almacena en el servidor principal en su **log_shipping_monitor_primary** tabla.  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_help_log_shipping_monitor_primary &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)   
 [sp_delete_log_shipping_alert_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
