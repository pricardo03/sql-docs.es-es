---
title: 'Restauración sin conexión de ejemplo: grupo de archivo principal y otro grupo de archivos (modelo de recuperación completa) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- offline restores [SQL Server]
- restore sequences [SQL Server], offline
ms.assetid: 7d6c50eb-dc84-4d66-855a-0b5f1bd89737
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 390db80fc88e3d115bad292e5bf0bf1a4a921639
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089793"
---
# <a name="example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model"></a>Ejemplo: Restauración sin conexión del grupo de archivo principal y de otro grupo de archivos (modelo de recuperación completa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tema solo es relevante para las bases de datos con el modelo de recuperación completa que contienen varios grupos de archivos.  
  
 En este ejemplo, la base de datos `adb` contiene tres grupos de archivos. Los grupos de archivos `A` y `C` son de lectura/escritura, y el grupo de archivos `B` es de solo lectura. Los grupos de archivos principal y `B` están dañados, pero los grupos de archivos `A` y `C` están intactos. Antes del desastre, todos los grupos de archivos estaban en línea.  
  
 El administrador de la base de datos decide restaurar y recuperar el grupo de archivos principal y el grupo de archivos `B`. La base de datos está utilizando el modelo de recuperación completa, por lo que, antes de iniciar la restauración, debe crearse una copia del final del registro de la base de datos. Cuando la base de datos se pone en línea, los grupos de archivos `A` y `C` se ponen en línea automáticamente.  
  
> [!NOTE]  
>  La secuencia de restauración sin conexión tiene menos pasos que la restauración en línea de un archivo de solo lectura. Para obtener un ejemplo, consulte [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md). Sin embargo, la base de datos completa estará sin conexión durante la secuencia.  
  
## <a name="tail-log-backup"></a>Copia del final del registro  
 Antes de restaurar la base de datos, el administrador de la base de datos debe realizar una copia de seguridad de registros después del error. Puesto que la base de datos está dañada, es necesario usar la opción NO_TRUNCATE al realizar la copia del final del registro:  
  
```  
BACKUP LOG adb TO tailLogBackup   
   WITH NORECOVERY, NO_TRUNCATE  
```  
  
 La copia del final del registro es la última copia de seguridad que se aplica en las secuencias de restauración siguientes.  
  
## <a name="restore-sequence"></a>Secuencia de restauración  
 Para restaurar los grupos de archivos principal y `B`, el administrador de la base de datos utiliza una secuencia de restauración sin la opción PARTIAL, como se muestra a continuación:  
  
```  
RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
WITH NORECOVERY  
RESTORE DATABASE adb FILEGROUP='B' FROM backup2   
WITH NORECOVERY  
RESTORE LOG adb FROM backup3 WITH NORECOVERY  
RESTORE LOG adb FROM backup4 WITH NORECOVERY  
RESTORE LOG adb FROM backup5 WITH NORECOVERY  
RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
```  
  
 Los archivos que no se restauran se ponen en línea automáticamente. Todos los grupos de archivos están ahora en línea.  
  
## <a name="see-also"></a>Consulte también  
 [Restauración con conexión &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [Restauraciones de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
