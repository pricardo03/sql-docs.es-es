---
title: sqlagent90, aplicación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server Agent
- sqlagent90 application
- SQL Server Agent, starting
- command prompt utilities [SQL Server], sqlagent90
ms.assetid: e8b80e8d-d0c9-4500-a868-0ce08233da08
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf72b26a7b5649b8d48a3d1da6dd6eab8d6c264a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035374"
---
# <a name="sqlagent90-application"></a>sqlagent90, aplicación
  La aplicación **sqlagent90** inicia el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desde el símbolo del sistema. Normalmente, el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] debe ejecutarse desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o utilizando métodos de SQL-SMO en una aplicación. Ejecute **sqlagent90** solo desde el símbolo del sistema cuando esté diagnosticando el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o cuando el proveedor principal de asistencia técnica le redirija a él.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlagent90  
-c [-v] [-iinstance_name]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-c**  
 Indica que el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se ejecuta desde el símbolo del sistema y es independiente del Administrador de control de servicios de Windows. Cuando se usa **-c** , el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no se puede controlar desde la aplicación Servicios de las Herramientas administrativas ni desde el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Este argumento es obligatorio.  
  
 **-v**  
 Indica que el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se ejecuta en modo detallado y escribe información de diagnóstico en la ventana del símbolo del sistema. La información de diagnóstico es la misma que la que se escribe en el registro de errores del Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **-i** *instance_name*  
 Indica que el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se conecta a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con nombre especificada por *instance_name*.  
  
## <a name="remarks"></a>Comentarios  
 Después de mostrar un mensaje de copyright, **sqlagent90** muestra la salida en la ventana del símbolo del sistema solo si se especificó el modificador **-v** . Para detener **sqlagent90**, pulse Crtl+C en el símbolo del sistema. No cierre la ventana del símbolo del sistema antes de detener **sqlagent90**.  
  
## <a name="see-also"></a>Vea también  
 [Tareas administrativas automatizadas &#40;Agente SQL Server&#41;](../ssms/agent/automated-administration-tasks-sql-server-agent.md)  
  
  
