---
title: Adjuntar una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.attachdatabase.f1
helpviewer_keywords:
- database attaching [SQL Server]
- attaching databases [SQL Server]
ms.assetid: b4efb0ae-cfe6-4d81-a4b4-6e4916885caa
author: stevestein
ms.author: sstein
ms.openlocfilehash: ca1ff898841b946c0823b71b065f360a59e69696
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071701"
---
# <a name="attach-a-database"></a>Adjuntar una base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este tema se describe cómo adjuntar una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puede usar esta característica para copiar, mover o actualizar una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="Prerequisites"></a> Requisitos previos  
  
-   La base de datos se debe separar primero. Si intenta adjuntar una base de datos que no se ha separado, se devolverá un error. Para obtener más información, vea [Separar una base de datos](../../relational-databases/databases/detach-a-database.md)  
  
-   Al adjuntar una base de datos, todos los archivos de datos deben estar disponibles (archivos MDF y LDF). Si algún archivo de datos tiene una ruta de acceso diferente a la que tenía cuando se creó la base de datos o cuando ésta se adjuntó por última vez, debe especificar la ruta actual.  
  
-   Cuando se adjunta una base de datos, si los archivos MDF y LDF se encuentran en directorios diferentes y una de las rutas de acceso incluye \\\\?\GlobalRoot, se producirá un error en la operación.  
  
###  <a name="Recommendations"></a> ¿Adjuntar es la mejor opción?  
Se recomienda mover las bases de datos mediante el procedimiento de reubicación programada `ALTER DATABASE`, en lugar del método de separar y adjuntar, al mover archivos de bases de datos dentro de la misma instancia. Para más información, consulte [Move User Databases](../../relational-databases/databases/move-user-databases.md). 
 
No se recomienda usar separar y adjuntar para el proceso de copia de seguridad y recuperación. No hay copias de seguridad del registro de transacciones y se pueden eliminar accidentalmente los archivos.
  
###  <a name="Security"></a> Seguridad  
Los permisos de acceso a archivos se establecen durante una serie de operaciones de base de datos, incluidas las operaciones de desasociar o adjuntar una base de datos. Para obtener información sobre los permisos de archivo que se establecen siempre que se separa y se adjunta una base de datos, vea [Proteger archivos de datos y de registro](https://technet.microsoft.com/library/ms189128.aspx) en los Libros en pantalla de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (sigue siendo una lectura válida). 
  
Se recomienda no adjuntar ni restaurar bases de datos de orígenes desconocidos o que no sean de confianza. Es posible que dichas bases de datos contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Para usar una base de datos desde un origen desconocido o que no sea de confianza, ejecute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) en la base de datos de un servidor que no sea de producción y examine también el código, como procedimientos almacenados u otro código definido por el usuario, en la base de datos. Para obtener más información sobre cómo adjuntar bases de datos y sobre los cambios que se realizan en los metadatos al adjuntar una base de datos, vea [Adjuntar y separar bases de datos (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
####  <a name="Permissions"></a> Permisos  
Requiere el permiso `CREATE DATABASE`, `CREATE ANY DATABASE` o `ALTER ANY DATABASE`.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  

### <a name="to-attach-a-database"></a>Para adjuntar una base de datos  
  
1.  En el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, haga clic para expandir esa vista de instancia en SSMS.  
  
2.  Haga clic con el botón derecho en **Bases de datos** y haga clic en **Adjuntar**.  
  
3.  En el cuadro de diálogo **Adjuntar bases de datos** , haga clic en **Agregar**para especificar la base de datos que se va a adjuntar y en el cuadro de diálogo **Buscar archivos de base de datos** , seleccione la unidad de disco en la que se halla la base de datos y expanda el árbol de directorios para buscar y seleccionar el archivo .mdf de la base de datos; por ejemplo:  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\AdventureWorks2012_Data.mdf`  
  
    > [!IMPORTANT]  
    > Trying to select a database that is already attached generates an error.  
  
     **Databases to attach**  
     Displays information about the selected databases.  
  
     \<no column header>  
     Displays an icon indicating the status of the attach operation. The possible icons are described in the **Status** description, below).  
  
     **MDF File Location**  
     Displays the path and file name of the selected MDF file.  
  
     **Database Name**  
     Displays the name of the database.  
  
     **Attach As**  
     Optionally, specifies a different name for the database to attach as.  
  
     **Owner**  
     Provides a drop-down list of possible database owners from which you can optionally select a different owner.  
  
     **Status**  
     Displays the status of the database according to the following table.  
  
    |Icono|Texto de estado|Descripción|  
    |----------|-----------------|-----------------|  
    |(Sin icono)|(Sin texto)|La operación de adjuntar no se ha iniciado o puede estar pendiente para este objeto. Es la opción predeterminada al abrir el diálogo.|  
    |Triángulo verde hacia la derecha|En curso|La operación de adjuntar se ha iniciado, pero no ha finalizado.|  
    |Marca de verificación verde|Correcto|El objeto se ha adjuntado correctamente.|  
    |Círculo rojo con una cruz blanca|Error|La operación de adjuntar ha detectado un error y no ha finalizado correctamente.|  
    |Círculo con dos cuadrantes negros (a la izquierda y la derecha) y dos cuadrantes blancos (en la parte superior e inferior)|Detenido|La operación de adjuntar no ha finalizado correctamente porque el usuario la ha detenido.|  
    |Círculo con una flecha curvada que apunta hacia la izquierda|Revertido|La operación de adjuntar se ha ejecutado correctamente, pero se ha revertido debido a un error al adjuntar otro objeto.|  
  
     **Message**  
     Displays either a blank message or a "File not found" hyperlink.  
  
     **Add**  
     Find the necessary main database files. When the user selects an .mdf file, applicable information is automatically filled in the respective fields of the **Databases to attach** grid.  
  
     **Remove**  
     Removes the selected file from the **Databases to attach** grid.  
  
     **"** *<database_name>* **" database details**  
     Displays the names of the files to be attached. To verify or change the pathname of a file, click the **Browse** button (**...**).  
  
    > [!NOTE]  
    > If a file does not exist, the **Message** column displays "Not found." If a log file is not found, it exists in another directory or has been deleted. You need to either update the file path in the **database details** grid to point to the correct location or remove the log file from the grid. If an .ndf data file is not found, you need to update its path in the grid to point to the correct location.  
  
     **Original File Name**  
     Displays the name of the attached file belonging to the database.  
  
     **File Type**  
     Indicates the type of file, **Data** or **Log**.  
  
     **Current File Path**  
     Displays the path to the selected database file. The path can be edited manually.  
  
     **Message**  
     Displays either a blank message or a "**File not found**" hyperlink.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
### <a name="to-attach-a-database"></a>Para adjuntar una base de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Use la instrucción [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) con la cláusula `FOR ATTACH`.  
  
     Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se adjuntan los archivos de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] y se cambia el nombre de la base de datos a `MyAdventureWorks`.  
  
    ```sql  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),   
        (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')   
        FOR ATTACH;  
    ```  
  
    > [!NOTE]  
    > También puede usar los procedimientos almacenados [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) o [sp_attach_single_file_db](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md) . Sin embargo, estos procedimientos almacenados se quitarán en una versión futura de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Se recomienda utilizar `CREATE DATABASE ... FOR ATTACH` en su lugar.  
  
##  <a name="FollowUp"></a> Seguimiento: Después de actualizar una base de datos de SQL Server  
Después de actualizar una base de datos mediante el método de adjuntarla, la base de datos queda disponible inmediatamente y se actualiza automáticamente. Si la base de datos tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, en función del valor de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la importación puede requerir varias horas y volver a generar puede requerir hasta diez veces más. Tenga en cuenta también que si la opción de actualización se establece en **Importar**y no hay disponible ningún catálogo de texto completo, se vuelven a generar los índices de texto completo asociados.  
  
Si el nivel de compatibilidad de una base de datos de usuario es 100 o superior antes de la actualización, permanece igual después de la misma. Si el nivel de compatibilidad es 90 antes de la actualización, en la base de datos actualizada, el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]
> Si va a adjuntar una base de datos de una instancia que ejecuta [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] o versiones anteriores que tenían una captura de datos de cambios (CDC) habilitada, también tendrá que ejecutar el comando siguiente para actualizar los metadatos de captura de datos de cambios (CDC).
  
```sql
USE <database name>
EXEC sys.sp_cdc_vupgrade  
``` 
 
## <a name="see-also"></a>Consulte también  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) 
 <br>[Administración de los metadatos cuando una base de datos pasa a estar disponible en otro servidor](manage-metadata-when-making-a-database-available-on-another-server.md)  
 [Separar una base de datos](../../relational-databases/databases/detach-a-database.md)  
  
  
