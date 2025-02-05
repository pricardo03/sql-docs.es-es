---
title: Administración de DQS | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- dqs administration
- administration
- dqs,adminstration
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a84ff61d1656743953f5f854a1b658b303a7acf1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992132"
---
# <a name="dqs-administration"></a>dqs, administración

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) permite administrar diversas actividades de DQS realizadas en [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], configurar las propiedades del servidor relacionadas con las actividades de DQS, configurar los valores de Reference Data Service y configurar los valores del registro de DQS. Todo esto se realizan a través de la característica **Administración** en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. En función del acceso de seguridad (rol) en DQS, se le concede o deniega el acceso a diversas funcionalidades de esta área.  
  
 Además de estas actividades de administración, en este tema, también se ofrece información sobre la actividad de administración, copias de seguridad y restauración de bases de datos de DQS, que no se realizan mediante [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
 La característica de administración de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] tiene las siguientes ventajas:  
  
-   Permite a los administradores de datos supervisar diversas actividades de DQS en un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
-   Permite a los administradores de DQS supervisar las actividades de DQS en un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]y *finalizar* una actividad en ejecución o *detener* un proceso en ejecución dentro de una actividad, si así se requiere.  
  
-   Configure los valores Reference Data Service tal como configura la conectividad con Windows Azure Marketplace y administra proveedores directos de servicios de datos de referencia externos.  
  
-   Configure los umbrales para la limpieza y las actividades de búsqueda de coincidencias.  
  
-   Habilite y deshabilite las notificaciones en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
-   Configure el registro según el nivel de gravedad de los eventos.  
  
##  <a name="AdminUsingClent"></a> Actividades de administración con el cliente de calidad de datos  
 Estas actividades se realizan mediante la característica de **Administración** en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
### <a name="activity-monitoring"></a>Supervisión de actividades  
 La pantalla de **Supervisión de actividades** en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] muestra información detallada sobre cada actividad realizada en [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. El administrador de datos utilizará esta pantalla principalmente para realizar una supervisión de alto nivel de todas las actividades que tienen lugar en el [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] al que está conectado la aplicación de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Esta pantalla no permite realizar ninguna supervisión del sistema. Además, esta pantalla también permite a los administradores de DQS controlar una actividad o un proceso dentro de una actividad; para ello, finaliza una actividad en ejecución o detiene un proceso en ejecución dentro de una actividad, si así se necesita. Los datos se muestran para la detección del conocimiento, administración de dominios, directiva de búsqueda de coincidencias, limpieza, coincidencias y limpieza basada en SQL Server Integration Services (SSIS).  
  
### <a name="configuration"></a>Configuración  
 La pantalla de **Configuración** en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] permite al administrador de DQS hacer lo siguiente:  
  
-   **Datos de referencia**: configurar los proveedores de servicios de datos de referencia: Microsoft Azure Marketplace o proveedores de servicios de datos de referencia directos. Una vez haya establecido los proveedores de servicios de datos de referencia, podrá asignar un dominio o un dominio compuesto a los datos de referencia durante la actividad de administración de dominios en una base de conocimiento y, posteriormente, usar la misma base de conocimiento para la actividad de limpieza en un proyecto de calidad de datos. Por otra parte, le permite especificar la configuración del proxy para la conexión a Internet con el fin de usar Windows Azure Marketplace.  
  
-   **Configuración general**: especifique los valores del umbral para la limpieza de datos y la coincidencia de datos, además de si quiere habilitar las notificaciones para la generación de perfiles en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Estos umbrales los utiliza DQS durante la limpieza asistida por PC y las actividades de búsqueda de coincidencias en un proyecto de calidad de datos.  
  
-   **Configuración de registro**: en los archivos de registro de DQS, se registran las actividades realizadas en DQS y resultan útiles para realizar el seguimiento de problemas operativos durante los procesos de mantenimiento y solución de problemas. Puede filtrar los mensajes que desee registrar para varias características de DQS (administración de dominios, detección del conocimiento, limpieza, coincidencias y servicios de datos de referencia) y módulos de DQS según el nivel de gravedad de los eventos.  
  
> [!NOTE]  
>  La pantalla de **Configuración** solo está disponible para los usuarios que tengan el rol dqs_administrator en la base de datos de DQS_MAIN.  
  
##  <a name="AdminOutsideClient"></a> Actividades de administración fuera de Data Quality Client  
 Estas actividades se realizan fuera de Data Quality Client:  
  
-   **Copia de seguridad y restauración de bases de datos de DQS**: las copias de seguridad y restauración de bases de datos de DQS son iguales que para cualquier base de datos de SQL Server, excepto algunas diferencias específicas de DQS.  
  
-   **Asociar y desasociar bases de datos de DQS**: los pasos para asociar y desasociar bases de datos de DQS son los mismos que para cualquier base de datos de SQL Server, excepto algunas diferencias específicas de DQS.  
  
 Para más información, consulte [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo supervisar actividades en DQS.|[Supervisar las actividades de DQS](../data-quality-services/monitor-dqs-activities.md)|  
|Describe cómo configurar valores de datos de referencia en DQS.|[Configurar DQS para usar datos de referencia](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Describe cómo configurar los umbrales para las actividades de limpieza y búsqueda de coincidencias.|[Configurar los valores de umbral para la limpieza y la coincidencia](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|Describe cómo habilitar o deshabilitar las notificaciones en DQS.|[Habilitar o deshabilitar notificaciones de generación de perfiles en DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|Describe cómo configurar el registro de DQS basado en el nivel de gravedad de los eventos.|[Configurar los niveles de gravedad de los archivos de registro de DQS](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|Describe cómo configurar las configuraciones avanzadas del registro de DQS.|[Configurar las opciones avanzadas de los archivos de registro de DQS](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|Describe cómo realizar copias de seguridad y restaurar bases de datos de DQS.|[Realizar copias de seguridad de bases de datos de DQS y restaurarlas](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|Describe cómo adjuntar y separar bases de datos de DQS.|[Separar y adjuntar bases de datos de DQS](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>Vea también  
 [Servicios de datos de referencia en DQS](../data-quality-services/reference-data-services-in-dqs.md)   
 [Administrar archivos de registro de DQS](../data-quality-services/manage-dqs-log-files.md)   
 [Administrar bases de datos de DQS](../data-quality-services/manage-dqs-databases.md)  
  
  
