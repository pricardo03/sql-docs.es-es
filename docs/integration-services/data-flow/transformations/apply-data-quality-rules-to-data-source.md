---
title: Aplicar reglas de calidad de los datos al origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bb34223b2bfcb896c2f5b6fa6ec01e7e3487a072
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112850"
---
# <a name="apply-data-quality-rules-to-data-source"></a>Aplicar reglas de calidad de los datos al origen de datos

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Puede utilizar Data Quality Services (DQS) para corregir los datos en el flujo de datos de paquete conectando la transformación de Limpieza de DQS con el origen de datos. Para obtener más información acerca de DQS, vea [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md). Para obtener más información sobre la transformación, vea [DQS Cleansing Transformation](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md).  
  
 Al procesar datos con la transformación Limpieza DQS, se crea un proyecto de calidad de datos en el servidor Data Quality Server. Utilice Data Quality Client para administrar el proyecto. Para más información, consulte [Abrir, desbloquear, cambiar nombre y eliminar un proyecto de calidad de los datos](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md).  
  
### <a name="to-correct-data-in-the-data-flow"></a>Para corregir datos en el flujo de datos  
  
1.  Cree un paquete.  
  
2.  Agregue y configure la transformación Limpieza de DQS. Para más información, consulte [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md).  
  
3.  Conecte la transformación Limpieza de DQS a un origen de datos.  
  
  
