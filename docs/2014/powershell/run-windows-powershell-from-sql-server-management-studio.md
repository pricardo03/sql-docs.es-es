---
title: Ejecutar Windows PowerShell desde SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b07f2e39421bdeb777af1e31fe414ec1fe2890c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62762426"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Ejecutar Windows PowerShell desde SQL Server Management Studio
  Puede iniciar sesiones de Windows PowerShell desde el **Explorador de objetos** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] inicia Windows PowerShell, carga el `sqlps` módulo y establece el contexto de la ruta de acceso al nodo asociado en el **Explorador de objetos** árbol.  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Al especificar la ejecución de PowerShell para un objeto en el **Explorador de objetos**, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] inicia una sesión de Windows PowerShell en la que los complementos PowerShell de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se han cargado y registrado. La ruta de acceso para la sesión se preestablece en la ubicación del objeto en el que hizo clic con el botón secundario en el Explorador de objetos. Por ejemplo, si hace clic con el botón derecho en el objeto de base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] en el Explorador de objetos y selecciona **Iniciar PowerShell**, la ruta de acceso de Windows PowerShell se establece en lo siguiente:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>Ejecutar PowerShell  
 **Para ejecutar PowerShell desde SQL Server Management Studio**  
  
1.  Abra el **Explorador de objetos**.  
  
2.  Navegue al nodo del objeto en el que trabajará.  
  
3.  Haga clic con el botón derecho en el objeto y seleccione **Iniciar PowerShell**.  
  
## <a name="permissions"></a>Permisos  
 Cuando se abre desde [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], PowerShell no se ejecuta con privilegios de Administrador, lo que puede impedir algunas actividades como llamadas a WMI.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
