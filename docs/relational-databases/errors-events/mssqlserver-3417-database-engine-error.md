---
title: MSSQLSERVER_3417 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1a9c91c785854b796351d7e3dfce12eacf044827
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132410"
---
# <a name="mssqlserver3417"></a>MSSQLSERVER_3417
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3417|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|REC_BADMASTER|  
|Texto del mensaje|No se puede recuperar la base de datos maestra. SQL Server no se puede ejecutar. Restaure la base de datos maestra desde una copia de seguridad completa, repárela o vuelva a crearla. Para obtener más información acerca de cómo volver a crear la base de datos maestra, vea los Libros en pantalla de SQL Server.|  
  
## <a name="explanation"></a>Explicación  
SQL Server no puede iniciar la base de datos **master**. Si no se pueden poner en línea **master** o **tempdb**, SQL Server no puede ejecutarse. Este error suele ir precedido de otros errores. Revise los registros de errores para localizar el motivo original.  
  
## <a name="user-action"></a>Acción del usuario  
Restaure la copia de seguridad de la base de datos o repare la base de datos.  
  
