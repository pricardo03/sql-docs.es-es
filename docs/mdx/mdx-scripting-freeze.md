---
title: FREEZE (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4738dab411fe55808034a6d9d81a16994089ea74
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138287"
---
# <a name="mdx-scripting---freeze"></a>Scripting de MDX: FREEZE


  Bloquea los valores de celda de un subcubo especificado a sus valores actuales. Cuando se bloquean los valores de celda, los cambios en otras celdas no tienen efecto sobre las celdas bloqueadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>Argumentos  
 *Subcube_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un subcubo.  
  
## <a name="remarks"></a>Comentarios  
 El **INMOVILIZAR** instrucción bloquea los valores de las celdas de un subcubo especificado, impidiendo que instrucciones posteriores en un MDX pasa de script de cambio de sus valores de cálculo posteriores.  
  
 En el siguiente ejemplo, A y B representan subcubos en un script de cálculo MDX:  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 En este punto, tanto A como B equivalen a 3.  
  
 Ahora volvemos a insertar el **inmovilizar** función para bloquear las celdas en el subcubo:  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 Ahora, A es igual a 2 y B es igual a 3.  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones para scripting de MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
