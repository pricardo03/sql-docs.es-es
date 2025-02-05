---
title: PredictProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bd8365b2d3aac82c184af549ef21952fd4c8e649
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893905"
---
# <a name="predictprobability-dmx"></a>PredictProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve la probabilidad de un estado especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una columna escalar.  
  
## <a name="return-type"></a>Tipo devuelto  
 Un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 Si se omite el estado predicho, se usa el estado que tenga la mayor probabilidad de predicción, sin incluir el depósito de estados que faltan. Para incluir el depósito de Estados que faltan \<, establezca el estado de predicción > en **INCLUDE_NULL**. Para devolver la probabilidad de los Estados que faltan, \<establezca el > de estado de predicción en NULL.  
  
> [!NOTE]  
>  Algunos modelos de minería de datos no proporcionan los valores de probabilidad y, por consiguiente, no pueden utilizar esta función. Además, los valores de probabilidad de cualquier valor del objetivo determinado se calcula de manera diferente o podría tener una interpretación distinta que dependa del tipo de modelo que esté consultando. Para obtener más información sobre cómo se calcula la probabilidad para un tipo de modelo determinado, vea el tema sobre el algoritmo individual del [contenido &#40;del&#41;modelo de minería de datos Analysis Services-minería de datos](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza una cláusula NATURAL PREDICTION JOIN para determinar si es probable que un individuo compre una bicicleta en función del modelo de minería de datos TM Decision Tree; también se determina la probabilidad de la predicción. En este ejemplo hay dos funciones PredictProbability, una para cada valor posible. Si omite este argumento, la función devuelve la probabilidad para el valor más probable.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictProbability([Bike Buyer], 1) AS [Bike Buyer = Yes],  
  PredictProbability([Bike Buyer], 0) AS [Bike Buyer = No]  
FROM [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Bike Buyer|Bike Buyer = Sí|Bike Buyer = No|  
|----------------|-----------------------|----------------------|  
|1|0.867074195848097|0.132755556974282|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;de funciones&#41;](../dmx/functions-dmx.md)   
 [Funciones &#40;de predicción generales DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
