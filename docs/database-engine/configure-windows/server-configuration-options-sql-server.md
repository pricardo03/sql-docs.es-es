---
title: Opciones de configuración de servidor (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/13/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
keywords:
- configuración del servidor (SQL Server)
helpviewer_keywords:
- surface area configuration [SQL Server], sp_configure
- configuration options [SQL Server], when take effect
- server management [SQL Server], configuration options
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], configuring
- configuration options [SQL Server], setting
- options [SQL Server], configuration
- RECONFIGURE statement
- performance [SQL Server], servers
- configuration options [SQL Server]
- RECONFIGURE WITH OVERRIDE statement
- SQL Server, configuring
- sp_configure
- stored procedures [SQL Server], configuration options
- server configuration [SQL Server]
- administering SQL Server, configuration options
ms.assetid: 9f38eba6-39b1-4f1d-ba24-ee4f7e2bc969
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7d0e379cf9d3bc6391e6c2c921824c7162b88def
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025624"
---
# <a name="server-configuration-options-sql-server"></a>Opciones de configuración de servidor (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Puede administrar y optimizar los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante opciones de configuración con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o el procedimiento almacenado del sistema sp_configure. Las opciones de configuración de servidores más utilizadas están disponibles mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]; es posible el acceso a todas las opciones de configuración mediante sp_configure. Antes de establecer estas opciones, debe considerar detenidamente los efectos en el sistema. Para obtener más información, vea [Ver o cambiar las propiedades del servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).  
  
>**IMPORTANTE:** Solo un administrador de la base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada debe cambiar las opciones avanzadas.  
  
## <a name="categories-of-configuration-options"></a>Categorías de las opciones de configuración  
 Las opciones de configuración tienen efecto en uno de estos dos momentos:  
  
-   Inmediatamente después de establecer la opción y ejecutar la instrucción **RECONFIGURE** (o, en algunos casos, **RECONFIGURE WITH OVERRIDE**). La reconfiguración de ciertas opciones invalidará planes en la caché de planes, provocando la compilación de nuevos planes. Para obtener más información, vea [DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md).
  
     -O bien-  
  
-   Después de realizar las acciones anteriores y reiniciar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Las opciones que necesitan que se reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo mostrarán inicialmente el valor modificado en la columna value. Después de reiniciar, el nuevo valor aparecerá tanto en la columna value como en la columna value_in_use.  
  
Para algunas opciones, es necesario reiniciar el servidor para que el valor de la nueva configuración surta efecto. Si establece el nuevo valor y ejecuta sp_configure antes de reiniciar el servidor, el nuevo valor aparecerá en la columna **value** de las opciones de configuración, pero no en la columna **value_in_use** . Después de reiniciar el servidor, el nuevo valor aparecerá en la columna **value_in_use** .  
  
Las opciones de configuración automática son aquellas que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta según las necesidades del sistema. En la mayoría de los casos, esto elimina la necesidad de establecer los valores manualmente. Como ejemplo se pueden citar las opciones **min server memory** y **max server memory** , así como la opción user connections.  
  
## <a name="configuration-options-table"></a>Tabla de opciones de configuración  
 La siguiente tabla contiene todas las opciones de configuración disponibles, la gama de valores posibles y los valores predeterminados. Las opciones de configuración están marcadas con códigos de letras de la forma siguiente:  
  
-   A = Opciones avanzadas, que solo las deben cambiar un administrador de base de datos con experiencia o un profesional certificado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y que requieren el valor 1 para Mostrar opciones avanzadas.  
  
-   RR = Opciones que requieren el reinicio del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   RP = Opciones que requieren el reinicio del motor de PolyBase.  
  
-   SC = Opciones de configuración automática.  
  
    |Opción de configuración|Valor mínimo|Valor máximo|Valor predeterminado|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[access check cache bucket count](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[access check cache quota](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[ad hoc distributed queries](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity I/O mask](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md) (A, RR)|-2147483648|2147483647|0|  
    |[affinity64 I/O mask](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md) (A, disponible solo en la versión de 64 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])|-2147483648|2147483647|0|  
    |[affinity mask](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) (A, RR), disponible solo en la versión de 64 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[Agent XPs](../../database-engine/configure-windows/agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> Cambia a 1 cuando se inicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El valor predeterminado es 0 si el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se establece para que se inicie automáticamente durante la instalación.|  
    |[allow updates](../../database-engine/configure-windows/allow-updates-server-configuration-option.md) (obsoleto. No debe usarse. Generará un error durante la reconfiguración).|0|1|0|  
    |[automatic soft-NUMA disabled](soft-numa-sql-server.md)|0|1|0|  
    |[Valor predeterminado de la suma de comprobación de copia de seguridad](../../database-engine/configure-windows/backup-checksum-default.md)|0|1|0|  
    |[compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0| 
    |[blocked process threshold](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[c2 audit mode](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md) (A, RR)|0|1|0|  
    |[clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)|0|1|0|  
    |[clr strict security](../../database-engine/configure-windows/clr-strict-security.md) (A) <br /> **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|0|1|0|  
    |[common criteria compliance enabled](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md) (A, RR)|0|1|0|  
    |[autenticación de la base de datos independiente (A)](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)|0|1|0|  
    |[cost threshold for parallelism](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[cursor threshold](../../database-engine/configure-windows/configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[default full-text language](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|3082|  
    |[default language](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[default trace enabled](../../database-engine/configure-windows/default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |[disallow results from triggers](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md) (SC)<br /><br /> **Requiere el reinicio de**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|0|1|0|  
    |[filestream_access_level](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[fill factor](../../database-engine/configure-windows/configure-the-fill-factor-server-configuration-option.md) (A, RR)|0|100|0|  
    |ft crawl bandwidth (max); vea [ft crawl bandwidth](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft crawl bandwidth (min); vea [ft crawl bandwidth](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |ft notify bandwidth (max); vea [ft notify bandwidth](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft notify bandwidth (min); vea [ft notify bandwidth](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |[index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) (A, SC)|704|2147483647|0|  
    |[in-doubt xact resolution](../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[lightweight pooling](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) (A, RR)|0|1|0|  
    |[locks](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md) (A, RR, SC)|5000|2147483647|0|  
    |[max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[max full-text crawl range](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[max server memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md) (A, SC)|16|2147483647|2147483647|  
    |[max text repl size](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[max worker threads](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> 1024 es el máximo recomendado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits y 2048 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits. **Nota:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] fue la última versión disponible en el sistema operativo de 32 bits.|0<br /><br /> Cero configura automáticamente el número máximo de subprocesos de trabajo dependientes del número de procesadores mediante la fórmula (256 + ( *\<procesadores>* -4) * 8) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits, y (512 + *\<procesadores>* - 4) * 8) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits. **Nota:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] fue la última versión disponible en el sistema operativo de 32 bits.|  
    |[media retention](../../database-engine/configure-windows/configure-the-media-retention-server-configuration-option.md) (A, RR)|0|365|0|  
    |[min memory per query](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md) (A, SC)|0|2147483647|0|  
    |[desencadenadores anidados](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[network packet size](../../database-engine/configure-windows/configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Ole Automation Procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[open objects](../../database-engine/configure-windows/open-objects-server-configuration-option.md) (A, RR, obsoleto)|0|2147483647|0|  
    |[optimize for ad hoc workloads](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](../../database-engine/configure-windows/ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[PolyBase Hadoop y Azure Blob Storage](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md) (RP)<br /><br /> **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|0|7|0|   
    |[precompute rank](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md) (A)|0|1|0|  
    |[priority boost](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) (A, RR)|0|1|0|  
    |[query governor cost limit](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[query wait](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[recovery interval](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md) (A, SC)|0|32767|0|  
    |[remote access](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md) (RR)|0|1|1|  
    |[remote admin connections](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[remote data archive](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md)|0|1|0|  
    |[remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[remote proc trans](../../database-engine/configure-windows/configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Opción Replication XPs](../../database-engine/configure-windows/replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[scan for startup procs](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md) (A, RR)|0|1|0|  
    |[server trigger recursion](../../database-engine/configure-windows/server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[set working set size](../../database-engine/configure-windows/set-working-set-size-server-configuration-option.md) (A, RR, obsoleto)|0|1|0|  
    |[show advanced options](../../database-engine/configure-windows/show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO y DMO XPs](../../database-engine/configure-windows/smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[transform noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |[two digit year cutoff](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[user connections](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md) (A, RR, SC)|0|32767|0|  
    |[user options](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>Vea también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
 [DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)
  
  
