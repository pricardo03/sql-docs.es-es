---
title: Orígenes de datos admitidos por Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SQL Server data processing extension [Reporting Services]
- XML data processing extension [Reporting Services]
- reports [Reporting Services], data
- data processing extensions [Reporting Services], data sources
- Oracle [Reporting Services]
- OLE DB data processing extension
- data sources [Reporting Services], about data sources
- ODBC data processing extension
- Reporting Services, data sources
ms.assetid: 9d11d055-a3be-45aa-99a7-46447a94ed42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 247dd2950365a1b75a3b911fe6dfda1a4dd044df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107371"
---
# <a name="data-sources-supported-by-reporting-services-ssrs"></a>Orígenes de datos admitidos por Reporting Services (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] recupera datos de informe de orígenes de datos mediante un nivel de datos modular y extensible que usa extensiones de procesamiento de datos. Para recuperar datos de informe de un origen de datos, debe seleccionar una extensión de procesamiento de datos que admita el tipo de origen de datos, la versión del software que se ejecuta en el origen de datos y la plataforma del origen de datos ( [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]de 32 ó 64 bits).  
  
 Al implementar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], automáticamente se instala un conjunto de extensiones de procesamiento de datos y se registra tanto en el cliente de creación de informes como en el servidor de informes para proporcionar acceso a diversos tipos de orígenes de datos. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instala los tipos de orígenes de datos siguientes:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para MDX, DMX, [!INCLUDE[msCoName](../../includes/msconame-md.md)] PowerPivot y los modelos tabulares  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Almacenamiento de datos paralelos  
  
-   Oracle  
  
-   SAP NetWeaver BI  
  
-   [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Lista de SharePoint  
  
-   Teradata  
  
-   OLE DB  
  
-   ODBC  
  
-   XML  
  
 Además, los administradores del sistema pueden instalar y registrar proveedores de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] estándar y extensiones de procesamiento de datos personalizadas. Para procesar y ver un informe, las extensiones de procesamiento de datos y los proveedores de datos se deben instalar y registrar en el servidor de informes; para obtener una vista previa de un informe, deben instalarse y registrarse en el cliente de creación de informes. Las extensiones de procesamiento de datos y los proveedores de datos se deben compilar de forma nativa para la plataforma donde estén instalados. Si implementa un origen de datos mediante programación usando el servicio web de SOAP, debe definir la extensión de origen de datos. Use los valores de extensión de datos del archivo **RSReportDesigner.config** . De forma predeterminada, el archivo se encuentra en la siguiente carpeta:  
  
```  
<drive letter>\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
```  
  
 Por ejemplo, la extensión de datos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es OLEDB-MD.  
  
 Se pueden descargar varios proveedores de datos estándar de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] de terceros en el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=51456) y en sitios de terceros. Además, puede buscar información sobre proveedores de datos de terceros en el foro público de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
>  Los proveedores de datos estándar de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] no admiten necesariamente toda la funcionalidad proporcionada por las extensiones de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Además, algunos proveedores de datos OLE DB y controladores ODBC se pueden usar para crear y obtener vistas previas de informes, pero no se han diseñado para admitir informes publicados en un servidor de informes. Por ejemplo, el proveedor OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para Jet no se admite en el servidor de informes. Para obtener más información, vea [Extensiones de procesamiento de datos y proveedores de datos de .NET Framework &#40;SSRS&#41;](data-processing-extensions-and-net-framework-data-providers-ssrs.md).  
  
 Para obtener más información acerca de las extensiones de procesamiento de datos personalizadas, vea [Implementing a Data Processing Extension](../extensions/data-processing/implementing-a-data-processing-extension.md). Para obtener más información sobre los proveedores de datos estándar de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , vea el espacio de nombres <xref:System.Data> .  
  
 Para obtener más información sobre las extensiones de procesamiento de datos admitidas por el Generador de informes, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md) en la [documentación del Generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com.  
  
## <a name="platform-support-for-report-data-sources"></a>Plataformas compatibles con los orígenes de datos de informe  
 Los orígenes de datos que puede usar en una implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] varían según la edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la versión de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la plataforma. Para obtener más información acerca de las características, consulte [características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). La tabla que se incluye más adelante en este tema proporciona información acerca de los orígenes de datos admitidos según la versión y la plataforma.  
  
 Las consideraciones sobre las plataformas para los orígenes de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] son independientes para el cliente de creación de informes y el servidor de informes.  
  
### <a name="on-the-report-authoring-client"></a>En el cliente de creación de informes  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] es una aplicación de 32 bits. [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] no se admite en una plataforma basada en Itanium. En una plataforma x64, para editar y obtener vistas previas de los informes en el Diseñador de informes, debe tener instalados proveedores de datos de 32 bits en el directorio de la plataforma (x86).  
  
### <a name="on-the-report-server"></a>En el servidor de informes  
 Al implementar un informe en un servidor de informes de 64 bits (x86), el servidor de informes debe tener instalados proveedores de datos de 64 bits compilados de forma nativa. No se admite la inclusión de un proveedor de datos de 32 bits en interfaces de 64 bits. Para obtener más información, vea la documentación del proveedor de datos.  
  
## <a name="supported-data-sources"></a>Orígenes de datos compatibles  
 En la siguiente tabla se incluyen las extensiones de procesamiento de datos y los proveedores de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] que puede usar para recuperar datos para los conjuntos de datos de informe y los modelos de informe. Para obtener más información acerca de una extensión o un proveedor de datos, haga clic en el vínculo de la segunda columna. Las columnas de la tabla se describen del modo siguiente:  
  
-   Origen de datos de informe: El tipo de datos que se tiene acceso; Por ejemplo, bases de datos relacionales, bases de datos multidimensionales, archivos sin formato o XML. Esta columna responde a la pregunta: "¿Qué tipos de datos puede [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilizar en un informe?"  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Tipo de origen de datos: Uno de los tipos de orígenes de datos se ve en la lista desplegable al definir un origen de datos en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta lista se rellena a partir de las DPE y los proveedores de datos instalados y registrados. Esta columna responde a la pregunta: "Tipo de origen de los datos que debe seleccionar en la lista desplegable al crear un origen de datos de informe?"  
  
-   Nombre del proveedor de datos de extensión/procesamiento de datos: El [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] extensión de procesamiento de datos u otro proveedor de datos que corresponde a la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tipo seleccionado del origen de datos. Esta columna responde a la pregunta: "Cuando se selecciona un tipo de origen de datos, qué proveedor de datos o de extensiones de procesamiento de datos correspondiente se usa?"  
  
-   Versión del proveedor de datos subyacente (opcional): Algunos tipos de orígenes de datos admiten más de un proveedor de datos. Puede tratarse de distintas versiones del mismo proveedor o de distintas implementaciones por parte de terceros para un tipo de proveedor de datos. El nombre del proveedor suele aparecer en la cadena de conexión después de configurarse un origen de datos. Esta columna responde a la pregunta: "Después de seleccionar el tipo de origen de datos, ¿qué proveedor de datos se selecciona en el cuadro de diálogo **Propiedades de conexión**?"  
  
-   Origen de datos *\<plataforma>* : La plataforma del origen de datos admitida por el proveedor de datos o de extensiones de procesamiento de datos para el origen de datos de destino. Esta columna responde a la pregunta: "¿Puede esta extensión de procesamiento de datos para el proveedor de datos recuperar datos desde un origen de datos en este tipo de plataforma?"  
  
-   Versión de origen de datos: La versión del origen de datos de destino admitido por la DPE o proveedor de datos. Esta columna responde a la pregunta: "¿Puede esta extensión de procesamiento de datos para el proveedor de datos recuperar datos desde esta versión del origen de datos?"  
  
-   RS *\<plataforma>* : Las plataformas para el servidor de informes y el cliente de creación de informes donde puede instalar una DPE o datos un proveedor personalizado. Las extensiones de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integradas se incluyen con todas las instalaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Una extensión de datos personalizada o un proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] se deben compilar de forma nativa para una plataforma específica. Esta columna responde a la pregunta: "Esta extensión de procesamiento de datos para el proveedor de datos se puede instalar en este tipo de plataforma?"  
  
###  <a name="DataSourcesTable"></a> Tipos de orígenes de datos  
  
|Origen de<br /><br /> datos de informe|Tipo de origen de datos de Reporting Services|Nombre de la extensión de procesamiento de datos o proveedor de datos|Versión del proveedor de datos subyacente<br /><br /> (Opcional)|Datos<br /><br /> `Source`<br /><br /> Plataforma x86|Datos<br /><br /> `Source`<br /><br /> Plataforma x64|Versión del origen de datos|RS<br /><br /> Plataforma x86|RS<br /><br /> Plataforma x64|  
|-------------------------------|-----------------------------------------|------------------------------------------------------|-------------------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|-------------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos relacional|[Microsoft SQL Server](#MicrosoftSQLServer)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Extiende System.Data.SqlClient|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.|S|S|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos relacional|[OLEDB](#OLEDBSQL)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Extiende System.Data.OledbClient|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.|S|S|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos relacional|[ODBC](#ODBC)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Extiende System.Data.OdbcClient|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.|S|S|  
|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|[Microsoft Azure SQL Database](#Azure)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Extiende System.Data.SqlClient|N/D|N/D|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|S|S|  
|[!INCLUDE[ssDW](../../includes/ssdw-md.md)] dispositivo|[Almacenamiento de datos paralelo de Microsoft](#PWD)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|N/D|N/D|N/D|[!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos multidimensional|[Microsoft SQL Server Analysis Services](#AnalysisServices)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Usa ADOMD.NET|S|S|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y versiones posteriores<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos multidimensional|[OLEDB](#OLEDBAS9)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Extiende System.Data.OledbClient<br /><br /> Versión 10.0|S|S|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos multidimensional|[OLEDB](#OLEDBAS9)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Extiende System.Data.OledbClient<br /><br /> Versión 9,0|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos multidimensional|OLEDB|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Extiende System.Data.OledbClient<br /><br /> Versión 8.0|S|N|N/D|S|N|  
|Listas de SharePoint|[Lista de Microsoft SharePoint](#SharePointList)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Obtiene los datos de las interfaces de las API del modelo de objetos de SharePoint o de Lists.asmx.<br /><br /> Vea la [Nota](#SharePointList).|N|S|Productos de SharePoint 2013<br /><br /> Productos de SharePoint 2010|S|S|  
|Listas de SharePoint|[Lista de Microsoft SharePoint](#SharePointList)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Obtiene los datos de las interfaces de las API del modelo de objetos de SharePoint o de Lists.asmx.<br /><br /> Vea la [Nota](#SharePointList).|S|S|[!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 y [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007|S|S|  
|XML|[XML](#XML)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Los orígenes de datos XML no tienen dependencias de plataformas.|N/D|N/D|[!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)] o documentos|S|S|  
|Modelo del servidor de informes|Modelo de informe|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada para un archivo SMDL publicado|Los orígenes de datos para un modelo usan extensiones de procesamiento de datos integradas.<br /><br /> Los modelos basados en Oracle requieren componentes del cliente Oracle.<br /><br /> Los modelos basados en Teradata requieren el proveedor de datos .NET para Teradata de Teradata.<br /><br /> Vea la documentación de Teradata para obtener información acerca de las plataformas compatibles.|N/D|N/D|Los modelos se pueden crear a partir de:[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<br /><br /> Oracle 9.2.0.3 o posterior<br /><br /> Teradata V14, v13, v12 y v6.2|S|S|  
|Base de datos multidimensional de SAP|[SAP NetWeaver BI](#SapBINetWeaver)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Vea la documentación de SAP para obtener información acerca de las plataformas compatibles.|N/D|N/D|SAP NetWeaver BI 3.5|S|N/D|  
|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)]|[Hyperion Essbase](#Hyperion)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Vea la documentación de Hyperion para obtener información acerca de las plataformas compatibles.|S|N/D|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 9.3.1|S|N/D|  
|Base de datos relacional de Oracle|[Oracle](#OracleClient)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Extiende System.Data.OracleClient.<br /><br /> Requiere componentes del cliente Oracle.|S|N/D|Oracle 10g, 9, 8.1.7|S|S|  
|Base de datos relacional de Teradata|[Teradata](#Teradata)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Extiende el proveedor de datos .NET para Teradata de Teradata.<br /><br /> Requiere el proveedor de datos .NET para Teradata de Teradata.<br /><br /> Vea la documentación de Teradata para obtener información acerca de las plataformas compatibles.|S|N/D|Teradata v14<br /><br /> Teradata versión 13<br /><br /> Teradata versión 12<br /><br /> Teradata versión 6.20|S|N|  
|Base de datos relacional de DB2|Nombre de extensión de datos registrada personalizada||Host Integration (HI) Server 2004<br /><br /> Vea la [documentación de HI Server](https://msdn.microsoft.com/library/gg241192\(v=bts.10\).aspx).|S|N/D|N/D|S|N|  
|Origen de datos OLE DB genérico|[OLEDB](#OLEDBStandard)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Cualquier origen de datos que admita OLE DB.<br /><br /> Vea la documentación del origen de datos para obtener información sobre las plataformas compatibles.|S|N/D|Cualquier origen de datos que admita OLE DB. Vea la [Nota](#OLEDBStandard).|S|N/D|  
|Origen de datos ODBC genérico|[ODBC](#ODBCGeneric)|Extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrada|Cualquier origen de datos que admita ODBC.<br /><br /> Vea la documentación del origen de datos para obtener información sobre las plataformas compatibles.|S|N/D|Cualquier origen de datos que admita ODBC. Vea la [Nota](#ODBCGeneric).|S|S|  
  
 Para obtener información sobre el uso de un origen de datos tabulares, vea [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Para obtener información sobre el uso de orígenes de datos externos, vea [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md).  
  
 Hay disponibles diversos proveedores de datos estándar de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] de terceros. Para obtener más información, busque en sitios web o foros de terceros.  
  
 Para instalar y registrar un extensión de procesamiento de datos personalizada o un proveedor de datos estándar de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , consulte la documentación de referencia del proveedor de datos. Para obtener más información, vea [Registrar un proveedor de datos estándar de .NET Framework &#40;SSRS&#41;](register-a-standard-net-framework-data-provider-ssrs.md).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
## <a name="reporting-services-data-processing-extensions"></a>Extensiones de procesamiento de datos de Reporting Services  
 Las siguientes extensiones de procesamiento de datos se instalan automáticamente con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]. Para obtener más información y para comprobar la instalación, consulte [RSReportDesigner Configuration File](../report-server/rsreportdesigner-configuration-file.md) y [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md).  
  
> [!NOTE]  
>  La extensión de procesamiento de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no se admite en este momento.  
  
 Para obtener más información sobre las extensiones de procesamiento de datos admitidas por el Generador de informes, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md) en la [documentación del Generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com.  
  
###  <a name="MicrosoftSQLServer"></a> Extensión de procesamiento de datos de Microsoft SQL Server  
 El tipo de origen de datos **Microsoft SQL Server** incluye y extiende el proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta extensión de procesamiento de datos se compila de forma nativa y se ejecuta en plataformas basadas en x86 e [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)].  
  
 En [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], el diseñador de consultas asociado a esta extensión de datos es el [diseñador de la herramienta de base de datos visual](../../ssms/visual-db-tools/visual-database-tool-designers.md). Si usa el diseñador de consultas en el modo gráfico, la consulta se analiza y es posible que se vuelva a escribir. Use el diseñador de consultas basado en texto si quiere controlar la sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] exacta que se usa para una consulta. Para obtener más información, vea [Herramientas Diseñador de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) e [Interfaz de usuario del diseñador gráfico de consultas](graphical-query-designer-user-interface.md).  
  
 Para obtener más información, vea [Tipo de conexión de SQL Server &#40;SSRS&#41;](sql-server-connection-type-ssrs.md).  
  
 En el Generador de informes, el diseñador de consultas asociado a esta extensión de datos es el Diseñador de consultas relacionales. Para obtener más información, vea [Relational Query Designer User Interface](../relational-query-designer-user-interface.md).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
###  <a name="Azure"></a> Extensión de procesamiento de la base de datos SQL Azure de Windows  
 El tipo de origen de datos **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]** ajusta y extiende el proveedor de datos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], el diseñador gráfico de consultas asociado a esta extensión de datos es la [Interfaz de usuario del Diseñador de consultas relacionales](../relational-query-designer-user-interface.md), no el [Diseñador de Visual Database Tools](../../ssms/visual-db-tools/visual-database-tool-designers.md) que usa con el tipo de origen de datos de **Microsoft SQL Server** .  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] diferencia automáticamente entre **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]** y **Microsoft SQL Server** tipos de origen de datos y se abre el diseñador gráfico de consultas asociado al tipo de origen de datos.  
  
 Si usa el diseñador de consultas en el modo gráfico, la consulta se analiza y es posible que se vuelva a escribir. También se dispone de un diseñador de consultas basado en texto para escribir consultas. Use el diseñador de consultas basado en texto si quiere controlar la sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] exacta que se usa para una consulta. Para obtener más información, vea [Interfaz de usuario del Diseñador de consultas basado en texto](../text-based-query-designer-user-interface.md).  
  
 Los datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se recuperan de forma similar, pero hay algunos requisitos que solo se aplican a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Para obtener más información, vea [Tipo de conexión SQL Azure &#40;SSRS&#41;](sql-azure-connection-type-ssrs.md).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
###  <a name="PWD"></a> Extensión de procesamiento del almacenamiento de datos paralelo de Microsoft SQL Server  
 En [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], el diseñador gráfico de consultas asociado a esta extensión de datos es la [Interfaz de usuario del Diseñador de consultas relacionales](../relational-query-designer-user-interface.md), no el [Diseñador de Visual Database Tools](../../ssms/visual-db-tools/visual-database-tool-designers.md) que usa con el tipo de origen de datos de **Microsoft SQL Server** .  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] diferencia automáticamente entre **almacenamiento de datos paralelos de SQL Server** y **Microsoft SQL Server** tipos de origen de datos y se abre el diseñador gráfico de consultas asociado al tipo de origen de datos.  
  
 Si usa el diseñador de consultas en el modo gráfico, la consulta se analiza y es posible que se vuelva a escribir. También se dispone de un diseñador de consultas basado en texto para escribir consultas. Use el diseñador de consultas basado en texto si quiere controlar la sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] exacta que se usa para una consulta. Para más información, vea [Interfaz de usuario del Diseñador de consultas basado en texto](../text-based-query-designer-user-interface.md).  
  
 [!INCLUDE[ssDWCurrentFull](../../includes/ssdwcurrentfull-md.md)] no admite el uso de procedimientos almacenados y funciones con valores de tabla en las consultas. Para obtener más información, vea [Tipo de conexión Almacenamiento de datos paralelo de SQL Server &#40;SSRS&#41;](sql-server-parallel-data-warehouse-connection-type-ssrs.md).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
###  <a name="AnalysisServices"></a> Extensión de procesamiento de datos de Microsoft SQL Server Analysis Services  
 Al seleccionar el tipo de origen de datos **Microsoft SQL Server Analysis Services**, está seleccionando una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que extiende el proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Esta extensión de procesamiento de datos se compila de forma nativa y se ejecuta en plataformas basadas en x86 y x64.  
  
 Este proveedor de datos usa el modelo de objetos ADOMD.NET para crear consultas con XML for Analysis (XMLA) versión 1.1. Los resultados se devuelven como un conjunto de filas planas. Para más información, vea [Tipo de conexión de Analysis Services para MDX &#40;SSRS&#41;](analysis-services-connection-type-for-mdx-ssrs.md), [Tipo de conexión de Analysis Services para DMX &#40;SSRS&#41;](analysis-services-connection-type-for-dmx-ssrs.md), [Interfaz de usuario del Diseñador de consultas MDX de Analysis Services](analysis-services-mdx-query-designer-user-interface.md) e [Interfaz de usuario del Diseñador de consultas DMX de Analysis Services](analysis-services-dmx-query-designer-user-interface.md).  
  
 Al conectarse a un origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , la extensión de procesamiento de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite parámetros de varios valores y asigna propiedades de celda y de miembro a las propiedades extendidas admitidas por [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obtener más información, vea [Propiedades de campo extendidas para una base de datos de Analysis Services &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
 También puede crear modelos a partir de orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
###  <a name="OLEDBAll"></a> OLE DB Data Processing Extension  
 La extensión de procesamiento de datos de OLE DB requiere la selección de una capa de proveedor de datos adicional basada en la versión del origen de datos que desee usar en el informe. Si no selecciona un proveedor de datos específico, se proporciona un proveedor predeterminado. Elija un proveedor de datos específico mediante el cuadro de diálogo **Propiedades de conexión** , al que se tiene acceso con el botón **Editar** de los cuadros de diálogo [Origen de datos](../data-source-properties-dialog-box-general.md) u [Origen de datos compartido](../shared-data-source-properties-dialog-box-general.md) .  
  
 Para obtener más información sobre el Diseñador de consultas asociado de OLE DB, vea [Herramientas Diseñador de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) e [Interfaz de usuario del diseñador gráfico de consultas](graphical-query-designer-user-interface.md). Para obtener más información acerca de la compatibilidad específica con los proveedores OLE DB, vea [La herramienta de diseñador de Visual Studio .NET es compatible con proveedores OLE DB específicos](https://support.microsoft.com/default.aspx/kb/811241) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base.  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
####  <a name="OLEDBSQL"></a> OLE DB para SQL Server  
 Al seleccionar el tipo de origen de datos **OLE DB**, está seleccionando una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que extiende el proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para OLE DB. Esta extensión de procesamiento de datos se compila de forma nativa y se ejecuta en plataformas basadas en x86 y x64.  
  
 Para obtener más información, vea [Tipo de conexión OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
####  <a name="OLEDBAS9"></a> OLE DB para Analysis Services 9.0  
 Para conectarse a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], seleccione el proveedor OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 9.0, seleccione el proveedor OLE DB de the data source type **OLE DB**y, a continuación, seleccione el proveedor de datos subyacente por el nombre. Esta combinación de la extensión de procesamiento de datos y del proveedor de datos se compila de forma nativa y se ejecuta en plataformas x86 y x64.  
  
> [!NOTE]  
>  Esta extensión de procesamiento de datos no admite los agregados de servidor, la asignación automática de propiedades de campo extendidas ni los parámetros de consulta. El proveedor de datos recomendado para un origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es **Microsoft SQL Server Analysis Services**.  
  
 Para obtener más información, vea [Tipo de conexión OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
#### <a name="ole-db-for-olap-70"></a>OLE DB para OLAP 7.0  
 No se admite el proveedor OLE DB para OLAP Services 7.0.  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
####  <a name="OracleOLEDB"></a> OLE DB para Oracle  
 La extensión de procesamiento de datos OLE DB para Oracle no admite los siguientes tipos de datos de Oracle: BLOB, CLOB, NCLOB, BFILE Y UROWID.  
  
 Se admiten los parámetros sin nombre dependientes de la posición. Esta extensión no admite los parámetros con nombre. Para usar parámetros con nombre, use la extensión de procesamiento de datos de [Oracle](#OracleClient) .  
  
 Para obtener más información acerca de la configuración de Oracle como un origen de datos, vea [Cómo utilizar Reporting Services para configurar y obtener acceso a orígenes de datos de Oracle](https://support.microsoft.com/kb/834305). Para obtener más información acerca de la configuración de permisos adicionales, vea la página en que se describe [cómo agregar permisos para la entidad de seguridad NETWORK SERVICE](https://support.microsoft.com/kb/870668) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base.  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
####  <a name="OLEDBStandard"></a> Proveedor de datos de .NET Framework estándar OLE DB  
 Para recuperar datos de un origen de datos que admita proveedores de datos OLE DB de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , use el tipo de origen de datos **OLE DB** y seleccione el proveedor de datos predeterminado o seleccione uno de los proveedores de datos instalados en el cuadro de diálogo **Cadena de conexión** .  
  
> [!NOTE]  
>  Aunque el proveedor de datos puede admitir que se obtenga una vista previa del informe en el cliente de creación de informes, no todos los proveedores de datos OLE DB están diseñados para admitir informes publicados en un servidor de informes.  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
###  <a name="ODBC"></a> ODBC Data Processing Extension  
 Al seleccionar el tipo de origen de datos **ODBC**, está seleccionando una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que extiende el proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para ODBC. Esta extensión de procesamiento de datos se compila de forma nativa y se ejecuta en plataformas basadas en x86 y [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] . Use esta extensión para conectarse y recuperar datos de cualquier origen de datos con un proveedor ODBC.  
  
> [!NOTE]  
>  Aunque el proveedor de datos puede admitir que se obtenga una vista previa del informe en el cliente de creación de informes, no todos los proveedores de datos ODBC están diseñados para admitir informes publicados en un servidor de informes.  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
####  <a name="ODBCGeneric"></a> Proveedor de datos estándar de .NET Framework ODBC  
 Para recuperar datos de un origen de datos que admita un proveedor de datos estándar de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ODBC, use el tipo de origen de datos **ODBC** y seleccione el proveedor de datos predeterminado o seleccione uno de los proveedores de datos instalados en el cuadro de diálogo **Cadena de conexión** .  
  
> [!NOTE]  
>  Aunque el proveedor de datos puede admitir que se obtenga una vista previa del informe en el cliente de creación de informes, no todos los proveedores de datos ODBC están diseñados para admitir informes publicados en un servidor de informes.  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
###  <a name="OracleClient"></a> Extensión de procesamiento de datos de Oracle  
 Al seleccionar el tipo de origen de datos **Oracle**, está seleccionando una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que extiende el proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para Oracle. El **Oracle** origen de datos incluye y extiende el <xref:System.Data.OracleClient> necesitan clases [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para recuperar los datos de informe de una base de datos de Oracle, el administrador debe instalar las herramientas cliente de Oracle. Este proveedor de datos usa Oracle Call Interface (OCI) de la versión 3 de Oracle 8i suministrada por el software cliente de Oracle. La versión de la aplicación cliente debe ser 8.1.7 o posterior. Estas herramientas deben estar instaladas en el cliente de creación de informes para obtener vistas previas de los informes y en el servidor de informes para ver los informes publicados.  
  
 Esta extensión admite los parámetros con nombre. En Oracle versión 9 o posterior, se admiten los parámetros de varios valores. En el caso de los parámetros sin nombre dependientes de la posición, use la extensión de procesamiento de datos OLE DB con el proveedor de datos Proveedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Oracle. Para obtener más información acerca de la configuración de Oracle como un origen de datos, vea [Cómo utilizar Reporting Services para configurar y obtener acceso a orígenes de datos de Oracle](https://support.microsoft.com/kb/834305). Para obtener más información acerca de la configuración de permisos adicionales, vea la página en que se describe [cómo agregar permisos para la entidad de seguridad NETWORK SERVICE](https://support.microsoft.com/kb/870668) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base.  
  
 Puede recuperar datos de procedimientos almacenados con varios parámetros de entrada, pero el procedimiento almacenado debe devolver solo un cursor de salida. Para obtener más información, vea la sección de Oracle en [Recuperar datos mediante DataReader](https://go.microsoft.com/fwlink/?LinkId=81758).  
  
 Para obtener más información, vea [Tipo de conexión de Oracle &#40;SSRS&#41;](oracle-connection-type-ssrs.md). Para obtener más información sobre el diseñador de consultas asociado, vea [Herramientas Diseñador de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) e [Interfaz de usuario del diseñador gráfico de consultas](graphical-query-designer-user-interface.md).  
  
 También se pueden crear modelos basados en una base de datos de Oracle.  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
###  <a name="Teradata"></a> Extensión de procesamiento de datos de Teradata  
 Al seleccionar el tipo de origen de datos **Teradata**, está seleccionando una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que extiende el proveedor de datos de .NET Framework para Teradata. Para recuperar datos de informe de una base de datos de Teradata, el administrador del sistema debe instalar el proveedor de datos de .NET Framework para Teradata en el cliente de creación de informes para poder editar y obtener vistas previas de los informes en el cliente, y en el servidor de informes para ver los informes publicados.  
  
 En los proyectos de servidor de informes, no hay un diseñador gráfico de consultas disponible para esta extensión. Debe usar el diseñador de consultas basado en texto para crear las consultas.  
  
 En la tabla siguiente se muestran las versiones del proveedor de datos .NET para Teradata compatibles con la definición de un origen de datos en una definición de informe en [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]:  
  
|[!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] versión 8.0|Versión de la base de datos de Teradata|Versión del proveedor de datos de .NET Framework para Teradata|  
|-----------------------------------|-------------------------------|-------------------------------------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|12.00|12.00|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|6.20|12.00|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|14.00|14.00.01|  
  
 Esta extensión admite los parámetros de varios valores. Pueden especificarse macros en una consulta mediante el comando EXECUTE en modo de consulta TEXT.  
  
 Para más información, vea [Tipo de conexión de Teradata &#40;SSRS&#41;](teradata-connection-type-ssrs.md).  
  
 También se pueden crear modelos basados en una base de datos de Teradata. Para obtener más información, consulte las notas del producto siguientes en el sitio de Teradata: [Microsoft SQL Server 2012 Reporting Services y Teradata Corporation](http://www.teradata.com/white-papers/Microsoft-SQL-Server-2012-Reporting-Services-and-Teradata-Corporation/?type=WP).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
###  <a name="SharePointList"></a> Extensión de datos de lista de SharePoint  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye la extensión de datos de Lista de SharePoint de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para que pueda usar listas de SharePoint como origen de datos en un informe. Puede recuperar datos de listas desde lo siguiente:  
  
-   [!INCLUDE[SPS2013](../../includes/sps2013-md.md)]  
  
-   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] y [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]  
  
-   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 y [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007  
  
 Hay tres implementaciones del proveedor de datos de Lista de SharePoint.  
  
1.  En un entorno de creación de informes como el Generador de informes o el Diseñador de informes de [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], o para un servidor de informes que se configura en modo nativo, los datos de la lista proceden del servicio web de Lists.asmx para el sitio de SharePoint.  
  
2.  En un servidor de informes que se configura en el modo integrado de SharePoint, los datos de la lista vienen del servicio web de Lists.asmx correspondiente o de las llamadas de programación a la API de SharePoint. En este modo, puede recuperar los datos de la lista de una granja de servidores de SharePoint.  
  
3.  Para [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] y [!INCLUDE[SPS2013](../../includes/sps2013-md.md)], el Complemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para Tecnologías de [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint le permite recuperar datos de lista de un servicio web Lists.asmx para un sitio de SharePoint o del sitio de SharePoint que forma parte de una granja de servidores de SharePoint. Este escenario también es conocido como *modo local* porque no se requiere un servidor de informes.  
  
 Las credenciales que puede especificar dependen de la implementación que la aplicación cliente use. Para obtener más información, vea [Tipo de conexión de lista de SharePoint &#40;SSRS&#41;](sharepoint-list-connection-type-ssrs.md).  
  
###  <a name="XML"></a> Extensión de procesamiento de datos XML  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye una extensión de procesamiento de datos XML que le permite usar datos XML en un informe. Los datos pueden recuperarse de un documento XML, un servicio web o una aplicación basada en Web a la que se pueda tener acceso mediante una dirección URL. Para más información, vea [Tipo de conexión XML &#40;SSRS&#41;](xml-connection-type-ssrs.md). Para obtener más información sobre el diseñador de consultas asociado, vea la sección dedicada al diseñador de consultas basado en texto en [Interfaz de usuario del diseñador gráfico de consultas](graphical-query-designer-user-interface.md). Para obtener ejemplos, vea [Reporting Services: uso de XML y orígenes de datos del servicio web](https://go.microsoft.com/fwlink/?LinkId=81654).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
###  <a name="SapBINetWeaver"></a> Extensión de procesamiento de datos SAP NetWeaver Business Intelligence  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye una extensión de procesamiento de datos que permite el uso de datos de un origen de datos de [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] en un informe.  
  
 Para obtener más información, vea [Tipo de conexión de SAP NetWeaver BI &#40;SSRS&#41;](sap-netweaver-bi-connection-type-ssrs.md). Para obtener más información acerca del diseñador de consultas asociado, vea [SAP NetWeaver BI Query Designer User Interface](sap-netweaver-bi-query-designer-user-interface.md).  
  
 Para obtener más información acerca de [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)], vea [Usar SQL Server 2008 Reporting Services con SAP NetWeaver Business Intelligence](https://go.microsoft.com/fwlink/?LinkId=167352).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
###  <a name="Hyperion"></a> Extensión de procesamiento de datos de Hyperion Essbase Business Intelligence  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye una extensión de procesamiento de datos que permite el uso de datos de un origen de datos de [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] en un informe.  
  
 Para obtener más información, vea [Tipo de conexión de Hyperion Essbase &#40;SSRS&#41;](hyperion-essbase-connection-type-ssrs.md). Para obtener más información acerca del diseñador de consultas asociado, vea [Hyperion Essbase Query Designer User Interface](hyperion-essbase-query-designer-user-interface.md).  
  
 Para obtener más información acerca de [!INCLUDE[extEssbase](../../includes/extessbase-md.md)], vea [Usar SQL Server 2005 Reporting Services con Hyperion Essbase](https://go.microsoft.com/fwlink/?LinkId=81970).  
  
 [Volver a la tabla de orígenes de datos](#DataSourcesTable)  
  
## <a name="see-also"></a>Vea también  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md)  
  
  
