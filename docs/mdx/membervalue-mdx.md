---
title: MemberValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4db81766060f8f1afde2241d0c89407ad3cbb864
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001405"
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)


  Devuelve el valor de un miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que se evalúa en un miembro.  
  
## <a name="return-value"></a>Valor devuelto  
 El valor de miembro devuelto incluye la información que se indica a continuación, en el orden en el que aparece en el valor devuelto:  
  
-   El enlace de valor, si se ha definido.  
  
-   La clave con el tipo de datos original si no hay enlace de nombres o si la clave y el título están enlazados a la misma columna.  
  
-   El título del miembro.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el enlace de valor, la clave de miembro y el título de la primera fecha de la dimensión Date del cubo Adventure Works.  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
