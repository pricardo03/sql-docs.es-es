---
title: Definición de un dispositivo lógico de copia de seguridad en una unidad de cinta (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], tapes
- backing up databases [SQL Server], tapes
- database backups [SQL Server], tapes
- tape backup devices, creating
ms.assetid: 66f36e1d-0287-4fac-8a51-71f9f0d7ad5b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 14a96a44967c41b185d3196c9d6577f67547e77a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62877946"
---
# <a name="define-a-logical-backup-device-for-a-tape-drive-sql-server"></a>Definir un dispositivo lógico de copia de seguridad en una unidad de cinta (SQL Server)
  En este tema se describe cómo definir un dispositivo lógico de copia de seguridad para una unidad de cinta en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Un dispositivo lógico es un nombre definido por el usuario que señala un dispositivo físico de copia de seguridad específico (un archivo de disco o unidad de cinta).  La inicialización del dispositivo físico tiene lugar posteriormente, cuando se escribe una copia de seguridad en el dispositivo de copia de seguridad.  
  
> [!NOTE]  
>  La compatibilidad con dispositivos de cinta de copia de seguridad se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para definir un dispositivo lógico de copia de seguridad en una unidad de cinta, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   La unidad o unidades de cinta deben ser compatibles con el sistema operativo Microsoft Windows.  
  
-   El dispositivo de cinta debe estar conectado físicamente al equipo donde se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No se admite la creación de copias de seguridad en dispositivos de cinta remotos.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe pertenecer al rol fijo de servidor **diskadmin** .  
  
 Requiere permiso para escribir en el disco.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>Para definir un dispositivo lógico de copia de seguridad en una unidad de cinta  
  
1.  Tras conectarse a la instancia apropiada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol correspondiente.  
  
2.  Expanda **Objetos de servidor**y, luego, haga clic con el botón derecho en **Dispositivos de copia de seguridad**.  
  
3.  Haga clic en **Nuevo dispositivo de copia de seguridad**, que abre el cuadro de diálogo **Dispositivo de copia de seguridad** .  
  
4.  Escriba un nombre para el dispositivo.  
  
5.  Para el destino, haga clic en **Cinta** y seleccione una unidad de cinta que aún no esté asociada a otro dispositivo de copia de seguridad. Si no hay ninguna disponible, la opción **Cinta** está inactiva.  
  
6.  Para definir el nuevo dispositivo, haga clic en **Aceptar**.  
  
 Para realizar una copia de seguridad en este nuevo dispositivo, agréguelo en el campo **Copia de seguridad en:** del cuadro de diálogo **Copia de seguridad de base de datos** (**General**). Para obtener más información, vea [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>Para definir un dispositivo lógico de copia de seguridad en una unidad de cinta  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql) para definir un dispositivo lógico de copia de seguridad para una cinta. En el ejemplo se agrega el dispositivo de copia de seguridad de cinta denominado `tapedump1`, con el nombre físico `\\.\tape0`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [sys.backup_devices &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [sp_dropdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdevice-transact-sql)   
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
