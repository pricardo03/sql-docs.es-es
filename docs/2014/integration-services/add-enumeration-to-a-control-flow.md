---
title: Agregar enumeración a un flujo de Control | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding enumerations
- Foreach Loop containers
- control flow [Integration Services], enumerations
- repeating workflows
- enumerations [Integration Services]
ms.assetid: f212b5fb-3cc4-422e-9b7c-89eb769a812a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cad9c6a3537fb523a13f0206eed6c8eee837ed06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061908"
---
# <a name="add-enumeration-to-a-control-flow"></a>Agregar enumeración a un flujo de control
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye el contenedor de bucles Para cada uno, un elemento de flujo de control que simplifica la inclusión de una construcción de bucle que enumera archivos y objetos en el flujo de control de un paquete. Para más información, vea [Contenedor Foreach Loop](control-flow/foreach-loop-container.md).  
  
 El contenedor de bucles Foreach no proporciona una funcionalidad, sino solamente la estructura en la que se genera el flujo de control repetible, se especifica un tipo de enumerador y se configura el enumerador. Para proporcionar la funcionalidad del contenedor, debe incluir por lo menos una tarea en el contenedor de bucles Foreach. Para más información, consulte [Integration Services Tasks](control-flow/integration-services-tasks.md).  
  
 El contenedor de bucles Foreach puede incluir un flujo de control con varias tareas y otros contenedores. Agregar tareas y contenedores a un contenedor de bucles Foreach es similar a agregarlas a un paquete, salvo que las tareas y contenedores se arrastran al contenedor de bucles Foreach en lugar de al paquete. Si el contenedor de bucles Foreach incluye más de una tarea o contenedor, puede conectarlos mediante restricciones de precedencia, tal y como se hace en un paquete. Para obtener más información, vea [Restricciones de precedencia](control-flow/precedence-constraints.md).  
  
### <a name="to-implement-a-foreach-loop-container-in-a-control-flow"></a>Para implementar un contenedor de bucles Foreach en un flujo de control  
  
1.  Agregue el contenedor de bucles Foreach al paquete. Para obtener más información, consulte [agregar o eliminar una tarea o un contenedor en un flujo de Control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  Agregue tareas y contenedores al contenedor de bucles Foreach. Para obtener más información, consulte [agregar o eliminar una tarea o un contenedor en un flujo de Control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  Conecte tareas y contenedores en el contenedor de bucles Foreach mediante restricciones de precedencia. Para más información, vea [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md).  
  
4.  Configure el contenedor de bucles Foreach. Para más información, vea [Configurar un contenedor de bucles Foreach](../../2014/integration-services/configure-a-foreach-loop-container.md).  
  
## <a name="see-also"></a>Vea también  
 [Agregar o eliminar tareas o contenedores en un flujo de control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Agrupar o desagrupar componentes](group-or-ungroup-components.md)   
 [Restricciones de precedencia](control-flow/precedence-constraints.md)   
 [Agregar iteración a un flujo de Control](add-iteration-to-a-control-flow.md)   
 [Flujo de control](control-flow/control-flow.md)  
  
  
