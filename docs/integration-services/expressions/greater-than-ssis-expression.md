---
title: '&gt; (Mayor que) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- greater than operator (>)
- '> (greater than operator)'
ms.assetid: 2e22efa3-eeb1-4984-a95c-9bccdcf98892
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b908609b362fdc92ca77f8678e8934d65d1c3e61
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080853"
---
# <a name="gt-greater-than-ssis-expression"></a>&gt; (Mayor que) (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Realiza una comparación para determinar si la primera expresión es mayor que la segunda. El evaluador de expresiones convierte automáticamente muchos tipos de datos antes de realizar la comparación.  
  
> [!NOTE]  
>  Este operador no admite comparaciones que usen los tipos de datos DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
 Sin embargo, algunos tipos de datos requieren que la expresión incluya una conversión explícita para que se pueda evaluar correctamente. Para más información sobre conversiones válidas entre tipos de datos, vea [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
expression1 > expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression1, expression2*  
 Es cualquier expresión válida. Ambas expresiones deben tener tipos de datos que se puedan convertir implícitamente.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Notas  
 Si una de las expresiones de la comparación es NULL, el resultado de la comparación es NULL. Si ambas expresiones son NULL, el resultado es NULL.  
  
 El conjunto de expresiones *expression1* y *expression2*debe cumplir una de las siguientes reglas:  
  
-   **Numeric**   *expression1* y *expression2* deben ser un tipo de datos numérico. La intersección de los tipos de datos debe ser un tipo de datos numérico, tal como se especifica en las reglas para las conversiones numéricas implícitas que realiza el evaluador de expresiones. La intersección de dos tipos de datos numéricos no puede ser NULL. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
-   **Character** *expression1* y *expression2* deben devolver un tipo de datos DT_STR o DT_WSTR. Las dos expresiones pueden tener tipos de datos de cadena distintos.  
  
    > [!NOTE]  
    >  En las comparaciones de cadenas se distingue mayúsculas de minúsculas, caracteres acentuados, tipos de kana y el ancho.  
  
-   **Fecha, hora o fecha y hora** Tanto *expression1* como *expression2* se deben evaluar con uno de los siguientes tipos de datos: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET o DT_FILETIME.  
  
    > [!NOTE]  
    >  El sistema no admite comparaciones entre una expresión que devuelve un tipo de datos de hora y una expresión que devuelve un tipo de datos de fecha o de fecha/hora. El sistema genera un error.  
  
     Al comparar expresiones, el sistema aplica las reglas de conversión siguientes en el orden enumerado:  
  
    -   Cuando las dos expresiones devuelven el mismo tipo de datos, se realiza una comparación de ese tipo de datos.  
  
    -   Si una expresión es un tipo de datos DT_DBTIMESTAMPOFFSET, la otra expresión se convierte en DT_DBTIMESTAMPOFFSET implícitamente y se realiza una comparación de DT_DBTIMESTAMPOFFSET. Para más información, consulte [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
    -   Si una expresión es un tipo de datos DT_DBTIMESTAMP2, la otra expresión se convierte en DT_DBTIMESTAMP2 implícitamente y se realiza una comparación de DT_DBTIMESTAMP2.  
  
    -   Si una expresión es un tipo de datos DT_DBTIME2, la otra expresión se convierte en DT_DBTIME2 implícitamente y se realiza una comparación de DT_DBTIME2.  
  
    -   Si una expresión es de un tipo de datos que no es DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 o DT_DBTIME2, las expresiones se convierten en el tipo de datos DT_DBTIMESTAMP antes de compararse.  
  
     Al comparar las expresiones, el sistema hace las suposiciones siguientes:  
  
    -   Si cada expresión es un tipo de datos que incluye fracciones de segundo, el sistema supone que el tipo de datos con el menor número de dígitos por fracciones de segundo tiene ceros para los dígitos restantes.  
  
    -   Si cada expresión es un tipo de datos de fecha, pero solo una tiene un ajuste de zona horaria, el sistema supone que el tipo de datos de fecha sin ajuste de zona horaria está en hora universal coordinada (UTC).  
  
 Para obtener más información acerca de los tipos de datos, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve TRUE si la fecha actual es una fecha anterior al 4 de julio de 2003. Para más información, vea [GETDATE &#40;expresión de SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md).  
  
```  
"7/4/2003" > GETDATE()  
```  
  
 Este ejemplo devuelve TRUE si el valor de la columna **ListPrice** es mayor que 500.  
  
```  
ListPrice > 500  
```  
  
 Este ejemplo usa la variable **LPrice**. Se devuelve TRUE si el valor de **LPrice** es mayor que 500. El tipo de datos de la variable debe ser numérico para que se pueda analizar la expresión.  
  
```  
@LPrice > 500  
```  
  
## <a name="see-also"></a>Consulte también  
 [&#60; &#40;Menor que&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/less-than-ssis-expression.md)   
 [&#62;= &#40;Mayor o igual que&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)   
 [&#60;= &#40;Menor o igual que&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)   
 [== &#40;Igual&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/equal-ssis-expression.md)   
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
