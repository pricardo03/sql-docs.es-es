---
title: Se detectaron extensiones obsoletas en el equipo de servidor de informes (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 40d245a2-0631-470e-81b3-1feb47e028cb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 93a971b82fa4bafd1d8fb51a148b7e488c7d6d20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093806"
---
# <a name="obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor"></a>Se detectaron extensiones obsoletas en el equipo del servidor de informes (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado una o más extensiones de representación que ya no están disponibles en la versión actual.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El servidor de informes está configurado para utilizar una o más extensiones que ya no están disponibles en esta versión. Entre estas extensiones se incluyen las siguientes:  
  
-   Extensión de representación en HTML OWC  
  
-   Extensión de representación 3,2 HTML  
  
 La actualización puede continuar, pero la funcionalidad no admitida ya no estará disponible en el servidor de informes actualizado.  
  
 Si necesita estas extensiones, no realice la actualización hasta encontrar una solución alternativa a estos requisitos. Puede que necesite obtener o generar una extensión de representación personalizada que proporcione la misma o similar funcionalidad.  
  
## <a name="corrective-action"></a>Acción correctora  
 Evalúe el conjunto actual de características que están incluidas en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para determinar si la funcionalidad admitida satisface los requisitos.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
