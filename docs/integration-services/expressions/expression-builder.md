---
title: Generador de expresiones | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionbuilder.f1
helpviewer_keywords:
- Expression Builder dialog box
ms.assetid: 4717ce33-bd4e-44bc-81e0-002de075b4d1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 28c4d0d29ab92f6fd4cc88a11c0d7c2a884673a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088731"
---
# <a name="expression-builder"></a>Generador de expresiones

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use el cuadro de diálogo **Generador de expresiones** para crear y editar una expresión de propiedad, o bien para escribir la expresión que establece el valor de una variable con una interfaz gráfica de usuario que incluye variables y proporciona una referencia integrada para las funciones, conversiones de tipo y operadores del lenguaje de expresiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Una expresión de propiedad es una expresión asignada a una propiedad. Cuando se evalúa la expresión, la propiedad se actualiza dinámicamente para utilizar el resultado de la evaluación de la expresión. De manera similar, una expresión que se utiliza en una variable permite que el valor de la variable se actualice con el resultado de la evaluación de la expresión.  
  
 Existen varias formas de utilizar expresiones:  
  
-   **Tareas** Puede actualizar la línea Para que usa una tarea Enviar correo. Para hacerlo, inserte una dirección de correo electrónico almacenada en una variable, o bien actualice la línea de asunto con la concatenación de una cadena como "Ventas para:" y la fecha actual devuelta por la función GETDATE.  
  
-   **Variables** Establecer el valor de una variable en el mes actual utilizando una expresión como `DATEPART("mm",GETDATE())`; o bien establecer el valor de una cadena mediante la concatenación del literal de cadena y la fecha actual utilizando la expresión `"Today's date is " + (DT_WSTR,30)(GETDATE())`.  
  
-   **Administradores de conexión** Establecer la página de códigos de un administrador de conexiones de archivos planos utilizando una variable que contenga un identificador de página de códigos diferente; o bien especificar el número de filas del archivo de datos que deben omitirse escribiendo en la expresión un entero positivo, como 3.  
  
 Para más información sobre las expresiones de propiedad y las expresiones de escritura, vea [Usar expresiones de propiedad en paquetes](../../integration-services/expressions/use-property-expressions-in-packages.md) y [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Variables**|Expanda la carpeta **Variables** y arrastre las variables hasta el cuadro **Expresión** .|  
|**Funciones matemáticas**<br /><br /> **Funciones de cadena**<br /><br /> **Funciones de fecha y hora**<br /><br /> **Funciones NULL**<br /><br /> **Conversiones de tipo**<br /><br /> **Operadores**|Expanda las carpetas y arrastre funciones, conversiones de tipo y operadores hasta el cuadro **Expresión** .|  
|**Expresión**|Edite o escriba una expresión.|  
|**Valor evaluado**|Muestra el resultado de evaluación de la expresión.|  
|**Evaluar expresión**|Haga clic en **Evaluar expresión** para ver el resultado de evaluación de la expresión.|  
  
## <a name="see-also"></a>Consulte también  
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)   
 [Editor de expresiones de propiedad](../../integration-services/expressions/property-expressions-editor.md)   
 [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Variables del sistema](../../integration-services/system-variables.md)  
  
  
