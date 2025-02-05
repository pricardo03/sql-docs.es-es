---
title: Sys.dm_filestream_non_transacted_handles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_non_transacted_handles_TSQL
- dm_filestream_non_transacted_handles
- dm_filestream_non_transacted_handles_TSQL
- sys.dm_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_non_transacted_handles dynamic management view
ms.assetid: 507ec125-67dc-450a-9081-94cde5444a92
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4dda607ace977be539dbed096a3d83ac5f220ea0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950980"
---
# <a name="sysdmfilestreamnontransactedhandles-transact-sql"></a>sys.dm_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra los identificadores de archivos no transaccionales abiertos asociados a los datos de FileTable.  
  
 Esta vista contiene una fila por cada identificador de archivo abierto. Dado que los datos de esta vista corresponden al estado interno activo del servidor, los datos cambian constantemente al abrirse y cerrarse los identificadores. Esta vista no contiene información histórica.  
  
 Para obtener más información, vea [Administrar FileTables](../../relational-databases/blob/manage-filetables.md).  
  
|**Columna**|**Tipo**|**Descripción**|  
|----------------|--------------|---------------------|  
|database_id|int|Id. de la base de datos asociado al identificador.|  
|object_id|int|Id. de objeto del objeto FileTable al que está asociado el identificador.|  
|handle_id|int|Id. de contexto del identificador único. Utilizado por el [sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md) procedimiento almacenado para eliminar un identificador específico.|  
|file_object_type|int|Tipo del identificador. Esto indica el nivel de la jerarquía con que se abrió el identificador, es decir, base de datos o elemento.|  
|file_object_type_desc|nvarchar(120)|"SIN DEFINIR",<br />"SERVER_ROOT",<br />"DATABASE_ROOT",<br />"TABLE_ROOT",<br />"TABLE_ITEM"|  
|correlation_process_id|varbinary (8)|Contiene un identificador único para el proceso que originó la solicitud.|  
|correlation_thread_id|varbinary (8)|Contiene un identificador único para el subproceso que originó la solicitud.|  
|file_context|varbinary (8)|Puntero al objeto de archivo utilizado por este identificador.|  
|state|int|Estado actual del identificador. Puede ser activo, cerrado o eliminado.|  
|state_desc|nvarchar(120)|"ACTIVO",<br />"CERRADA",<br />"ELIMINAR"|  
|current_workitem_type|int|Indica que este identificador se está procesando actualmente.|  
|current_workitem_type_desc|nvarchar(120)|"NoSetWorkItemType",<br />"FFtPreCreateWorkitem",<br />"FFtGetPhysicalFileNameWorkitem",<br />"FFtPostCreateWorkitem",<br />"FFtPreCleanupWorkitem",<br />"FFtPostCleanupWorkitem",<br />"FFtPreCloseWorkitem",<br />"FFtQueryDirectoryWorkItem",<br />"FFtQueryInfoWorkItem",<br />"FFtQueryVolumeInfoWorkItem",<br />"FFtSetInfoWorkitem",<br />"FFtWriteCompletionWorkitem"|  
|fcb_id|bigint|Identificador del bloque de control de archivos de FileTable|  
|item_id|varbinary(892)|El identificador de elemento de un archivo o un directorio. Puede ser NULL para los identificadores de raíz del servidor.|  
|is_directory|bit|Esto es un directorio.|  
|item_name|nvarchar(512)|Nombre del elemento.|  
|opened_file_name|nvarchar(512)|Ruta de acceso de la que se solicita originalmente su apertura.|  
|database_directory_name|nvarchar(512)|Parte de opened_file_name que representa el nombre del directorio de la base de datos.|  
|table_directory_name|nvarchar(512)|Parte de opened_file_name que representa el nombre del directorio de la tabla.|  
|remaining_file_name|nvarchar(512)|Parte de opened_file_name que representa el nombre del directorio restante.|  
|open_time|datetime|Hora en que se abrió el identificador.|  
|flags|int|ShareFlagsUpdatedToFcb = 0x1,<br />DeleteOnClose = 0x2,<br />NewFile = 0x4,<br />PostCreateDoneForNewFile = 0x8,<br />StreamFileOverwritten = 0x10,<br />RequestCancelled = 0x20,<br />NewFileCreationRolledBack = 0x40|  
|login_id|int|Id. de la entidad de seguridad que abrió el identificador.|  
|login_name|nvarchar(512)|Nombre de la entidad de seguridad que abrió el identificador.|  
|login_sid|varbinary(85)|SID de la entidad de seguridad que abrió el identificador.|  
|read_access|bit|Abierto para acceso de lectura.|  
|write_access|bit|Abierto para acceso de escritura.|  
|delete_access|bit|Abierto para acceso de eliminación.|  
|share_read|bit|Abrir con share_read permitido.|  
|share_write|bit|Abrir con share_write permitido.|  
|share_delete|bit|Abierto con share_delete permitido.|  
  
## <a name="see-also"></a>Vea también  
 [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
