---
title: Realizar copias de seguridad y restaurar los índices y catálogos de texto completo | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], backing up
- full-text search [SQL Server], back up and restore
- recovery [full-text search]
- backups [SQL Server], full-text indexes
- full-text indexes [SQL Server], restoring
- restore operations [full-text search]
ms.assetid: 6a4080d9-e43f-4b7b-a1da-bebf654c1194
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 51ab502a0b4aa1c0740a41fee15bee098bddfd5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024434"
---
# <a name="back-up-and-restore-full-text-catalogs-and-indexes"></a>Realizar copias de seguridad de los catálogos de texto completo y restaurarlos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se explica cómo hacer una copia de seguridad y restaurar los índices de texto completo creados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el catálogo de texto completo es un concepto lógico y no reside en un grupo de archivos. Por consiguiente, para hacer una copia de seguridad de un catálogo de texto completo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe identificar cada grupo de archivos que contenga un índice de texto completo que pertenezca al catálogo. A continuación, debe hacer copia de seguridad de cada uno de estos grupos de archivos, uno por uno.  
  
> [!IMPORTANT]  
>  Se pueden importar los catálogos de texto completo al actualizar una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Cada catálogo de texto completo importado es un archivo de base de datos en su propio grupo de archivos. Para hacer una copia de seguridad de un catálogo importado, basta con hacer una copia de seguridad de su grupo de archivos. Para obtener más información, vea [Realizar copias de seguridad y restaurar catálogos de texto completo](https://go.microsoft.com/fwlink/?LinkID=121052), en los Libros en pantalla de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
##  <a name="backingup"></a> Hacer la copia de seguridad de los índices de texto completo de un catálogo de texto completo  
  
###  <a name="Find_FTIs_of_a_Catalog"></a> Encontrar los índices de texto completo de un catálogo de texto completo  
 Puede recuperar las propiedades de los índices de texto completo mediante la instrucción [SELECT](../../t-sql/queries/select-transact-sql.md) siguiente, que selecciona las columnas de las vistas de catálogo [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) y [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) .  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @TableID int;  
SET @TableID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product'));  
SELECT object_name(@TableID), i.is_enabled, i.change_tracking_state,   
   i.has_crawl_completed, i.crawl_type, c.name as fulltext_catalog_name   
   FROM sys.fulltext_indexes i, sys.fulltext_catalogs c   
   WHERE i.fulltext_catalog_id = c.fulltext_catalog_id;  
GO  
```  
  
  
###  <a name="Find_FG_of_FTI"></a> Buscar el grupo de archivos o archivo que contiene un índice de texto completo  
 Cuando se crea un índice de texto completo, se coloca en una de las ubicaciones siguientes:  
  
-   Un grupo de archivos especificado por el usuario.  
  
-   El mismo grupo de archivos que la vista o tabla base, para una tabla sin particiones.  
  
-   El grupo de archivos principal, para una tabla con particiones.  
  
> [!NOTE]  
>  Para obtener información sobre cómo crear un índice de texto completo, vea [Crear y administrar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md) y [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
 Para buscar el grupo de archivos de índice de texto completo en una tabla o vista, use la consulta siguiente, donde *object_name* es el nombre de la tabla o vista:  
  
```  
SELECT name FROM sys.filegroups f, sys.fulltext_indexes i   
   WHERE f.data_space_id = i.data_space_id   
      and i.object_id = object_id('object_name');  
GO  
  
```  
  
  
###  <a name="Back_up_FTIs_of_FTC"></a> Realizar la copia de seguridad de los grupos de archivos que contienen índices de texto completo  
 Después de buscar los grupos de archivos que contienen los índices de un catálogo de texto completo, necesita hacer una copia de seguridad de cada uno de los grupos de archivos. Durante el proceso de copia de seguridad, es posible que no se quiten ni agreguen catálogos de texto completo.  
  
 La primera copia de seguridad de un grupo de archivos debe ser una copia de seguridad de archivos completa. Después de haber creado una copia de seguridad de archivos completa para un grupo de archivos, podría hacer una copia de seguridad únicamente de los cambios en un grupo de archivos creando una serie de una o varias copias de seguridad diferenciales de los archivos que se basen en la copia de seguridad de archivos completa.  
  
 **Para realizar copias de seguridad de archivos y grupos de archivos**  
  
-   [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
  
##  <a name="Restore_FTI"></a> Restaurar un índice de texto completo  
 Al restaurar un grupo de archivos que se ha incluido en una copia de seguridad, se restauran los archivos de índice de texto completo, así como los demás archivos del grupo de archivos. De forma predeterminada, el grupo de archivos se restaura en la ubicación del disco en la que se creó la copia de seguridad del grupo de archivos.  
  
 Si una tabla indizada de texto completo estaba en línea y se estaba ejecutando un rellenado cuando se creó la copia de seguridad, el rellenado se reanuda después de la restauración.  
  
 **Para restaurar un grupo de archivos**  
  
-   [Restaurar archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Restaurar archivos y grupos de archivos en archivos existentes &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
## <a name="see-also"></a>Consulte también  
 [Administrar y supervisar la búsqueda de texto completo para una instancia de servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)   
 [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
