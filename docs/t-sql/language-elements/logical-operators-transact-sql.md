---
title: Operadores lógicos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], logical
- testing truth
- truth testing
- "TRUE"
- "FALSE"
- logical operators [SQL Server], Transact-SQL
ms.assetid: edd92f08-76fb-4fd7-a4b6-8520d6a81df1
author: rothja
ms.author: jroth
ms.openlocfilehash: a26896076c0c9ee12eae61a3e324090379b10df2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122127"
---
# <a name="logical-operators-transact-sql"></a>Operadores lógicos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Los operadores lógicos comprueban la veracidad de alguna condición. Al igual que los operadores de comparación, devuelven el tipo de datos **Boolean** con el valor TRUE, FALSE o UNKNOWN.  
  
|Operador|Significado|  
|--------------|-------------|  
|[ALL](../../t-sql/language-elements/all-transact-sql.md)|TRUE si el conjunto completo de comparaciones es TRUE.|  
|[AND](../../t-sql/language-elements/and-transact-sql.md)|TRUE si ambas expresiones booleanas son TRUE.|  
|[ANY](../../t-sql/language-elements/any-transact-sql.md)|TRUE si cualquier miembro del conjunto de comparaciones es TRUE.|  
|[BETWEEN](../../t-sql/language-elements/between-transact-sql.md)|TRUE si el operando está dentro de un intervalo.|  
|[EXISTS](../../t-sql/language-elements/exists-transact-sql.md)|TRUE si una subconsulta contiene cualquiera de las filas.|  
|[IN](../../t-sql/language-elements/in-transact-sql.md)|TRUE si el operando es igual a uno de la lista de expresiones.|  
|[LIKE](../../t-sql/language-elements/like-transact-sql.md)|TRUE si el operando coincide con un patrón.|  
|[NOT](../../t-sql/language-elements/not-transact-sql.md)|Invierte el valor de cualquier otro operador booleano.|  
|[OR](../../t-sql/language-elements/or-transact-sql.md)|TRUE si cualquiera de las dos expresiones booleanas es TRUE.|  
|[SOME](../../t-sql/language-elements/some-any-transact-sql.md)|TRUE si alguna de las comparaciones de un conjunto es TRUE.|  
  
## <a name="see-also"></a>Consulte también  
 [Prioridad de los operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operator-precedence-transact-sql.md)  
  
  
