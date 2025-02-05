---
title: TRY_CAST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRY_CAST_TSQL
- TRY_CAST
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 313f1bd13cf1b12a0685eeb101998792e0586767
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098769"
---
# <a name="trycast-transact-sql"></a>TRY_CAST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve una conversión de valor al tipo de datos especificado si la conversión se realiza correctamente; de lo contrario, devuelve NULL.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TRY_CAST ( expression AS data_type [ ( length ) ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Valor que se va a convertir. Cualquier expresión válida.  
  
 *data_type*  
 Tipo de datos al que se va a convertir *expression*.  
  
 *length*  
 Número entero opcional que especifica la longitud del tipo de datos de destino.  
  
 El intervalo de valores aceptables está determinado por el valor de *data_type*.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve una conversión de valor al tipo de datos especificado si la conversión se realiza correctamente; de lo contrario, devuelve NULL.  
  
## <a name="remarks"></a>Notas  
 **TRY_CAST** toma el valor que se le ha pasado e intenta convertirlo al *data_type* especificado. Si la conversión se realiza correctamente, **TRY_CAST** devuelve el valor como el *data_type* especificado; si se produce un error, se devuelve NULL. Pero si se solicita una conversión que no se permite explícitamente, **TRY_CAST** generará un error.  
  
 **TRY_CAST** no es una palabra clave reservada y está disponible en todos los niveles de compatibilidad. **TRY_CAST** tiene la misma semántica que **TRY_CONVERT** al conectarse a los servidores remotos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-trycast-returns-null"></a>A. TRY_CAST devuelve NULL  
 En el ejemplo siguiente se muestra que TRY_CAST devuelve NULL cuando se produce un error en la conversión.  
  
```sql  
SELECT   
    CASE WHEN TRY_CAST('test' AS float) IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 En el ejemplo siguiente se demuestra que la expresión debe tener el formato esperado.  
  
```sql  
SET DATEFORMAT dmy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-trycast-fails-with-an-error"></a>B. TRY_CAST genera un error  
 En el ejemplo siguiente, se muestra que TRY_CAST devuelve un error cuando la conversión no está explícitamente permitida.  
  
```sql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 El resultado de esta instrucción es un error, ya que un entero no se puede convertir en un tipo de datos xml.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-trycast-succeeds"></a>C. TRY_CAST se realiza correctamente  
 Este ejemplo demuestra que la expresión debe tener el formato esperado.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte también  
 [TRY_CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
