---
title: Visor de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataviewer.f1
helpviewer_keywords:
- Data Viewer dialog box
ms.assetid: 6351309a-688f-4e82-9697-1712130f10a1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ea9797e325216efc8373b350fac76cb87a00aa19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049381"
---
# <a name="data-viewer"></a>Visor de datos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Si una ruta de acceso se configura para utilizar un visor de datos, el Visor de datos muestra los datos por búfer a medida que éstos se mueven entre dos componentes de flujo de datos.  
  
## <a name="options"></a>Opciones  
 **Flecha de color verde**  
 Haga clic en esta opción para mostrar los datos del siguiente búfer. Si los datos pueden moverse en un único búfer, esta opción no está disponible.  
  
 **Separar**  
 Separe el visor de datos.  
  
 **Nota** La separación de un visor de datos no elimina el visor de datos. Si el visor de datos se ha separado, los datos continúan circulando por la ruta de acceso, pero los datos del visor no se actualizan para coincidir con los datos de cada búfer.  
  
 **Adjuntar**  
 Adjunte un visor de datos.  
  
 **Nota** Cuando el visor de datos se adjunta, muestra información de cada búfer en el flujo de datos y, a continuación, realiza una pausa. Puede utilizar la flecha de color verde para avanzar por los búferes.  
  
 **Copiar datos**  
 Copie datos del búfer actual al Portapapeles.  
  
## <a name="see-also"></a>Consulte también  
 [Depurar el flujo de datos](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
  
