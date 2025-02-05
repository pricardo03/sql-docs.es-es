---
title: Tarea de archivo flexible | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: cc95201ec856d5e7daa998c7de52b91981af5552
ms.sourcegitcommit: 2efb0fa21ff8093384c1df21f0e8910db15ef931
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316637"
---
# <a name="flexible-file-task"></a>Tarea de archivo flexible

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

La tarea de archivo flexible permite a los usuarios realizar operaciones de archivo en varios servicios de almacenamiento compatibles.
Los servicios de almacenamiento admitidos actualmente son:

- Sistema de archivos local
- [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)

La tarea de archivo flexible es un componente del [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para agregar una tarea de archivo flexible a un paquete, arrástrela desde el cuadro de herramientas de SSIS al lienzo del diseñador. Después, haga doble clic en la tarea o haga clic con el botón derecho y seleccione **Editar**, para abrir el cuadro de diálogo **Flexible File Task Editor** (Editor de la tarea de archivo flexible).

La propiedad **Operación** especifica la operación de archivo que se va a realizar.
Actualmente solo se admite la operación de **copia**.

Para la operación de **copia**, están disponibles las propiedades siguientes.

- **SourceConnectionType:** especifica el tipo del administrador de conexiones de origen.
- **SourceConnection:** especifica el administrador de conexiones de origen.
- **SourceFolderPath:** especifica la ruta de acceso a la carpeta de origen.
- **SourceFileName:** especifica el nombre de archivo de origen. Si se deja en blanco, se copiará en la carpeta de origen.
- **SearchRecursively:** especifica si las subcarpetas se copian recursivamente.
- **DestinationConnectionType:** especifica el tipo del administrador de conexiones de destino.
- **DestinationConnection:** especifica el administrador de conexiones de destino.
- **DestinationFolderPath:** especifica la ruta de acceso a la carpeta de destino.
- **DestinationFileName:** especifica el nombre de archivo de destino.

***Notas sobre la configuración de permisos de la entidad de servicio***

Para que la **conexión de prueba** funcione (ya sea Blob Storage o Data Lake Storage Gen2), se debe asignar al menos el rol **Lector de datos de Storage Blob** a la entidad de servicio en la cuenta de almacenamiento.
Esto se hace con [RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal).

Para el almacenamiento de blobs, los permisos de lectura y escritura se conceden mediante la asignación de al menos los roles **Lector de datos de Storage Blob** y **Colaborador de datos de Storage Blob**, respectivamente.

Para Data Lake Storage Gen2, el permiso lo determina RBAC y las [ACL](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-how-to-set-permissions-storage-explorer).
Preste atención a que las ACL se configuran mediante el identificador de objeto (OID) de la entidad de servicio para el registro de la aplicación como se detalla [aquí](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control#how-do-i-set-acls-correctly-for-a-service-principal).
Esto es diferente del identificador de aplicación (cliente) que se usa con la configuración de RBAC.
Cuando a una entidad de seguridad se le conceden permisos de datos RBAC a través de un rol integrado, o bien a través de un rol personalizado, estos permisos se evalúan primero tras la autorización de una solicitud.
Si la operación solicitada está autorizada por las asignaciones RBAC de la entidad de seguridad, la autorización se resuelve inmediatamente y no se realiza ninguna comprobación adicional de la ACL.
Como alternativa, si la entidad de seguridad no tiene una asignación RBAC, o la operación de la solicitud no coincide con el permiso asignado, se realizan comprobaciones de ACL para determinar si la entidad de seguridad está autorizada para realizar la operación solicitada.

- Para el permiso de lectura, conceda al menos el permiso **Execute** a partir del sistema de archivos de origen, junto con el permiso **Read** para los archivos que se van a copiar. Como alternativa, conceda al menos el rol **Lector de datos de Storage Blob** con RBAC.
- Para el permiso de escritura, conceda al menos el permiso **Execute** a partir del sistema de archivos de receptor, junto con el permiso **Write** para la carpeta de receptor. Como alternativa, conceda al menos el rol **Colaborador de datos de Storage Blob** con RBAC.

Vea [este](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control) artículo para obtener más información.
