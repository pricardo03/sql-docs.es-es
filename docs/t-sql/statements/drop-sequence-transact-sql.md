---
title: DROP SEQUENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SEQUENCE
- DROP_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SEQUENCE statement
- sequence number object, dropping
ms.assetid: c25772d3-61af-4aa7-b58b-a6f67a793e3d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 740c8bff60f56b94304b789e901ec3b1d945fd17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077724"
---
# <a name="drop-sequence-transact-sql"></a>DROP SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Quita un objeto de flujo de la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP SEQUENCE [ IF EXISTS ] { database_name.schema_name.sequence_name | schema_name.sequence_name | sequence_name } [ ,...n ]  
 [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Quita condicionalmente la secuencia solo si ya existe.  
  
 *database_name*  
 Es el nombre de la base de datos en la que se creó el objeto de secuencia.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece el objeto de secuencia.  
  
 *sequence_name*  
 Es el nombre de la secuencia que se va a quitar. El tipo es **sysname**.  
  
## <a name="remarks"></a>Notas  
 Después de generar un número, un objeto de flujo no tiene ninguna relación continua con el número que generó, de modo que se puede quitar el objeto de secuencia, aunque el número generado todavía esté en uso.  
  
 Se puede quitar un objeto de secuencia mientras hace referencia a él un de procedimiento almacenado o desencadenador, porque no está enlazado a un esquema. No se puede quitar un objeto de flujo si se hace referencia a él como un valor predeterminado en una tabla. El mensaje de error enumerará el objeto que hace referencia a la secuencia.  
  
 Para enumerar todos los objetos de secuencia de la base de datos, ejecute la siguiente instrucción.  
  
```  
SELECT sch.name + '.' + seq.name AS [Sequence schema and name]   
    FROM sys.sequences AS seq  
    JOIN sys.schemas AS sch  
        ON seq.schema_id = sch.schema_id ;  
GO  
```  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER o CONTROL en el esquema.  
  
### <a name="audit"></a>Auditar  
 Para auditar **DROP SEQUENCE**, supervise **SCHEMA_OBJECT_CHANGE_GROUP**.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita un objeto de secuencia denominado `CountBy1` de la base de datos actual.  
  
```  
DROP SEQUENCE CountBy1 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
