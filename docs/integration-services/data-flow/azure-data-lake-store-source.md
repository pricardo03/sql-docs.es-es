---
title: Origen de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7b3bda4e977d5a3f7b6c3029d5151bca8af267ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045429"
---
# <a name="azure-data-lake-store-source"></a>Origen de Azure Data Lake Store

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El componente **Origen de Azure Data Lake Store** permite que un paquete SSIS lea datos de un Azure Data Lake Store. Los formatos de archivo compatibles son los siguientes: texto y Avro.
  
 El **Origen de Azure Data Lake Store** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
> [!NOTE]
> Para garantizar que el Administrador de conexiones de Azure Data Lake Store y los componentes que lo utilizan (es decir, Origen de Data Lake Store y Destino de Azure Data Lake Store) se puedan conectar a los servicios, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). 
  
## <a name="configure-the-azure-data-lake-store-source"></a>Configurar Origen de Azure Data Lake Store
 1. Para ver el editor del origen de Origen de Azure Data Lake Store, arrastre y coloque **Origen de Azure Data Lake Store** en el diseñador de flujos de datos y haga doble clic en él para abrir el editor.  
  
2.  En el campo **Administrador de conexiones de Azure Data Lake Store** , especifique un administrador de conexiones de Azure Data Lake Store o cree uno nuevo que haga referencia a un servicio de Azure Data Lake Store.  
  
    1.  Para el campo **Ruta de acceso del archivo** , especifique la ruta de acceso archivo de origen en Azure Data Lake Store.   
  
    2.  En el campo **Formato de archivo** , especifique el formato del archivo de origen.  
  
        Si el formato de archivo es Text, debe especificar el valor **Carácter de delimitador de columna** . Seleccione también **Nombres de columna de la primera fila de datos** si la primera fila del archivo contiene nombres de columna.  
  
3.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.   

## <a name="text-qualifier"></a>Calificador de texto

El **origen de Azure Data Lake Store** no admite un calificador de texto. Si tiene que especificar un calificador de texto para procesar correctamente los archivos, le recomendamos que descargue los archivos en el equipo local y que los procese con el **origen de archivo plano**. El origen de archivo plano le permite especificar un calificador de texto. Para obtener más información, consulte [Origen de archivo plano](flat-file-source.md).
