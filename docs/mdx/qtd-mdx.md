---
title: Qtd (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8856b28d8eec76d2bc262c4209b007c0a7fa04
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020640"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer nodo relacionado y terminando con el miembro especificado, como restringida por la *trimestre* nivel en la dimensión de tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Si un miembro expressionis no se especifica, el valor predeterminado es el miembro actual de la primera jerarquía con un nivel de tipo *trimestres* en la primera dimensión de tipo *tiempo* en el grupo de medida.  
  
 El **Qtd** función es una función abreviada para la [PeriodsToDate &#40;MDX&#41; ](../mdx/periodstodate-mdx.md) función cuyo argumento de expresión de nivel se establece en *trimestre*. Es decir, `Qtd(Member_Expression)` es funcionalmente equivalente a `PeriodsToDate(Quarter_Level_Expression, Member_Expression)`.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la suma de los `Measures.[Order Quantity]` miembro, se agregan durante los primeros dos meses del tercer trimestre del año 2003 incluidos en el `Date` dimensión, desde el **Adventure Works** cubo.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
