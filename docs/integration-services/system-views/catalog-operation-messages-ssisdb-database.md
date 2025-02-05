---
title: catalog.operation_messages (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- catalog.operation_messages view [Integration Services]
- operation_messages view [Integration Services]
ms.assetid: 0b3cbe38-ce24-47ca-83ef-6538a5299d1a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7e12e63be770a7547e61b1fd546171d4f5cae4ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045227"
---
# <a name="catalogoperationmessages-ssisdb-database"></a>catalog.operation_messages (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los mensajes registrados durante las operaciones del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|operation_message_id|**bigint**|El identificador único (ID) del mensaje.|  
|operation_id|**bigint**|El identificador único de la operación.|  
|message_time|**datetimeoffset(7)**|Es la hora en la que se creó el mensaje.|  
|message_type|**smallint**|Tipo del mensaje mostrado.|  
|message_source_type|**smallint**|El identificador del tipo de origen del mensaje.|  
|message|**nvarchar(max)**|Texto del mensaje.|  
|extended_info_id|**bigint**|Es el id. de la información adicional relacionada con el mensaje de la operación, que se encuentra en la vista [extended_operation_info](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md).|  
  
## <a name="remarks"></a>Notas  
 Esta vista muestra una fila para cada mensaje registrado durante una operación en el catálogo. El mensaje lo puede genera el servidor, el proceso de ejecución del paquete o el motor de ejecución.  
  
 Esta vista muestra los siguientes tipos de mensaje:  
  
|Valor de **message_type**|Descripción|  
|-----------------------------|-----------------|  
|-1|Desconocido|  
|120|Error|  
|110|Advertencia|  
|70|Información|  
|10|Validación previa|  
|20|Validación posterior|  
|30|Ejecución previa|  
|40|Ejecución posterior|  
|60|Progreso|  
|50|StatusChange|  
|100|QueryCancel|  
|130|TaskFailed|  
|90|Diagnostic|  
|200|Personalizado|  
|140|DiagnosticEx<br /><br /> Siempre que una tarea Ejecutar paquete ejecuta un paquete secundario, registra este evento. El mensaje de evento consta de los valores de los parámetros pasados a los paquetes secundarios.<br /><br /> El valor de la columna de mensaje para DiagnosticEx es texto XML.|  
|400|NonDiagnostic|  
|80|VariableValueChanged|  
  
 Esta vista muestra los siguientes tipos de origen de mensaje:  
  
|**message_source_type**|Descripción|  
|-------------------------------|-----------------|  
|10|API de entrada, como procedimientos almacenados de T-SQL y CLR|  
|20|Proceso externo para ejecutar paquetes (ISServerExec.exe)|  
|30|Objetos de nivel de paquete|  
|40|Tareas de flujo de control|  
|50|Contenedores de flujo de control|  
|60|Tarea Flujo de datos|  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso de lectura en la operación  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
