---
title: Sugerencias de combinación (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Join Hint
- Join_Hint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- HASH join hint
- REMOTE join hint
- LOOP join hint
- join hints
- MERGE join hint
- hints [SQL Server], join
ms.assetid: 09069f4a-f2e3-4717-80e1-c0110058efc4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f6f89e973d5f021dbd48a1bc7fc8234f9c9b6a89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902016"
---
# <a name="hints-transact-sql---join"></a>Sugerencias (Transact-SQL): combinación
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Las sugerencias de combinación especifican que el optimizador de consultas aplique una estrategia de combinación entre dos tablas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener información general sobre las combinaciones y la sintaxis de combinación, vea [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
> [!CAUTION]  
>  Como el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suele seleccionar el mejor plan de ejecución de una consulta, se recomienda que únicamente los administradores de bases de datos y desarrolladores experimentados utilicen las sugerencias como último recurso.
  
 **Se aplica a:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<join_hint> ::=   
     { LOOP | HASH | MERGE | REMOTE }  
```  
  
## <a name="arguments"></a>Argumentos  
 LOOP | HASH | MERGE  
 Especifica que la combinación de la consulta utiliza bucles, hash o mezclas. El uso de LOOP | HASH | MERGE JOIN aplica una combinación particular entre dos tablas. LOOP no se puede especificar junto con RIGHT o FULL como un tipo de combinación.  
  
 REMOTE  
 Especifica que la operación de combinación se realice en el sitio de la tabla derecha. Esto es útil cuando la tabla izquierda es una tabla local y la tabla derecha es una tabla remota. REMOTE solo se debe utilizar cuando la tabla izquierda tenga menos filas que la tabla derecha.  
  
 Si la tabla derecha es local, la combinación se realiza localmente. Si ambas tablas son remotas pero de orígenes de datos diferentes, REMOTE hace que la combinación se realice en el sitio de la tabla derecha. Si ambas tablas son tablas remotas pero del mismo origen de datos, REMOTE no es necesario.  
  
 REMOTE no se puede utilizar cuando uno de los valores que se va a comparar en el predicado de combinación se convierte a una intercalación distinta mediante la cláusula COLLATE.  
  
 REMOTE solo puede utilizarse en operaciones INNER JOIN.  
  
## <a name="remarks"></a>Notas  
 Las sugerencias de combinación se especifican en la cláusula FROM de una consulta. Las sugerencias de combinación exigen una estrategia de combinación entre dos tablas. Si se especifica una sugerencia de combinación entre dos tablas, el optimizador de consultas aplica automáticamente el orden de combinación de todas las tablas combinadas de la consulta, basándose en la posición de las palabras clave ON. Cuando se utiliza CROSS JOIN sin la cláusula ON, se pueden utilizar paréntesis para indicar el orden de combinación.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-hash"></a>A. Usar HASH  
 En el siguiente ejemplo se especifica que la operación `JOIN` de la consulta está realizada por una combinación `HASH`. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT p.Name, pr.ProductReviewID  
FROM Production.Product AS p  
LEFT OUTER HASH JOIN Production.ProductReview AS pr  
ON p.ProductID = pr.ProductID  
ORDER BY ProductReviewID DESC;  
```  
  
### <a name="b-using-loop"></a>B. Usar LOOP  
 En el siguiente ejemplo se especifica que la operación `JOIN` de la consulta está realizada por una combinación `LOOP`. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
    INNER LOOP JOIN Sales.SalesPerson AS sp  
    ON spqh.SalesPersonID = sp.SalesPersonID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
### <a name="c-using-merge"></a>C. Usar MERGE  
 En el siguiente ejemplo se especifica que la operación `JOIN` de la consulta está realizada por una combinación `MERGE`. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT poh.PurchaseOrderID, poh.OrderDate, pod.ProductID, pod.DueDate, poh.VendorID   
FROM Purchasing.PurchaseOrderHeader AS poh  
INNER MERGE JOIN Purchasing.PurchaseOrderDetail AS pod   
    ON poh.PurchaseOrderID = pod.PurchaseOrderID;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Sugerencias &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)  
  
  
