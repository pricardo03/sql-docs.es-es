---
title: Propiedades personalizadas de la tarea de control CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2a073699-79a2-4ea1-a68e-fc17a80b74ba
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 52abc0392a20325288be4803f83b5350af63429e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947140"
---
# <a name="cdc-control-task-custom-properties"></a>Propiedades personalizadas de la tarea de control CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  En la tabla siguiente se describen las propiedades personalizadas de la tarea de control CDC. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|Conexión|Conexión ADO.NET|Una conexión ADO.NET en la base de datos CDC de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para acceder a las tablas de cambios y al estado CDC si se almacenan en la misma base de datos.<br /><br /> Es preciso realizar la conexión a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilitada para CDC y donde se encuentre la tabla de cambios seleccionada.|  
|TaskOperation|Integer (enumeración)|Operación seleccionada para la tarea de control CDC. Los valores posibles son **Mark Initial Load Start**, **Mark Initial Load End**, **Mark CDC Start**, **Get Processing Range**, **Mark Processed Range**y **Reset CDC State**.<br /><br /> Si selecciona **MarkCdcStart**, **MarkInitialLoadStart**o **MarkInitialLoadEnd** al trabajar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC (es decir, no en Oracle), el usuario especificado en el administrador de conexiones tiene que ser  **db_owner** o **sysadmin**.<br /><br /> Para obtener más información acerca de estas operaciones, vea [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md) y [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).|  
|OperationParameter|String|Utilizado actualmente a la operación **MarkCdcStart** . Este parámetro permite que se requiera una entrada adicional para la operación específica. Por ejemplo, el número de LSN necesario para la operación **MarkCdcStart**|  
|StateVariable|String|Una variable de paquete SSIS que almacena el estado CDC del contexto CDC actual. La tarea de control CDC lee y escribe el estado en **StateVariable** y no lo carga ni lo almacena en un almacenamiento persistente a menos que se seleccione **AutomaticStatePersistence** . Vea [Definir una variable de estado](../../integration-services/data-flow/define-a-state-variable.md).|  
|AutomaticStatePersistence|Boolean|La tarea control CDC lee el estado CDC de la variable de paquete de estado CDC. Después de una operación, la tarea de control CDC actualiza el valor de la variable de paquete de estado CDC. La propiedad **AutomaticStatePersistence** indica la tarea de control CDC que es responsable de conservar el valor de estado CDC entre las ejecuciones de los paquetes SSIS.<br /><br /> Cuando esta propiedad es **true**, la tarea de control CDC carga automáticamente el valor de la variable de estado CDC desde una tabla de estado. Cuando la tarea de control CDC actualiza el valor de la variable de estado CDC, también actualiza su valor en el mismo estado **table.stores**, el estado de una tabla especial y actualiza la variable de estado. El programador puede controlar la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla de estado y su nombre. La estructura de esta tabla de estado está predefinida.<br /><br /> Cuando es **false**, la tarea de control CDC no se ocupa de conservar su valor. Cuando es true, la tarea de control CDC almacena el estado de una tabla especial y actualiza StateVariable.<br /><br /> El valor predeterminado es **true**, que indica que la persistencia de estado se actualiza automáticamente.|  
|StateConnection|Conexión ADO.NET|Una conexión de ADO.NET a la base de datos en la que reside la tabla de estado al usar **AutomaticStatePersistence**. El valor predeterminado es el mismo para **Conexión**.|  
|StateName|String|Nombre asociado al estado persistente. Los paquetes de carga plena y CDC que funcionan con el mismo contexto CDC especifican un nombre de contexto CDC común. Este nombre se usa para buscar la fila de estado en la tabla de estado.<br /><br /> Esta propiedad solo se aplica cuando **AutomaticStatePersistence** se establece en **true**.|  
|StateTable|String|Especifica el nombre de la tabla donde se almacena el estado del contexto CDC. Esta tabla debe estar accesible mediante la conexión configurada para este componente. Esta tabla debe incluir las columnas varchar denominadas **name** y **state**. (La columna **state** necesita tener como mínimo 256 caracteres).<br /><br /> Esta propiedad solo se aplica cuando **AutomaticStatePersistence** se establece en **true**.|  
|CommandTimeout|integer|Este valor indica el tiempo de espera (en segundos) que se usará al comunicarse con la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se utiliza este valor siempre que el tiempo de respuesta de la base de datos sea muy lento y el valor predeterminado (30 segundos) no sea suficiente.|  
  
## <a name="see-also"></a>Consulte también  
 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)   
 [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
  
