---
title: Tarea de creación de clúster de Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1420b0954faef9d031a6b80503f19dd981ec2b8f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947322"
---
# <a name="azure-hdinsight-create-cluster-task"></a>Tarea de creación de clúster de HDInsight de Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


La **tarea de creación de clúster de Azure HDInsight** permite que un paquete SSIS cree un clúster de Azure HDInsight en la suscripción de Azure y el grupo de recursos especificados.
  
La **tarea de creación de clúster de Azure HDInsight** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
> [!NOTE]  
> - La creación de un nuevo clúster de HDInsight puede tardar entre 10 y 20 minutos.  
> - Hay un costo asociado con la creación y ejecución de un clúster de Azure HDInsight. Vea el tema [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) para más información.  
  
Para agregar una **tarea de creación de clúster de HDInsight de Azure**, arrástrela y colóquela en el Diseñador SSIS y haga doble clic (o haga clic con el botón derecho y, después, haga clic en **Editar** ) para ver el siguiente cuadro de diálogo del **Editor de la tarea de creación de clúster de HDInsight de Azure** .  
  
En la tabla siguiente se proporciona una descripción de los campos de este cuadro de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Descripción**|  
|AzureResourceManagerConnection|Seleccione un administrador de conexiones de Azure Resource Manager o cree uno nuevo que se usará para crear el clúster de HDInsight.|  
|AzureStorageConnection|Seleccione un administrador de conexiones de almacenamiento de Azure existente o cree uno que haga referencia a una cuenta de almacenamiento de Azure que se asociará con el clúster de HDInsight.|
|SubscriptionId|Especifique el identificador de la suscripción en la que se creará el clúster de HDInsight.|
|ResourceGroup|Especifique el grupo de recursos de Azure en el que se creará el clúster de HDInsight.|
|Ubicación|Especifique la ubicación del clúster de HDInsight. El clúster debe crearse en la misma ubicación que la cuenta de Azure Storage especificada.|  
|nombreDeClúster|Especifique un nombre para el clúster de HDInsight que se va a crear.|  
|ClusterSize|Especifique el número de nodos que quiere crear en el clúster.|  
|BlobContainer|Especifique el nombre del contenedor de almacenamiento predeterminado que quiere asociar con el clúster de HDInsight.|  
|UserName|Especifique el nombre de usuario que se usará para conectarse al clúster de HDInsight.|  
|Contraseña|Especifique la contraseña que se usará para conectarse al clúster de HDInsight.|
|SshUserName|Especifique el nombre de usuario que se usa para acceder de forma remota al clúster de HDInsight con SSH.|
|SshPassword|Especifique la contraseña usada para acceder de forma remota al clúster de HDInsight con SSH.|
|FailIfExists|Especifique si la tarea debe generar un error si el clúster ya existe.|  
  
> [!NOTE]  
> Las ubicaciones del clúster de HDInsight y de la cuenta de Azure Storage deben ser la misma.
