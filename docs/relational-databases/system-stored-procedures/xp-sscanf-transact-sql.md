---
title: xp_sscanf (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sscanf_TSQL
- xp_sscanf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sscanf
ms.assetid: 619a9df1-7008-407e-a75a-bc6f851454a8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e46fe3243f39f8783743bf11e08b6368d67116eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091901"
---
# <a name="xpsscanf-transact-sql"></a>xp_sscanf (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lee datos de la cadena en las posiciones de los argumentos especificados por cada argumento de formato.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xp_sscanf { string OUTPUT , format } [ ,argument [ ,...n ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
 **string**  
 Es la cadena de caracteres de la que se van a extraer los argumentos.  
  
 OUTPUT  
 Cuando se especifica, coloca el valor de *argumento* en el parámetro de salida.  
  
 *format*  
 Es una cadena de caracteres con formato similar a lo que es compatible con el lenguaje C **sscanf** función. Actualmente, solo se acepta el formato %s.  
  
 *argument*  
 Es un **varchar** variable se establece en el valor de la correspondiente *formato* argumento.  
  
 *n*  
 Es un marcador de posición que indica que se pueden especificar hasta 50 argumentos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **xp_sscanf** devuelve el siguiente mensaje:  
  
 `Command(s) completed successfully.`  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se utiliza `xp_sscanf` para extraer dos valores de una cadena de origen, basándose en sus posiciones dentro de la cadena de formato.  
  
```  
DECLARE @filename varchar (20), @message varchar (20);  
EXEC xp_sscanf 'sync -b -fproducts10.tmp -rrandom', 'sync -b -f%s -r%s',   
  @filename OUTPUT, @message OUTPUT;  
SELECT @filename, @message;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------- --------------------   
products10.tmp        random  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados extendidos generales &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sprintf &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-sprintf-transact-sql.md)  
  
  
