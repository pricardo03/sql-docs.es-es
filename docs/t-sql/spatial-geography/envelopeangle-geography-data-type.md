---
title: EnvelopeAngle (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e3289956dd79c852eef6534ad1f72623ad4dcaa6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066464"
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el ángulo máximo entre el punto devuelto por el método `EnvelopeCenter()` y un punto de la instancia de **geography** en grados.  
  
 Este método del tipo de datos **geography** admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de valor devuelto de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
 Este método devuelve un punto de la instancia de **geography** en grados. Cuando se usa con EnvelopeCenter(), `EnvelopeAngle()` devuelve un círculo de límite de una instancia de **geography**.  
  
 En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], este método se ha extendido a las instancias de **FullGlobe**.  
  
 La limitación de hemisferio aplicada a `EnvelopeAngle()` en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] se ha quitado. Sin embargo, en instancias con ángulos mayores que 90 grados, se devolverán 180 grados. `EnvelopeAngle()` no es exacta en instancias de **geography** que ocupen más de un hemisferio.  
  
## <a name="examples"></a>Ejemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
