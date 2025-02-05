---
title: sysdatatypemappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3d58525ec4bcedc4249466be93628a7c1baa21bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910145"
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **sysdatatypemappings** vista se utiliza para mostrar la asignación entre tipos de datos de SQL Server y los tipos de datos de un sistema de administración de base de datos (DBMS) de que no son de SQL Server. Esta vista se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|Id. de la asignación del tipo de datos.|  
|**source_dbms**|**sysname**|Indica el nombre del sistema DBMS desde el que se asignan los tipos de datos, que puede ser uno de los valores siguientes:<br /><br /> **MSSQLSERVER** = el origen es una base de datos de SQL Server.<br /><br /> **ORACLE** = el origen es una base de datos de Oracle.|  
|**source_version**|**sysname**|Indica la versión de producto del sistema DBMS de origen.|  
|**source_type**|**sysname**|Indica el tipo de datos que aparece en el sistema DBMS de origen.|  
|**source_length_min**|**bigint**|La longitud mínima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una longitud.|  
|**source_length_max**|**bigint**|La longitud máxima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una longitud.|  
|**source_precision_min**|**bigint**|La precisión mínima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una precisión.|  
|**source_precision_max**|**bigint**|La precisión máxima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una precisión.|  
|**source_scale_min**|**int**|La escala mínima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una escala.|  
|**source_scale_max**|**int**|La escala máxima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una escala.|  
|**source_nullable**|**bit**|Indica si el tipo de datos de destino admite valores NULL.|  
|**source_createparams**|**int**|Exclusivamente para uso interno.|  
|**destination_dbms**|**sysname**|Indica el nombre del sistema DBMS de destino y puede ser uno de los siguientes valores:<br /><br /> **MSSQLSERVER** = el destino es una base de datos de SQL Server.<br /><br /> **ORACLE** = el destino es una base de datos de Oracle.<br /><br /> **DB2** = el destino es una base de datos IBM DB2.<br /><br /> **SYBASE** = el destino es una base de datos de Sybase.|  
|**destination_version**|**sysname**|Versión de producto del sistema DBMS de destino.|  
|**destination_type**|**sysname**|Tipo de datos del sistema DBMS de destino.|  
|**destination_length**|**bigint**|Longitud del tipo de datos del sistema DBMS de destino.|  
|**destination_precision**|**bigint**|Precisión del tipo de datos del sistema DBMS de destino.|  
|**destination_scale**|**int**|Escala del tipo de datos del sistema DBMS de destino.|  
|**destination_nullable**|**bit**|Indica si el tipo de datos del sistema DBMS de destino admite un valor NULL.|  
|**destination_createparams**|**int**|Exclusivamente para uso interno.|  
|**dataloss**|**bit**|Indica si se pierden datos durante la asignación de tipos de datos entre el sistema DBMS de origen y de destino.|  
|**is_default**|**bit**|Indica si la asignación de tipos de datos se utiliza de manera predeterminada.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
