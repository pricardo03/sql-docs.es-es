---
title: () (Paréntesis) (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ffdc00f4f8f0c009512eace3b3724a7fc419e8a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967940"
---
# <a name="-parentheses-ssis-expression"></a>() (Paréntesis) (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Identifica el orden de evaluación de las expresiones. Las expresiones escritas entre paréntesis tienen la prioridad de evaluación más alta. Las expresiones anidadas escritas entre paréntesis se evalúan desde dentro hacia fuera.  
  
 Los paréntesis también se usan para hacer que resulte más fácil comprender las expresiones complejas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es cualquier expresión válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 El tipo de datos de *expression*. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo muestra cómo el uso de paréntesis modifica la prioridad de los operadores. La primera expresión se evalúa como 100, mientras que la segunda se evalúa como 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
