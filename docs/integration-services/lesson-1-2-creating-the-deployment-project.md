---
title: 'Paso 2: Crear el proyecto de implementación | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 80c5e4e9fe4faf0bfc11d9ed1e193d4ca43f2c18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902709"
---
# <a name="lesson-1-2---creating-the-deployment-project"></a>Lección 1-2: Crear el proyecto de implementación

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


En [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], la unidad que se puede implementar es un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Antes de que pueda implementar paquetes, debe crear un nuevo proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y agregar todos los paquetes y archivos auxiliares que desee implementar con los paquetes en ese proyecto.  
  
### <a name="to-create-the-integration-services-project"></a>Para crear el proyecto de Integration Services  
  
1.  Haga clic en **Inicio**, seleccione **Todos los programas**, **Microsoft SQL Server**y, después, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto** para crear un proyecto nuevo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
3.  En el cuadro de diálogo **Nuevo proyecto** , seleccione **Proyecto de Integration Services** en el panel **Plantillas** .  
  
4.  En el cuadro **Nombre** , cambie el nombre predeterminado por **Deployment Tutorial**. Opcionalmente, desactive la casilla **Crear directorio para la solución** .  
  
5.  Acepte la ubicación predeterminada o haga clic en **Examinar** para buscar la carpeta que quiere usar.  
  
6.  En el cuadro de diálogo **Ubicación del proyecto** , haga clic en la carpeta y, después, en **Abrir**.  
  
7.  Haga clic en **Aceptar**.  
  
8.  De forma predeterminada, se crea un paquete vacío, denominado Package.dtsx, que se agrega al nuevo proyecto. Sin embargo, no utilizará este paquete; en su lugar, agregará paquetes existentes al proyecto. Puesto que todos los paquetes de un proyecto se incluirán en la implementación, deber eliminar Package.dtsx. Para eliminarlo, haga clic con el botón derecho en el paquete y, después, haga clic en **Eliminar**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 3: Adición de paquetes y otros archivos](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
## <a name="see-also"></a>Consulte también  
[Proyectos de Integration Services &#40;SSIS&#41;](~/integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
  

