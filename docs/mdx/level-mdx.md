---
title: Nivel (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b419cbb05aa616f163f5878bda83c9d68203575d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905660"
---
# <a name="level-mdx"></a>Level (MDX)


  Devuelve el nivel de un miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Level  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un miembro.  
  
### <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el **nivel** función para devolver todos los meses del cubo Adventure Works.  
  
```  
SELECT[Date].[Fiscal].[Month].[February 2002].Level.Members ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 En el ejemplo siguiente se usa el **nivel** función para devolver el nombre del nivel para el All-Purpose Bike Stand en la jerarquía de atributo Model Name del cubo Adventure Works.  
  
```  
WITH MEMBER Measures.x AS   
   [Product].[Model Name].[All-Purpose Bike Stand].Level.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
