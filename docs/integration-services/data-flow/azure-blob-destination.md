---
title: Destino de blob de Azure | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobdest.f1
- sql14.dts.designer.afpblobdest.f1
ms.assetid: 820a1e7a-7182-4c7b-ab56-5b4097a7e042
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3194e2dbb6563b5260fcc390e84e73a17e09542c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045459"
---
# <a name="azure-blob-destination"></a>Destino de blobs de Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 El componente **Azure Blob Destination** (Destino de blobs de Azure) permite que un paquete SSIS escriba datos en un blob de Azure. Los formatos de archivo compatibles son los siguientes: CSV y AVRO. 
   
 Arrastre y coloque el **destino de blobs de Azure** en el diseñador de flujos de datos y haga doble clic en él para ver el editor.  
  
 **Destino de blob de Azure** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
1.  En el campo **Azure storage connection manager** (Administrador de conexiones de almacenamiento de Azure), especifique un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que haga referencia a una cuenta de almacenamiento de Azure.  
  
2.  En el campo **Nombre de contenedor de blobs** , especifique el nombre del contenedor de blobs que contiene los archivos de origen.  
  
3.  En el campo **Nombre de blob** , especifique la ruta de acceso al blob.  
  
4.  En el campo **Blob file format** (Formato de archivo de blob), especifique el formato de blob que desea utilizar.  
  
5.  Si el formato de archivo es CSV, debe especificar el valor **Column delimiter character** (Carácter delimitador de columna). Seleccione también **Nombres de columna de la primera fila de datos** si la primera fila del archivo contiene nombres de columna.  
  
6.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.  
  
  
