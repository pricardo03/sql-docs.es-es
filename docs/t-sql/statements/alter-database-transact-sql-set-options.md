---
title: Opciones de ALTER DATABASE SET (Transact-SQL) | Microsoft Docs
description: Aprenda a configurar las opciones de base de datos, como la optimización automática, el cifrado y el almacén de consultas, en SQL Server y Azure SQL Database.
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- online database state [SQL Server]
- database options [SQL Server]
- emergency database state [SQL Server]
- databases [SQL Server], options
- read-only databases
- recovery models [SQL Server], switching
- ALTER DATABASE statement, SET options
- offline database state [SQL Server]
- snapshot isolation framework option
- checksums [SQL Server]
- automatic tuning
- SQL plan regression correction
- auto_create_statistics
- auto_update_statistics
- query store options
ms.assetid: f76fbd84-df59-4404-806b-8ecb4497c9cc
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current
ms.openlocfilehash: ecd914603883f83d5434327c5528688936aee420
ms.sourcegitcommit: 63c6f3758aaacb8b72462c2002282d3582460e0b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68495461"
---
# <a name="alter-database-set-options-transact-sql"></a>Opciones de ALTER DATABASE SET (Transact-SQL)

Establece opciones para la base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Para más información sobre otras opciones de ALTER DATABASE, consulte [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).

Haga clic en una de las pestañas siguientes para obtener la sintaxis, los argumentos, los comentarios, los permisos y los ejemplos de una versión de SQL concreta con la que está trabajando.

Para obtener más información sobre las convenciones de sintaxis, vea [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="click-a-product"></a>Haga clic en un producto.

En la siguiente fila, haga clic en cualquier nombre de producto que le interese. Al hacer clic, en esta página web se muestra otro contenido, adecuado para el producto que seleccione.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**\* _SQL Server \*_** &nbsp;|[Grupo de bases de datos elásticas o base de datos única de<br />SQL Database](alter-database-transact-sql-set-options.md?view=azuresqldb-current)|[Instancia administrada de<br />SQL Database](alter-database-transact-sql-set-options.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)|||

&nbsp;

## <a name="sql-server"></a>SQL Server

La creación de reflejo de la base de datos, [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], y los niveles de compatibilidad son opciones de `SET`, pero se describen en otros artículos debido a su extensión. Para más información, consulte [Creación de reflejo de la base de datos de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md), [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md) y [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).

Las configuraciones con ámbito de base de datos se utilizan para establecer varias configuraciones de base de datos en el nivel de base de datos individual. Para obtener más información, vea [ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

> [!NOTE]
> Es posible configurar muchas opciones SET de la base de datos para la sesión actual mediante [Instrucciones SET](../../t-sql/statements/set-statements-transact-sql.md), aunque generalmente las configuran las aplicaciones al realizar la conexión. Las opciones SET de nivel de sesión reemplazan a los valores **ALTER DATABASE SET** . Las opciones de base de datos descritas a continuación son valores que se pueden establecer en las sesiones que no proporcionan explícitamente otros valores de opciones SET.

## <a name="syntax"></a>Sintaxis

```
ALTER DATABASE { database_name | CURRENT }
SET
{
    <option_spec> [ ,...n ] [ WITH <termination> ]
}

<option_spec> ::=
{
    <auto_option>
  | <automatic_tuning_option>
  | <change_tracking_option>
  | <containment_option>
  | <cursor_option>
  | <database_mirroring_option>
  | <date_correlation_optimization_option>
  | <db_encryption_option>
  | <db_state_option>
  | <db_update_option>
  | <db_user_access_option>
  | <delayed_durability_option>
  | <external_access_option>
  | FILESTREAM ( <FILESTREAM_option> )
  | <HADR_options>
  | <mixed_page_allocation_option>
  | <parameterization_option>
  | <query_store_options>
  | <recovery_option>
  | <remote_data_archive_option>
  | <service_broker_option>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <termination>
  | <temporal_history_retention>
}
;

<auto_option> ::=
{
    AUTO_CLOSE { ON | OFF }
  | AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }
  | AUTO_SHRINK { ON | OFF }
  | AUTO_UPDATE_STATISTICS { ON | OFF }
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}

<automatic_tuning_option> ::=
{
  AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { ON | OFF } )
}

<change_tracking_option> ::=
{
  CHANGE_TRACKING
   {
       = OFF
     | = ON [ ( <change_tracking_option_list > [,...n] ) ]
     | ( <change_tracking_option_list> [,...n] )
   }
}

<change_tracking_option_list> ::=
   {
       AUTO_CLEANUP = { ON | OFF }
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }
   }

<containment_option> ::=
   CONTAINMENT = { NONE | PARTIAL }

<cursor_option> ::=
{
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }
  | CURSOR_DEFAULT { LOCAL | GLOBAL }
}

<database_mirroring_option>
  ALTER DATABASE Database Mirroring

<date_correlation_optimization_option> ::=
    DATE_CORRELATION_OPTIMIZATION { ON | OFF }
  
<db_encryption_option> ::=
    ENCRYPTION { ON | OFF | SUSPEND | RESUME }

<db_state_option> ::=
    { ONLINE | OFFLINE | EMERGENCY }

<db_update_option> ::=
    { READ_ONLY | READ_WRITE }

<db_user_access_option> ::=
    { SINGLE_USER | RESTRICTED_USER | MULTI_USER }

<delayed_durability_option> ::=
    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }

<external_access_option> ::=
{
    DB_CHAINING { ON | OFF }
  | TRUSTWORTHY { ON | OFF }
  | DEFAULT_FULLTEXT_LANGUAGE = { <lcid> | <language name> | <language alias> }
  | DEFAULT_LANGUAGE = { <lcid> | <language name> | <language alias> }
  | NESTED_TRIGGERS = { OFF | ON }
  | TRANSFORM_NOISE_WORDS = { OFF | ON }
  | TWO_DIGIT_YEAR_CUTOFF = { 1753, ..., 2049, ..., 9999 }
}
<FILESTREAM_option> ::=
{
    NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL
  | DIRECTORY_NAME = <directory_name>
}
<HADR_options> ::=
    ALTER DATABASE SET HADR

<mixed_page_allocation_option> ::=
    MIXED_PAGE_ALLOCATION { OFF | ON }

<parameterization_option> ::=
    PARAMETERIZATION { SIMPLE | FORCED }

<query_store_options> ::=
{
    QUERY_STORE
    {
          = OFF
        | = ON [ ( <query_store_option_list> [,...n] ) ]
        | ( < query_store_option_list> [,...n] )
        | CLEAR [ ALL ]
    }
}

<query_store_option_list> ::=
{
      OPERATION_MODE = { READ_WRITE | READ_ONLY }
    | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )
    | DATA_FLUSH_INTERVAL_SECONDS = number
    | MAX_STORAGE_SIZE_MB = number
    | INTERVAL_LENGTH_MINUTES = number
    | SIZE_BASED_CLEANUP_MODE = { AUTO | OFF }
    | QUERY_CAPTURE_MODE = { ALL | AUTO | CUSTOM | NONE }
    | MAX_PLANS_PER_QUERY = number
    | WAIT_STATS_CAPTURE_MODE = { ON | OFF }
    | QUERY_CAPTURE_POLICY = ( <query_capture_policy_option_list> [,...n] )
}

<query_capture_policy_option_list> :: =
{
    STALE_CAPTURE_POLICY_THRESHOLD = number { DAYS | HOURS }
    | EXECUTION_COUNT = number
    | TOTAL_COMPILE_CPU_TIME_MS = number
    | TOTAL_EXECUTION_CPU_TIME_MS = number      
}

<recovery_option> ::=
{
    RECOVERY { FULL | BULK_LOGGED | SIMPLE }
  | TORN_PAGE_DETECTION { ON | OFF }
  | PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }
}

<remote_data_archive_option> ::=
{
    REMOTE_DATA_ARCHIVE =
    {
        ON ( SERVER = <server_name> ,
                  {CREDENTIAL = <db_scoped_credential_name>
                     | FEDERATED_SERVICE_ACCOUNT = ON | OFF
                  }
               )
      | OFF
    }
}

<service_broker_option> ::=
{
    ENABLE_BROKER
  | DISABLE_BROKER
  | NEW_BROKER
  | ERROR_BROKER_CONVERSATIONS  
  | HONOR_BROKER_PRIORITY { ON | OFF}
}

<snapshot_option> ::=
{
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }
  | READ_COMMITTED_SNAPSHOT {ON | OFF }
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = {ON | OFF }
}
<sql_option> ::=
{
    ANSI_NULL_DEFAULT { ON | OFF }
  | ANSI_NULLS { ON | OFF }
  | ANSI_PADDING { ON | OFF }
  | ANSI_WARNINGS { ON | OFF }
  | ARITHABORT { ON | OFF }
  | COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 | 90 }
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }
  | NUMERIC_ROUNDABORT { ON | OFF }
  | QUOTED_IDENTIFIER { ON | OFF }
  | RECURSIVE_TRIGGERS { ON | OFF }
}

<target_recovery_time_option> ::=
    TARGET_RECOVERY_TIME = target_recovery_time { SECONDS | MINUTES }

<termination>::=
{
    ROLLBACK AFTER number [ SECONDS ]
  | ROLLBACK IMMEDIATE
  | NO_WAIT
}
<temporal_history_retention>::=TEMPORAL_HISTORY_RETENTION { ON | OFF }
```

## <a name="arguments"></a>Argumentos

*database_name*         
Es el nombre de la base de datos que se va a modificar.

CURRENT         
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Ejecuta la acción de la base de datos actual. `CURRENT` no se admite para todas las opciones en todos los contextos. Si `CURRENT` produce un error, proporcione el nombre de la base de datos.

**\<auto_option> ::=**        

Controla las opciones automáticas.        

<a name="auto_close"></a> AUTO_CLOSE { ON | OFF }         
ON         
La base de datos se cierra correctamente y se liberan sus recursos después de que salga el último usuario.

La base de datos se vuelve a abrir automáticamente cuando un usuario intenta utilizarla de nuevo. Por ejemplo, al generar una instrucción `USE database_name`. La base de datos puede cerrarse limpiamente con la opción AUTO_CLOSE establecida en ON. Si es así, la base de datos no se vuelve a abrir hasta que un usuario intente usar la base de datos la próxima vez que [!INCLUDE[ssDE](../../includes/ssde-md.md)] se reinicie.

OFF         
La base de datos permanece abierta después de que haya salido el último usuario.

La opción AUTO_CLOSE es útil para las bases de datos de escritorio porque permite administrar los archivos de la base de datos como archivos normales. Se pueden mover, copiar para realizar copias de seguridad e incluso enviar por correo electrónico a otros usuarios. El proceso AUTO_CLOSE es asincrónico. La apertura y cierre repetidos de la base de datos no reduce el rendimiento.

> [!NOTE]
> La opción AUTO_CLOSE no está disponible en una base de datos independiente o en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
> Puede determinar el estado de esta opción si examina la columna is_auto_close_on de la vista de catálogo sys.databases o la propiedad IsAutoClose de la función DATABASEPROPERTYEX.
>
> Si AUTO_CLOSE es ON, algunas columnas de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) y de la función DATABASEPROPERTYEX devuelven NULL porque la base de datos no está disponible para recuperar los datos. Para resolver este problema, ejecute la instrucción USE para abrir la base de datos.
>
> La creación de reflejo de la base de datos requiere AUTO_CLOSE OFF.

Cuando la base de datos se establece en AUTOCLOSE = ON, una operación que inicia el cierre automático de la base de datos borra la caché de planes para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al borrar la memoria caché de planes, se provoca una nueva compilación de todos los planes de ejecución posteriores y puede ocasionar una disminución repentina y temporal del rendimiento de las consultas. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 y posterior, para cada almacén de caché borrado de la memoria caché de planes, el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contendrá el siguiente mensaje informativo: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado %d instancias de vaciado del almacén de caché "%s" (parte de la memoria caché de planes) debido a determinadas operaciones de mantenimiento de base de datos o reconfiguración". Este mensaje se registra cada cinco minutos siempre que se vacíe la memoria caché dentro de ese intervalo de tiempo.

<a name="auto_create_statistics"></a> AUTO_CREATE_STATISTICS { ON | OFF }         
ON         
El optimizador de consultas crea las estadísticas en columnas únicas de los predicados de consulta, según sea necesario, para mejorar los planes de consulta y el rendimiento de las consultas. Estas estadísticas de columna única se crean cuando el optimizador de consultas las compila. Las estadísticas de columna única solamente se crean en las columnas que ya no son la primera columna de un objeto de estadísticas existente.

El valor predeterminado es ON. Recomendamos utilizar la configuración predeterminada para la mayoría de las bases de datos.

OFF         
El optimizador de consultas no crea estadísticas en columnas únicas de los predicados de consulta cuando está compilando consultas. Establecer esta opción en OFF puede producir planes de consulta poco óptimos y un rendimiento degradado de las consultas.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_create_stats_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAutoCreateStatistics de la función DATABASEPROPERTYEX.

Para más información, vea la sección "Utilizar las opciones de estadísticas de toda la base de datos" del tema [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

INCREMENTAL = ON | OFF         
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Establezca AUTO_CREATE_STATISTICS en ON y establezca INCREMENTAL en ON. Esta configuración crea automáticamente estadísticas como incrementales siempre que se admitan estadísticas incrementales. El valor predeterminado es OFF. Para más información, consulte [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md).

<a name="auto_shrink"></a> AUTO_SHRINK { ON | OFF }     
ON         
Los archivos de la base de datos se pueden reducir periódicamente.

Pueden reducirse automáticamente los archivos de datos y los archivos de registro. AUTO_SHRINK reduce el tamaño del registro de transacciones solo si establece la base de datos en el modelo de recuperación SIMPLE o si realiza una copia de seguridad del registro. Cuando se establece en OFF, los archivos de la base de datos no se reducen de forma automática durante las comprobaciones periódicas del espacio no utilizado.

La opción AUTO_SHRINK reduce los archivos cuando no se utiliza más de un 25% del espacio del archivo. La opción hace que el archivo se reduzca a uno de dos tamaños. Se reduce al que sea más grande de los siguientes:

- el tamaño donde el 25 por ciento del archivo es espacio no utilizado
- el tamaño del archivo cuando se creó

No puede reducir una base de datos de solo lectura.

OFF         
Los archivos de la base de datos no se reducen automáticamente durante las comprobaciones periódicas del espacio no utilizado.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_shrink_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAutoShrink de la función DATABASEPROPERTYEX.

> [!NOTE]
> La opción AUTO_SHRINK no está disponible en una base de datos independiente.

<a name="auto_update_statistics"></a> AUTO_UPDATE_STATISTICS { ON | OFF }         
ON         
Especifica que el optimizador de consultas actualiza las estadísticas cuando son usadas por una consulta y pudieran estar obsoletas. Las estadísticas se vuelven obsoletas después de que operaciones de inserción, actualización, eliminación o combinación cambien la distribución de los datos en la tabla o la vista indizada. El Optimizador de consultas determina cuándo las estadísticas pueden quedar obsoletas contando el número de modificaciones de datos desde la actualización más reciente de las estadísticas, comparando el número de modificaciones con respecto a un umbral. El umbral se basa en el número de filas de la tabla o la vista indizada.

El optimizador de consultas comprueba que hay estadísticas obsoletas antes de que compile una consulta y ejecuta un plan de consulta almacenado en caché. El optimizador de consultas utiliza las columnas, tablas y vistas indexadas en el predicado de consulta para determinar qué estadísticas podrían estar obsoletas. El optimizador de consultas determina esta información antes de compilar una consulta. Antes de ejecutar un plan de consulta almacenado en la memoria caché, [!INCLUDE[ssDE](../../includes/ssde-md.md)] comprueba que el plan de consulta hace referencia a las estadísticas actualizadas.

La opción AUTO_UPDATE_STATISTICS se aplica a las estadísticas creadas para índices y columnas únicas de los predicados de consulta, así como a las estadísticas creadas con la instrucción CREATE STATISTICS. Esta opción también se aplica a las estadísticas filtradas.

El valor predeterminado es ON. Recomendamos utilizar la configuración predeterminada para la mayoría de las bases de datos.

Utilice la opción AUTO_UPDATE_STATISTICS_ASYNC para especificar si las estadísticas se actualizan sincrónica o asincrónicamente.

OFF         
Especifica que el optimizador de consultas no actualiza las estadísticas cuando una consulta las utiliza. El optimizador de consultas tampoco actualiza las estadísticas cuando podrían estar obsoletas. Establecer esta opción en OFF puede producir planes de consulta poco óptimos y un rendimiento degradado de las consultas.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_update_stats_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAutoUpdateStatistics de la función DATABASEPROPERTYEX.

Para más información, vea la sección "Utilizar las opciones de estadísticas de toda la base de datos" del tema [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

<a name="auto_update_statistics_async"></a> AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }         
ON         
Especifica que las actualizaciones de las estadísticas para la opción AUTO_UPDATE_STATISTICS son asincrónicas. El optimizador de consultas no espera a que finalicen las actualizaciones de las estadísticas para compilar las consultas.

La configuración de esta opción en ON no surte efecto a menos que AUTO_UPDATE_STATISTICS se establezca en ON.

De forma predeterminada, la opción AUTO_UPDATE_STATISTICS_ASYNC está configurada en OFF y el optimizador de consultas actualiza las estadísticas sincrónicamente.

OFF         
Especifica que las actualizaciones de las estadísticas para la opción AUTO_UPDATE_STATISTICS son sincrónicas. El optimizador de consultas espera a que finalicen las actualizaciones de las estadísticas para compilar las consultas.

La configuración de esta opción en OFF no surte efecto a menos que AUTO_UPDATE_STATISTICS esté configurado en ON.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_update_stats_async_on en la vista de catálogo sys.databases.

Para saber más sobre cuándo usar las actualizaciones de estadísticas sincrónicas o asincrónicas, vea la sección "Utilizar las opciones de estadísticas de toda la base de datos" del tema [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

<a name="auto_tuning"></a> **\<automatic_tuning_option> ::=**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)])

Habilita o deshabilita la opción [Ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md) de `FORCE_LAST_GOOD_PLAN`.

FORCE_LAST_GOOD_PLAN = { ON | OFF }         
ON         
El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] fuerza automáticamente el último buen plan conocido en las consultas de [!INCLUDE[tsql-md](../../includes/tsql-md.md)], donde el nuevo plan de SQL provoca regresiones de rendimiento. El parámetro [!INCLUDE[ssde_md](../../includes/ssde_md.md)] supervisa continuamente el rendimiento de la consulta [!INCLUDE[tsql-md](../../includes/tsql-md.md)] con el plan forzado.

Si hay mejoras de rendimiento, el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] seguirá usando el último buen plan conocido. Si no se detectan mejoras de rendimiento, el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] generará un nuevo plan de SQL. La instrucción generará un error si el Almacén de consultas no está habilitado o si no está en modo de *lectura-escritura*.

OFF         
El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] informa de posibles regresiones de rendimiento de consultas provocadas por cambios de plan de SQL en la vista [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md), aunque estas recomendaciones no se aplican automáticamente. Para supervisar las recomendaciones activas y corregir los problemas identificados, los usuarios pueden aplicar los scripts de [!INCLUDE[tsql-md](../../includes/tsql-md.md)] que se muestran en la vista. Este es el valor predeterminado.

**\<change_tracking_option> ::=**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y[!INCLUDE[ssSDSFull](../../includes/sssds-md.md)]

Controla las opciones de seguimiento de cambios. Puede habilitar el seguimiento de cambios, establecer y cambiar opciones, y deshabilitar el seguimiento de cambios. Para ver ejemplos, consulte la sección de ejemplos más adelante en este artículo.

ON         
Habilita el seguimiento de cambios para la base de datos. Si habilita el seguimiento de cambios, también puede establecer las opciones AUTO CLEANUP y CHANGE RETENTION.

AUTO_CLEANUP = { ON | OFF }        
ON         
La información sobre el seguimiento de cambios se quita de forma automática después del período de retención especificado.

OFF         
Los datos del seguimiento de cambios no se quitan de la base de datos.

CHANGE_RETENTION =*retention_period* { DAYS | HOURS | MINUTES }       

Especifica el período mínimo para mantener la información del seguimiento de cambios en la base de datos. Los datos solamente se quitan cuando el valor AUTO_CLEANUP es ON.

*retention_period* es un entero que especifica el componente numérico del período de retención.

El período de retención predeterminado es de 2 días. El período de retención mínimo es de 1 minuto. El tipo de retención predeterminado es DAYS.

OFF         
Deshabilita el seguimiento de cambios para la base de datos. Deshabilite el seguimiento de cambios en todas las tablas para poder deshabilitarlo en la base de datos.

**\<containment_option> ::=**          
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Controla las opciones de contención de la base de datos.

CONTAINMENT = { NONE | PARTIAL}         
Ninguno         
La base de datos no es una base de datos independiente.

PARTIAL         
La base de datos es una base de datos independiente. El establecimiento de la contención de la base de datos en parcial producirá un error si la base de datos tiene habilitados la replicación, la captura de datos modificados o el seguimiento de cambios. La comprobación de errores se detiene después de un error. Para obtener más información acerca de las bases de datos independientes, vea [Contained Databases](../../relational-databases/databases/contained-databases.md).

**\<cursor_option> ::=**        

Controla las opciones del cursor.

CURSOR_CLOSE_ON_COMMIT { ON | OFF }         
ON         
Todos los cursores abiertos cuando confirma o deshace una transacción se cierran.

OFF         
Los cursores permanecen abiertos cuando se confirma una transacción. Cuando se revierte se cierran todos los cursores, excepto los que están definidos como INSENSITIVE o STATIC.

La configuración del nivel de conexión, establecida mediante la instrucción SET, invalida la configuración predeterminada de la base de datos para CURSOR_CLOSE_ON_COMMIT. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión que establece CURSOR_CLOSE_ON_COMMIT en OFF para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md).

Puede determinar el estado de esta opción si examina la columna is_cursor_close_on_commit_on de la vista de catálogo sys.databases o la propiedad IsCloseCursorsOnCommitEnabled de la función DATABASEPROPERTYEX.

CURSOR_DEFAULT { LOCAL | GLOBAL }         
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Controla si el ámbito del cursor utiliza LOCAL o GLOBAL.

LOCAL         
Cuando especifica LOCAL y no define un cursor como GLOBAL cuando crea el cursor, el alcance del cursor es local. Específicamente, el alcance es local para el proceso por lotes, el procedimiento almacenado o el activador en el que creó el cursor. El nombre del cursor solamente es válido dentro de este ámbito.

Es posible hacer referencia al cursor mediante variables de cursor locales del lote, procedimiento almacenado, desencadenador o parámetro OUTPUT del procedimiento almacenado. La asignación del cursor se desasigna implícitamente cuando el lote, el procedimiento almacenado o el desencadenador finaliza. El cursor se desasigna a menos que se haya pasado de nuevo en un parámetro OUTPUT. El cursor se podría pasar en un parámetro OUTPUT. Si el cursor se vuelve a pasar de esta forma, se desasigna cuando la última variable que hace referencia a él se desasigna o se sale del ámbito.

GLOBAL         
Si se especifica GLOBAL y no se define ningún cursor como LOCAL al crearlo, el ámbito del cursor es global para la conexión. Se puede hacer referencia al nombre del cursor en cualquier procedimiento almacenado o lote que se ejecute durante la conexión.

El cursor se desasigna implícitamente solamente cuando se realiza la desconexión. Para más información, consulte [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_local_cursor_default en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsLocalCursorsDefault de la función DATABASEPROPERTYEX.

**\<database_mirroring>**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Para las descripciones del argumento, consulte [Creación de reflejo de la base de datos de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md).

**\<date_correlation_optimization_option> ::=**         
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Controla la opción date_correlation_optimization.

DATE_CORRELATION_OPTIMIZATION { ON | OFF }         
ON         
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene estadísticas de correlación donde una restricción FOREIGN KEY vincula dos tablas cualesquiera en la base de datos y las tablas tienen columnas **datetime**.

OFF         
No se mantiene ninguna estadística de correlación.

Para establecer DATE_CORRELATION_OPTIMIZATION en ON, no debe haber ninguna conexión activa con la base de datos, salvo la conexión que está ejecutando la instrucción ALTER DATABASE. Después se admitirán múltiples conexiones.

La configuración actual de esta opción se puede determinar mediante el examen de la columna is_date_correlation_on de la vista de catálogo sys.databases.

**\<db_encryption_option> ::=**        

Controla el estado del cifrado de la base de datos.

ENCRYPTION {ON | OFF | SUSPEND | RESUME}         
ON         
Establece la base de datos que se va a cifrar.

OFF         
Establece la base de datos que no se va a cifrar. 

SUSPEND         
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)])         
Puede utilizarse para pausar el examen de cifrado después de que el cifrado de datos transparente se haya habilitado o deshabilitado, o después de cambiar la clave de cifrado.

RESUME         
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)])         
Se puede usar para reanudar un examen de cifrado pausado anteriormente.

Para más información sobre el cifrado de base de datos, consulte [Cifrado de datos transparente](../../relational-databases/security/encryption/transparent-data-encryption.md) y [Cifrado de datos transparente con Azure SQL Database](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).

Cuando el cifrado está habilitado en el nivel de la base de datos, se cifrarán todos los grupos de archivos. Todos los grupos de archivos nuevos heredarán la propiedad de cifrado. Si en la base de datos hay grupos de archivos establecidos en **READ ONLY**, se producirá un error en la operación de cifrado de la base de datos.

Puede ver el estado del cifrado de la base de datos, así como el estado del análisis de cifrado, mediante la vista de administración dinámica [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md).

**\<db_state_option> ::=**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Controla el estado de la base de datos.

OFFLINE         
La base de datos está cerrada, se ha cerrado correctamente y se ha marcado como sin conexión. La base de datos no se puede modificar mientras está desconectada.

ONLINE         
La base de datos está abierta y disponible para su uso.

EMERGENCY         
La base de datos está marcada como READ_ONLY, el registro está deshabilitado y el acceso está limitado a miembros del rol fijo de servidor sysadmin. EMERGENCY se utiliza principalmente para la solución de problemas. Por ejemplo, una base de datos marcada como sospechosa debido a un archivo de registro dañado se puede establecer en el estado EMERGENCY. Este valor puede habilitar el acceso de solo lectura del administrador del sistema a la base de datos. Solamente los miembros del rol fijo de servidor sysadmin pueden establecer una base de datos en el estado EMERGENCY.

> [!NOTE]
> **Permisos:** se necesita el permiso `ALTER DATABASE` para la base de datos de asunto con el fin de cambiar una base de datos al estado Sin conexión o Emergencia. Se requiere el permiso `ALTER ANY DATABASE` de nivel de servidor para mover una base de datos de Sin conexión a En línea.

Puede determinar el estado de esta opción mediante las columnas state y state_desc en la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). También puede determinar el estado mediante el examen de la propiedad Status de la función [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md). Para más información, consulte [Database States](../../relational-databases/databases/database-states.md).

Una base de datos marcada como RESTORING no se puede establecer como OFFLINE, ONLINE o EMERGENCY. Es posible que una base de datos se encuentre en estado RESTORING durante una operación de restauración activa o cuando se produce un error en una operación de restauración de una base de datos o de un archivo de registro, debido a un archivo de copia de seguridad dañado.

**\<db_update_option> ::=**       

Controla si se permiten las actualizaciones en la base de datos.

READ_ONLY         
Los usuarios pueden leer datos de la base de datos, pero no pueden modificarlos.

> [!NOTE]
> Para mejorar el rendimiento de las consultas, actualice las estadísticas antes de establecer una base de datos en READ_ONLY. Si se necesitan estadísticas adicionales después de establecer una base de datos en READ_ONLY, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] creará las estadísticas en tempdb. Para más información sobre las estadísticas para una base de datos de solo lectura, vea [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

READ_WRITE         
La base de datos está disponible para operaciones de lectura y escritura.

Para cambiar este estado, debe tener acceso exclusivo a la base de datos. Para obtener más información, vea la cláusula SINGLE_USER.

> [!NOTE]
> En las bases de datos federadas de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], SET { READ_ONLY | READ_WRITE } está deshabilitado.

**\<db_user_access_option> ::=**      

Controla el acceso del usuario a la base de datos.

SINGLE_USER         
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Especifica que solamente puede tener acceso a la base de datos un usuario cada vez. Si especifica SINGLE_USER y otros usuarios se conectan a la base de datos, la instrucción ALTER DATABASE se bloquea hasta que todos los usuarios se desconecten de la base de datos especificada. Para invalidar este comportamiento, vea la cláusula WITH \<termination>.

La base de datos permanece en modo SINGLE_USER incluso si el usuario que estableció la opción cierra la sesión. A partir de ese momento, un usuario distinto, pero solo uno, puede conectarse a la base de datos.

Antes de establecer la base de datos como SINGLE_USER, compruebe que la opción AUTO_UPDATE_STATISTICS_ASYNC está establecida en OFF. Cuando se establece en ON, el subproceso en segundo plano usado para actualizar las estadísticas realiza una conexión con la base de datos y no se podrá acceder a la base de datos en modo de usuario único. Para ver el estado de esta opción, consulte la columna is_auto_update_stats_async_on en la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). Si la opción está establecida en ON, realice las tareas siguientes:

1. Establezca AUTO_UPDATE_STATISTICS_ASYNC en OFF.

2. Compruebe si hay trabajos de estadísticas asincrónicos consultando la vista de administración dinámica [sys.dm_exec_background_job_queue](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md).

Si hay trabajos activos, permita que estos se completen o termínelos de forma manual mediante [KILL STATS JOB](../../t-sql/language-elements/kill-stats-job-transact-sql.md).

RESTRICTED_USER         
Solo permite a los miembros del rol fijo de base de datos `db_owner` y de los roles fijos de servidor `dbcreator` y `sysadmin` conectarse a la base de datos. RESTRICTED_USER no limita su número. Desconecte todas las conexiones con la base de datos mediante el margen de tiempo especificado por la cláusula de terminación de la instrucción ALTER DATABASE. Una vez que la base de datos ha cambiado al estado RESTRICTED_USER, se rechazan los intentos de conexión por parte de usuarios no cualificados.

MULTI_USER         
Todos los usuarios que tengan los permisos correspondientes pueden conectarse a la base de datos.

Puede determinar el estado de esta opción mediante el examen de la columna user_access en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad UserAccess de la función DATABASEPROPERTYEX.

**\<delayed_durability_option> ::=**          
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Controla si las transacciones se confirman con perdurabilidad total o diferida.

DISABLED         
Todas las transacciones tras SET DISABLED son totalmente perdurables. Se omiten las opciones de perdurabilidad que se establecen en un bloque ATOMIC o en una instrucción de confirmación.

ALLOWED         
Todas las transacciones tras SET ALLOWED son totalmente perdurables o de perdurabilidad diferida, dependiendo de la opción de perdurabilidad establecida en el bloque ATOMIC o instrucción de confirmación.

FORCED         
Todas las transacciones tras SET FORCED son totalmente perdurables. Se omiten las opciones de perdurabilidad que se establecen en un bloque ATOMIC o en una instrucción de confirmación.

**\<external_access_option> ::=**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Controla si recursos externos como los objetos de otra base de datos pueden tener acceso a la base de datos.

DB_CHAINING { ON | OFF }         
ON         
La base de datos puede ser el origen o el destino de un encadenamiento de propiedad entre bases de datos.

OFF         
La base de datos no puede participar en el encadenamiento de propiedad entre bases de datos.

> [!IMPORTANT]
> La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconoce esta configuración si la opción del servidor cross db ownership chaining server es 0 (OFF). Si cross db ownership chaining es 1 (ON), todas las bases de datos de usuario pueden participar en cadenas de propiedad entre bases de datos, independientemente del valor de esta opción. Esta opción se establece mediante [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).

Para establecer esta opción, se necesita el permiso CONTROL SERVER en la base de datos.

La opción DB_CHAINING no se puede establecer en estas bases de datos del sistema: maestra, modelo y tempdb.

Puede determinar el estado de esta opción mediante el examen de la columna is_db_chaining_on en la vista de catálogo sys.databases.

TRUSTWORTHY { ON | OFF }         
ON         
Los módulos de base de datos (por ejemplo, las funciones definidas por el usuario o los procedimientos almacenados) que utilizan un contexto de suplantación pueden tener acceso a recursos externos a la base de datos.

OFF         
Los módulos de base de datos en un contexto de suplantación no pueden tener acceso a recursos externos a la base de datos.

TRUSTWORTHY se establece en OFF siempre que la base de datos se adjunta.

De forma predeterminada, el valor TRUSTWORTHY se establece en OFF en todas las bases de datos de sistema, excepto msdb. No es posible cambiar este valor para las bases de datos model y tempdb. Se recomienda no establecer la opción TRUSTWORTHY en ON en la base de datos maestra.

Para establecer esta opción, se requiere el permiso de `CONTROL SERVER` en la base de datos.

Puede determinar el estado de esta opción mediante el examen de la columna is_trustworthy_on en la vista de catálogo sys.databases.

DEFAULT_FULLTEXT_LANGUAGE         
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Especifica el valor de idioma predeterminado para las columnas indizadas de texto completo.

> [!IMPORTANT]
> Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.

DEFAULT_LANGUAGE         
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Especifica el idioma predeterminado de los nuevos inicios de sesión creados. El idioma se puede especificar proporcionando el identificador local (LCID), el nombre de idioma o el alias de idioma. Para una lista de nombres y alias de idioma aceptables, consulte [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md). Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.

NESTED_TRIGGERS         
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Especifica si un desencadenador AFTER puede actuar en cascada; es decir, realizar una acción que inicia otro desencadenador que, a su vez, inicia otro desencadenador, etc. Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.

TRANSFORM_NOISE_WORDS         
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Se utiliza para suprimir un mensaje de error si las palabras irrelevantes producen un error en una operación booleana en una consulta de texto completo. Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.

TWO_DIGIT_YEAR_CUTOFF         
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Especifica un número entero comprendido entre 1753 y 9999 que representa el año límite para interpretar años de dos dígitos como años de cuatro dígitos. Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.

**\<FILESTREAM_option> ::=**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Controla los valores de objetos FileTable.

NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }         
OFF         
El acceso no transaccional a los datos de FileTable está deshabilitado.

READ_ONLY         
Los procesos no transaccionales pueden leer datos FILESTREAM en los objetos FileTable de esta base de datos.

FULL         
Permite el acceso no transaccional completo a datos de FILESTREAM en objetos FileTable.

DIRECTORY_NAME = *\<directory_name>*          
Un nombre de directorio compatible con Windows. Este nombre debe ser único entre todos los nombres de directorio de nivel de base de datos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La comparación de unicidad no distingue mayúsculas de minúsculas, independientemente de la configuración de intercalación. Esta opción se debe establecer antes de crear un objeto FileTable en esta base de datos.

**\<HADR_options> ::=**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Consulte [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md).

**\<mixed_page_allocation_option> ::=**          
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Controla si la base de datos puede crear páginas iniciales con una extensión mixta para las primeras ocho páginas de una tabla o un índice.

MIXED_PAGE_ALLOCATION { OFF | ON }         
OFF         
La base de datos siempre crea páginas iniciales mediante extensiones uniformes. OFF Es el valor predeterminado.

ON         
La base de datos puede crear páginas iniciales mediante extensiones mixtas.

Esta opción es ON para todas las bases de datos del sistema. **tempdb** es la única base de datos del sistema que admite OFF.

**\<PARAMETERIZATION_option> ::=**         

Controla la opción de parametrización. Para obtener más información sobre la parametrización, vea la [Guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md#SimpleParam).

PARAMETERIZATION { SIMPLE | FORCED }         
SIMPLE         
Las consultas incluyen parámetros en función del comportamiento predeterminado de la base de datos.

FORCED         
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye parámetros para todas las consultas de la base de datos.

La configuración actual de esta opción se puede determinar mediante el examen de la columna is_parameterization_forced de la vista de catálogo sys.databases.

**\<query_store_options> ::=**          
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

ON | OFF | CLEAR [ ALL ]         
Controla si el almacén de consultas está habilitado en esta base de datos y también controla la eliminación del contenido del almacén de consultas. Para obtener más información, vea [Escenarios de uso del Almacén de consultas](../../relational-databases/performance/query-store-usage-scenarios.md).     

ON         
Habilita el almacén de consultas.

OFF         
Deshabilita el almacén de consultas. OFF Es el valor predeterminado.

CLEAR         
Quita el contenido del almacén de consultas.

> [!NOTE]
> En [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], debe ejecutar `ALTER DATABASE SET QUERY_STORE` desde la base de datos de usuario. No se admite la ejecución de la instrucción desde otra instancia de almacén de datos.

OPERATION_MODE { READ_ONLY | READ_WRITE }         
Describe el modo de operación del almacén de consultas. 

READ_WRITE         
El almacén de consultas recopila y continúa el plan de consultas y la información de estadística del tiempo de ejecución. 

READ_ONLY         
La información se puede leer del almacén de consultas, pero no se agrega información nueva. Si se ha agotado el espacio máximo emitido del almacén de consultas, el almacén de consultas cambiará el modo de operación a READ_ONLY.

CLEANUP_POLICY         
Describe la directiva de retención de datos del almacén de consultas. STALE_QUERY_THRESHOLD_DAYS determina el número de días durante los que se conserva la información de una consulta en el almacén de consultas. STALE_QUERY_THRESHOLD_DAYS es de tipo **bigint**.

DATA_FLUSH_INTERVAL_SECONDS         
Determina la frecuencia con la que los datos escritos en el almacén de consultas se conservan en el disco. Para optimizar el rendimiento, los datos recopilados por el almacén de consultas se escriben de manera asincrónica en el disco. La frecuencia con la que se produce esta transferencia asincrónica se configura mediante el argumento DATA_FLUSH_INTERVAL_SECONDS. DATA_FLUSH_INTERVAL_SECONDS es de tipo **bigint**.
 
MAX_STORAGE_SIZE_MB         
Determina el espacio emitido en el almacén de consultas. MAX_STORAGE_SIZE_MB es de tipo **bigint**.

INTERVAL_LENGTH_MINUTES         
Determina el intervalo de tiempo en el que se agregan los datos de estadísticas de ejecución en tiempo de ejecución al almacén de consultas. Para optimizar el uso del espacio, se agregan las estadísticas de ejecución en tiempo de ejecución en el almacén de estadísticas de tiempo de ejecución en una ventana de tiempo fijo. Esta ventana de tiempo fijo se configura con el argumento INTERVAL_LENGTH_MINUTES. INTERVAL_LENGTH_MINUTES es de tipo **bigint**.

SIZE_BASED_CLEANUP_MODE { AUTO | OFF }         
Controla si la limpieza se activa automáticamente cuando la cantidad total de datos se acerca al tamaño máximo.

AUTO         
La limpieza según el tamaño se activará automáticamente cuando el tamaño en disco alcance el 90 % de **max_storage_size_mb**. La limpieza según el tamaño quita primero las consultas menos caras y más antiguas. Se detiene en aproximadamente el 80 % de **max_storage_size_mb**. Este valor es el valor de configuración predeterminado.

OFF         
La limpieza según el tamaño no se activará automáticamente.

SIZE_BASED_CLEANUP_MODE es de tipo **nvarchar**.

QUERY_CAPTURE_MODE { ALL | AUTO | NONE | CUSTOM }         
Designa el modo de captura de consulta que está activo. Cada modo define directivas de captura de consulta específicas.

> [!NOTE]
> Los cursores, las consultas dentro de procedimientos almacenados y las consultas compiladas de forma nativa siempre se capturan cuando el modo de captura de consulta se establece en ALL, AUTO o CUSTOM.

ALL         
Captura todas las consultas. ALL es el valor de configuración predeterminado. Es el valor de configuración predeterminado a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].

AUTO         
Captura consultas pertinentes en función del consumo de recursos y el recuento de ejecuciones. Es el valor de configuración predeterminado a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 3.0.

Ninguno         
Detiene la captura de nuevas consultas. El almacén de consultas seguirá recopilando estadísticas de compilación y tiempo de ejecución para las consultas que ya se capturaron. Use esta configuración con precaución ya que podría omitir la captura de consultas importantes.

CUSTOM         
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 3.0)

Permite controlar las opciones de QUERY_CAPTURE_POLICY.

QUERY_CAPTURE_MODE es de tipo **nvarchar**.

max_plans_per_query         
Define el número máximo de planes que se tienen para cada consulta. El valor predeterminado es 200. MAX_PLANS_PER_QUERY es del tipo **int**.

**\<query_capture_policy_option_list> :: =**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 3.0)

Controla las opciones de directiva de captura de almacén de consultas. Excepto en STALE_CAPTURE_POLICY_THRESHOLD, estas opciones definen las condiciones OR que se tienen que dar para que las consultas se capturen en el valor definido en el umbral de la directiva de capturas obsoletas.

STALE_CAPTURE_POLICY_THRESHOLD = *number* { DAYS | HOURS }         
Define el período de intervalo de evaluación para determinar si se debe capturar una consulta. El valor predeterminado es de 1 día y puede establecerse de 1 hora a 7 días. *number* es del tipo **int**.

EXECUTION_COUNT         
Define el número de veces que se ejecuta una consulta durante el período de evaluación. El valor predeterminado es 30, lo que significa que, si se usa el valor predeterminado en el umbral de la directiva de capturas obsoletas, una consulta deberá ejecutarse por lo menos 30 veces en un día para que se conserve en el Almacén de consultas. EXECUTION_COUNT es del tipo **int**.

TOTAL_COMPILE_CPU_TIME_MS         
Define el tiempo total de CPU de compilación transcurrido que usa una consulta durante el período de evaluación. El valor predeterminado es 1000, lo que significa que, si se usa el valor predeterminado en el umbral de la directiva de capturas obsoletas, una consulta deberá invertir un total de al menos un segundo de tiempo de CPU durante la compilación de consulta en un día para conservarse en el Almacén de consultas. TOTAL_COMPILE_CPU_TIME_MS es del tipo **int**.

TOTAL_EXECUTION_CPU_TIME_MS         
Define el tiempo de ejecución total de CPU transcurrido que ha utilizado una consulta durante el período de evaluación. El valor predeterminado es 100, lo que significa que, si se usa el valor predeterminado en el umbral de la directiva de capturas obsoletas, una consulta deberá invertir un total de al menos 100 ms de tiempo de CPU durante la ejecución en un día para que se conserve en el Almacén de consultas. TOTAL_EXECUTION_CPU_TIME_MS es del tipo **int**.

**\<recovery_option> ::=**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Controla las opciones de recuperación de base de datos y la comprobación de errores de E/S de disco.

FULL         
Proporciona una restauración completa tras un error del medio, utilizando copias de seguridad del registro de transacciones. Si un archivo de datos está dañado, la recuperación del medio puede restaurar todas las transacciones confirmadas. Para más información, consulte [Modelos de recuperación](../../relational-databases/backup-restore/recovery-models-sql-server.md).

BULK_LOGGED         
Proporciona una recuperación tras un error del medio. Combina el máximo rendimiento y la mínima cantidad de uso de espacio de registro para determinadas operaciones a gran escala o masivas. Para información sobre las operaciones que se pueden registrar mínimamente, consulte [El registro de transacciones](../../relational-databases/logs/the-transaction-log-sql-server.md). En el modelo de recuperación BULK_LOGGED, el registro de estas operaciones es mínimo. Para más información, consulte [Modelos de recuperación](../../relational-databases/backup-restore/recovery-models-sql-server.md).

SIMPLE         
Se proporciona una estrategia de copia de seguridad sencilla que utiliza un espacio de registro mínimo. Se puede volver a utilizar el espacio de registro de forma automática cuando ya no se necesite para la recuperación tras errores del servidor. Para más información, consulte [Modelos de recuperación](../../relational-databases/backup-restore/recovery-models-sql-server.md).

> [!IMPORTANT]
> El modelo de recuperación simple es más fácil de administrar que los otros dos modelos, pero a costa de un mayor riesgo de perder los datos si se daña un archivo de datos. Todos los cambios se pierden, desde la copia de seguridad de base de datos más reciente o desde la copia de seguridad diferencial de la base de datos, y se deben volver a incluir de forma manual.

El modelo de recuperación predeterminado se determina mediante el modelo de recuperación de la base de datos **model** . Para más información sobre cómo seleccionar el modelo de recuperación adecuado, consulte [Modelos de recuperación](../../relational-databases/backup-restore/recovery-models-sql-server.md).

Puede determinar el estado de esta opción mediante las columnas **recovery_model** y **recovery_model_desc** en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad Recovery de la función DATABASEPROPERTYEX.

TORN_PAGE_DETECTION { ON | OFF }         
ON         
Las páginas incompletas se pueden detectar mediante el [!INCLUDE[ssDE](../../includes/ssde-md.md)].

OFF         
Las páginas incompletas no se pueden detectar mediante el [!INCLUDE[ssDE](../../includes/ssde-md.md)].

> [!IMPORTANT]
> La estructura de sintaxis TORN_PAGE_DETECTION ON | OFF se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta estructura de sintaxis en nuevos trabajos de desarrollo y prevea modificar las aplicaciones que actualmente la utilizan. Utilice la opción PAGE_VERIFY en su lugar.

<a name="page_verify"></a> PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }         
Detecta páginas de bases de datos dañadas por errores de ruta de E/S de disco. Los errores de ruta de acceso de E/S de disco pueden ser la causa de problemas de daños en la base de datos. Estos errores suelen producirse por errores de alimentación o errores de hardware de disco que ocurren en el momento en el que la página se escribe en disco.

CHECKSUM         
Calcula una suma de comprobación del contenido de toda la página y almacena el valor en el encabezado de página si se escribe una página en el disco. Si la página se lee desde el disco, la suma de comprobación se vuelve a calcular y se compara con el valor de suma de comprobación almacenado en el encabezado de página. Si el valor no coincide, se genera el mensaje de error 824 (indica un error de la suma de comprobación) para el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como para el registro de eventos de Windows. Un error de la suma de comprobación indica un problema de ruta de E/S. Para determinar la causa, es necesario investigar el hardware, los controladores de firmware, el BIOS, los controladores de filtro (por ejemplo, software antivirus) y otros componentes de ruta de E/S.

TORN_PAGE_DETECTION         
Guarda una pauta específica de 2 bits por cada sector de 512 bytes en la página de base de datos de 8 kilobytes (KB) y la almacena en el encabezado de página de la base de datos al escribir la página en el disco. Si la página se lee desde el disco, los bits rasgados almacenados en el encabezado de página se comparan con la información del sector de la página real.

Los valores no coincidentes indican que solamente se ha escrito en el disco una parte de la página. En esta situación, se genera el mensaje de error 824 (que indica un error de página rasgada) tanto para el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como para el registro de eventos de Windows. Las páginas rasgadas se suelen detectar mediante la recuperación de la base de datos si se trata realmente de la escritura incompleta de una página. No obstante, otros errores de ruta de E/S pueden generar una página rasgada en cualquier momento.

Ninguno         
Las escrituras de páginas de bases de datos no generarán un valor CHECKSUM o TORN_PAGE_DETECTION. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no comprobará ninguna suma de comprobación o página rasgada durante una lectura aunque haya un valor CHECKSUM o TORN_PAGE_DETECTION en el encabezado de página.

Tenga en cuenta los siguientes puntos importantes cuando utilice la opción PAGE_VERIFY:

- El valor predeterminado es CHECKSUM.
- Si una base de datos de usuario o del sistema se actualiza a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, se mantiene el valor de PAGE_VERIFY (NONE o TORN_PAGE_DETECTION). Se recomienda utilizar CHECKSUM.

    > [!NOTE]
    > En las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la opción de base de datos PAGE_VERIFY está establecida en NONE para la base de datos tempdb y no se puede modificar. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, el valor predeterminado para la base de datos tempdb es CHECKSUM para las nuevas instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al actualizar una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el valor predeterminado sigue siendo NONE. La opción se puede modificar. Se recomienda usar CHECKSUM para la base de datos tempdb.

- Es posible que TORN_PAGE_DETECTION utilice menos recursos, pero proporciona en cambio un subconjunto mínimo de la protección de CHECKSUM.
- PAGE_VERIFY se puede configurar sin dejar la base de datos sin conexión, ni bloquearla ni impedir la simultaneidad en ella.
- CHECKSUM y TORN_PAGE_DETECTION se excluyen mutuamente. No se pueden habilitar ambas opciones al mismo tiempo.

Si se detecta un error de suma de comprobación o de página rasgada, puede realizar una recuperación mediante la restauración de los datos o una regeneración del índice, si el error se limita únicamente a las páginas de índice. Si detecta un error de suma de comprobación, ejecute DBCC CHECKDB para determinar el tipo de página o páginas de base de datos afectadas. Para más información sobre las opciones de restauración, consulte [Argumentos RESTORE](../../t-sql/statements/restore-statements-arguments-transact-sql.md). Aunque la restauración de los datos resolverá el problema de los datos dañados, es necesario diagnosticar y corregir la causa (por ejemplo, un error del hardware de disco) lo antes posible, para evitar errores continuos.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vuelve a intentar cualquier lectura que genere un error con una suma de comprobación, una página rasgada u otros errores de E/S, en cuatro ocasiones. Si la lectura se realiza correctamente en cualquiera de los reintentos, se escribe un mensaje en el registro de errores. El comando que desencadenó la lectura continuará. El comando genera el mensaje de error 824 si los reintentos no se realizan correctamente.

Para más información sobre los mensajes de error 823, 824 y 825, vea:

- [Cómo solucionar un error 823 Msg en SQL Server](https://support.microsoft.com/help/2015755)
- [Cómo solucionar problemas de 824 Msg en SQL Server](https://support.microsoft.com/help/2015756)
- [Cómo solucionar problemas de Msg: reintento de lectura](https://support.microsoft.com/help/2015757).

La configuración actual de esta opción se puede determinar mediante el examen de la columna *page_verify_option* de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) o la propiedad *IsTornPageDetectionEnabled* de la función [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md).

**\<remote_data_archive_option> ::=**          
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Habilita o deshabilita Stretch Database para la base de datos. Para obtener más información, vea [Stretch Database](../../sql-server/stretch-database/stretch-database.md).

REMOTE_DATA_ARCHIVE = { ON ( SERVER = \<server_name> , { CREDENTIAL = \<db_scoped_credential_name> | FEDERATED_SERVICE_ACCOUNT = ON | OFF } )| OFF         
ON         
Habilita Stretch Database para la base de datos. Para más información, incluidos los requisitos previos adicionales, vea [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md) (Habilitar Stretch Database para una base de datos).

**Permisos**: Para habilitar Stretch Database en una base de datos o una tabla, se necesitan los permisos `db_owner`. Para habilitar Stretch Database en una base de datos también se necesitan permisos `CONTROL DATABASE`.

SERVER = \<server_name>         
Especifica la dirección del servidor de Azure. Incluye la parte `.database.windows.net` del nombre. Por ejemplo, `MyStretchDatabaseServer.database.windows.net`.

CREDENTIAL = \<db_scoped_credential_name>         
Especifica la credencial de ámbito de base de datos que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para conectarse al servidor de Azure. Asegúrese de que la credencial existe antes de ejecutar este comando. Para más información, consulte [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

FEDERATED_SERVICE_ACCOUNT = { ON | OFF }         
Puede usar una cuenta de servicio federado para que el servidor SQL Server local se comunique con el servidor remoto de Azure cuando se cumplan estas condiciones.

- La cuenta de servicio con la que se está ejecutando la instancia de SQL Server es una cuenta de dominio.
- La cuenta de dominio pertenece a un dominio cuyo Active Directory está federado con Azure Active Directory.
- El servidor remoto de Azure está configurado para admitir la autenticación de Azure Active Directory.
- La cuenta de servicio con la que se ejecuta la instancia de SQL Server debe configurarse como una cuenta `dbmanager` o `sysadmin` en el servidor remoto de Azure.

Si indica que la cuenta de servicio federada está activada, no podrá especificar además el argumento CREDENTIAL. Proporcione el argumento CREDENTIAL si especifica OFF.

OFF         
Deshabilita Stretch Database para la base de datos. Para obtener más información, vea [Deshabilitar Stretch Database y recuperar datos remotos](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).

Solo puede deshabilitar Stretch Database para una base de datos una vez que la base de datos ya no contenga ninguna tabla que esté habilitada para Stretch Database. Después de deshabilitar Stretch Database, la migración de datos se detiene. Además, los resultados de la consulta ya no incluyen los resultados de las tablas remotas.

Al deshabilitar Stretch no se quita la base de datos remota. Si quiere eliminar la base de datos remota, tiene que quitarla mediante Azure Portal.
 
**\<service_broker_option> ::=**          
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Controla las siguientes opciones de [!INCLUDE[ssSB](../../includes/sssb-md.md)]: habilita o deshabilita la entrega de mensajes, establece un nuevo identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] o establece prioridades de conversación en ON u OFF.

ENABLE_BROKER         
Indica que se habilite [!INCLUDE[ssSB](../../includes/sssb-md.md)] para la base de datos especificada. Se inicia la entrega de mensajes y la marca is_broker_enabled se establece en TRUE en la vista de catálogo sys.databases. La base de datos conserva el identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente. Service Broker no puede habilitarse mientras la base de datos sea la entidad de seguridad en una configuración de creación de reflejo de la base de datos.

> [!NOTE]
> ENABLE_BROKER requiere un bloqueo exclusivo de base de datos. Si otras sesiones tienen recursos bloqueados en la base de datos, ENABLE_BROKER esperará hasta que las demás sesiones liberen sus bloqueos. Para habilitar [!INCLUDE[ssSB](../../includes/sssb-md.md)] en una base de datos de usuario, asegúrese de que ninguna otra sesión esté utilizando la base de datos antes de ejecutar la instrucción ALTER DATABASE SET ENABLE_BROKER, por ejemplo, colocando la base de datos en modo de usuario único. Para habilitar [!INCLUDE[ssSB](../../includes/sssb-md.md)] en la base de datos msdb, detenga en primer lugar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que [!INCLUDE[ssSB](../../includes/sssb-md.md)] pueda obtener el bloqueo necesario.

DISABLE_BROKER         
Indica que se deshabilite [!INCLUDE[ssSB](../../includes/sssb-md.md)] para la base de datos especificada. Se detiene la entrega de mensajes y la marca is_broker_enabled se establece en FALSE en la vista de catálogo sys.databases. La base de datos conserva el identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.

NEW_BROKER         
Especifica que la base de datos debe recibir un identificador de agente nuevo. La base de datos actúa como un nuevo agente de servicio. Como tal, todas las conversaciones existentes en la base de datos se quitan inmediatamente sin generar mensajes de finalización de diálogo. Cualquier ruta que haga referencia al identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] anterior se debe volver a crear con el nuevo identificador.

ERROR_BROKER_CONVERSATIONS         
Especifica que la entrega de mensajes de [!INCLUDE[ssSB](../../includes/sssb-md.md)] está habilitada. Este valor conserva el identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente para la base de datos. [!INCLUDE[ssSB](../../includes/sssb-md.md)] finaliza todas las conversaciones de la base de datos con un error. Este valor permite que las aplicaciones realicen una ejecución regular de las conversaciones existentes.

HONOR_BROKER_PRIORITY {ON | OFF}         
ON         
Las operaciones de envío tienen en cuenta los niveles de prioridad asignados a las conversaciones. Los mensajes de las conversaciones que tienen niveles de prioridad altos se envían antes que los que tienen asignados niveles de prioridad bajos.

OFF         
Las operaciones de envío se ejecutan como si todas las conversaciones tuvieran el nivel de prioridad predeterminado.

Los cambios de la opción HONOR_BROKER_PRIORITY tienen efecto inmediato para los diálogos nuevos o los que no tiene ningún mensaje en espera de ser enviado. Los diálogos con mensajes que se van a enviar cuando se ejecuta ALTER DATABASE no adoptarán el nuevo valor hasta que se envíe alguno de los mensajes del diálogo. La cantidad de tiempo que transcurre hasta que se inicien todos los diálogos con el nuevo valor puede variar considerablemente.

El valor actual de esta propiedad se notifica en la columna is_broker_priority_honored de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

**\<snapshot_option> ::=**         

Calcula el nivel de aislamiento de la transacción.

ALLOW_SNAPSHOT_ISOLATION { ON | OFF }         
ON         
Habilita la opción de instantánea en el nivel de base de datos. Cuando se habilita, las instrucciones DML inician la generación de versiones de fila aunque ninguna transacción utilice el aislamiento de instantánea. Una vez habilitada esta opción, las transacciones pueden especificar el nivel de aislamiento de transacción SNAPSHOT. Si se ejecuta una transacción en el nivel de aislamiento SNAPSHOT, todas las instrucciones verán una instantánea de los datos tal como estaban al inicio de la transacción. Si una transacción ejecutada en el nivel de aislamiento SNAPSHOT tiene acceso a los datos de varias bases de datos, ALLOW_SNAPSHOT_ISOLATION debe establecerse en ON en todas las bases de datos o cada instrucción de la transacción debe utilizar sugerencias de bloqueo en cualquier referencia de una cláusula FROM a una tabla de una base de datos donde ALLOW_SNAPSHOT_ISOLATION sea OFF.

OFF         
Desactiva la opción de instantánea en el nivel de base de datos. Las transacciones no pueden especificar el nivel de aislamiento de la transacción SNAPSHOT.

Si se establece ALLOW_SNAPSHOT_ISOLATION en un estado nuevo (de ON a OFF o de OFF a ON), ALTER DATABASE no devuelve el control al autor de la llamada hasta confirmar todas las transacciones existentes de la base de datos. Si la base de datos ya se encuentra en el estado especificado en la instrucción ALTER DATABASE, se devuelve de inmediato el control al autor de la llamada. Use [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) para determinar si hay transacciones de ejecución prolongada si la instrucción ALTER DATABASE no devuelve resultados rápidamente. Si se cancela la instrucción ALTER DATABASE, la base de datos permanece en el estado en que estaba al iniciar ALTER DATABASE. La vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) indica el estado de las transacciones de aislamiento de instantáneas en la base de datos. Si **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON, ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF se pausará durante seis segundos y reintentará la operación.

No puede cambiar el estado de ALLOW_SNAPSHOT_ISOLATION si la base de datos está establecida en OFFLINE.

Si establece ALLOW_SNAPSHOT_ISOLATION en una base de datos READ_ONLY, la configuración se mantendrá si la base de datos se establece posteriormente en READ_WRITE.

Puede cambiar la configuración de ALLOW_SNAPSHOT_ISOLATION para las bases de datos maestra, model, msdb y tempdb. La configuración se mantiene cada vez que la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se detiene y se reinicia si cambia la configuración para tempdb. Si cambia la configuración para la base de datos model, dicha configuración se convierte en la configuración predeterminada para todas las bases de datos nuevas que se crean, excepto para tempdb.

La opción es ON de forma predeterminada para las bases de datos maestra y msdb.

La configuración actual de esta opción se puede determinar mediante el examen de la columna snapshot_isolation_state de la vista de catálogo sys.databases.

READ_COMMITTED_SNAPSHOT { ON | OFF }         
ON         
Habilita la opción de instantánea de lectura confirmada en el nivel de base de datos. Cuando se habilita, las instrucciones DML inician la generación de versiones de fila aunque ninguna transacción utilice el aislamiento de instantánea. Una vez habilitada esta opción, las transacciones que especifican el nivel de aislamiento de lectura confirmada usan versiones de fila en lugar de bloqueos. Todas las instrucciones ven una instantánea de los datos tal como estaban al inicio de la instrucción si una transacción se ejecuta en el nivel de aislamiento de lectura conformada.

OFF         
Desactiva la opción de instantánea de lectura confirmada en el nivel de base de datos. Las transacciones que especifican el nivel de aislamiento READ COMMITTED utilizan el bloqueo.

Para establecer READ_COMMITTED_SNAPSHOT en ON u OFF, no puede haber ninguna conexión activa a la base de datos, excepto la que ejecuta el comando ALTER DATABASE. Sin embargo, no es necesario que la base de datos esté en modo de usuario único. No puede cambiar el estado de esta opción si la base de datos está establecida en OFFLINE.

Si establece READ_COMMITTED_SNAPSHOT en una base de datos READ_ONLY, la configuración se mantendrá si la base de datos se establece después en READ_WRITE.

READ_COMMITTED_SNAPSHOT no se puede cambiar a ON para las bases de datos maestra, tempdb o msdb. Si cambia la configuración para model, dicha configuración se convierte en predeterminada para todas las bases de datos creadas, excepto para tempdb.

La configuración actual de esta opción se puede determinar mediante el examen de la columna is_read_committed_snapshot_on de la vista de catálogo sys.databases.

> [!WARNING]
>Cuando se crea una tabla con **DURABILITY = SCHEMA_ONLY** y posteriormente se cambia **READ_COMMITTED_SNAPSHOT** mediante **ALTER DATABASE**, se pierden los datos de la tabla.

MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }         
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

ON         
Cuando el nivel de aislamiento de transacción se establece en uno inferior a SNAPSHOT, todas las operaciones interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] en las tablas optimizadas para memoria se ejecutan con aislamiento SNAPSHOT. Los ejemplos de los niveles de aislamiento inferiores a la instantánea son READ COMMITTED o READ UNCOMMITTED. Estas operaciones se ejecutan si el nivel de aislamiento de transacción se establece explícitamente en el nivel de sesión o el valor predeterminado se utiliza de forma implícita.

OFF         
No eleva el nivel de aislamiento de transacción para las operaciones interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] en las tablas optimizadas para memoria.

No puede cambiar el estado de MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT si la base de datos está establecida en OFFLINE.

De forma predeterminada, la opción está desactivada.

La configuración actual de esta opción se puede determinar mediante el examen de la columna **memory_optimized_elevate_to_snapshot** de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

**\<sql_option> ::=**         

Controla las opciones de cumplimiento con ANSI en el nivel de base de datos.

ANSI_NULL_DEFAULT { ON | OFF }         
Determina el valor predeterminado, NULL o NOT NULL, de una columna o del [tipo definido por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) para los que no se ha definido la nulabilidad explícitamente en las instrucciones CREATE TABLE o ALTER TABLE. Las columnas para las que se hayan definido restricciones siguen las reglas de las restricciones, independientemente de esta configuración.

ON         
El valor predeterminado es NULL.

OFF         
El valor predeterminado es NOT NULL.

La configuración del nivel de conexión, establecida mediante la instrucción SET, invalida la configuración predeterminada del nivel de base de datos para ANSI_NULL_DEFAULT. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_NULL_DEFAULT en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).

Para la compatibilidad con ANSI, si se establece la opción de base de datos ANSI_NULL_DEFAULT en ON, el valor predeterminado cambia a NULL.

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_null_default_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiNullDefault de la función DATABASEPROPERTYEX.

ANSI_NULLS { ON | OFF }         
ON         
Todas las comparaciones con un valor NULL se evalúan como UNKNOWN.

OFF         
Las comparaciones de valores no UNICODE con un valor NULL se evalúan como TRUE si ambos valores son NULL.

> [!IMPORTANT]
> En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_NULLS siempre estará ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.

La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para ANSI_NULLS. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_NULLS en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md).

El valor de SET ANSI_NULLS también debe estar en ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_nulls_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiNullsEnabled de la función DATABASEPROPERTYEX.

ANSI_PADDING { ON | OFF }         
ON         
Las cadenas se rellenan a la misma longitud antes de la conversión. También se rellenan hasta la misma longitud antes de la inserción en un tipo de datos **varchar** o **nvarchar**.

OFF         
Inserta espacios en blanco finales en los valores de caracteres en las columnas **varchar** o **nvarchar**. También deja los ceros a la derecha en los valores binarios insertados en columnas **varbinary**. Los valores no se rellenan hasta completar la longitud de la columna.

Si se especifica OFF, esta opción solamente afecta a la definición de las columnas nuevas.

> [!IMPORTANT]
> En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_PADDING siempre estará en ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Se recomienda establecer siempre ANSI_PADDING en ON. ANSI_PADDING también debe estar en ON al crear o tratar índices en columnas calculadas o vistas indizadas.

**char(_n_)** y **binary(_n_)** las columnas que admiten valores NULL se rellenan hasta la longitud de la columna cuando ANSI_PADDING se establece en ON. Los ceros y los espacios en blanco finales se recortan si ANSI_PADDING es OFF. Las columnas **char(_n_)** y **binary(_n_)** que no permiten valores NULL siempre se rellenan hasta completar la longitud de la columna.

La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada del nivel de base de datos para ANSI_PADDING. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_PADDING en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_padding_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiPaddingEnabled de la función DATABASEPROPERTYEX.

ANSI_WARNINGS { ON | OFF }         
ON         
Se emiten errores o advertencias si se dan condiciones tales como la división por cero. También se emiten errores y advertencias cuando aparecen valores null en funciones de agregado.

OFF         
No se genera ninguna advertencia ni se devuelven valores NULL si se producen condiciones como la división por cero.

El valor de SET ANSI_WARNINGS debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para ANSI_WARNINGS. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_WARNINGS en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_warnings_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiWarningsEnabled de la función DATABASEPROPERTYEX.

ARITHABORT { ON | OFF }         
ON         
Se finaliza una consulta cuando se produce un error de desbordamiento o de división por cero durante su ejecución.

OFF         
Aparece un mensaje de advertencia cuando se produce uno de estos errores. La consulta, el proceso por lotes o la transacción continúa procesándose como si no se hubiera producido ningún error aunque se muestre una advertencia.

El valor de SET ARITHABORT debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

Puede determinar el estado de esta opción mediante el examen de la columna is_arithabort_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsArithmeticAbortEnabled de la función DATABASEPROPERTYEX.

COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 | 90 }         

Para más información, consulte [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).

CONCAT_NULL_YIELDS_NULL { ON | OFF }         
ON         
El resultado de una operación de concatenación es NULL si alguno de los operandos es NULL. Por ejemplo, la concatenación de la cadena de caracteres "Esto es" y NULL da como resultado el valor NULL, y no el valor "Esto es".

OFF         
El valor NULL se trata como una cadena de caracteres vacía.

El valor de CONCAT_NULL_YIELDS_NULL también debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

> [!IMPORTANT]
> En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], CONCAT_NULL_YIELDS_NULL siempre estará en ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.

La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para CONCAT_NULL_YIELDS_NULL. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen CONCAT_NULL_YIELDS_NULL en ON para la sesión al realizar la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_concat_null_yields_null_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsNullConcat de la función DATABASEPROPERTYEX.

QUOTED_IDENTIFIER { ON | OFF }         
ON         
Las comillas dobles se pueden usar para identificadores delimitados.

Todas las cadenas delimitadas por comillas dobles se interpretan como identificadores de objetos. Los identificadores entre comillas no tienen que adaptarse a las reglas de [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Pueden ser palabras clave e incluir caracteres que no se permiten en los identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Si una comilla simple (') forma parte de la cadena literal, puede representarse mediante comillas dobles (").

OFF         
Los identificadores no se pueden incluir entre comillas y deben seguir todas las reglas de [!INCLUDE[tsql](../../includes/tsql-md.md)] para los identificadores. Los literales se pueden delimitar con comillas simples o dobles.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también permite delimitar los identificadores con corchetes ([ ]). Los identificadores entre corchetes pueden usarse siempre, independientemente del valor de QUOTED_IDENTIFIER. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).

Al crear una tabla, la opción QUOTED IDENTIFIER siempre se almacena como ON en los metadatos de la tabla. La opción se almacena incluso si está establecida en OFF al crear la tabla.

La configuración en el nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para QUOTED_IDENTIFIER. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión estableciendo QUOTED_IDENTIFIER en ON. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_quoted_identifier_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsQuotedIdentifiersEnabled de la función DATABASEPROPERTYEX.

NUMERIC_ROUNDABORT { ON | OFF }         
ON         
Se genera un error cuando se produce una pérdida de precisión en una expresión.

OFF         
Las pérdidas de precisión no generan mensajes de error y el resultado se redondea con la precisión de la columna o variable que lo almacena.

El valor de NUMERIC_ROUNDABORT debe ser OFF al crear o realizar cambios en índices de columnas calculadas o vistas indizadas.

Puede determinar el estado de esta opción mediante el examen de la columna is_numeric_roundabort_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsNumericRoundAbortEnabled de la función DATABASEPROPERTYEX.

RECURSIVE_TRIGGERS { ON | OFF }         
ON        
Se permite la activación recursiva de desencadenadores AFTER.

OFF         
Puede determinar el estado de esta opción mediante el examen de la columna is_recursive_triggers_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsRecursiveTriggersEnabled de la función DATABASEPROPERTYEX.

> [!NOTE]
> La recursividad directa solo se evita cuando RECURSIVE_TRIGGERS se establece en OFF. Para deshabilitar la recursividad indirecta, también debe establecer la opción de servidor desencadenadores anidados en 0.

Puede determinar el estado de esta opción si examina la columna is_recursive_triggers_on de la vista de catálogo sys.databases o la propiedad IsRecursiveTriggersEnabled de la función DATABASEPROPERTYEX.

**\<target_recovery_time_option> ::=**          
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

Especifica la frecuencia de puntos de comprobación indirectos por base de datos. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], el valor predeterminado para nuevas bases de datos es de un minuto, lo cual indica que la base de datos usará puntos de comprobación indirectos. Para versiones anteriores, el valor predeterminado es 0, lo cual indica que la base de datos usará puntos de comprobación automáticos, cuya frecuencia depende del valor de intervalo de recuperación de la instancia de servidor. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda un minuto para la mayoría de los sistemas.

TARGET_RECOVERY_TIME **=** *target_recovery_time* { SECONDS | MINUTES }         
*target_recovery_time*         
Especifica el límite máximo de tiempo para recuperar la base de datos especificada en caso de bloqueo. *target_recovery_time* es del tipo **int**.

SECONDS         
Indica que *target_recovery_time* se expresa como el número de segundos. 

MINUTES         
Indica que *target_recovery_time* se expresa como el número de minutos.

Para más información sobre los puntos de control indirectos, consulte [Puntos de control de base de datos](../../relational-databases/logs/database-checkpoints-sql-server.md).

**WITH \<termination> ::=**         

Especifica el momento en que se revierten las transacciones incompletas cuando la base de datos pasa de un estado a otro. Si se omite la cláusula de terminación, la instrucción ALTER DATABASE espera indefinidamente a que se produzca un bloqueo en la base de datos. Solamente se puede especificar una cláusula de terminación y debe seguir a las cláusulas SET.

> [!NOTE]
> No todas las opciones de base de datos usan la cláusula WITH \<termination>. Para más información, consulte la tabla ubicada en "[Opciones de configuración](#SettingOptions) de la sección "Comentarios" de este artículo.

ROLLBACK AFTER *number* [SECONDS] | ROLLBACK IMMEDIATE         

Especifica si la operación de reversión se ejecuta transcurrido un número de segundos determinado o de forma inmediata. *number* es del tipo **int**.

NO_WAIT         
Especifica que la solicitud producirá un error si el cambio de opción o estado de la base de datos solicitado no puede completarse inmediatamente. Completarse inmediatamente significa que no se espera a que las transacciones se confirmen o reviertan por su cuenta.

## <a name="SettingOptions"></a> Configurar opciones         
Para recuperar la configuración actual de las opciones de base de datos, use la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) o [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md).

Una vez configurada una opción de la base de datos, la modificación surte efecto de inmediato.

Puede cambiar los valores predeterminados de cualquiera de las opciones de las bases de datos recién creadas. Para ello, cambie la opción adecuada de base de datos en la base de datos de modelo.

No todas las opciones de base de datos usan la cláusula WITH \<termination> ni se pueden especificar en combinación con otras opciones. En la siguiente tabla se incluyen estas opciones, su estado y el estado de terminación.

|Categoría de opciones|Se puede especificar con otras opciones|Puede usar la cláusula WITH \<termination>|
|----------------------|-----------------------------------------|---------------------------------------------|
|\<db_state_option>|Sí|Sí|
|\<db_user_access_option>|Sí|Sí|
|\<db_update_option>|Sí|Sí|
|\<delayed_durability_option>|Sí|Sí|
|\<external_access_option>|Sí|No|
|\<cursor_option>|Sí|No|
|\<auto_option>|Sí|No|
|\<sql_option>|Sí|No|
|\<recovery_option>|Sí|No|
|\<target_recovery_time_option>|No|Sí|
|\<database_mirroring_option>|No|No|
|ALLOW_SNAPSHOT_ISOLATION|No|No|
|READ_COMMITTED_SNAPSHOT|No|Sí|
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|Sí|Sí|
|\<service_broker_option>|Sí|No|
|DATE_CORRELATION_OPTIMIZATION|Sí|Sí|
|\<parameterization_option>|Sí|Sí|
|\<change_tracking_option>|Sí|Sí|
|\<db_encryption_option>|Sí|No|

La memoria caché de planes para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se borra si se establece alguna de las opciones siguientes:

|||
|-|-|
|OFFLINE|READ_WRITE|
|ONLINE|MODIFY FILEGROUP DEFAULT|
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|
|COLLATE|MODIFY FILEGROUP READ_ONLY|
|READ_ONLY||

La memoria caché de procedimientos también se vacía en los escenarios siguientes.

- Una base de datos tiene la opción de base de datos AUTO_CLOSE establecida en ON. Cuando ninguna conexión de usuario hace referencia a la base de datos ni la usa, la tarea de segundo plano intenta cerrar la base de datos y apagarla de modo automático.
- Ejecuta varias consultas con una base de datos que tiene opciones predeterminadas. Después, la base de datos se quita.
- Se quita una instantánea de base de datos para una base de datos de origen.
- Volvió a generar correctamente el registro de transacciones para una base de datos.
- Restaura una copia de seguridad de una base de datos
- Separa una base de datos.

Al borrar la memoria caché de planes, se provoca una nueva compilación de todos los planes de ejecución posteriores y puede ocasionar una disminución repentina y temporal del rendimiento de las consultas. Para cada almacén de caché borrado de la caché de planes, el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contendrá el siguiente mensaje informativo: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado %d instancias de vaciado del almacén de caché "%s" (parte de la memoria caché de planes) debido a determinadas operaciones de mantenimiento de base de datos o reconfiguración". Este mensaje se registra cada cinco minutos siempre que se vacíe la memoria caché dentro de ese intervalo de tiempo.

## <a name="examples"></a>Ejemplos

### <a name="a-setting-options-on-a-database"></a>A. Configurar opciones en una base de datos

En el siguiente ejemplo se establece el modelo de recuperación y las opciones de comprobación de páginas de datos para la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
SET RECOVERY FULL PAGE_VERIFY CHECKSUM;
GO

```

### <a name="b-setting-the-database-to-read_only"></a>B. Establecer la base de datos en READ_ONLY

El cambio del estado de una base de datos o un grupo de archivos a READ_ONLY o READ_WRITE requiere el acceso exclusivo a la base de datos. En el siguiente ejemplo la base de datos se establece en el modo `SINGLE_USER` para obtener acceso exclusivo. A continuación, el ejemplo establece el estado de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en `READ_ONLY` y devuelve el acceso a la base de datos a todos los usuarios.

> [!NOTE]
>En este ejemplo se utiliza la opción de terminación `WITH ROLLBACK IMMEDIATE` en la primera instrucción `ALTER DATABASE` . Todas las transacciones incompletas se revierten y las restantes conexiones con la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] se desconectan de inmediato.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
SET SINGLE_USER
WITH ROLLBACK IMMEDIATE;
GO
ALTER DATABASE AdventureWorks2012
SET READ_ONLY
GO
ALTER DATABASE AdventureWorks2012
SET MULTI_USER;
GO

```

### <a name="c-enabling-snapshot-isolation-on-a-database"></a>C. Habilitar el aislamiento de instantánea en una base de datos

En el siguiente ejemplo se habilita la opción del marco de aislamiento de instantánea para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .

```sql
USE AdventureWorks2012;
USE master;
GO
ALTER DATABASE AdventureWorks2012
SET ALLOW_SNAPSHOT_ISOLATION ON;
GO
-- Check the state of the snapshot_isolation_framework
-- in the database.
SELECT name, snapshot_isolation_state,
    snapshot_isolation_state_desc AS description
FROM sys.databases
WHERE name = N'AdventureWorks2012';
GO

```

El conjunto de resultados muestra que el marco de aislamiento de instantánea está habilitado.

|NAME |snapshot_isolation_state |description|
|-------------------- |------------------------|----------|
|AdventureWorks2012 |1| ON |

### <a name="d-enabling-modifying-and-disabling-change-tracking"></a>D. Habilitar, modificar y deshabilitar el seguimiento de cambios

En el ejemplo siguiente se habilita el seguimiento de cambios para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y se establece el período de retención en `2` días.

```sql
ALTER DATABASE AdventureWorks2012
SET CHANGE_TRACKING = ON
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);
```

En el ejemplo siguiente se muestra cómo cambiar el período de retención a `3` días.

```sql
ALTER DATABASE AdventureWorks2012
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);
```

En el ejemplo siguiente se muestra cómo deshabilitar el seguimiento de cambios para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .

```sql
ALTER DATABASE AdventureWorks2012
SET CHANGE_TRACKING = OFF;
```

### <a name="e-enabling-the-query-store"></a>E. Habilitar el almacén de consultas

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

En el ejemplo siguiente se habilita el almacén de consultas y configura los parámetros de almacén de consultas.

```sql
ALTER DATABASE AdventureWorks2012
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1024,
      INTERVAL_LENGTH_MINUTES = 60
    );
```

### <a name="f-enabling-the-query-store-with-wait-statistics"></a>F. Habilitar el almacén de consultas con las estadísticas de espera

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)])

En el ejemplo siguiente se habilita el almacén de consultas y configura los parámetros de almacén de consultas.

```sql
ALTER DATABASE AdventureWorks2016
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE, 
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1024, 
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO, 
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
    );
```

### <a name="g-enabling-the-query-store-with-custom-capture-policy-options"></a>G. Habilitar el almacén de consultas con las opciones de directiva de captura personalizadas

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)])

En el ejemplo siguiente se habilita el almacén de consultas y configura los parámetros de almacén de consultas.

```sql
ALTER DATABASE AdventureWorks2016 
SET QUERY_STORE = ON 
    (
      OPERATION_MODE = READ_WRITE, 
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1024, 
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO, 
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100 
      )
    );
```

## <a name="see-also"></a>Consulte también

- [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)
- [Creación de reflejo de la base de datos de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)
- [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)
- [Estadísticas](../../relational-databases/statistics/statistics.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [Habilitar y deshabilitar el seguimiento de cambios](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [Procedimiento recomendado con el Almacén de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](alter-database-transact-sql-set-options.md?view=sql-server-2017)|**_\*Grupo de bases de datos elásticas o base de datos única de<br />SQL Database\*_** &nbsp;|[Instancia administrada de<br />SQL Database](alter-database-transact-sql-set-options.md?view=azuresqldb-mi-current)||[SQL Data<br />Warehouse](alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)||||

&nbsp;

## <a name="azure-sql-database-single-databaseelastic-pool"></a>Grupo de bases de datos elásticas o base de datos única de Azure SQL Database

Los niveles de compatibilidad son opciones de `SET`, pero se describe en [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).

> [!NOTE]
> Es posible configurar muchas opciones SET de la base de datos para la sesión actual mediante [Instrucciones SET](../../t-sql/statements/set-statements-transact-sql.md), aunque generalmente las configuran las aplicaciones al realizar la conexión. Las opciones SET de nivel de sesión reemplazan a los valores **ALTER DATABASE SET** . Las opciones de base de datos descritas a continuación son valores que se pueden establecer en las sesiones que no proporcionan explícitamente otros valores de opciones SET.

## <a name="syntax"></a>Sintaxis

```
ALTER DATABASE { database_name | Current }
SET
{
    <option_spec> [ ,...n ] [ WITH <termination> ]
}
;

<option_spec> ::=
{
    <auto_option>
  | <automatic_tuning_option>
  | <change_tracking_option>
  | <cursor_option>
  | <db_encryption_option>
  | <db_update_option>
  | <db_user_access_option>
  | <delayed_durability_option>
  | <parameterization_option>
  | <query_store_options>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <termination>
  | <temporal_history_retention>
}
;
<auto_option> ::=
{
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }
  | AUTO_SHRINK { ON | OFF }
  | AUTO_UPDATE_STATISTICS { ON | OFF }
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}

<automatic_tuning_option> ::=
{AUTOMATIC_TUNING = { AUTO | INHERIT | CUSTOM }
  | AUTOMATIC_TUNING ( CREATE_INDEX = { DEFAULT | ON | OFF } )
  | AUTOMATIC_TUNING ( DROP_INDEX = { DEFAULT | ON | OFF } )
  | AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { DEFAULT | ON | OFF } )
}

<change_tracking_option> ::=
{
  CHANGE_TRACKING
   {
       = OFF
     | = ON [ ( <change_tracking_option_list > [,...n] ) ]
     | ( <change_tracking_option_list> [,...n] )
   }
}

<change_tracking_option_list> ::=
   {
       AUTO_CLEANUP = { ON | OFF }
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }
   }

<cursor_option> ::=
{
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }
}

<db_encryption_option> ::=
  ENCRYPTION { ON | OFF }

<db_update_option> ::=
  { READ_ONLY | READ_WRITE }

<db_user_access_option> ::=
  { RESTRICTED_USER | MULTI_USER }

<delayed_durability_option> ::=DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }

<parameterization_option> ::=
  PARAMETERIZATION { SIMPLE | FORCED }

<query_store_options> ::=
{
  QUERY_STORE
  {
    = OFF
    | = ON [ ( <query_store_option_list> [,... n] ) ]
    | ( < query_store_option_list> [,... n] )
    | CLEAR [ ALL ]
  }
}

<query_store_option_list> ::=
{
  OPERATION_MODE = { READ_WRITE | READ_ONLY }
  | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )
  | DATA_FLUSH_INTERVAL_SECONDS = number
  | MAX_STORAGE_SIZE_MB = number
  | INTERVAL_LENGTH_MINUTES = number
  | SIZE_BASED_CLEANUP_MODE = [ AUTO | OFF ]
  | QUERY_CAPTURE_MODE = [ ALL | AUTO | NONE ]
  | MAX_PLANS_PER_QUERY = number
}

<snapshot_option> ::=
{
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }
  | READ_COMMITTED_SNAPSHOT {ON | OFF }
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }
}
<sql_option> ::=
{
    ANSI_NULL_DEFAULT { ON | OFF }
  | ANSI_NULLS { ON | OFF }
  | ANSI_PADDING { ON | OFF }
  | ANSI_WARNINGS { ON | OFF }
  | ARITHABORT { ON | OFF }
  | COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }
  | NUMERIC_ROUNDABORT { ON | OFF }
  | QUOTED_IDENTIFIER { ON | OFF }
  | RECURSIVE_TRIGGERS { ON | OFF }
}

<termination>::=
{
    ROLLBACK AFTER integer [ SECONDS ]
  | ROLLBACK IMMEDIATE
  | NO_WAIT
}

<temporal_history_retention>::=TEMPORAL_HISTORY_RETENTION { ON | OFF }
```

## <a name="arguments"></a>Argumentos

*database_name*         
Es el nombre de la base de datos que se va a modificar.

CURRENT         
`CURRENT` realiza la acción en la base de datos actual. `CURRENT` no se admite para todas las opciones en todos los contextos. Si `CURRENT` produce un error, proporcione el nombre de la base de datos.

**\<auto_option> ::=**

Controla las opciones automáticas.
<a name="auto_create_statistics"></a> AUTO_CREATE_STATISTICS { ON | OFF }         
ON         
El optimizador de consultas crea las estadísticas en columnas únicas de los predicados de consulta, según sea necesario, para mejorar los planes de consulta y el rendimiento de las consultas. Estas estadísticas de columna única se crean cuando el optimizador de consultas las compila. Las estadísticas de columna única solamente se crean en las columnas que ya no son la primera columna de un objeto de estadísticas existente.

El valor predeterminado es ON. Recomendamos utilizar la configuración predeterminada para la mayoría de las bases de datos.

OFF         
El optimizador de consultas no crea estadísticas en columnas únicas de los predicados de consulta cuando está compilando consultas. Establecer esta opción en OFF puede producir planes de consulta poco óptimos y un rendimiento degradado de las consultas.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_create_stats_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAutoCreateStatistics de la función DATABASEPROPERTYEX.

Para más información, vea la sección "Utilizar las opciones de estadísticas de toda la base de datos" del tema [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

INCREMENTAL = ON | OFF         
Establezca AUTO_CREATE_STATISTICS en ON y establezca INCREMENTAL en ON. Esta configuración crea automáticamente estadísticas como incrementales siempre que se admitan estadísticas incrementales. El valor predeterminado es OFF. Para más información, consulte [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md).

<a name="auto_shrink"></a> AUTO_SHRINK { ON | OFF }         
ON         
Los archivos de la base de datos se pueden reducir periódicamente.

Pueden reducirse automáticamente los archivos de datos y los archivos de registro. AUTO_SHRINK reduce el tamaño del registro de transacciones solo si establece la base de datos en el modelo de recuperación SIMPLE o si realiza una copia de seguridad del registro. Cuando se establece en OFF, los archivos de la base de datos no se reducen de forma automática durante las comprobaciones periódicas del espacio no utilizado.

La opción AUTO_SHRINK reduce los archivos cuando no se utiliza más de un 25% del espacio del archivo. La opción hace que el archivo se reduzca a uno de dos tamaños. Se reduce al que sea más grande de los siguientes:

- El tamaño donde el 25 por ciento del archivo es espacio no utilizado
- El tamaño del archivo cuando se creó

No puede reducir una base de datos de solo lectura.

OFF         
Los archivos de la base de datos no se reducen automáticamente durante las comprobaciones periódicas del espacio no utilizado.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_shrink_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAutoShrink de la función DATABASEPROPERTYEX.

> [!NOTE]
> La opción AUTO_SHRINK no está disponible en una base de datos independiente.

<a name="auto_update_statistics"></a> AUTO_UPDATE_STATISTICS { ON | OFF }         
ON         
Especifica que el optimizador de consultas actualiza las estadísticas cuando son usadas por una consulta y pudieran estar obsoletas. Las estadísticas se vuelven obsoletas después de que operaciones de inserción, actualización, eliminación o combinación cambien la distribución de los datos en la tabla o la vista indizada. El optimizador de consultas determina cuándo han podido quedar obsoletas las estadísticas contando el número de modificaciones de datos desde la actualización más reciente de las estadísticas, comparando el número de modificaciones con respecto a un umbral. El umbral se basa en el número de filas de la tabla o la vista indizada.

El optimizador de consultas comprueba que hay estadísticas obsoletas antes de que compile una consulta y ejecuta un plan de consulta almacenado en caché. El Optimizador de consultas utiliza las columnas, tablas y vistas indexadas en el predicado de consulta para determinar qué estadísticas podrían estar obsoletas. El optimizador de consultas determina esta información antes de que compile una consulta. Antes de ejecutar un plan de consulta almacenado en la memoria caché, [!INCLUDE[ssDE](../../includes/ssde-md.md)] comprueba que el plan de consulta hace referencia a las estadísticas actualizadas.

La opción AUTO_UPDATE_STATISTICS se aplica a las estadísticas creadas para índices y columnas únicas de los predicados de consulta, así como a las estadísticas creadas con la instrucción CREATE STATISTICS. Esta opción también se aplica a las estadísticas filtradas.

El valor predeterminado es ON. Recomendamos utilizar la configuración predeterminada para la mayoría de las bases de datos.

Utilice la opción AUTO_UPDATE_STATISTICS_ASYNC para especificar si las estadísticas se actualizan sincrónica o asincrónicamente.

OFF         
Especifica que el optimizador de consultas no actualiza las estadísticas cuando una consulta las utiliza. El optimizador de consultas tampoco actualiza las estadísticas cuando podrían estar obsoletas. Establecer esta opción en OFF puede producir planes de consulta poco óptimos y un rendimiento degradado de las consultas.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_update_stats_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAutoUpdateStatistics de la función DATABASEPROPERTYEX.

Para más información, vea la sección "Utilizar las opciones de estadísticas de toda la base de datos" del tema [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

<a name="auto_update_statistics_async"></a> AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }         
ON         
Especifica que las actualizaciones de las estadísticas para la opción AUTO_UPDATE_STATISTICS son asincrónicas. El optimizador de consultas no espera a que finalicen las actualizaciones de las estadísticas para compilar las consultas.

La configuración de esta opción en ON no surte efecto a menos que AUTO_UPDATE_STATISTICS se establezca en ON.

De forma predeterminada, la opción AUTO_UPDATE_STATISTICS_ASYNC está configurada en OFF y el optimizador de consultas actualiza las estadísticas sincrónicamente.

OFF         
Especifica que las actualizaciones de las estadísticas para la opción AUTO_UPDATE_STATISTICS son sincrónicas. El optimizador de consultas espera a que finalicen las actualizaciones de las estadísticas para compilar las consultas.

La configuración de esta opción en OFF no surte efecto a menos que AUTO_UPDATE_STATISTICS esté configurado en ON.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_update_stats_async_on en la vista de catálogo sys.databases.

Para saber más sobre cuándo usar las actualizaciones de estadísticas sincrónicas o asincrónicas, vea la sección "Utilizar las opciones de estadísticas de toda la base de datos" del tema [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

<a name="auto_tuning"></a> **\<automatic_tuning_option> ::=**          
**Se aplica a**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].

Controla las opciones automáticas para el [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md).

AUTOMATIC_TUNING = { AUTO | INHERIT | CUSTOM }         
AUTO         
Si el valor de ajuste automático se establece en AUTO, se aplicarán los valores predeterminados de configuración de Azure al ajuste automático.

INHERIT         
Si se usa el valor INHERIT, se heredará la configuración predeterminada del servidor primario. Esto es especialmente útil si quiere personalizar la configuración de ajuste automático en un servidor primario y que todas las bases de datos del servidor hereden esta configuración personalizada. Tenga en cuenta que, para que la herencia funcione correctamente, las tres opciones de ajuste individuales, FORCE_LAST_GOOD_PLAN, CREATE_INDEX y DROP_INDEX, deben estar configuradas en DEFAULT en las bases de datos.

CUSTOM         
Si usa el valor CUSTOM, tendrá que configurar manualmente todas las opciones de ajuste automático disponibles en las bases de datos.

Habilita o deshabilita la opción `CREATE_INDEX` de administración de índices automática del [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md).

CREATE_INDEX = { DEFAULT | ON | OFF }         
DEFAULT         
Hereda la configuración predeterminada del servidor. En este caso, las opciones para habilitar o deshabilitar las características de Ajuste automático individuales están definidas en el nivel de servidor.

ON         
Cuando se habilita, se generan automáticamente los índices que faltan en una base de datos. Después de la creación del índice, se comprueban las mejoras de rendimiento de la carga de trabajo. Cuando el índice creado ya no proporciona ventajas en el rendimiento de la carga de trabajo, se revierte automáticamente. Los índices creados automáticamente se marcan como un índice generado por el sistema.

OFF         
No genera automáticamente índices que faltan en la base de datos.

Habilita o deshabilita la opción `DROP_INDEX` de administración de índices automática del [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md).

DROP_INDEX = { DEFAULT | ON | OFF }         
DEFAULT         
Hereda la configuración predeterminada del servidor. En este caso, las opciones para habilitar o deshabilitar las características de Ajuste automático individuales están definidas en el nivel de servidor.

ON         
Quita de forma automática los índices duplicados o que ya no son útiles para la carga de trabajo de rendimiento.

OFF         
No quita automáticamente índices que faltan en la base de datos.

Habilita o deshabilita la opción `FORCE_LAST_GOOD_PLAN` de corrección de planes automática del [ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md).

FORCE_LAST_GOOD_PLAN = { DEFAULT | ON | OFF }         
DEFAULT         
Hereda la configuración predeterminada del servidor. En este caso, las opciones para habilitar o deshabilitar las características de Ajuste automático individuales están definidas en el nivel de servidor.

ON         
El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] fuerza automáticamente el último buen plan conocido en las consultas de [!INCLUDE[tsql-md](../../includes/tsql-md.md)], donde el nuevo plan de SQL provoca regresiones de rendimiento. El parámetro [!INCLUDE[ssde_md](../../includes/ssde_md.md)] supervisa continuamente el rendimiento de la consulta [!INCLUDE[tsql-md](../../includes/tsql-md.md)] con el plan forzado. Si hay mejoras de rendimiento, el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] seguirá usando el último buen plan conocido. Si no se detectan mejoras de rendimiento, el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] generará un nuevo plan de SQL. La instrucción generará un error si el Almacén de consultas no está habilitado o si no está en modo de *lectura-escritura*.

OFF         
El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] informa de posibles regresiones de rendimiento de consultas provocadas por cambios de plan de SQL en la vista [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md), aunque estas recomendaciones no se aplican automáticamente. Para supervisar las recomendaciones activas y corregir los problemas identificados, los usuarios pueden aplicar los scripts de [!INCLUDE[tsql-md](../../includes/tsql-md.md)] que se muestran en la vista. Este es el valor predeterminado.

**\<change_tracking_option> ::=**         

Controla las opciones de seguimiento de cambios. Puede habilitar el seguimiento de cambios, establecer y cambiar opciones, y deshabilitar el seguimiento de cambios. Para ver ejemplos, consulte la sección de ejemplos más adelante en este artículo.

ON         
Habilita el seguimiento de cambios para la base de datos. Si habilita el seguimiento de cambios, también puede establecer las opciones AUTO CLEANUP y CHANGE RETENTION.

AUTO_CLEANUP = { ON | OFF }         
ON         
La información sobre el seguimiento de cambios se quita de forma automática después del período de retención especificado.

OFF         
Los datos del seguimiento de cambios no se quitan de la base de datos.

CHANGE_RETENTION =*retention_period* { DAYS | HOURS | MINUTES } Especifica el período mínimo para mantener la información del seguimiento de cambios en la base de datos. Los datos solamente se quitan cuando el valor AUTO_CLEANUP es ON.

*retention_period* es un entero que especifica el componente numérico del período de retención.

El período de retención predeterminado es de 2 días. El período de retención mínimo es de 1 minuto. El tipo de retención predeterminado es DAYS.

OFF         
Deshabilita el seguimiento de cambios para la base de datos. Deshabilite el seguimiento de cambios en todas las tablas para poder deshabilitarlo en la base de datos.

**\<cursor_option> ::=**

Controla las opciones del cursor.

CURSOR_CLOSE_ON_COMMIT { ON | OFF }         
ON         
Todos los cursores abiertos cuando confirma o deshace una transacción se cierran.

OFF         
Los cursores permanecen abiertos cuando se confirma una transacción. Cuando se revierte se cierran todos los cursores, excepto los que están definidos como INSENSITIVE o STATIC.

La configuración del nivel de conexión, establecida mediante la instrucción SET, invalida la configuración predeterminada de la base de datos para CURSOR_CLOSE_ON_COMMIT. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión que establece CURSOR_CLOSE_ON_COMMIT en OFF para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md).

Puede determinar el estado de esta opción si examina la columna is_cursor_close_on_commit_on de la vista de catálogo sys.databases o la propiedad `IsCloseCursorsOnCommitEnabled` de la función DATABASEPROPERTYEX. El cursor se desasigna implícitamente solamente cuando se realiza la desconexión. Para más información, consulte [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md).

**\<db_encryption_option> ::=**         

Controla el estado del cifrado de la base de datos.

ENCRYPTION {ON | OFF}         
Establece que se cifre (ON) o no se cifre (OFF) la base de datos. Para más información sobre el cifrado de base de datos, consulte [Cifrado de datos transparente](../../relational-databases/security/encryption/transparent-data-encryption.md) y [Cifrado de datos transparente con Azure SQL Database](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).

Cuando el cifrado está habilitado en el nivel de la base de datos, se cifrarán todos los grupos de archivos. Todos los grupos de archivos nuevos heredarán la propiedad de cifrado. Si en la base de datos hay grupos de archivos establecidos en **READ ONLY**, se producirá un error en la operación de cifrado de la base de datos.

Puede ver el estado del cifrado de la base de datos mediante la vista de administración dinámica [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md).

**\<db_update_option> ::=**         

Controla si se permiten las actualizaciones en la base de datos.

READ_ONLY         
Los usuarios pueden leer datos de la base de datos, pero no pueden modificarlos.

> [!NOTE]
>Para mejorar el rendimiento de las consultas, actualice las estadísticas antes de establecer una base de datos en READ_ONLY. Si se necesitan estadísticas adicionales después de establecer una base de datos en READ_ONLY, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] creará las estadísticas en tempdb. Para más información sobre las estadísticas para una base de datos de solo lectura, vea [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

READ_WRITE         
La base de datos está disponible para operaciones de lectura y escritura.

Para cambiar este estado, debe tener acceso exclusivo a la base de datos. Para obtener más información, vea la cláusula SINGLE_USER.

> [!NOTE]
> En las bases de datos federadas de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], SET { READ_ONLY | READ_WRITE } está deshabilitado.

**\<db_user_access_option> ::=**         

Controla el acceso del usuario a la base de datos.

RESTRICTED_USER         
RESTRICTED_USER permite que solamente se conecten a la base de datos los miembros del rol fijo de base de datos db_owner y de los roles fijos de servidor dbcreator y sysadmin, aunque no limita su número. Todas las conexiones a la base de datos se desconectan en el margen de tiempo especificado por la cláusula de terminación de la instrucción ALTER DATABASE. Una vez que la base de datos ha cambiado al estado RESTRICTED_USER, se rechazan los intentos de conexión por parte de usuarios no cualificados. **RESTRICTED_USER** no se puede modificar con Instancia administrada de SQL Database.

MULTI_USER         
Todos los usuarios que tengan los permisos correspondientes pueden conectarse a la base de datos.

Puede determinar el estado de esta opción si examina la columna user_access de la vista de catálogo sys.databases o la propiedad UserAccess de la función DATABASEPROPERTYEX.

**\<delayed_durability_option> ::=**         

Controla si las transacciones se confirman con perdurabilidad total o diferida.

DISABLED         
Todas las transacciones tras SET DISABLED son totalmente perdurables. Se omiten las opciones de perdurabilidad que se establecen en un bloque ATOMIC o en una instrucción de confirmación.

ALLOWED         
Todas las transacciones tras SET ALLOWED son totalmente perdurables o de perdurabilidad diferida, dependiendo de la opción de perdurabilidad establecida en el bloque ATOMIC o instrucción de confirmación.

FORCED         
Todas las transacciones tras SET FORCED son totalmente perdurables. Se omiten las opciones de perdurabilidad que se establecen en un bloque ATOMIC o en una instrucción de confirmación.

**\<PARAMETERIZATION_option> ::=**         

Controla la opción de parametrización.

PARAMETERIZATION { SIMPLE | FORCED }         
SIMPLE         
Las consultas incluyen parámetros en función del comportamiento predeterminado de la base de datos.

FORCED         
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye parámetros para todas las consultas de la base de datos.

El valor actual de esta opción se puede determinar mediante el examen de la columna `is_parameterization_forced` en la vista de catálogo `sys.databases`.

**\<query_store_options> ::=**

ON | OFF | CLEAR [ ALL ]         
Controla si el almacén de consultas está habilitado en esta base de datos y también controla la eliminación del contenido del almacén de consultas.

ON         
Habilita el almacén de consultas.

OFF         
Deshabilita el almacén de consultas. Este es el valor predeterminado.

CLEAR         
Quita el contenido del almacén de consultas.

OPERATION_MODE         
Describe el modo de operación del almacén de consultas. Los valores válidos son READ_ONLY y READ_WRITE. En el modo READ_WRITE, el almacén de consultas recopila y continúa el plan de consultas y la información de estadística del tiempo de ejecución. En el modo READ_ONLY, la información se puede leer del almacén de consultas, pero no se agrega información nueva. Si se ha agotado el espacio máximo del almacén de consultas, el almacén de consultas cambiará el modo de operación a READ_ONLY.

CLEANUP_POLICY         
Describe la directiva de retención de datos del almacén de consultas. STALE_QUERY_THRESHOLD_DAYS determina el número de días durante los que se conserva la información de una consulta en el almacén de consultas. STALE_QUERY_THRESHOLD_DAYS es de tipo **bigint**.

DATA_FLUSH_INTERVAL_SECONDS         
Determina la frecuencia con la que los datos escritos en el almacén de consultas se conservan en el disco. Para optimizar el rendimiento, los datos recopilados por el almacén de consultas se escriben de manera asincrónica en el disco. La frecuencia con la que se produce esta transferencia asincrónica se configura mediante el argumento DATA_FLUSH_INTERVAL_SECONDS. DATA_FLUSH_INTERVAL_SECONDS es de tipo **bigint**.

MAX_STORAGE_SIZE_MB         
Determina el espacio asignado al almacén de consultas. MAX_STORAGE_SIZE_MB es de tipo **bigint**.

INTERVAL_LENGTH_MINUTES         
Determina el intervalo de tiempo en el que se agregan los datos de estadísticas de ejecución en tiempo de ejecución al almacén de consultas. Para optimizar el uso del espacio, se agregan las estadísticas de ejecución en tiempo de ejecución en el almacén de estadísticas de tiempo de ejecución en una ventana de tiempo fijo. Esta ventana de tiempo fijo se configura con el argumento INTERVAL_LENGTH_MINUTES. INTERVAL_LENGTH_MINUTES es de tipo **bigint**.

SIZE_BASED_CLEANUP_MODE         
Controla si la limpieza se activará automáticamente cuando la cantidad total de datos se acerque al tamaño máximo:

OFF         
La limpieza según el tamaño no se activará automáticamente.

AUTO         
La limpieza según el tamaño se activará automáticamente cuando el tamaño en disco alcance el 90 % de **max_storage_size_mb**. La limpieza según el tamaño quita primero las consultas menos caras y más antiguas. Se detiene aproximadamente en el 80 % de **max_storage_size_mb**. Es el valor de configuración predeterminado.

SIZE_BASED_CLEANUP_MODE es de tipo **nvarchar**.

QUERY_CAPTURE_MODE         
Designa el modo de captura de consulta que está activo:

ALL         
Se capturan todas las consultas. Es el valor de configuración predeterminado.

AUTO         
Captura consultas pertinentes en función del consumo de recursos y el recuento de ejecuciones. Es el valor de configuración predeterminado para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

Ninguno         
Detiene la captura de nuevas consultas. El almacén de consultas seguirá recopilando estadísticas de compilación y tiempo de ejecución para las consultas que ya se capturaron. Use esta configuración con precaución ya que podría omitir la captura de consultas importantes.

QUERY_CAPTURE_MODE es de tipo **nvarchar**.

max_plans_per_query         
Entero que representa el número máximo de planes que se tienen para cada consulta. El valor predeterminado es 200.

**\<snapshot_option> ::=**         

Determina el nivel de aislamiento de transacción.

ALLOW_SNAPSHOT_ISOLATION { ON | OFF }         
ON         
Habilita la opción de instantánea en el nivel de base de datos. Cuando se habilita, las instrucciones DML inician la generación de versiones de fila aunque ninguna transacción utilice el aislamiento de instantánea. Una vez habilitada esta opción, las transacciones pueden especificar el nivel de aislamiento de transacción SNAPSHOT. Si se ejecuta una transacción en el nivel de aislamiento SNAPSHOT, todas las instrucciones verán una instantánea de los datos tal como estaban al inicio de la transacción. Si una transacción ejecutada en el nivel de aislamiento SNAPSHOT tiene acceso a los datos de varias bases de datos, ALLOW_SNAPSHOT_ISOLATION debe establecerse en ON en todas las bases de datos o cada instrucción de la transacción debe utilizar sugerencias de bloqueo en cualquier referencia de una cláusula FROM a una tabla de una base de datos donde ALLOW_SNAPSHOT_ISOLATION sea OFF.

OFF         
Desactiva la opción de instantánea en el nivel de base de datos. Las transacciones no pueden especificar el nivel de aislamiento de la transacción SNAPSHOT.

Si se establece ALLOW_SNAPSHOT_ISOLATION en un estado nuevo (de ON a OFF o de OFF a ON), ALTER DATABASE no devuelve el control al autor de la llamada hasta confirmar todas las transacciones existentes de la base de datos. Si la base de datos ya se encuentra en el estado especificado en la instrucción ALTER DATABASE, se devuelve de inmediato el control al autor de la llamada. Use [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) para determinar si hay transacciones de ejecución prolongada si la instrucción ALTER DATABASE no devuelve resultados rápidamente. Si se cancela la instrucción ALTER DATABASE, la base de datos permanece en el estado en que estaba al iniciar ALTER DATABASE. La vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) indica el estado de las transacciones de aislamiento de instantáneas en la base de datos. Si **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON, ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF se pausará durante seis segundos y reintentará la operación.

No puede cambiar el estado de ALLOW_SNAPSHOT_ISOLATION si la base de datos está establecida en OFFLINE.

Si establece ALLOW_SNAPSHOT_ISOLATION en una base de datos READ_ONLY, la configuración se mantendrá si la base de datos se establece posteriormente en READ_WRITE.

Puede cambiar la configuración de ALLOW_SNAPSHOT_ISOLATION para las bases de datos maestra, model, msdb y tempdb. La configuración se mantiene cada vez que la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se detiene y se reinicia si cambia la configuración para tempdb. Si cambia la configuración para la base de datos model, dicha configuración se convierte en la configuración predeterminada para todas las bases de datos nuevas que se crean, excepto para tempdb.

La opción es ON de forma predeterminada para las bases de datos maestra y msdb.

La configuración actual de esta opción se puede determinar mediante el examen de la columna snapshot_isolation_state de la vista de catálogo sys.databases.

READ_COMMITTED_SNAPSHOT { ON | OFF }         
ON         
Habilita la opción de instantánea de lectura confirmada en el nivel de base de datos. Cuando se habilita, las instrucciones DML inician la generación de versiones de fila aunque ninguna transacción utilice el aislamiento de instantánea. Una vez habilitada esta opción, las transacciones que especifican el nivel de aislamiento de lectura confirmada usan versiones de fila en lugar de bloqueos. Todas las instrucciones ven una instantánea de los datos tal como estaban al inicio de la instrucción si una transacción se ejecuta en el nivel de aislamiento de lectura conformada.

OFF         
Desactiva la opción de instantánea de lectura confirmada en el nivel de base de datos. Las transacciones que especifican el nivel de aislamiento READ COMMITTED utilizan el bloqueo.

Para establecer READ_COMMITTED_SNAPSHOT en ON u OFF, no puede haber ninguna conexión activa a la base de datos, excepto la que ejecuta el comando ALTER DATABASE. Sin embargo, no es necesario que la base de datos esté en modo de usuario único. No puede cambiar el estado de esta opción si la base de datos está establecida en OFFLINE.

Si establece READ_COMMITTED_SNAPSHOT en una base de datos READ_ONLY, la configuración se mantendrá si la base de datos se establece después en READ_WRITE.

READ_COMMITTED_SNAPSHOT no se puede cambiar a ON para las bases de datos maestra, tempdb o msdb. Si cambia la configuración para model, dicha configuración se convierte en predeterminada para todas las bases de datos creadas, excepto para tempdb.

La configuración actual de esta opción se puede determinar mediante el examen de la columna is_read_committed_snapshot_on de la vista de catálogo sys.databases.

> [!WARNING]
> Cuando se crea una tabla con `DURABILITY = SCHEMA_ONLY` y posteriormente se cambia **READ_COMMITTED_SNAPSHOT** con `ALTER DATABASE`, se pierden los datos de la tabla.

MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }         
ON         
Cuando el nivel de aislamiento de transacción se establece en uno inferior a SNAPSHOT, todas las operaciones interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] en las tablas optimizadas para memoria se ejecutan con aislamiento SNAPSHOT. Los ejemplos de los niveles de aislamiento inferiores a la instantánea son READ COMMITTED o READ UNCOMMITTED. Estas operaciones se ejecutan si el nivel de aislamiento de transacción se establece explícitamente en el nivel de sesión o el valor predeterminado se utiliza de forma implícita.

OFF         
No eleva el nivel de aislamiento de transacción para las operaciones interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] en las tablas optimizadas para memoria.

No puede cambiar el estado de MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT si la base de datos está establecida en OFFLINE.

El valor predeterminado es OFF.

La configuración actual de esta opción se puede determinar mediante el examen de la columna **memory_optimized_elevate_to_snapshot** de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

**\<sql_option> ::=**         

Controla las opciones de cumplimiento con ANSI en el nivel de base de datos.

ANSI_NULL_DEFAULT { ON | OFF }         
Determina el valor predeterminado, NULL o NOT NULL, de una columna o del [tipo definido por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) para los que no se ha definido la nulabilidad explícitamente en las instrucciones CREATE TABLE o ALTER TABLE. Las columnas para las que se hayan definido restricciones siguen las reglas de las restricciones, independientemente de esta configuración.

ON         
El valor predeterminado es NULL.

OFF         
El valor predeterminado es NOT NULL.

La configuración del nivel de conexión, establecida mediante la instrucción SET, invalida la configuración predeterminada del nivel de base de datos para ANSI_NULL_DEFAULT. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_NULL_DEFAULT en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).

Para la compatibilidad con ANSI, si se establece la opción de base de datos ANSI_NULL_DEFAULT en ON, el valor predeterminado cambia a NULL.

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_null_default_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiNullDefault de la función DATABASEPROPERTYEX.

ANSI_NULLS { ON | OFF }         
ON         
Todas las comparaciones con un valor NULL se evalúan como UNKNOWN.

OFF         
Las comparaciones de valores no UNICODE con un valor NULL se evalúan como TRUE si ambos valores son NULL.

> [!IMPORTANT]
> En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_NULLS siempre estará ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.

  La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para ANSI_NULLS. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_NULLS en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md).

El valor de SET ANSI_NULLS también debe estar en ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_nulls_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiNullsEnabled de la función DATABASEPROPERTYEX.

ANSI_PADDING { ON | OFF }         
ON         
Las cadenas se rellenan a la misma longitud antes de la conversión. También se rellenan hasta la misma longitud antes de la inserción en un tipo de datos **varchar** o **nvarchar**.

OFF         
Inserta espacios en blanco finales en los valores de caracteres en las columnas **varchar** o **nvarchar**. También deja los ceros a la derecha en los valores binarios insertados en columnas **varbinary**. Los valores no se rellenan hasta completar la longitud de la columna.

Si se especifica OFF, esta opción solamente afecta a la definición de las columnas nuevas.

> [!IMPORTANT]
> En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_PADDING siempre estará en ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Se recomienda establecer siempre ANSI_PADDING en ON. ANSI_PADDING también debe estar en ON al crear o tratar índices en columnas calculadas o vistas indizadas.

**char(_n_)** y **binary(_n_)** las columnas que admiten valores NULL se rellenan hasta la longitud de la columna cuando ANSI_PADDING se establece en ON. Los ceros y los espacios en blanco finales se recortan si ANSI_PADDING es OFF. Las columnas **char(_n_)** y **binary(_n_)** que no permiten valores NULL siempre se rellenan hasta completar la longitud de la columna.

  La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada del nivel de base de datos para ANSI_PADDING. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_PADDING en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_padding_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiPaddingEnabled de la función DATABASEPROPERTYEX.

ANSI_WARNINGS { ON | OFF }         
ON         
Se emiten errores o advertencias si se dan condiciones tales como la división por cero. También se emiten errores y advertencias cuando aparecen valores null en funciones de agregado.

OFF         
No se genera ninguna advertencia ni se devuelven valores NULL si se producen condiciones como la división por cero.

El valor de SET ANSI_WARNINGS debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

  La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para ANSI_WARNINGS. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_WARNINGS en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_warnings_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiWarningsEnabled de la función DATABASEPROPERTYEX.

ARITHABORT { ON | OFF }         
ON         
Se finaliza una consulta cuando se produce un error de desbordamiento o de división por cero durante su ejecución.

OFF         
Aparece un mensaje de advertencia cuando se produce uno de estos errores. La consulta, el proceso por lotes o la transacción continúa procesándose como si no se hubiera producido ningún error aunque se muestre una advertencia.

El valor de SET ARITHABORT debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

  Puede determinar el estado de esta opción mediante el examen de la columna is_arithabort_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad `IsArithmeticAbortEnabled` de la función DATABASEPROPERTYEX.

COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 }         
Para más información, consulte [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).

CONCAT_NULL_YIELDS_NULL { ON | OFF }         
ON         
El resultado de una operación de concatenación es NULL si alguno de los operandos es NULL. Por ejemplo, la concatenación de la cadena de caracteres "Esto es" y NULL da como resultado el valor NULL, y no el valor "Esto es".

OFF         
El valor NULL se trata como una cadena de caracteres vacía.

El valor de CONCAT_NULL_YIELDS_NULL también debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

> [!IMPORTANT]
> En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], CONCAT_NULL_YIELDS_NULL siempre estará en ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.

La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para CONCAT_NULL_YIELDS_NULL. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen CONCAT_NULL_YIELDS_NULL en ON para la sesión al realizar la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_concat_null_yields_null_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsNullConcat de la función DATABASEPROPERTYEX.

QUOTED_IDENTIFIER { ON | OFF }         
ON         
Las comillas dobles se pueden usar para identificadores delimitados.

Todas las cadenas delimitadas por comillas dobles se interpretan como identificadores de objetos. Los identificadores entre comillas no tienen que adaptarse a las reglas de [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Pueden ser palabras clave e incluir caracteres que no se permiten en los identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Si una comilla simple (') forma parte de la cadena literal, puede representarse mediante comillas dobles (").

OFF         
Los identificadores no se pueden incluir entre comillas y deben seguir todas las reglas de [!INCLUDE[tsql](../../includes/tsql-md.md)] para los identificadores. Los literales se pueden delimitar con comillas simples o dobles.

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también permite delimitar los identificadores con corchetes ([ ]). Los identificadores entre corchetes pueden usarse siempre, independientemente del valor de QUOTED_IDENTIFIER. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).

  Al crear una tabla, la opción QUOTED IDENTIFIER siempre se almacena como ON en los metadatos de la tabla. La opción se almacena incluso si está establecida en OFF al crear la tabla.

La configuración en el nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para QUOTED_IDENTIFIER. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión estableciendo QUOTED_IDENTIFIER en ON. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).

  Puede determinar el estado de esta opción mediante el examen de la columna is_quoted_identifier_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsQuotedIdentifiersEnabled de la función DATABASEPROPERTYEX.

NUMERIC_ROUNDABORT { ON | OFF }         
ON         
Se genera un error cuando se produce una pérdida de precisión en una expresión.

OFF         
Las pérdidas de precisión no generan mensajes de error y el resultado se redondea con la precisión de la columna o variable que lo almacena.

El valor de NUMERIC_ROUNDABORT debe ser OFF al crear o realizar cambios en índices de columnas calculadas o vistas indizadas.

Puede determinar el estado de esta opción mediante el examen de la columna is_numeric_roundabort_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsNumericRoundAbortEnabled de la función DATABASEPROPERTYEX.

RECURSIVE_TRIGGERS { ON | OFF }         
ON         
Se permite la activación recursiva de desencadenadores AFTER.

OFF         
Puede determinar el estado de esta opción mediante el examen de la columna is_recursive_triggers_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsRecursiveTriggersEnabled de la función DATABASEPROPERTYEX.

> [!NOTE]
> La recursividad directa solo se evita cuando RECURSIVE_TRIGGERS se establece en OFF. Para deshabilitar la recursividad indirecta, también debe establecer la opción de servidor desencadenadores anidados en 0.

Puede determinar el estado de esta opción si examina la columna is_recursive_triggers_on de la vista de catálogo sys.databases o la propiedad IsRecursiveTriggersEnabled de la función DATABASEPROPERTYEX.

**\<target_recovery_time_option> ::=**         

Especifica la frecuencia de puntos de comprobación indirectos por base de datos. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], el valor predeterminado para nuevas bases de datos es de un minuto, lo cual indica que la base de datos usará puntos de comprobación indirectos. Para versiones anteriores, el valor predeterminado es 0, lo cual indica que la base de datos usará puntos de comprobación automáticos, cuya frecuencia depende del valor de intervalo de recuperación de la instancia de servidor. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda un minuto para la mayoría de los sistemas.

TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS | MINUTES }         
*target_recovery_time*         
Especifica el límite máximo de tiempo para recuperar la base de datos especificada en caso de bloqueo.

SECONDS         
Indica que *target_recovery_time* se expresa como el número de segundos.

MINUTES         
Indica que *target_recovery_time* se expresa como el número de minutos.

Para más información sobre los puntos de control indirectos, consulte [Puntos de control de base de datos](../../relational-databases/logs/database-checkpoints-sql-server.md).

**WITH \<termination> ::=**         

Especifica el momento en que se revierten las transacciones incompletas cuando la base de datos pasa de un estado a otro. Si se omite la cláusula de terminación, la instrucción ALTER DATABASE espera indefinidamente a que se produzca un bloqueo en la base de datos. Solamente se puede especificar una cláusula de terminación y debe seguir a las cláusulas SET.

> [!NOTE]
> No todas las opciones de base de datos usan la cláusula WITH \<termination>. Para más información, consulte la tabla ubicada en "[Opciones de configuración](#SettingOptions) de la sección "Comentarios" de este artículo.

ROLLBACK AFTER *integer* [SECONDS] | ROLLBACK IMMEDIATE         
Especifica si la operación de reversión se ejecuta transcurrido un número de segundos determinado o de forma inmediata.

NO_WAIT         
Especifica que la solicitud producirá un error si el cambio de opción o estado de la base de datos solicitado no puede completarse inmediatamente. Completarse inmediatamente significa que no se espera a que las transacciones se confirmen o reviertan por su cuenta.

## <a name="SettingOptions"></a> Configurar opciones         

Para recuperar la configuración actual de las opciones de base de datos, use la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) o [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md).

Una vez configurada una opción de la base de datos, la modificación surte efecto de inmediato.

Puede cambiar los valores predeterminados de cualquiera de las opciones de las bases de datos recién creadas. Para ello, cambie la opción adecuada de base de datos en la base de datos de modelo.

No todas las opciones de base de datos usan la cláusula WITH \<termination> ni se pueden especificar en combinación con otras opciones. En la siguiente tabla se incluyen estas opciones, su estado y el estado de terminación.

|Categoría de opciones|Se puede especificar con otras opciones|Puede usar la cláusula WITH \<termination>|
|----------------------|-----------------------------------------|---------------------------------------------|
|\<auto_option>|Sí|No|
|\<change_tracking_option>|Sí|Sí|
|\<cursor_option>|Sí|No|
|\<db_encryption_option>|Sí|No|
|\<db_update_option>|Sí|Sí|
|\<db_user_access_option>|Sí|Sí|
|\<delayed_durability_option>|Sí|Sí|
|\<parameterization_option>|Sí|Sí|
|ALLOW_SNAPSHOT_ISOLATION|No|No|
|READ_COMMITTED_SNAPSHOT|No|Sí|
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|Sí|Sí|
|DATE_CORRELATION_OPTIMIZATION|Sí|Sí|
|\<sql_option>|Sí|No|
|\<target_recovery_time_option>|No|Sí|

## <a name="examples"></a>Ejemplos

### <a name="a-setting-the-database-to-read_only"></a>A. Establecer la base de datos en READ_ONLY
El cambio del estado de una base de datos o un grupo de archivos a READ_ONLY o READ_WRITE requiere el acceso exclusivo a la base de datos. En el siguiente ejemplo la base de datos se establece en el modo `RESTRICTED_USER` para limitar el acceso. A continuación, el ejemplo establece el estado de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en `READ_ONLY` y devuelve el acceso a la base de datos a todos los usuarios.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
SET RESTRICTED_USER;
GO
ALTER DATABASE AdventureWorks2012
SET READ_ONLY
GO
ALTER DATABASE AdventureWorks2012
SET MULTI_USER;
GO

```

### <a name="b-enabling-snapshot-isolation-on-a-database"></a>B. Habilitar el aislamiento de instantánea en una base de datos
En el siguiente ejemplo se habilita la opción del marco de aislamiento de instantánea para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .

```sql
USE AdventureWorks2012;
USE master;
GO
ALTER DATABASE AdventureWorks2012
SET ALLOW_SNAPSHOT_ISOLATION ON;
GO
-- Check the state of the snapshot_isolation_framework
-- in the database.
SELECT name, snapshot_isolation_state,
    snapshot_isolation_state_desc AS description
FROM sys.databases
WHERE name = N'AdventureWorks2012';
GO
```

El conjunto de resultados muestra que el marco de aislamiento de instantánea está habilitado.

|NAME |snapshot_isolation_state |description|
|-------------------- |------------------------|----------|
|AdventureWorks2012 |1| ON |

### <a name="c-enabling-modifying-and-disabling-change-tracking"></a>C. Habilitar, modificar y deshabilitar el seguimiento de cambios

En el ejemplo siguiente se habilita el seguimiento de cambios para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y se establece el período de retención en `2` días.

```sql
ALTER DATABASE AdventureWorks2012
SET CHANGE_TRACKING = ON
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);
```

En el ejemplo siguiente se muestra cómo cambiar el período de retención a `3` días.

```sql
ALTER DATABASE AdventureWorks2012
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);
```

En el ejemplo siguiente se muestra cómo deshabilitar el seguimiento de cambios para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .

```sql
ALTER DATABASE AdventureWorks2012
SET CHANGE_TRACKING = OFF;
```

### <a name="d-enabling-the-query-store"></a>D. Habilitar el almacén de consultas

En el ejemplo siguiente se habilita el almacén de consultas y configura los parámetros de almacén de consultas.

```sql
ALTER DATABASE AdventureWorks2012
SET QUERY_STORE = ON
(
      OPERATION_MODE = READ_WRITE
    , CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 )
    , DATA_FLUSH_INTERVAL_SECONDS = 900
    , MAX_STORAGE_SIZE_MB = 1024
    , INTERVAL_LENGTH_MINUTES = 60
    );
```

## <a name="see-also"></a>Consulte también

- [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)
- [Creación de reflejo de la base de datos de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)
- [Estadísticas](../../relational-databases/statistics/statistics.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-currentls)
- [Habilitar y deshabilitar el seguimiento de cambios](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [Procedimiento recomendado con el Almacén de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](alter-database-transact-sql-set-options.md?view=sql-server-2017)|[Grupo de bases de datos elásticas o base de datos única de<br />SQL Database](alter-database-transact-sql-set-options.md?view=azuresqldb-current) |**_\* Instancia administrada de <br />SQL Database \*_** &nbsp;||[SQL Data<br />Warehouse](alter-database-transact-sql-set-options.md?view=azure-sqldw-latest)||||

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Instancia administrada de Azure SQL Database

Los niveles de compatibilidad son opciones de `SET`, pero se describe en [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).

> [!NOTE]
> Es posible configurar muchas opciones SET de la base de datos para la sesión actual mediante [Instrucciones SET](../../t-sql/statements/set-statements-transact-sql.md), aunque generalmente las configuran las aplicaciones al realizar la conexión. Las opciones SET de nivel de sesión reemplazan a los valores **ALTER DATABASE SET** . Las opciones de base de datos descritas a continuación son valores que se pueden establecer en las sesiones que no proporcionan explícitamente otros valores de opciones SET.

## <a name="syntax"></a>Sintaxis

```
ALTER DATABASE { database_name | Current }
SET
{
    <optionspec> [ ,...n ]
}
;

<optionspec> ::=
{
    <auto_option>
  | <change_tracking_option>
  | <cursor_option>
  | <db_encryption_option>
  | <delayed_durability_option>
  | <parameterization_option>
  | <query_store_options>
  | <snapshot_option>
  | <sql_option>
  | <target_recovery_time_option>
  | <termination>
  | <temporal_history_retention>
}
;
<auto_option> ::=
{
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }
  | AUTO_SHRINK { ON | OFF }
  | AUTO_UPDATE_STATISTICS { ON | OFF }
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}

<automatic_tuning_option> ::=
{
  AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { ON | OFF } )
}

<change_tracking_option> ::=
{
  CHANGE_TRACKING
   {
       = OFF
     | = ON [ ( <change_tracking_option_list > [,...n] ) ]
     | ( <change_tracking_option_list> [,...n] )
   }
}

<change_tracking_option_list> ::=
   {
       AUTO_CLEANUP = { ON | OFF }
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }
   }

<cursor_option> ::=
{
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }
}

<db_encryption_option> ::=
  ENCRYPTION { ON | OFF }

<delayed_durability_option> ::=DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }

<parameterization_option> ::=
  PARAMETERIZATION { SIMPLE | FORCED }

<query_store_options> ::=
{
  QUERY_STORE
  {
    = OFF
    | = ON [ ( <query_store_option_list> [,... n] ) ]
    | ( < query_store_option_list> [,... n] )
    | CLEAR [ ALL ]
  }
}

<query_store_option_list> ::=
{
  OPERATION_MODE = { READ_WRITE | READ_ONLY }
  | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )
  | DATA_FLUSH_INTERVAL_SECONDS = number
  | MAX_STORAGE_SIZE_MB = number
  | INTERVAL_LENGTH_MINUTES = number
  | SIZE_BASED_CLEANUP_MODE = [ AUTO | OFF ]
  | QUERY_CAPTURE_MODE = [ ALL | AUTO | NONE ]
  | MAX_PLANS_PER_QUERY = number
}

<snapshot_option> ::=
{
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }
  | READ_COMMITTED_SNAPSHOT {ON | OFF }
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }
}
<sql_option> ::=
{
    ANSI_NULL_DEFAULT { ON | OFF }
  | ANSI_NULLS { ON | OFF }
  | ANSI_PADDING { ON | OFF }
  | ANSI_WARNINGS { ON | OFF }
  | ARITHABORT { ON | OFF }
  | COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }
  | NUMERIC_ROUNDABORT { ON | OFF }
  | QUOTED_IDENTIFIER { ON | OFF }
  | RECURSIVE_TRIGGERS { ON | OFF }
}

<temporal_history_retention>::=TEMPORAL_HISTORY_RETENTION { ON | OFF }
```

## <a name="arguments"></a>Argumentos

*database_name*         
Es el nombre de la base de datos que se va a modificar.

CURRENT         
`CURRENT` realiza la acción en la base de datos actual. `CURRENT` no se admite para todas las opciones en todos los contextos. Si `CURRENT` produce un error, proporcione el nombre de la base de datos.

**\<auto_option> ::=**         

Controla las opciones automáticas.

<a name="auto_create_statistics"></a> AUTO_CREATE_STATISTICS { ON | OFF }         
ON         
El optimizador de consultas crea las estadísticas en columnas únicas de los predicados de consulta, según sea necesario, para mejorar los planes de consulta y el rendimiento de las consultas. Estas estadísticas de columna única se crean cuando el optimizador de consultas las compila. Las estadísticas de columna única solamente se crean en las columnas que ya no son la primera columna de un objeto de estadísticas existente.

El valor predeterminado es ON. Recomendamos utilizar la configuración predeterminada para la mayoría de las bases de datos.

OFF         
El optimizador de consultas no crea estadísticas en columnas únicas de los predicados de consulta cuando está compilando consultas. Establecer esta opción en OFF puede producir planes de consulta poco óptimos y un rendimiento degradado de las consultas.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_create_stats_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAutoCreateStatistics de la función DATABASEPROPERTYEX.

Para más información, vea la sección "Utilizar las opciones de estadísticas de toda la base de datos" del tema [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

INCREMENTAL = ON | OFF         
Establezca AUTO_CREATE_STATISTICS en ON y establezca INCREMENTAL en ON. Esta configuración crea automáticamente estadísticas como incrementales siempre que se admitan estadísticas incrementales. El valor predeterminado es OFF. Para más información, consulte [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md).

<a name="auto_shrink"></a> AUTO_SHRINK { ON | OFF }         
ON         
Los archivos de la base de datos se pueden reducir periódicamente.

Pueden reducirse automáticamente los archivos de datos y los archivos de registro. AUTO_SHRINK reduce el tamaño del registro de transacciones solo si establece la base de datos en el modelo de recuperación SIMPLE o si realiza una copia de seguridad del registro. Cuando se establece en OFF, los archivos de la base de datos no se reducen de forma automática durante las comprobaciones periódicas del espacio no utilizado.

La opción AUTO_SHRINK reduce los archivos cuando no se utiliza más de un 25% del espacio del archivo. La opción hace que el archivo se reduzca a uno de dos tamaños. Se reduce al que sea más grande de los siguientes:

- El tamaño donde el 25 por ciento del archivo es espacio no utilizado
- El tamaño del archivo cuando se creó

No puede reducir una base de datos de solo lectura.

OFF         
Los archivos de la base de datos no se reducen automáticamente durante las comprobaciones periódicas del espacio no utilizado.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_shrink_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAutoShrink de la función DATABASEPROPERTYEX.

> [!NOTE]
> La opción AUTO_SHRINK no está disponible en una base de datos independiente.

<a name="auto_update_statistics"></a> AUTO_UPDATE_STATISTICS { ON | OFF }         
ON         
Especifica que el optimizador de consultas actualiza las estadísticas cuando son usadas por una consulta y pudieran estar obsoletas. Las estadísticas se vuelven obsoletas después de que operaciones de inserción, actualización, eliminación o combinación cambien la distribución de los datos en la tabla o la vista indizada. El optimizador de consultas determina cuándo han podido quedar obsoletas las estadísticas contando el número de modificaciones de datos desde la actualización más reciente de las estadísticas, comparando el número de modificaciones con respecto a un umbral. El umbral se basa en el número de filas de la tabla o la vista indizada.

El optimizador de consultas comprueba que hay estadísticas obsoletas antes de que compile una consulta y ejecuta un plan de consulta almacenado en caché. El Optimizador de consultas utiliza las columnas, tablas y vistas indexadas en el predicado de consulta para determinar qué estadísticas podrían estar obsoletas. El optimizador de consultas determina esta información antes de que compile una consulta. Antes de ejecutar un plan de consulta almacenado en la memoria caché, [!INCLUDE[ssDE](../../includes/ssde-md.md)] comprueba que el plan de consulta hace referencia a las estadísticas actualizadas.

La opción AUTO_UPDATE_STATISTICS se aplica a las estadísticas creadas para índices y columnas únicas de los predicados de consulta, así como a las estadísticas creadas con la instrucción CREATE STATISTICS. Esta opción también se aplica a las estadísticas filtradas.

El valor predeterminado es ON. Recomendamos utilizar la configuración predeterminada para la mayoría de las bases de datos.

Utilice la opción AUTO_UPDATE_STATISTICS_ASYNC para especificar si las estadísticas se actualizan sincrónica o asincrónicamente.

OFF         
Especifica que el optimizador de consultas no actualiza las estadísticas cuando una consulta las utiliza. El optimizador de consultas tampoco actualiza las estadísticas cuando podrían estar obsoletas. Establecer esta opción en OFF puede producir planes de consulta poco óptimos y un rendimiento degradado de las consultas.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_update_stats_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAutoUpdateStatistics de la función DATABASEPROPERTYEX.

Para más información, vea la sección "Utilizar las opciones de estadísticas de toda la base de datos" del tema [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

<a name="auto_update_statistics_async"></a> AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }         
ON         
Especifica que las actualizaciones de las estadísticas para la opción AUTO_UPDATE_STATISTICS son asincrónicas. El optimizador de consultas no espera a que finalicen las actualizaciones de las estadísticas para compilar las consultas.

La configuración de esta opción en ON no surte efecto a menos que AUTO_UPDATE_STATISTICS se establezca en ON.

De forma predeterminada, la opción AUTO_UPDATE_STATISTICS_ASYNC está configurada en OFF y el optimizador de consultas actualiza las estadísticas sincrónicamente.

OFF         
Especifica que las actualizaciones de las estadísticas para la opción AUTO_UPDATE_STATISTICS son sincrónicas. El optimizador de consultas espera a que finalicen las actualizaciones de las estadísticas para compilar las consultas.

La configuración de esta opción en OFF no surte efecto a menos que AUTO_UPDATE_STATISTICS esté configurado en ON.

Puede determinar el estado de esta opción mediante el examen de la columna is_auto_update_stats_async_on en la vista de catálogo sys.databases.

Para saber más sobre cuándo usar las actualizaciones de estadísticas sincrónicas o asincrónicas, vea la sección "Utilizar las opciones de estadísticas de toda la base de datos" del tema [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

<a name="auto_tuning"></a> **\<automatic_tuning_option> ::=**          
**Se aplica a**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].

Habilita o deshabilita la opción [Ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md) de `FORCE_LAST_GOOD_PLAN`.

FORCE_LAST_GOOD_PLAN = { ON | OFF }         
ON         
El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] fuerza automáticamente el último buen plan conocido en las consultas de [!INCLUDE[tsql-md](../../includes/tsql-md.md)], donde el nuevo plan de SQL provoca regresiones de rendimiento. El parámetro [!INCLUDE[ssde_md](../../includes/ssde_md.md)] supervisa continuamente el rendimiento de la consulta [!INCLUDE[tsql-md](../../includes/tsql-md.md)] con el plan forzado. Si hay mejoras de rendimiento, el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] seguirá usando el último buen plan conocido. Si no se detectan mejoras de rendimiento, el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] generará un nuevo plan de SQL. La instrucción generará un error si el Almacén de consultas no está habilitado o si no está en modo de *lectura-escritura*. 

OFF         
El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] informa de posibles regresiones de rendimiento de consultas provocadas por cambios de plan de SQL en la vista [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md), aunque estas recomendaciones no se aplican automáticamente. Para supervisar las recomendaciones activas y corregir los problemas identificados, los usuarios pueden aplicar los scripts de [!INCLUDE[tsql-md](../../includes/tsql-md.md)] que se muestran en la vista. Este es el valor predeterminado.

**\<change_tracking_option> ::=**

Controla las opciones de seguimiento de cambios. Puede habilitar el seguimiento de cambios, establecer y cambiar opciones, y deshabilitar el seguimiento de cambios. Para ver ejemplos, consulte la sección de ejemplos más adelante en este artículo.

ON         
Habilita el seguimiento de cambios para la base de datos. Si habilita el seguimiento de cambios, también puede establecer las opciones AUTO CLEANUP y CHANGE RETENTION.

AUTO_CLEANUP = { ON | OFF }         
ON         
La información sobre el seguimiento de cambios se quita de forma automática después del período de retención especificado.

OFF         
Los datos del seguimiento de cambios no se quitan de la base de datos.

CHANGE_RETENTION =*retention_period* { DAYS | HOURS | MINUTES }         
Especifica el período mínimo para mantener la información del seguimiento de cambios en la base de datos. Los datos solamente se quitan cuando el valor AUTO_CLEANUP es ON.

*retention_period* es un entero que especifica el componente numérico del período de retención.

El período de retención predeterminado es de 2 días. El período de retención mínimo es de 1 minuto. El tipo de retención predeterminado es DAYS.

OFF         
Deshabilita el seguimiento de cambios para la base de datos. Deshabilite el seguimiento de cambios en todas las tablas para poder deshabilitarlo en la base de datos.

**\<cursor_option> ::=**         

Controla las opciones del cursor.

CURSOR_CLOSE_ON_COMMIT { ON | OFF }         
ON         
Todos los cursores abiertos cuando confirma o deshace una transacción se cierran.

OFF         
Los cursores permanecen abiertos cuando se confirma una transacción. Cuando se revierte se cierran todos los cursores, excepto los que están definidos como INSENSITIVE o STATIC.

La configuración del nivel de conexión, establecida mediante la instrucción SET, invalida la configuración predeterminada de la base de datos para CURSOR_CLOSE_ON_COMMIT. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión que establece CURSOR_CLOSE_ON_COMMIT en OFF para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET CURSOR_CLOSE_ON_COMMIT](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md).

Puede determinar el estado de esta opción si examina la columna is_cursor_close_on_commit_on de la vista de catálogo sys.databases o la propiedad IsCloseCursorsOnCommitEnabled de la función DATABASEPROPERTYEX. El cursor se desasigna implícitamente solamente cuando se realiza la desconexión. Para más información, consulte [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md).

**\<db_encryption_option> ::=**         

Controla el estado del cifrado de la base de datos.

ENCRYPTION { ON | OFF }         
Establece que se cifre (ON) o no se cifre (OFF) la base de datos. Para más información sobre el cifrado de base de datos, consulte [Cifrado de datos transparente](../../relational-databases/security/encryption/transparent-data-encryption.md) y [Cifrado de datos transparente con Azure SQL Database](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).

Cuando el cifrado está habilitado en el nivel de la base de datos, se cifrarán todos los grupos de archivos. Todos los grupos de archivos nuevos heredarán la propiedad de cifrado. Si en la base de datos hay grupos de archivos establecidos en **READ ONLY**, se producirá un error en la operación de cifrado de la base de datos.

Puede ver el estado del cifrado de la base de datos mediante la vista de administración dinámica [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md).

**\<db_update_option> ::=**         

Controla si se permiten las actualizaciones en la base de datos.

READ_ONLY         
Los usuarios pueden leer datos de la base de datos, pero no pueden modificarlos.

> [!NOTE]
> Para mejorar el rendimiento de las consultas, actualice las estadísticas antes de establecer una base de datos en READ_ONLY. Si se necesitan estadísticas adicionales después de establecer una base de datos en READ_ONLY, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] creará las estadísticas en tempdb. Para más información sobre las estadísticas para una base de datos de solo lectura, vea [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md).

READ_WRITE         
La base de datos está disponible para operaciones de lectura y escritura.

Para cambiar este estado, debe tener acceso exclusivo a la base de datos.

**\<db_user_access_option> ::=**         

Controla el acceso del usuario a la base de datos.

RESTRICTED_USER         
RESTRICTED_USER permite que solamente se conecten a la base de datos los miembros del rol fijo de base de datos db_owner y de los roles fijos de servidor dbcreator y sysadmin, aunque no limita su número. Todas las conexiones a la base de datos se desconectan en el margen de tiempo especificado por la cláusula de terminación de la instrucción ALTER DATABASE. Una vez que la base de datos ha cambiado al estado RESTRICTED_USER, se rechazan los intentos de conexión por parte de usuarios no cualificados. **RESTRICTED_USER** no se puede modificar con Instancia administrada de SQL Database.

MULTI_USER         
Todos los usuarios que tengan los permisos correspondientes pueden conectarse a la base de datos.

Puede determinar el estado de esta opción si examina la columna user_access de la vista de catálogo sys.databases o la propiedad UserAccess de la función DATABASEPROPERTYEX.

**\<delayed_durability_option> ::=**         

Controla si las transacciones se confirman con perdurabilidad total o diferida.

DISABLED         
Todas las transacciones tras SET DISABLED son totalmente perdurables. Se omiten las opciones de perdurabilidad que se establecen en un bloque ATOMIC o en una instrucción de confirmación.

ALLOWED         
Todas las transacciones tras SET ALLOWED son totalmente perdurables o de perdurabilidad diferida, dependiendo de la opción de perdurabilidad establecida en el bloque ATOMIC o instrucción de confirmación.

FORCED         
Todas las transacciones tras SET FORCED son totalmente perdurables. Se omiten las opciones de perdurabilidad que se establecen en un bloque ATOMIC o en una instrucción de confirmación.

**\<PARAMETERIZATION_option> ::=**         

Controla la opción de parametrización.

PARAMETERIZATION { SIMPLE | FORCED }         
SIMPLE         
Las consultas incluyen parámetros en función del comportamiento predeterminado de la base de datos.

FORCED         
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye parámetros para todas las consultas de la base de datos.

La configuración actual de esta opción se puede determinar mediante el examen de la columna is_parameterization_forced de la vista de catálogo sys.databases.

**\<query_store_options> ::=**         

ON | OFF | CLEAR [ ALL ]         
Controla si el almacén de consultas está habilitado en esta base de datos y también controla la eliminación del contenido del almacén de consultas.

ON         
Habilita el almacén de consultas.

OFF         
Deshabilita el almacén de consultas. Este es el valor predeterminado.

CLEAR         
Quita el contenido del almacén de consultas.

OPERATION_MODE         
Describe el modo de operación del almacén de consultas. Los valores válidos son READ_ONLY y READ_WRITE. En el modo READ_WRITE, el almacén de consultas recopila y continúa el plan de consultas y la información de estadística del tiempo de ejecución. En el modo READ_ONLY, la información se puede leer del almacén de consultas, pero no se agrega información nueva. Si se ha agotado el espacio máximo del almacén de consultas, el almacén de consultas cambiará el modo de operación a READ_ONLY.

CLEANUP_POLICY         
Describe la directiva de retención de datos del almacén de consultas. STALE_QUERY_THRESHOLD_DAYS determina el número de días durante los que se conserva la información de una consulta en el almacén de consultas. STALE_QUERY_THRESHOLD_DAYS es de tipo **bigint**.

DATA_FLUSH_INTERVAL_SECONDS         
Determina la frecuencia con la que los datos escritos en el almacén de consultas se conservan en el disco. Para optimizar el rendimiento, los datos recopilados por el almacén de consultas se escriben de manera asincrónica en el disco. La frecuencia con la que se produce esta transferencia asincrónica se configura mediante el argumento DATA_FLUSH_INTERVAL_SECONDS. DATA_FLUSH_INTERVAL_SECONDS es de tipo **bigint**.

MAX_STORAGE_SIZE_MB         
Determina el espacio asignado al almacén de consultas. MAX_STORAGE_SIZE_MB es de tipo **bigint**.

INTERVAL_LENGTH_MINUTES         
Determina el intervalo de tiempo en el que se agregan los datos de estadísticas de ejecución en tiempo de ejecución al almacén de consultas. Para optimizar el uso del espacio, se agregan las estadísticas de ejecución en tiempo de ejecución en el almacén de estadísticas de tiempo de ejecución en una ventana de tiempo fijo. Esta ventana de tiempo fijo se configura con el argumento INTERVAL_LENGTH_MINUTES. INTERVAL_LENGTH_MINUTES es de tipo **bigint**.

SIZE_BASED_CLEANUP_MODE         
Controla si la limpieza se activará automáticamente cuando la cantidad total de datos se acerque al tamaño máximo:

OFF         
La limpieza según el tamaño no se activará automáticamente.

AUTO         
La limpieza según el tamaño se activará automáticamente cuando el tamaño en disco alcance el 90 % de **max_storage_size_mb**. La limpieza según el tamaño quita primero las consultas menos caras y más antiguas. Se detiene aproximadamente en el 80 % de **max_storage_size_mb**. Es el valor de configuración predeterminado.

SIZE_BASED_CLEANUP_MODE es de tipo **nvarchar**.

QUERY_CAPTURE_MODE         
Designa el modo de captura de consulta que está activo.

ALL         
Se capturan todas las consultas. Es el valor de configuración predeterminado.

AUTO         
Captura consultas pertinentes en función del consumo de recursos y el recuento de ejecuciones. Es el valor de configuración predeterminado para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

Ninguno         
Detiene la captura de nuevas consultas. El almacén de consultas seguirá recopilando estadísticas de compilación y tiempo de ejecución para las consultas que ya se capturaron. Use esta configuración con precaución ya que podría omitir la captura de consultas importantes.

QUERY_CAPTURE_MODE es de tipo **nvarchar**.

max_plans_per_query         
Entero que representa el número máximo de planes que se tienen para cada consulta. El valor predeterminado es 200.

**\<snapshot_option> ::=**         

Determina el nivel de aislamiento de transacción.

ALLOW_SNAPSHOT_ISOLATION { ON | OFF }         
ON         
Habilita la opción de instantánea en el nivel de base de datos. Cuando se habilita, las instrucciones DML inician la generación de versiones de fila aunque ninguna transacción utilice el aislamiento de instantánea. Una vez habilitada esta opción, las transacciones pueden especificar el nivel de aislamiento de transacción SNAPSHOT. Si se ejecuta una transacción en el nivel de aislamiento SNAPSHOT, todas las instrucciones verán una instantánea de los datos tal como estaban al inicio de la transacción. Si una transacción ejecutada en el nivel de aislamiento SNAPSHOT tiene acceso a los datos de varias bases de datos, ALLOW_SNAPSHOT_ISOLATION debe establecerse en ON en todas las bases de datos o cada instrucción de la transacción debe utilizar sugerencias de bloqueo en cualquier referencia de una cláusula FROM a una tabla de una base de datos donde ALLOW_SNAPSHOT_ISOLATION sea OFF.

OFF         
Desactiva la opción de instantánea en el nivel de base de datos. Las transacciones no pueden especificar el nivel de aislamiento de la transacción SNAPSHOT.

Si se establece ALLOW_SNAPSHOT_ISOLATION en un estado nuevo (de ON a OFF o de OFF a ON), ALTER DATABASE no devuelve el control al autor de la llamada hasta confirmar todas las transacciones existentes de la base de datos. Si la base de datos ya se encuentra en el estado especificado en la instrucción ALTER DATABASE, se devuelve de inmediato el control al autor de la llamada. Use [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) para determinar si hay transacciones de ejecución prolongada si la instrucción ALTER DATABASE no devuelve resultados rápidamente. Si se cancela la instrucción ALTER DATABASE, la base de datos permanece en el estado en que estaba al iniciar ALTER DATABASE. La vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) indica el estado de las transacciones de aislamiento de instantáneas en la base de datos. Si **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON, ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF se pausará durante seis segundos y reintentará la operación.

No puede cambiar el estado de ALLOW_SNAPSHOT_ISOLATION si la base de datos está establecida en OFFLINE.

Si establece ALLOW_SNAPSHOT_ISOLATION en una base de datos READ_ONLY, la configuración se mantendrá si la base de datos se establece posteriormente en READ_WRITE.

Puede cambiar la configuración de ALLOW_SNAPSHOT_ISOLATION para las bases de datos maestra, model, msdb y tempdb. La configuración se mantiene cada vez que la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se detiene y se reinicia si cambia la configuración para tempdb. Si cambia la configuración para la base de datos model, dicha configuración se convierte en la configuración predeterminada para todas las bases de datos nuevas que se crean, excepto para tempdb.

La opción es ON de forma predeterminada para las bases de datos maestra y msdb.

La configuración actual de esta opción se puede determinar mediante el examen de la columna snapshot_isolation_state de la vista de catálogo sys.databases.

READ_COMMITTED_SNAPSHOT { ON | OFF }         
ON         
Habilita la opción de instantánea de lectura confirmada en el nivel de base de datos. Cuando se habilita, las instrucciones DML inician la generación de versiones de fila aunque ninguna transacción utilice el aislamiento de instantánea. Una vez habilitada esta opción, las transacciones que especifican el nivel de aislamiento de lectura confirmada usan versiones de fila en lugar de bloqueos. Todas las instrucciones ven una instantánea de los datos tal como estaban al inicio de la instrucción si una transacción se ejecuta en el nivel de aislamiento de lectura conformada.

OFF         
Desactiva la opción de instantánea de lectura confirmada en el nivel de base de datos. Las transacciones que especifican el nivel de aislamiento READ COMMITTED utilizan el bloqueo.

Para establecer READ_COMMITTED_SNAPSHOT en ON u OFF, no puede haber ninguna conexión activa a la base de datos, excepto la que ejecuta el comando ALTER DATABASE. Sin embargo, no es necesario que la base de datos esté en modo de usuario único. No puede cambiar el estado de esta opción si la base de datos está establecida en OFFLINE.

Si establece READ_COMMITTED_SNAPSHOT en una base de datos READ_ONLY, la configuración se mantendrá si la base de datos se establece después en READ_WRITE.

READ_COMMITTED_SNAPSHOT no se puede cambiar a ON para las bases de datos maestra, tempdb o msdb. Si cambia la configuración para model, dicha configuración se convierte en predeterminada para todas las bases de datos creadas, excepto para tempdb.

La configuración actual de esta opción se puede determinar mediante el examen de la columna is_read_committed_snapshot_on de la vista de catálogo sys.databases.

> [!WARNING]
>Cuando se crea una tabla con **DURABILITY = SCHEMA_ONLY** y posteriormente se cambia **READ_COMMITTED_SNAPSHOT** mediante **ALTER DATABASE**, se pierden los datos de la tabla.

MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }         
ON         
Cuando el nivel de aislamiento de transacción se establece en uno inferior a SNAPSHOT, todas las operaciones interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] en las tablas optimizadas para memoria se ejecutan con aislamiento SNAPSHOT. Los ejemplos de los niveles de aislamiento inferiores a la instantánea son READ COMMITTED o READ UNCOMMITTED. Estas operaciones se ejecutan si el nivel de aislamiento de transacción se establece explícitamente en el nivel de sesión o el valor predeterminado se utiliza de forma implícita.

OFF         
No eleva el nivel de aislamiento de transacción para las operaciones interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] en las tablas optimizadas para memoria.

No puede cambiar el estado de MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT si la base de datos está establecida en OFFLINE.

El valor predeterminado es OFF.

La configuración actual de esta opción se puede determinar mediante el examen de la columna **memory_optimized_elevate_to_snapshot** de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

**\<sql_option> ::=**         

Controla las opciones de cumplimiento con ANSI en el nivel de base de datos.

ANSI_NULL_DEFAULT { ON | OFF }         
Determina el valor predeterminado, NULL o NOT NULL, de una columna o del [tipo definido por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) para los que no se ha definido la nulabilidad explícitamente en las instrucciones CREATE TABLE o ALTER TABLE. Las columnas para las que se hayan definido restricciones siguen las reglas de las restricciones, independientemente de esta configuración.

ON         
El valor predeterminado es NULL.

OFF         
El valor predeterminado es NOT NULL.

La configuración del nivel de conexión, establecida mediante la instrucción SET, invalida la configuración predeterminada del nivel de base de datos para ANSI_NULL_DEFAULT. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_NULL_DEFAULT en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_NULL_DFLT_ON](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).

Para la compatibilidad con ANSI, si se establece la opción de base de datos ANSI_NULL_DEFAULT en ON, el valor predeterminado cambia a NULL.

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_null_default_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiNullDefault de la función DATABASEPROPERTYEX.

ANSI_NULLS { ON | OFF }         
ON         
Todas las comparaciones con un valor NULL se evalúan como UNKNOWN.

OFF         
Las comparaciones de valores no UNICODE con un valor NULL se evalúan como TRUE si ambos valores son NULL.

> [!IMPORTANT]
> En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_NULLS siempre estará ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.

  La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para ANSI_NULLS. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_NULLS en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_NULLS](../../t-sql/statements/set-ansi-nulls-transact-sql.md).

El valor de SET ANSI_NULLS también debe estar en ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_nulls_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiNullsEnabled de la función DATABASEPROPERTYEX.

ANSI_PADDING { ON | OFF }         
ON         
Las cadenas se rellenan a la misma longitud antes de la conversión. También se rellenan hasta la misma longitud antes de la inserción en un tipo de datos **varchar** o **nvarchar**.

OFF         
Inserta espacios en blanco finales en los valores de caracteres en las columnas **varchar** o **nvarchar**. También deja los ceros a la derecha en los valores binarios insertados en columnas **varbinary**. Los valores no se rellenan hasta completar la longitud de la columna.

Si se especifica OFF, esta opción solamente afecta a la definición de las columnas nuevas.

> [!IMPORTANT]
> En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_PADDING siempre estará en ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Se recomienda establecer siempre ANSI_PADDING en ON. ANSI_PADDING también debe estar en ON al crear o tratar índices en columnas calculadas o vistas indizadas.

**char(_n_)** y **binary(_n_)** las columnas que admiten valores NULL se rellenan hasta la longitud de la columna cuando ANSI_PADDING se establece en ON. Los ceros y los espacios en blanco finales se recortan si ANSI_PADDING es OFF. Las columnas **char(_n_)** y **binary(_n_)** que no permiten valores NULL siempre se rellenan hasta completar la longitud de la columna.

  La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada del nivel de base de datos para ANSI_PADDING. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_PADDING en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_PADDING](../../t-sql/statements/set-ansi-padding-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_padding_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiPaddingEnabled de la función DATABASEPROPERTYEX.

ANSI_WARNINGS { ON | OFF }         
ON         
Se emiten errores o advertencias si se dan condiciones tales como la división por cero. También se emiten errores y advertencias cuando aparecen valores null en funciones de agregado.

OFF         
No se genera ninguna advertencia ni se devuelven valores NULL si se producen condiciones como la división por cero.

El valor de SET ANSI_WARNINGS debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

  La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para ANSI_WARNINGS. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión mediante el establecimiento de ANSI_WARNINGS en ON para la sesión. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET ANSI_WARNINGS](../../t-sql/statements/set-ansi-warnings-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_ansi_warnings_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsAnsiWarningsEnabled de la función DATABASEPROPERTYEX.

ARITHABORT { ON | OFF }         
ON         
Se finaliza una consulta cuando se produce un error de desbordamiento o de división por cero durante su ejecución.

OFF         
Aparece un mensaje de advertencia cuando se produce uno de estos errores. La consulta, el proceso por lotes o la transacción continúa procesándose como si no se hubiera producido ningún error aunque se muestre una advertencia.

El valor de SET ARITHABORT debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

  Puede determinar el estado de esta opción mediante el examen de la columna is_arithabort_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsArithmeticAbortEnabled de la función DATABASEPROPERTYEX.

COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 }         
Para más información, consulte [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).

CONCAT_NULL_YIELDS_NULL { ON | OFF }         
ON         
El resultado de una operación de concatenación es NULL si alguno de los operandos es NULL. Por ejemplo, la concatenación de la cadena de caracteres "Esto es" y NULL da como resultado el valor NULL, y no el valor "Esto es".

OFF         
El valor NULL se trata como una cadena de caracteres vacía.

El valor de CONCAT_NULL_YIELDS_NULL también debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.

> [!IMPORTANT]
> En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], CONCAT_NULL_YIELDS_NULL siempre estará en ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.

La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para CONCAT_NULL_YIELDS_NULL. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen CONCAT_NULL_YIELDS_NULL en ON para la sesión al realizar la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET CONCAT_NULL_YIELDS_NULL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).

Puede determinar el estado de esta opción mediante el examen de la columna is_concat_null_yields_null_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsNullConcat de la función DATABASEPROPERTYEX.

QUOTED_IDENTIFIER { ON | OFF }         
ON         
Las comillas dobles se pueden usar para identificadores delimitados.

Todas las cadenas delimitadas por comillas dobles se interpretan como identificadores de objetos. Los identificadores entre comillas no tienen que adaptarse a las reglas de [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Pueden ser palabras clave e incluir caracteres que no se permiten en los identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Si una comilla simple (') forma parte de la cadena literal, puede representarse mediante comillas dobles (").

OFF         
Los identificadores no se pueden incluir entre comillas y deben seguir todas las reglas de [!INCLUDE[tsql](../../includes/tsql-md.md)] para los identificadores. Los literales se pueden delimitar con comillas simples o dobles.

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también permite delimitar los identificadores con corchetes ([ ]). Los identificadores entre corchetes pueden usarse siempre, independientemente del valor de QUOTED_IDENTIFIER. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).

  Al crear una tabla, la opción QUOTED IDENTIFIER siempre se almacena como ON en los metadatos de la tabla. La opción se almacena incluso si está establecida en OFF al crear la tabla.

La configuración en el nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para QUOTED_IDENTIFIER. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión estableciendo QUOTED_IDENTIFIER en ON. Los clientes ejecutan la instrucción cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md).

  Puede determinar el estado de esta opción mediante el examen de la columna is_quoted_identifier_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsQuotedIdentifiersEnabled de la función DATABASEPROPERTYEX.

NUMERIC_ROUNDABORT { ON | OFF }         
ON         
Se genera un error cuando se produce una pérdida de precisión en una expresión.

OFF         
Las pérdidas de precisión no generan mensajes de error y el resultado se redondea con la precisión de la columna o variable que lo almacena.

El valor de NUMERIC_ROUNDABORT debe ser OFF al crear o realizar cambios en índices de columnas calculadas o vistas indizadas.

Puede determinar el estado de esta opción mediante el examen de la columna is_numeric_roundabort_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsNumericRoundAbortEnabled de la función DATABASEPROPERTYEX.

RECURSIVE_TRIGGERS { ON | OFF }         
ON         
Se permite la activación recursiva de desencadenadores AFTER.

OFF         
Puede determinar el estado de esta opción mediante el examen de la columna is_recursive_triggers_on en la vista de catálogo sys.databases. También puede determinar el estado mediante el examen de la propiedad IsRecursiveTriggersEnabled de la función DATABASEPROPERTYEX.

> [!NOTE]
> La recursividad directa solo se evita cuando RECURSIVE_TRIGGERS se establece en OFF. Para deshabilitar la recursividad indirecta, también debe establecer la opción de servidor desencadenadores anidados en 0.

Puede determinar el estado de esta opción si examina la columna is_recursive_triggers_on de la vista de catálogo sys.databases o la propiedad IsRecursiveTriggersEnabled de la función DATABASEPROPERTYEX.

**\<target_recovery_time_option> ::=**         

Especifica la frecuencia de puntos de comprobación indirectos por base de datos. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], el valor predeterminado para nuevas bases de datos es de un minuto, lo cual indica que la base de datos usará puntos de comprobación indirectos. Para versiones anteriores, el valor predeterminado es 0, lo cual indica que la base de datos usará puntos de comprobación automáticos, cuya frecuencia depende del valor de intervalo de recuperación de la instancia de servidor. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda un minuto para la mayoría de los sistemas.

TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS | MINUTES }         
*target_recovery_time*         
Especifica el límite máximo de tiempo para recuperar la base de datos especificada en caso de bloqueo.

SECONDS         
Indica que *target_recovery_time* se expresa como el número de segundos.

MINUTES         
Indica que *target_recovery_time* se expresa como el número de minutos.

Para más información sobre los puntos de control indirectos, consulte [Puntos de control de base de datos](../../relational-databases/logs/database-checkpoints-sql-server.md).

ROLLBACK AFTER *integer* [SECONDS] | ROLLBACK IMMEDIATE         
Especifica si la operación de reversión se ejecuta transcurrido un número de segundos determinado o de forma inmediata.

NO_WAIT         
Especifica que la solicitud producirá un error si el cambio de opción o estado de la base de datos solicitado no puede completarse inmediatamente. Completarse inmediatamente significa que no se espera a que las transacciones se confirmen o reviertan por su cuenta.

## <a name="SettingOptions"></a> Configurar opciones         
Para recuperar la configuración actual de las opciones de base de datos, use la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) o [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md).

Una vez configurada una opción de la base de datos, la modificación surte efecto de inmediato.

Puede cambiar los valores predeterminados de cualquiera de las opciones de las bases de datos recién creadas. Para ello, cambie la opción adecuada de base de datos en la base de datos de modelo.

## <a name="examples"></a>Ejemplos

### <a name="a-setting-the-database-to-read_only"></a>A. Establecer la base de datos en READ_ONLY
El cambio del estado de una base de datos o un grupo de archivos a READ_ONLY o READ_WRITE requiere el acceso exclusivo a la base de datos. En el ejemplo siguiente, la base de datos se establece en el modo `RESTRICTED_USER` para restringir el acceso. A continuación, el ejemplo establece el estado de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en `READ_ONLY` y devuelve el acceso a la base de datos a todos los usuarios.

```sql
USE master;
GO
ALTER DATABASE AdventureWorks2012
SET RESTRICTED_USER;
GO
ALTER DATABASE AdventureWorks2012
SET READ_ONLY
GO
ALTER DATABASE AdventureWorks2012
SET MULTI_USER;
GO

```

### <a name="b-enabling-snapshot-isolation-on-a-database"></a>B. Habilitar el aislamiento de instantánea en una base de datos
En el siguiente ejemplo se habilita la opción del marco de aislamiento de instantánea para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .

```sql
USE AdventureWorks2012;
USE master;
GO
ALTER DATABASE AdventureWorks2012
SET ALLOW_SNAPSHOT_ISOLATION ON;
GO
-- Check the state of the snapshot_isolation_framework
-- in the database.
SELECT name, snapshot_isolation_state,
    snapshot_isolation_state_desc AS description
FROM sys.databases
WHERE name = N'AdventureWorks2012';
GO
```

El conjunto de resultados muestra que el marco de aislamiento de instantánea está habilitado.

|NAME |snapshot_isolation_state |description|
|-------------------- |------------------------|----------|
|AdventureWorks2012 |1| ON |

### <a name="c-enabling-modifying-and-disabling-change-tracking"></a>C. Habilitar, modificar y deshabilitar el seguimiento de cambios
En el ejemplo siguiente se habilita el seguimiento de cambios para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y se establece el período de retención en `2` días.

```sql
ALTER DATABASE AdventureWorks2012
SET CHANGE_TRACKING = ON
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);
```

En el ejemplo siguiente se muestra cómo cambiar el período de retención a `3` días.

```sql
ALTER DATABASE AdventureWorks2012
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);
```

En el ejemplo siguiente se muestra cómo deshabilitar el seguimiento de cambios para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .

```sql
ALTER DATABASE AdventureWorks2012
SET CHANGE_TRACKING = OFF;
```

### <a name="d-enabling-the-query-store"></a>D. Habilitar el almacén de consultas
En el ejemplo siguiente se habilita el almacén de consultas y configura los parámetros de almacén de consultas.

```sql
ALTER DATABASE AdventureWorks2012
SET QUERY_STORE = ON 
  (  
      OPERATION_MODE = READ_WRITE
    , CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 )
    , DATA_FLUSH_INTERVAL_SECONDS = 900
    , MAX_STORAGE_SIZE_MB = 1024
    , INTERVAL_LENGTH_MINUTES = 60
    );
```

## <a name="see-also"></a>Consulte también

- [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)
- [Creación de reflejo de la base de datos de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)
- [Estadísticas](../../relational-databases/statistics/statistics.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=azuresqldb-mi-current)
- [Habilitar y deshabilitar el seguimiento de cambios](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)
- [Procedimiento recomendado con el Almacén de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](alter-database-transact-sql-set-options.md?view=sql-server-2017)|[Grupo de bases de datos elásticas o base de datos única de<br />SQL Database](alter-database-transact-sql-set-options.md?view=azuresqldb-current)|[Instancia administrada de<br />SQL Database](alter-database-transact-sql-set-options.md?view=azuresqldb-mi-current)|**_\* SQL Data<br />Warehouse \*_** &nbsp;||||

&nbsp;

## <a name="azure-sql-data-warehouse"></a>Almacenamiento de datos SQL de Azure

## <a name="syntax"></a>Sintaxis

```
ALTER DATABASE { database_name }
SET
{
    <optionspec> [ ,...n ]
}
;

<option_spec>::=
{
<RESULT_SET_CACHING>
}
;

<RESULT_SET_CACHING>::=
{
RESULT_SET_CACHING {ON | OFF}
}

```

## <a name="arguments"></a>Argumentos

*database_name*

Es el nombre de la base de datos que se va a modificar.

<a name="result_set_caching"></a> RESULT_SET_CACHING { ON | OFF }   
Se aplica a Azure SQL Data Warehouse (versión preliminar)

Este comando debe ejecutarse mientras se está conectado a la base de datos `master`.  Los cambios realizados a esta configuración de base de datos se aplicarán inmediatamente.  Los costos de almacenamiento se aplican mediante el almacenamiento en caché de conjuntos de resultados de consultas. Después de deshabilitar el almacenamiento en caché de resultados para una base de datos, la caché de resultados que persistía anteriormente se eliminará inmediatamente del almacenamiento de Azure SQL Data Warehouse. Se ha incorporado una nueva columna, is_result_set_caching_on, en `sys.databases` para mostrar la configuración de almacenamiento en caché de resultados de una base de datos.  

ON   
especifica que los conjuntos de resultados de consultas devueltos de esta base de datos se almacenarán en caché en el almacenamiento de Azure SQL Data Warehouse.

OFF   
especifica que los conjuntos de resultados de consultas devueltos de esta base de datos no se almacenarán en caché en el almacenamiento de Azure SQL Data Warehouse. Los usuarios pueden ver si una consulta se ejecutó con un acierto o un fallo de caché de resultados realizando una consulta a sys.pdw_request_steps con un valor de request_id específico.   Si hay un acierto de caché, el resultado de la consulta tendrá un único paso con los siguientes detalles:

|**Nombre de columna** |**Operador** |**Value** |
|----|----|----|
| operation_type|=|ReturnOperation|
|step_index|=|0|
|location_type|=|Control|
comando|Like|%DWResultCacheDb%|
| | |

## <a name="remarks"></a>Notas

Si se cumplen todos los requisitos siguientes, el conjunto de resultados almacenado en caché se vuelve a usar para una consulta:

1. El usuario que ejecuta la consulta tiene acceso a todas las tablas a las que se hace referencia en la consulta.
1. Hay una coincidencia exacta entre la nueva consulta y la anterior que ha generado el almacenamiento en caché del conjunto de resultados.
1. No hay cambios de datos ni esquema en las tablas a partir de las que se ha generado el conjunto de resultados almacenado.  

Una vez activado el almacenamiento en caché del conjunto de resultados de una base de datos, se almacenan en caché los resultados de todas las consultas hasta que la caché está llena, excepto las consultas con funciones no deterministas como DateTime.Now().   Las consultas con grandes conjuntos de resultados (por ejemplo, > 1 millón de filas) pueden experimentar un rendimiento más lento durante la primera ejecución mientras se crea la caché de resultados.

## <a name="permissions"></a>Permisos

Se requieren estos permisos:

- Inicio de sesión principal en el nivel de servidor (creado por el proceso de aprovisionamiento), o
- Miembro del rol de base de datos `dbmanager`.

El propietario de la base de datos no puede modificarla a menos que sea miembro del rol dbmanager.

## <a name="examples"></a>Ejemplos

### <a name="enable-result-set-caching-for-a-database"></a>Habilitación del almacenamiento en caché de conjuntos de resultados para una base de datos

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING ON;
```

### <a name="disable-result-set-caching-for-a-database"></a>Deshabilitación del almacenamiento en caché de conjuntos de resultados para una base de datos

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING OFF;
```

### <a name="check-result-set-caching-setting-for-a-database"></a>Comprobación de la configuración de almacenamiento en caché de conjuntos de resultados para una base de datos

```sql
SELECT name, is_result_set_caching_on
FROM sys.databases;
```

### <a name="check-for-number-of-queries-with-result-set-cache-hit-and-cache-miss"></a>Comprobación del número de consultas con acierto de caché y fallo de caché de conjuntos de resultados

```sql
SELECT  
Queries=CacheHits+CacheMisses,
CacheHits,
CacheMisses 
CacheHitPct=CacheHits*1.0/(CacheHits+CacheMisses)
FROM  
(SELECT  
CacheHits=count(distinct case when s.command like '%DWResultCacheDb%' and
r.resource_class IS NULL and s.operation_type = 'ReturnOperation' and  
s.step_index = 0 then s.request_id else null end) , 
CacheMisses=count(distinct case when r.resource_class IS NOT NULL then  
s.request_id else null end) 
     FROM sys.dm_pdw_request_steps s  
     JOIN sys.dm_pdw_exec_requests r  
     ON s.request_id = r.request_id) A;
```

### <a name="check-for-result-set-cache-hit-or-cache-miss-for-a-query"></a>Comprobación del acierto de caché y fallo de caché de conjunto de resultados para una consulta

```sql
If
(SELECT step_index  
FROM sys.dm_pdw_request_steps  
WHERE request_id = 'QID58286' and operation_type = 'ReturnOperation' and command like '%DWResultCacheDb%') = 0
SELECT 1 as is_cache_hit  
ELSE
SELECT 0 as is_cache_hit;
```

### <a name="check-for-all-queries-with-result-set-cache-hits"></a>Comprobación de todas las consultas con aciertos de caché de conjunto de resultados

```sql
SELECT *  
FROM sys.dm_pdw_request_steps  
WHERE command like '%DWResultCacheDb%' and step_index = 0;
```

## <a name="see-also"></a>Vea también

- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [Procedimientos recomendados para Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-best-practices#maintain-statistics)
- [Diseño de tablas en Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-tables-overview#statistics)
- [Elementos del lenguaje de SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-language-elements)

::: moniker-end
