---
title: Instalar Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 486e4216-a946-4c6e-828c-61bc905f7ec1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a1151b2e4cd8c51caca3bae4d97e9d616720fda0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481283"
---
# <a name="install-data-quality-services"></a>Instalar Data Quality Services
  [!INCLUDE[ssDQSnoversionLong](../../includes/ssdqsnoversionlong-md.md)] (DQS) contiene los dos componentes siguientes: **[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]** y **[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]**.  
  
|Componente DQS|Descripción|  
|-------------------|-----------------|  
|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] se instala sobre el Motor de base de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e incluye tres bases de datos: DQS_MAIN, DQS_PROJECTS y DQS_STAGING_DATA. DQS_MAIN contiene procedimientos almacenados DQS, el motor DQS y las bases de conocimiento publicadas. DQS_PROJECTS contiene información del proyecto de calidad de los datos. DQS_STAGING_DATA es el área de almacenamiento provisional donde puede copiar los datos de origen para realizar operaciones de DQS y después exportar los datos procesados.|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] es una aplicación independiente que permite conectar con [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]y proporciona una interfaz gráfica de usuario muy intuitiva para realizar operaciones de calidad de datos y otras tareas administrativas relacionadas con DQS.|  
  
> [!IMPORTANT]
>  Además de los dos componentes anteriores de DQS, también puede:  
> 
>  -   Usar la Transformación Limpieza de DQS de Integration Services que realiza la limpieza de los datos dentro del proceso de empaquetado de Integration Services y que se instala automáticamente con Integration Services. Para obtener información sobre cómo instalar Integration Services, vea [Instalar Integration Services](../../integration-services/install-windows/install-integration-services.md).  
> -   Habilitar la integración con DQS en Master Data Services para usar la funcionalidad de coincidencia de DQS en el complemento Master Data Services para Excel. Para obtener más información, consulte [Habilitar la integración de Data Quality Services con Master Data Services](../../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md).  
  
 La instalación de DQS es un proceso que consta de tres partes:  
  
-   [Tareas previas a la instalación](#PreInstallationTasks): compruebe los requisitos del sistema antes de instalar DQS.  
  
-   [Tareas de instalación de Data Quality Services](#DQSInstallation): instale DQS mediante el programa de instalación de SQL Server.  
  
-   [Tareas posteriores a la instalación](#PostInstallationTasks): realice estas tareas después de terminar con el programa de instalación de SQL Server para terminar de instalar DQS.  
  
> [!NOTE]  
>  Este tema no incluye instrucciones para ejecutar el programa de instalación desde la línea de comandos. Para obtener información acerca de las opciones de línea de comandos para instalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] y el cliente, vea [parámetros de función](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Feature) en [instalar SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
##  <a name="PreInstallationTasks"></a> Tareas de preinstalación:  
 Antes de instalar DQS, asegúrese de que el equipo cumple los requisitos mínimos del sistema. En la tabla siguiente se proporciona información sobre los requisitos mínimos del sistema para los componentes DQS:  
  
|Componente DQS|Requisitos mínimos del sistema|  
|-------------------|---------------------------------|  
|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]|Memoria (RAM):<br />-Como mínimo: 2 GB<br />-Se recomienda: 4 GB o más.<br /><br /> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obtener más información, consulte [acerca de que el motor de base de datos de SQL Server](../../database-engine/sql-server-database-engine-overview.md).|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|.NET Framework 4 (se instala durante la instalación del [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] , si no está ya instalado)<br /><br /> Internet Explorer 6.0 SP1 o posterior|  
  
> [!IMPORTANT]
>  -   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] y [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] se pueden instalar en el mismo equipo o en equipos diferentes. Los dos componentes se pueden instalar de forma independiente y en cualquier orden. Sin embargo, para usar el [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)], necesitará que esté instalado un [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] para conectar con él.  
> -   Puede conectarse a la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] usando la versión actual o una versión anterior de [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] y la Transformación Limpieza de DQS. Para obtener información sobre cómo actualizar la versión existente de DQS a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vea [Actualizar Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
> -   Aunque Microsoft Excel no es un requisito previo para instalar Data Quality Client, Microsoft Excel 2003 o posterior debe estar instalado en el equipo Data Quality Client para realizar diversas operaciones en la aplicación cliente como es importar los valores de dominio de un archivo de Excel o asignar los datos de origen en un archivo de Excel para actividades como la detección, la limpieza o la correspondencia.  
  
 Para obtener información detallada sobre los requisitos mínimos del sistema para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [requisitos de Hardware y Software para instalar SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
##  <a name="DQSInstallation"></a> Tareas de instalación de Data Quality Services  
 Tiene que usar el programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para instalar los componentes DQS. Al ejecutar el programa de instalación de SQL Server, tiene que pasar por una serie de páginas del asistente de instalación para seleccionar las opciones adecuadas en función de sus requisitos. En la tabla siguiente se muestran únicamente aquellas páginas del Asistente para instalación cuyas opciones que seleccione pueden afectar a la instalación de DQS:  
  
|Página|Acción|  
|----------|------------|  
|Selección de características|Seleccione:<br /><br /> **Data Quality Services** debajo de **Servicios de Motor de base de datos** para instalar el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]. <br />Si activa la casilla **Data Quality Services** , el programa de instalación de SQL Server copiará un archivo de instalador, DQSInstaller.exe, bajo el directorio de la instancia de SQL Server en el equipo. Debe ejecutar este archivo una vez completado el programa de instalación de SQL Server para *completar* la instalación del [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Además, debe realizar algunos pasos adicionales para configurar el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] para poder usarlo. Para obtener más información, vea [Tareas posteriores a la instalación](#PostInstallationTasks).<br /><br /> **Data Quality Client** para instalar el [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)].<br /><br /> (Recomendado) **Herramientas de administración - Completa** en **Herramientas de administración - Básica** para instalar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Proporciona una interfaz gráfica de usuario para administrar la instancia de SQL Server y le ayudará a realizar las tareas adicionales posteriores a la instalación que se indican en la siguiente sección.|  
|Configuración del motor de base de datos|Haga clic en **Agregar usuario actual** para agregar la cuenta de usuario de Windows al rol fijo de servidor sysadmin. Esto es necesario para que pueda ejecutar el archivo DQSInstaller.exe más adelante y completar la instalación del [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .|  
  
##  <a name="PostInstallationTasks"></a> Tareas posteriores a la instalación  
 Una vez completado el Asistente para la instalación de SQL Server, debe realizar los pasos adocionales mencionados en esta sección para completar la instalación del [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , configurarlo y, a continuación, usarlo.  
  
|Acción|Descripción|Temas relacionados|  
|------------|-----------------|--------------------|  
|Completar la instalación del [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]|Ejecute el archivo DQSInstaller.exe. Al ejecutar el archivo DQSInstaller.exe:<br /><br /> Se crean las bases de datos DQS_MAIN, DQS_PROJECTS y DQS_STAGING_DATA.<br /><br /> Se crean los inicios de sesión ##MS_dqs_db_owner_login## y ##MS_dqs_service_login##.<br /><br /> Se crean los roles dqs_administrator, dqs_kb_editor y dqs_kb_operator en la base de datos DQS_MAIN.<br /><br /> Se crea el procedimiento almacenado DQInitDQS_MAIN en la base de datos maestra.<br /><br /> El archivo DQS_install.log se crea normalmente en el Server\MSSQL12 de C:\Program Files\Microsoft SQL. *< Nombre_instancia >* carpeta \MSSQL\Log. El archivo contiene información sobre las acciones que se realizan en la ejecución del archivo DQSInstaller.exe.<br /><br /> Si una base de datos de Master Data Services se encuentra en la misma instancia de SQL Server que el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], se crea un usuario asignado al inicio de sesión de Master Data Services y se le concede el rol dqs_administrator en la base de datos DQS_MAIN.<br /><br /> <br /><br /> De este modo se completa la instalación del [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .|[Ejecutar DQSInstaller.exe para completar la instalación del servidor de calidad de datos](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)|  
|Conceder roles de DQS a los usuarios|Para iniciar sesión en [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] mediante [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)], un usuario debe tener alguno de los tres roles siguientes en la base de datos DQS_MAIN: **dqs_administrator**, **dqs_kb_editor**, o **dqs_kb_ operador**. De forma predeterminada, si la cuenta de usuario es miembro del rol fijo de servidor sysadmin, puede iniciar sesión en el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] mediante el [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] aunque no se haya concedido ninguno de los roles de DQS a su cuenta de usuario. Para obtener más información acerca de los tres roles de DQS, vea [Seguridad DQS](../dqs-security.md).<br /><br /> Nota: Los tres roles de DQS no están disponibles para las bases de datos DQS_PROJECTS y DQS_STAGING_DATA.|[Conceder roles de DQS a los usuarios](grant-dqs-roles-to-users.md)|  
|Hacer que los datos estén disponibles para las operaciones de DQS|Asegúrese de que puede tener acceso a los datos de origen para las operaciones de DQS y que puede exportar los datos procesados a una tabla de una base de datos.|[Acceso a datos para las operaciones de DQS](access-data-for-the-dqs-operations.md)|  
  
## <a name="see-also"></a>Vea también  
 [Vídeo: Instalar y configurar DQS](https://go.microsoft.com/fwlink/?LinkId=238241)   
 [Actualizar ensamblados de SQLCLR después de actualizar .NET Framework](upgrade-sqlclr-assemblies-after-net-framework-update.md)   
 [Exportar e importar bases de conocimiento de DQS mediante DQSInstaller.exe](export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)   
 [Actualizar Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md)   
 [Quitar objetos del servidor de calidad de datos](../../sql-server/install/remove-data-quality-server-objects.md)   
 [Instalar las características de BI de SQL Server 2014](../../sql-server/install/install-sql-server-business-intelligence-features.md)   
 [Desinstalar SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)   
 [Data Quality Services](../data-quality-services.md)   
 [Solucionar problemas de instalación y actualización en DQS](https://social.technet.microsoft.com/wiki/contents/articles/3776.aspx)  
  
  
