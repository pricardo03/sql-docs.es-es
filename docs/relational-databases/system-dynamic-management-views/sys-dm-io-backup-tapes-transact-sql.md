---
title: Sys.dm_io_backup_tapes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_backup_tapes
- dm_io_backup_tapes_TSQL
- sys.dm_io_backup_tapes_TSQL
- dm_io_backup_tapes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_backup_tapes dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
author: stevestein
ms.author: sstein
ms.openlocfilehash: c58f34404119592308515f95934e23cfc94e1fc6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900393"
---
# <a name="sysdmiobackuptapes-transact-sql"></a>sys.dm_io_backup_tapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la lista de los dispositivos de cinta y el estado de las solicitudes de montaje para copias de seguridad.   
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**physical_device_name**|**nvarchar (520)**|Nombre del dispositivo físico real en el que se puede realizar una copia de seguridad. No admite valores NULL.|  
|**logical_device_name**|**nvarchar(256)**|Nombre especificado por el usuario para la unidad (desde **sys.backup_devices**). Es NULL si no hay ningún nombre especificado por el usuario. Acepta valores NULL.|  
|**status**|**int**|Estado de la cinta:<br /><br /> 1 = Abierta, disponible para su uso<br /><br /> 2 = Pendiente de montaje<br /><br /> 3 = En uso<br /><br /> 4 = En carga<br /><br /> **Nota:** Mientras se carga una cinta (**estado = 4**), la etiqueta del medio no se lee aún. Las columnas que copian los valores de etiqueta de medios, como **media_sequence_number**, muestran valores anticipados que pueden diferir de los valores reales de la cinta. Después de que se ha leído la etiqueta, **estado** cambia a **3** (en uso), y las columnas de etiqueta del medio reflejan, a continuación, la cinta real que se carga.<br /><br /> No admite valores NULL.|  
|**status_desc**|**nvarchar (520)**|Descripción del estado de la cinta:<br /><br /> AVAILABLE<br /><br /> MOUNT PENDING<br /><br /> IN USE<br /><br /> LOADING MEDIA<br /><br /> No admite valores NULL.|  
|**mount_request_time**|**datetime**|Hora a la que se solicitó el montaje. NULL si no hay ningún montaje pendiente (**estado! = 2**). Acepta valores NULL.|  
|**mount_expiration_time**|**datetime**|Hora a la que expirará la solicitud de montaje (tiempo de espera). NULL si no hay ningún montaje pendiente (**estado! = 2**). Acepta valores NULL.|  
|**database_name**|**nvarchar(256)**|Base de datos para la que se va a realizar una copia de seguridad en este dispositivo. Acepta valores NULL.|  
|**spid**|**int**|Id. de sesión. Identifica el usuario de la cinta. Acepta valores NULL.|  
|**command**|**int**|Comando que realiza la copia de seguridad. Acepta valores NULL.|  
|**command_desc**|**nvarchar(120)**|Descripción del comando. Acepta valores NULL.|  
|**media_family_id**|**int**|Índice de la familia de medios (1.. *n*), *n* es el número de familias de medios en el conjunto de medios. Acepta valores NULL.|  
|**media_set_name**|**nvarchar(256)**|Nombre del conjunto de medios (si existe), tal como se especifica en la opción MEDIANAME al crear el conjunto de medios. Acepta valores NULL.|  
|**media_set_guid**|**uniqueidentifier**|Identificador único del conjunto de medios. Acepta valores NULL.|  
|**media_sequence_number**|**int**|Índice de volumen en una familia de medios (1.. *n*). Acepta valores NULL.|  
|**tape_operation**|**int**|Operación que se está realizando la cinta:<br /><br /> 1 = Lectura<br /><br /> 2 = Formato<br /><br /> 3 = Inicialización<br /><br /> 4 = Anexión<br /><br /> Acepta valores NULL.|  
|**tape_operation_desc**|**nvarchar(120)**|Operación que se realiza con la cinta:<br /><br /> READ<br /><br /> FORMAT<br /><br /> INIT<br /><br /> APPEND<br /><br /> Acepta valores NULL.|  
|**mount_request_type**|**int**|Tipo de solicitud de montaje:<br /><br /> 1 = Cinta específica. La cinta identificada en el **media_\***  campos es necesario.<br /><br /> 2 = Siguiente familia de medios. Se solicita la siguiente familia de medios, todavía sin restaurar. Se utiliza cuando se realiza la restauración desde un número de dispositivos que es inferior al número de familias de medios.<br /><br /> 3 = Cinta de continuación. La familia de medios se amplía y se solicita una cinta de continuación.<br /><br /> Acepta valores NULL.|  
|**mount_request_type_desc**|**nvarchar(120)**|Tipo de solicitud de montaje:<br /><br /> SPECIFIC TAPE<br /><br /> NEXT MEDIA FAMILY<br /><br /> CONTINUATION VOLUME<br /><br /> Acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 El usuario debe tener el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Puedo O relacionados con funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

