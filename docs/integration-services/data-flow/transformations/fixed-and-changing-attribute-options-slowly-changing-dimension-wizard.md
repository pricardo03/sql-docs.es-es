---
title: Opciones de atributos fijos y variables (Asistente para dimensiones de variación lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c5dd0fcdf9cceb0e1290f56bd4c6eb2459e6da3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944403"
---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>Opciones de atributos fijos y variables (Asistente para dimensiones variables)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilice el cuadro de diálogo **Opciones de atributos fijos y variables** para especificar cómo se debe responder a los cambios realizados en los atributos fijos y variables.  
  
 Para obtener más información acerca de este asistente, vea [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Atributos fijos**  
 En el caso de los atributos fijos, indique si la tarea debe dar un error cuando se detecte un cambio en un atributo fijo.  
  
 **Atributos variables**  
 En el caso de los atributos variables, indique si la tarea debe cambiar todos los registros no actualizados o expirados, además de los actuales, cuando se detecten cambios en un atributo variable. Los registros expirados son los que se han reemplazado por uno nuevo mediante un cambio en un atributo histórico (un cambio del Tipo 2). La selección de esta opción puede imponer requisitos adicionales de procesamiento en un objeto multidimensional generado en el almacenamiento de datos relacional.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar salidas mediante el Asistente para dimensión de variación lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
