---
title: sp_help_jobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobhistory_TSQL
- sp_help_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobhistory
ms.assetid: a944d44e-411b-4735-8ce4-73888d4262d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 10033b2525ba28e79bd31a73bd9e71a7cca15e42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054932"
---
# <a name="sphelpjobhistory-transact-sql"></a>sp_help_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información acerca de los trabajos en los servidores de un dominio de administración multiservidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_jobhistory [ [ @job_id = ] job_id ]   
     [ , [ @job_name = ] 'job_name' ]   
     [ , [ @step_id = ] step_id ]   
     [ , [ @sql_message_id = ] sql_message_id ]   
     [ , [ @sql_severity = ] sql_severity ]   
     [ , [ @start_run_date = ] start_run_date ]   
     [ , [ @end_run_date = ] end_run_date ]   
     [ , [ @start_run_time = ] start_run_time ]   
     [ , [ @end_run_time = ] end_run_time ]   
     [ , [ @minimum_run_duration = ] minimum_run_duration ]   
     [ , [ @run_status = ] run_status ]   
     [ , [ @minimum_retries = ] minimum_retries ]   
     [ , [ @oldest_first = ] oldest_first ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @mode = ] 'mode' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id` El número de identificación del trabajo. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
`[ @job_name = ] 'job_name'` El nombre del trabajo. *job_name* es **sysname**, su valor predeterminado es null.  
  
`[ @step_id = ] step_id` El número de identificación del paso. *step_id* es **int**, su valor predeterminado es null.  
  
`[ @sql_message_id = ] sql_message_id` El número de identificación del mensaje de error devuelto por Microsoft SQL Server cuando se ejecuta el trabajo. *sql_message_id* es **int**, su valor predeterminado es null.  
  
`[ @sql_severity = ] sql_severity` El nivel de gravedad del mensaje de error devuelto por SQL Server cuando se ejecuta el trabajo. *sql_severity* es **int**, su valor predeterminado es null.  
  
`[ @start_run_date = ] start_run_date` La fecha en que se inició el trabajo. *start_run_date*es **int**, su valor predeterminado es null. *start_run_date* se debe escribir con el formato AAAAMMDD, donde AAAA es un año con cuatro cifras, MM es un mes con dos cifras y DD es el día con dos cifras.  
  
`[ @end_run_date = ] end_run_date` La fecha en que se completó el trabajo. *end_run_date* es **int**, su valor predeterminado es null. *end_run_date*se debe escribir con el formato AAAAMMDD, donde AAAA es el año de cuatro dígitos, MM es un mes con dos cifras y DD es el día con dos cifras.  
  
`[ @start_run_time = ] start_run_time` La hora en que se inició el trabajo. *start_run_time* es **int**, su valor predeterminado es null. *start_run_time*se debe escribir con el formato HHMMSS, donde HH es la hora del día, MM es un minutos del día con dos cifras y SS son los segundos dos caracteres del día.  
  
`[ @end_run_time = ] end_run_time` El tiempo que el trabajo completado su ejecución. *end_run_time* es **int**, su valor predeterminado es null. *end_run_time*se debe escribir con el formato HHMMSS, donde HH es la hora del día, MM es un minutos del día con dos cifras y SS son los segundos dos caracteres del día.  
  
`[ @minimum_run_duration = ] minimum_run_duration` La longitud mínima de tiempo para la finalización del trabajo. *minimum_run_duration* es **int**, su valor predeterminado es null. *minimum_run_duration*se debe escribir con el formato HHMMSS, donde HH es la hora del día, MM es un minutos del día con dos cifras y SS son los segundos dos caracteres del día.  
  
`[ @run_status = ] run_status` El estado de ejecución del trabajo. *run_status* es **int**, su valor predeterminado es null, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Error|  
|**1**|se ha realizado correctamente|  
|**2**|Reintento (solo pasos)|  
|**3**|Canceled|  
|**4**|Mensaje en curso|  
|**5**|Desconocido|  
  
`[ @minimum_retries = ] minimum_retries` El número mínimo de veces que un trabajo debe intentar volver a ejecutar. *minimum_retries* es **int**, su valor predeterminado es null.  
  
`[ @oldest_first = ] oldest_first` Es si se debe presentar la salida con los trabajos más antiguos en primer lugar. *oldest_first* es **int**, su valor predeterminado es **0**, que presenta los trabajos más recientes en primer lugar. **1** presenta los trabajos más antiguos en primer lugar.  
  
`[ @server = ] 'server'` El nombre del servidor en el que se realizó el trabajo. *servidor* es **nvarchar (30)** , su valor predeterminado es null.  
  
`[ @mode = ] 'mode'` Indica si SQL Server imprime todas las columnas del conjunto de resultados (**completa**) o un resumen de las columnas. *modo* es **varchar(7)** , su valor predeterminado es **resumen**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 La lista de columnas depende del valor de *modo*. El conjunto de columnas más completo se muestra a continuación y se devuelve cuando *modo* es FULL.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Número de identificación de la entrada en el historial.|  
|**job_id**|**uniqueidentifier**|Número de identificación del trabajo.|  
|**job_name**|**sysname**|Nombre del trabajo.|  
|**step_id**|**int**|Número de identificación de paso (será **0** para un historial de trabajos).|  
|**step_name**|**sysname**|Nombre de paso (será NULL para un historial de trabajos).|  
|**sql_message_id**|**int**|Para pasos [!INCLUDE[tsql](../../includes/tsql-md.md)], número de error de [!INCLUDE[tsql](../../includes/tsql-md.md)] más reciente encontrado en la ejecución del comando.|  
|**sql_severity**|**int**|Para pasos [!INCLUDE[tsql](../../includes/tsql-md.md)], nivel de gravedad más alto de los errores de [!INCLUDE[tsql](../../includes/tsql-md.md)] encontrado en la ejecución del comando.|  
|**message**|**nvarchar(1024)**|Mensaje del historial de trabajos o pasos.|  
|**run_status**|**int**|Resultado del trabajo o del paso.|  
|**run_date**|**int**|Fecha en que empezó la ejecución del trabajo o del paso.|  
|**run_time**|**int**|Hora en que empezó la ejecución del trabajo o del paso.|  
|**run_duration**|**int**|Tiempo transcurrido en la ejecución del trabajo o paso en formato HHMMSS.|  
|**operator_emailed**|**nvarchar(20)**|Operador que recibió mensajes de correo electrónico relativos a este trabajo (es NULL para el historial de pasos).|  
|**operator_netsent**|**nvarchar(20)**|Operador que recibió mensajes de red relativos a este trabajo (es NULL para el historial de pasos).|  
|**operator_paged**|**nvarchar(20)**|Operador que recibió mensajes de localizador relativos a este trabajo (es NULL para el historial de pasos).|  
|**retries_attempted**|**int**|Número de veces que se ha vuelto a intentar el paso (siempre es 0 para un historial de trabajos).|  
|**servidor**|**nvarchar(30)**|Servidor en el que se ejecuta el paso o el trabajo. Siempre es (**local**).|  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_jobhistory** devuelve un informe con el historial de los trabajos programados especificados. Si no se especifican parámetros, el informe contiene el historial de todos los trabajos programados.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Los miembros de la **SQLAgentUserRole** rol de base de datos solamente puede ver el historial de trabajos que les pertenecen.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-all-job-information-for-a-job"></a>A. Mostrar toda la información de un trabajo  
 En el siguiente ejemplo se muestra toda la información del trabajo `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobhistory   
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-that-match-certain-conditions"></a>b. Mostrar información de trabajos que cumplen determinadas condiciones  
 En el siguiente ejemplo se imprimen todas las columnas y toda la información de los trabajos o pasos de trabajo que no progresaron y devolvieron el mensaje de error `50100` (mensaje de error definido por el usuario) y una gravedad de `20`.  
  
```  
USE msdb  
GO  
  
EXEC dbo.sp_help_jobhistory  
    @sql_message_id = 50100,  
    @sql_severity = 20,  
    @run_status = 0,  
    @mode = N'FULL' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
