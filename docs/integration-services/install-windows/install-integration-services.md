---
title: Instalación de SQL Server Integration Services (SSIS) | Microsoft Docs
description: Obtenga información sobre cómo instalar Microsoft SQL Server Integration Services (SSIS) y cómo obtener otras descargas de SSIS
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 143bba36c1f85877fd3a0504dd8345c754ec055d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023590"
---
# <a name="install-integration-services"></a>Instalar Integration Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un único programa de instalación para instalar alguno de sus componentes o todos, incluido [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Use el programa de instalación para instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con o sin otros componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un único equipo.    
    
 En este artículo se destacan consideraciones importantes que se deberían conocer antes de instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. La información de este artículo le ayudará a evaluar las opciones de instalación para que pueda realizar selecciones que deriven en una instalación correcta.    
    
## <a name="get-ready-to-install-integration-services"></a>Preparación de la instalación de Integration Services    
 Antes de instalar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], revise esta información:    
    
-   [Requisitos de hardware y software para instalar SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
    
-   [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)    
    
## <a name="install-standalone-or-side-by-side"></a>Instalación independiente o en paralelo    
Puede instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en las configuraciones siguientes:    
    
-   Puede instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un equipo que no tenga ninguna instancia anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
-   Puede instalar [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] en paralelo con una instancia existente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].    
    
Al actualizar a la versión más reciente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un equipo que tiene instalada una versión anterior de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], la versión actual se instala en paralelo con la versión anterior.    
    
Para más información sobre cómo actualizar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Actualizar Integration Services](../../integration-services/install-windows/upgrade-integration-services.md).

## <a name="get-sql-server-with-integration-services"></a>Obtención de SQL Server con Integration Services

Si todavía no tiene Microsoft SQL Server, descargue una edición de evaluación gratuita o la Developer Edition gratuita de las [descargas de SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). SSIS no se incluye en SQL Server Express Edition.

## <a name="install-integration-services"></a>Instalar Integration Services    
 Después de revisar los requisitos de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y asegurarse de que el equipo los cumple, puede comenzar a instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].    
     
Si está usando el Asistente para la instalación con el fin de instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], usará una serie de páginas para especificar los componentes y las opciones.

-   En la página **Selección de características**, en **Características compartidas**, seleccione **Integration Services**.

-   En **Características de instancia**, puede seleccionar **Servicios de Motor de base de datos** para hospedar la base de datos del Catálogo de SSIS, `SSISDB`, para almacenar, administrar, ejecutar y supervisar los paquetes SSIS.

-   Para instalar ensamblados administrados para la programación de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], también en **Características compartidas**, seleccione **SDK de las herramientas de cliente**.

> [!NOTE]
> Algunos componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que puede seleccionar para instalarlos en la página **Selección de características** del Asistente para la instalación instalan un subconjunto parcial de componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Estos componentes resultan útiles para tareas específicas, pero las funciones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] son limitadas. Por ejemplo, la opción **Servicios de motor de base de datos** instala los componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necesarios para el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para asegurarse de que la instalación de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]es completa, debe seleccionar **Integration Services** en la página **Selección de características** .

### <a name="installing-a-dedicated-server-for-etl-processes"></a>Instalación de un servidor dedicado para procesos de ETL

Para usar un servidor dedicado para los procesos de extracción, transformación y carga (ETL), instale una instancia local de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] al instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] suele almacenar los paquetes en una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y se basa en el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar estos paquetes. Si el servidor ETL no tiene ninguna instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)], tiene que programar o ejecutar los paquetes desde un servidor que sí tenga una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. El resultado es que los paquetes no se ejecutan en el servidor ETL, sino en el servidor desde el que se inician. Como resultado, los recursos del servidor ETL dedicado no se utilizan como se pretendía. Además, los procesos ETL en ejecución pueden agotar los recursos de otros servidores.

### <a name="configuring-ssis-event-logging"></a>Configuración del registro de eventos SSIS
    
De forma predeterminada, en una instalación nueva, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para no registrar en el registro de eventos de aplicación los eventos relacionados con la ejecución de paquetes. Esta configuración impide la generación de demasiadas entradas en el registro de eventos al usar la característica de recopilador de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Los eventos que no se registran son EventID 12288, "Se ha iniciado el paquete" y EventID 12289, "El paquete finalizó correctamente". Para registrar estos eventos en el registro de eventos de aplicación, abra el Registro para editarlo. A continuación, en el Registro, busque el nodo HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS y cambie el valor DWORD de la opción LogPackageExecutionToEventLog de 0 a 1.    
    
## <a name="install-additional-components-for-integration-services"></a>Instalación de componentes adicionales para Integration Services

Para una instalación completa de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], seleccione los componentes que necesita en esta lista:

-   **Integration Services (SSIS)** . Instale SSIS con el Asistente para la instalación de SQL Server. Al seleccionar SSIS, se instala lo siguiente:

    -   Compatibilidad con el Catálogo de SSIS en el Motor de base de datos de SQL Server.

    -   Si lo prefiere, la característica Escalabilidad horizontal de SSIS, que consta de un patrón y los trabajadores.

    -   Componentes SSIS de 32 bits y 64 bits.

    -   Al instalar SSIS **no** se instalan las herramientas necesarias para diseñar y desarrollar paquetes SSIS.

-   **Motor de base de datos de SQL Server**. Instale el motor de base de datos con el Asistente para la instalación de SQL Server. Al seleccionar el motor de base de datos, puede crear y hospedar la base de datos del Catálogo de SSIS, `SSISDB`, para almacenar, administrar, ejecutar y supervisar los paquetes SSIS.

-   **SQL Server Data Tools (SSDT)** . Para descargar e instalar SSDT, vea [Descargar SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md). Instalar SSDT le permite diseñar e implementar paquetes SSIS. SSDT instala lo siguiente:

    -   Herramientas de diseño y desarrollo del paquete SSIS, incluido el Diseñador SSIS.

    -   Componentes SSIS de 32 bits solamente.

    -   Una versión limitada de Visual Studio (si no hay ya instalada una edición de Visual Studio).

    -   Visual Studio Tools for Applications (VSTA), el editor de scripts usado por la tarea de script y el componente de script de SSIS.

    -   Asistentes de SSIS, incluido el Asistente para implementación y el Asistente para actualización de paquetes.

    -   Asistente para importación y exportación de SQL Server.

-   **Feature Pack de Integration Services para Azure**. Para descargar e instalar el Feature Pack, vea [Microsoft SQL Server 2017 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=54798) (Feature Pack de Microsoft SQL Server 2017 Integration Services para Azure). Al instalar el Feature Pack, los paquetes se conectan a los servicios de almacenamiento y análisis de la nube de Azure, incluidos los servicios siguientes:

    -   Almacenamiento de blobs de Azure.

    -   HDInsight de Azure.

    -   Azure Data Lake Store.

    -   Azure SQL Data Warehouse.

-   **Componentes adicionales opcionales**. Si lo prefiere, puede descargar otros componentes de terceros desde el Feature Pack de SQL Server.

    -   Microsoft Connector for SAP BW para Microsoft SQL Server. Para obtener estos componentes, visite [Microsoft SQL Server 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992).

    -   Microsoft Conector versión 5.0 para Oracle de Attunity y Microsoft Connector versión 5.0 para Teradata de Attunity. Para obtener estos componentes, visite [Microsoft Connectors v5.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=55179) (Microsoft Connectors v5.0 para Oracle y Teradata).
