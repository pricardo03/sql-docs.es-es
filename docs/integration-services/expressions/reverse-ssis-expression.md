---
title: REVERSE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7c4078c4efd38d2313b6b7c89e8fe7721086bc40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967855"
---
# <a name="reverse-ssis-expression"></a>REVERSE (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Devuelve una expresión de caracteres en orden inverso.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres que se va a invertir.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Notas  
 El argumento *character_expression* ha de tener el tipo de datos DT_WSTR.  
  
 REVERSE devuelve un resultado NULL si el valor de *character_expression* es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo usa un literal de cadena. El resultado devuelto es "ekiB niatnuoM".  
  
```  
REVERSE("Mountain Bike")  
```  
  
 En este ejemplo se utiliza una variable. Si **Name** contiene Touring Bike, el resultado devuelto es "ekiB gniruoT".  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
