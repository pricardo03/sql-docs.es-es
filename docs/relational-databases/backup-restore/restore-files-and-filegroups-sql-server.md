---
title: Restaurar archivos y grupos de archivos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restorefilesandfilegrps.general.f1
- sql13.swb.bselectfilegrpsfiles.f1
- sql13.swb.restorefilesandfilegrps.options.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], restoring files and filegroups
- restoring [SQL Server], files
ms.assetid: 72603b21-3065-4b56-8b01-11b707911b05
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 81a832b4372dc2b35893c329d0b7ca909224fb9f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041508"
---
# <a name="restore-files-and-filegroups-sql-server"></a>Restaurar archivos y grupos de archivos (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo restaurar archivos y grupos de archivos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   [Seguridad](#Security)  
  
-   **Para restaurar archivos y grupos de archivos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El administrador del sistema encargado de restaurar los archivos y grupos de archivos debe ser la única persona que esté utilizando la base de datos que se vaya a restaurar.  
  
-   RESTORE no se permite en una transacción explícita o implícita.  
  
-   En el modelo de recuperación simple, el archivo debe pertenecer a un grupo de archivos de solo lectura.  
  
-   En el modelo de recuperación completa o el modelo de recuperación optimizado para cargas masivas de registros, para poder restaurar archivos, debe realizar una copia de seguridad del registro de transacciones activo (conocido como el final del registro). Para obtener más información, vea [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  
  
-   Para restaurar una base de datos cifrada, debe tener acceso al certificado o la clave asimétrica que se usó para cifrarla. La base de datos no se puede restaurar sin el certificado o la clave asimétrica. Como resultado, se debe conservar el certificado que se usa para cifrar la clave de cifrado de base de datos mientras se necesite la copia de seguridad. Para obtener más información, consulte [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Si la base de datos que se va a restaurar no existe, el usuario debe tener permisos CREATE DATABASE para poder ejecutar RESTORE. Si la base de datos existe, los permisos RESTORE corresponden de forma predeterminada a los miembros de los roles fijos de servidor **sysadmin** y **dbcreator** , y al propietario (**dbo**) de la base de datos (para la opción FROM DATABASE_SNAPSHOT, la base de datos siempre existe).  
  
 Los permisos RESTORE se conceden a los roles en los que la información acerca de la pertenencia está siempre disponible para el servidor. Debido a que la pertenencia a un rol fijo de base de datos solo se puede comprobar cuando la base de datos es accesible y no está dañada, lo que no siempre ocurre cuando se ejecuta RESTORE, los miembros del rol fijo de base de datos **db_owner** no tienen permisos RESTORE.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-restore-files-and-filegroups"></a>Para restaurar archivos y grupos de archivos  
  
1.  Después de conectarse a la instancia adecuada de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol.  
  
2.  Expanda **Bases de datos**. En función de la base de datos, seleccione una base de datos de usuario o expanda **Bases de datos del sistema**y, a continuación, seleccione una base de datos del sistema.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, después, haga clic en **Restaurar**.  
  
4.  Haga clic en **Archivos y grupos de archivos**para abrir el cuadro de diálogo **Restaurar archivos y grupos de archivos** .  
  
5.  En la página **General** , en el cuadro de lista **A una base de datos** , especifique la base de datos que desea restaurar. Puede especificar una nueva base de datos o elegir una base de datos existente de la lista desplegable. La lista incluye todas las bases de datos del servidor, y excluye las bases de datos del sistema **master** y **tempdb**.  
  
6.  Para especificar el origen y la ubicación de los conjuntos de copias de seguridad que se deben restaurar, haga clic en una de las opciones siguientes:  
  
    -   **Desde base de datos**  
  
         Escriba un nombre de base de datos en el cuadro de lista. La lista contiene solo las bases de datos de las que se ha realizado una copia de seguridad, según el historial de copias de seguridad de **msdb** .  
  
    -   **Desde dispositivo**  
  
         Haga clic en el botón Examinar. En el cuadro de diálogo **Especificar dispositivos de copia de seguridad** , seleccione uno de los tipos de dispositivo enumerados en el cuadro de lista **Tipo de medio de copia de seguridad** . Para seleccionar uno o varios dispositivos del cuadro de lista **Medio para copia de seguridad** , haga clic en **Agregar**.  
  
         Después de agregar los dispositivos que desee al cuadro de lista **Medio de copia de seguridad** , haga clic en **Aceptar** para volver a la página **General** .  
  
7.  En la cuadrícula **Seleccionar los conjuntos de copia de seguridad que se van a restaurar** , seleccione las copias de seguridad que desea restaurar. En esta cuadrícula se muestran las copias de seguridad disponibles en la ubicación especificada. De forma predeterminada, se sugiere un plan de recuperación. Para anular el plan de recuperación sugerido, puede cambiar las selecciones de la cuadrícula. Se anulará automáticamente la selección de aquellas copias de seguridad que dependan de una copia de seguridad cuya selección fue anulada.  
  
    |Encabezado de columna|Valores|  
    |-----------------|------------|  
    |**Restaurar**|Las casillas activadas indican los conjuntos de copias de seguridad que se restaurarán.|  
    |**Nombre**|Nombre del conjunto de copia de seguridad.|  
    |**Tipo de archivo**|Especifica el tipo de datos en la copia de seguridad: **Datos**, **Registro** o **Datos de FILESTREAM**. Los datos contenidos en tablas están en archivos de **datos** . Los datos del registro de transacciones están en archivos de **registro** . Los datos de objetos binarios grandes (BLOB) que están almacenados en el sistema de archivos se encuentran en archivos de **datos de FILESTREAM** .|  
    |**Tipo**|Tipo de copia de seguridad realizada: **Completa**, **Diferencial** o **Registro de transacciones**.|  
    |**Server**|Nombre de la instancia del motor de base de datos que ha realizado la operación de copia de seguridad.|  
    |**Nombre lógico de archivo**|Nombre lógico del archivo.|  
    |**Base de datos**|Nombre de la base de datos para la operación de copia de seguridad.|  
    |**Fecha de inicio**|Fecha y hora en la que se inició la operación de copia de seguridad, presentadas en la configuración regional del cliente.|  
    |**Fecha final**|Fecha y hora en la que finalizó la operación de copia de seguridad, presentadas en la configuración regional del cliente.|  
    |**Tamaño**|Tamaño del conjunto de copias de seguridad, en bytes.|  
    |**Nombre de usuario**|Nombre del usuario que realizó la operación de copia de seguridad.|  
  
8.  Para ver o seleccionar las opciones avanzadas, haga clic en **Opciones** en el panel **Seleccionar una página**.  
  
9. En el panel **Opciones de restauración** , puede elegir cualquiera de las opciones siguientes si son apropiadas para su situación.  
  
     **Restaurar como grupo de archivos**  
     Indica que se está restaurando un grupo de archivos completo.  
  
     **Sobrescribir la base de datos existente**  
     Especifica que la operación de restauración debe sobrescribir las bases de datos especificadas y sus archivos relacionados, aunque ya exista otra base de datos u otro archivo con el mismo nombre.  
  
     La elección de esta opción equivale a utilizar la opción REPLACE en una instrucción RESTORE de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
     **Preguntar antes de restaurar cada copia de seguridad**  
     Se le pedirá una confirmación antes de restaurar cada conjunto de copias de seguridad.  
  
     Esta opción es especialmente útil cuando hay que intercambiar cintas para distintos conjuntos de medios, como cuando el servidor dispone de un dispositivo de cinta.  
  
     **Restringir el acceso a la base de datos restaurada**  
     Hace que la base de datos restaurada esté disponible solo para los miembros de **db_owner**, **dbcreator**o **sysadmin**.  
  
     La selección de esta opción equivale al uso de la opción RESTRICTED_USER en una instrucción RESTORE de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
10. Si lo desea, puede restaurar la base de datos a una nueva ubicación si especifica un nuevo destino de restauración para cada archivo de la cuadrícula **Restaurar los archivos de base de datos como** .  
  
    |Encabezado de columna|Valores|  
    |-----------------|------------|  
    |**Nombre del archivo original**|La ruta de acceso completa de un archivo de copia de seguridad de origen.|  
    |**Tipo de archivo**|Especifica el tipo de datos en la copia de seguridad: **Datos**, **Registro** o **Datos de FILESTREAM**. Los datos contenidos en tablas están en archivos de **datos** . Los datos del registro de transacciones están en archivos de **registro** . Los datos de objetos binarios grandes (BLOB) que están almacenados en el sistema de archivos se encuentran en archivos de **datos de FILESTREAM** .|  
    |**Restaurar como**|La ruta de acceso completa del archivo de base de datos que se va a restaurar. Para especificar un nuevo archivo de restauración, haga clic en el cuadro de texto y edite la ruta de acceso y el nombre de archivo que aparecen de forma predeterminada. El hecho de cambiar la ruta de acceso o el nombre de archivo de la columna **Restaurar como** equivale a utilizar la opción MOVE en una instrucción RESTORE de [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
  
11. El panel **Estado de recuperación** determina el estado de la base de datos después de la operación de restauración.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     **Leave the database ready for use by rolling back the uncommitted transactions. Additional transaction logs cannot be restored. (RESTORE WITH RECOVERY)**  
     Recovers the database. This is the default behavior. Choose this option only if you are restoring all of the necessary backups now. This option is equivalent to specifying WITH RECOVERY in a [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE statement.  
  
     **Leave the database non-operational, and don't roll back the uncommitted transactions. Additional transaction logs can be restored. (RESTORE WITH NORECOVERY)**  
     Leaves the database in the restoring state. To recover the database, you will need to perform another restore using the preceding RESTORE WITH RECOVERY option (see above). This option is equivalent to specifying WITH NORECOVERY in a [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE statement.  
  
     If you select this option, the **Preserve replication settings** option is unavailable.  
  
     **Leave the database in read-only mode. Roll back the uncommitted transactions, but save the rollback operation in a file so the recovery effects can be undone. (RESTORE WITH STANDBY)**  
     Leaves the database in a standby state. This option is equivalent to specifying WITH STANDBY in a [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE statement.  
  
     Choosing this option requires that you specify a standby file.  
  
     **Rollback undo file**  
     Specify a standby file name in the **Rollback undo file** text box. This option is required if you leave the database in read-only mode (RESTORE WITH STANDBY).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-restore-files-and-filegroups"></a>Para restaurar archivos y grupos de archivos  
  
1.  Ejecute la instrucción RESTORE DATABASE para restaurar la copia de seguridad de archivos y grupos de archivos; para ello, especifique lo siguiente:  
  
    -   El nombre de la base de datos que se va a restaurar.  
  
    -   El dispositivo de copia de seguridad desde el que se restaurará la copia de seguridad completa de la base de datos.  
  
    -   La cláusula FILE de cada archivo que desee restaurar.  
  
    -   La cláusula FILEGROUP de cada grupo de archivos que desee restaurar.  
  
    -   La cláusula NORECOVERY. Si los archivos no se han modificado desde que se creó la copia de seguridad, especifique la cláusula RECOVERY.  
  
2.  Si los archivos se han modificado después de que se creara la copia de seguridad, ejecute la instrucción RESTORE LOG para aplicar la copia de seguridad del registro de transacciones y especifique:  
  
    -   El nombre de la base de datos a la que se aplicará el registro de transacciones.  
  
    -   El dispositivo de copia de seguridad desde el que se restaurará la copia de seguridad del registro de transacciones.  
  
    -   La cláusula NORECOVERY, si hay otra copia de seguridad del registro de transacciones que se deba aplicar después de la actual; de lo contrario, especifique la cláusula RECOVERY.  
  
         Las copias de seguridad del registro de transacciones, si se han aplicado, deben incluir el período de tiempo en el que se hizo la copia de seguridad de los archivos y grupos de archivos hasta el final del registro, a menos que se restauren TODOS los archivos de la base de datos.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En este ejemplo se restauran los archivos y grupos de archivos de la base de datos `MyDatabase` . Para restaurar la base de datos a la hora actual, se aplican dos registros de transacciones.  
  
```sql  
USE master;  
GO  
-- Restore the files and filesgroups for MyDatabase.  
RESTORE DATABASE MyDatabase  
   FILE = 'MyDatabase_data_1',  
   FILEGROUP = 'new_customers',  
   FILE = 'MyDatabase_data_2',  
   FILEGROUP = 'first_qtr_sales'  
   FROM MyDatabase_1  
   WITH NORECOVERY;  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyDatabase  
   FROM MyDatabase_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyDatabase  
   FROM MyDatabase_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Restaurar una copia de seguridad de registros de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
