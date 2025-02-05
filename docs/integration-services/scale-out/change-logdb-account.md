---
title: Cambiar la cuenta para el registro de escalabilidad horizontal de SSIS | Microsoft Docs
description: En este artículo se describe cómo cambiar la cuenta de usuario para el registro de Escalabilidad horizontal de SSIS.
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 92cf3e13f1e386a77ba4621b817567af95b42884
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896984"
---
# <a name="change-the-account-for-scale-out-logging"></a>Cambiar la cuenta para el registro del escalabilidad horizontal

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Al ejecutar paquetes de SSIS en escalabilidad horizontal, los mensajes de eventos se registrarán en la base de datos de SSISDB con un usuario creado automáticamente y llamado **##MS_SSISLogDBWorkerAgentLogin##** . El inicio de sesión de este usuario usará la autenticación de SQL Server.

Si quiere cambiar la cuenta que se usa para el registro de la escalabilidad horizontal, siga estos pasos:

> [!NOTE]
> Si usa una cuenta de usuario de Windows para el registro, use la misma cuenta que la que ejecuta el servicio de trabajador de escalabilidad horizontal. En caso contrario, se producirá un error en el inicio de sesión de SQL Server.

## <a name="1-create-a-user-for-ssisdb"></a>1. Crear un usuario de SSISDB
Para obtener instrucciones de creación de un usuario de base de datos, vea [Crear un usuario de base de datos](../../relational-databases/security/authentication-access/create-a-database-user.md).

## <a name="2-add-the-user-to-the-database-role-ssisclusterworker"></a>2. Agregar el usuario al rol de base de datos ssis_cluster_worker

Para obtener instrucciones sobre cómo combinar un rol de base de datos, vea [Combinar un rol](../../relational-databases/security/authentication-access/join-a-role.md).

## <a name="3-update-the-logging-information-in-ssisdb"></a>3. Actualizar la información de registro en SSISDB
Realice una llamada al procedimiento almacenado `[catalog].[update_logdb_info]` usando el nombre de SQL Server y la cadena de conexión como parámetros, tal como se muestra en el siguiente ejemplo:

    ```sql
    SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
    SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
    EXEC [internal].[update_logdb_info] @serverName, @connectionString
    GO
    ```

## <a name="4-restart-the-scale-out-worker-service"></a>4. Reiniciar el servicio de trabajador de escalabilidad horizontal
Reinicie el servicio de trabajador de escalabilidad horizontal para aplicar el cambio.

## <a name="next-steps"></a>Pasos siguientes
-   [Administrador de escalabilidad horizontal de Integration Services](integration-services-ssis-scale-out-manager.md)
