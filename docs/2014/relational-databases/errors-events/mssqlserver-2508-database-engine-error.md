---
title: MSSQLSERVER_2508 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2508 (Database Engine error)
ms.assetid: c37d40e5-c665-4d66-a727-5cb845634fcc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7b09fcbc5e6e291ae87945d55bc534a0a63fb0c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869162"
---
# <a name="mssqlserver2508"></a>MSSQLSERVER_2508
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2508|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_OUT_OF_DATE_PAGE_OR_ROW_COUNT|  
|Texto del mensaje|El recuento de %.*ls para el objeto "%.\*ls", id. de índice %d, id. de partición %I64d, id. de unidad de asignación %I64d (tipo %.\*ls) no es correcto. Ejecute DBCC UPDATEUSAGE.|  
  
## <a name="explanation"></a>Explicación  
 En las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], los valores del recuento de filas por tabla y por índice, y del recuento de páginas pueden llegar a ser incorrectos. Las bases de datos que se crearon en versiones anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] pueden contener recuentos incorrectos. DBCC CHECKDB se ha mejorado para detectar estos errores y devuelve este mensaje de advertencia cuando se encuentra el error.  
  
## <a name="user-action"></a>Acción del usuario  
 Ejecute DBCC UPDATEUSAGE con el objeto o índice especificado, o con la base de datos que contiene el objeto para corregir los recuentos no válidos.  
  
  
