---
title: 'Paso 4: Prueba del paquete del tutorial de la lección 2 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 907dd855186236e05eb103fd771a28ff0bc916ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086569"
---
# <a name="lesson-2-4-test-the-lesson-2-tutorial-package"></a>Lección 2-4: Prueba del paquete del tutorial de la lección 2

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Con el contenedor de bucles Foreach y el administrador de conexiones de archivos planos ya configurados, el paquete de la lección 2 puede iterar a través de los 14 archivos planos de la carpeta Datos de ejemplo. Cada vez que un nombre de archivo coincide con los criterios especificados, el contenedor de bucles Foreach rellena la variable definida por el usuario con el nombre de archivo. Esta variable, a su vez, actualiza la propiedad ConnectionString del administrador de conexiones de archivos planos, que se conecta a ese archivo plano. Después, el contenedor de bucles Foreach ejecuta la tarea de flujo de datos sin modificar sobre los datos del archivo plano.  
  
> [!NOTE]  
> Si ha ejecutado el paquete de la lección 1, tendrá que eliminar los registros de la tabla dbo.NewFactCurrencyRate de la base de datos AdventureWorksDW2012 antes de ejecutar el paquete de esta lección. La lección 2 intenta insertar registros ya insertados en la lección 1, lo que produce un error.  
  
## <a name="check-the-package-layout"></a>Comprobación del diseño del paquete  
Antes de probar el paquete, compruebe que los flujos de datos y de control del paquete de la lección 2 contienen los objetos mostrados en los diagramas siguientes. El flujo de datos de la lección 2 es igual que en la lección 1.  
  
**Flujo de control**  
  
![Flujo de control del paquete](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**Flujo de datos**  
  
![Flujo de datos del paquete](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
## <a name="test-the-lesson-2-tutorial-package"></a>Prueba del paquete del tutorial de la lección 2  
  
1.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Lesson 2.dtsx** y seleccione **Ejecutar paquete**.  
  
    El paquete se ejecuta. Puede comprobar el estado de cada bucle en la ventana **Salida** o si hace clic en la pestaña **Progreso**. Por ejemplo, puede ver que se han agregado 1.097 líneas a la tabla de destino desde el archivo Currency_VEB.txt.  
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar**, haga clic en **Detener depuración**.  
  
## <a name="go-to-next-lesson"></a>Ir a la lección siguiente  
[Lección 3: Adición de registro con SSIS](../integration-services/lesson-3-add-logging-with-ssis.md)  
  
## <a name="see-also"></a>Vea también  
[Ejecución de proyectos y paquetes](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

