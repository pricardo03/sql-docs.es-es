---
title: Quite las instrucciones que quiten objetos del sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d420e2dba1dfdb284b0002eca6d8408c4e019e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093074"
---
# <a name="remove-statements-that-drop-system-objects"></a>Quitar instrucciones que quiten objetos del sistema
  El Asesor de actualizaciones ha detectado instrucciones que quitan objetos del sistema. Los objetos del sistema, incluidos los procedimientos almacenados extendidos, se implementan en la base de datos de **recursos** de solo lectura (mssqlsystemresource) y no se pueden quitar. Modifique las aplicaciones para revocar o denegar el permiso EXECUTE en los objetos del sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Las instrucciones como DROP TABLE, DROP PROCEDURE y **sp_dropextendedproc** no se pueden utilizar para quitar objetos del sistema, porque estos objetos se implementan en la base de datos de solo lectura **resource** .  
  
## <a name="corrective-action"></a>Acción correctora  
 Quite  de las aplicaciones todas las instrucciones que intenten quitar objetos del sistema. Modifique las aplicaciones para revocar o denegar el permiso EXECUTE en los objetos del sistema. También puede utilizar la herramienta de configuración de área expuesta (SAC) para deshabilitar algunos de estos objetos. Por ejemplo, el procedimiento almacenado extendido **xp_cmdshell** se puede habilitar o deshabilitar utilizando la herramienta SAC.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
