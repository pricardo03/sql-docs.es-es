---
title: Carpeta de instantáneas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replicationutilities.specifysnapshotfolder.f1
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 92abee758d5eda99aebddc874550eb9cd2e87ca5
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769512"
---
# <a name="snapshot-folder"></a>Carpeta de instantáneas
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

La página **Carpeta de instantáneas** aparece en el Asistente para configurar la distribución y en el Asistente para nueva publicación. La ubicación que se especifique para la carpeta de instantáneas se utilizará como la predeterminada para todos los publicadores habilitados en este asistente (la carpeta de instantáneas predeterminada no se aplica a los publicadores que se habilitan posteriormente mediante el cuadro de diálogo **Propiedades del distribuidor** ). Puede sobrescribir este valor predeterminado en cualquier publicador de la página **Publicadores** del Asistente para configurar la distribución o el cuadro de diálogo **Propiedades del distribuidor** .  
  
La carpeta de instantáneas es simplemente un directorio designado como recurso compartido; los agentes que leen y escriben en esta carpeta deben tener permisos de acceso suficientes a ella. Para obtener más información sobre cómo proteger la carpeta adecuadamente, consulte [Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md). Antes de implementar la replicación, compruebe que los agentes de replicación podrán conectarse a la carpeta de instantáneas. Inicie la sesión con la cuenta que utilizará cada agente y, a continuación, intente tener acceso a la carpeta de instantáneas.  

Para una instancia administrada de Azure SQL Database, la carpeta de instantáneas debe ser un recurso compartido de archivos de Azure. 
  
## <a name="options"></a>Opciones  
 **Snapshot folder**  
 Escriba la ruta de acceso de la carpeta donde desea almacenar los archivos de instantáneas.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda utilizar un recurso de red compartido como ubicación para la carpeta de instantáneas. Los agentes en otros equipos no tienen acceso a las rutas de acceso locales (las que empiezan con una letra de unidad como C:\\).  
  
## <a name="see-also"></a>Consulte también  
 [Modificación de las opciones de instantánea](../../relational-databases/replication/snapshot-options.md)   
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
