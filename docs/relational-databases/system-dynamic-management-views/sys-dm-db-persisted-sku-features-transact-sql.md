---
title: Sys. DM _ _db_persisted_sku_features (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server], feature restrictions
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd8c4d6fb71e98a13cab1b01f34b7c5dc7e99331
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345068"
---
# <a name="sysdmdbpersistedskufeatures-transact-sql"></a>sys.dm_db_persisted_sku_features (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Algunas características de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] cambian la manera en que [!INCLUDE[ssDE](../../includes/ssde-md.md)] almacena información en los archivos de base de datos. Estas características están restringidas a ediciones concretas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una base de datos que contiene estas características no se puede mover a una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no los admita. Use la vista de administración dinámica sys. DM _ _db_persisted_sku_features para enumerar las características específicas de la edición que están habilitadas en la base de datos actual.
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|Nombre externo de la característica que está habilitada en la base de datos pero no admitida en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta característica se debe quitar para poder migrar la base de datos a todas las ediciones disponibles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|feature_id|**int**|Id. de la característica asociado a la característica. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW DATABASE STATE en la base de datos.  
  
## <a name="remarks"></a>Comentarios  
 Si no se usa ninguna característica que pueda estar restringida por una edición específica en la base de datos, la vista no devuelve ninguna fila.  
  
 Sys. DM _ _db_persisted_sku_features puede enumerar las siguientes características de cambio de base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos como restringidas a ediciones específicas:  
  
-   **ChangeCapture**: Indica que una base de datos tiene habilitada la captura de datos modificados. Para quitar la captura de datos modificados, use el procedimiento almacenado [Sys. sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) . Para obtener más información, vea [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
-   **ColumnStoreIndex**: Indica que al menos una tabla tiene un índice de almacén de columnas. Para permitir que una base de datos se mueva a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edición de que no admite esta característica, utilice la instrucción [Drop index](../../t-sql/statements/drop-index-transact-sql.md) o [ALTER index](../../t-sql/statements/alter-index-transact-sql.md) para quitar el índice de almacén de columnas. Para obtener más información, consulte [índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
    **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   **Compresión**: Indica que al menos una tabla o un índice utiliza la compresión de datos o el formato de almacenamiento vardecimal. Para permitir que una base de datos se mueva a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edición de que no admite esta característica, utilice la instrucción [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o [ALTER index](../../t-sql/statements/alter-index-transact-sql.md) para quitar la compresión de datos. Para quitar el formato de almacenamiento vardecimal, utilice la instrucción sp_tableoption. Para obtener más información, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
-   **MultipleFSContainers**: Indica que la base de datos utiliza varios contenedores de FILESTREAM. La base de datos tiene un grupo de archivos FILESTREAM con varios contenedores (archivos). Para obtener más información, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
-   **InMemoryOLTP**: Indica que la base de datos utiliza OLTP en memoria. La base de datos tiene un grupo de archivos MEMORY_OPTIMIZED_DATA. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
  **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). 
  
-   **Particiones.** Indica que la base de datos contiene tablas con particiones, índices con particiones, esquemas de partición o funciones de partición. Para poder mover una base de datos a una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no sea Enterprise o Developer, no basta con modificar la tabla para que esté en una sola partición. Es necesario quitar la tabla con particiones. Si la tabla contiene datos, utilice SWITCH PARTITION para convertir cada partición en una tabla sin particiones. A continuación, elimine la tabla con particiones, el esquema de partición y la función de partición.  
  
-   **TransparentDataEncryption.** Indica que una base de datos se ha cifrado utilizando el cifrado de datos transparente. Para quitar el cifrado de datos transparente, utilice la instrucción ALTER DATABASE. Para obtener más información, vea [Cifrado de datos transparente &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  

> [!NOTE]
> A partir [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] de Service Pack 1, estas características, excepto **TransparentDataEncryption.** están disponibles en varias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ediciones y no se limitan únicamente a las ediciones Enterprise o developer.

 Para determinar si una base de datos utiliza alguna característica que esté restringida a ediciones concretas, ejecute la instrucción siguiente en la base de datos:  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas &#40;de administración dinámica relacionadas con bases de datos TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [Ediciones y características admitidas de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Ediciones y las características admitidas de SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
