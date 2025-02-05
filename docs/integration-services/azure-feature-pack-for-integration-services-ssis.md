---
title: Azure Feature Pack para Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9241725a9f1da67ef93701b62c5cc4e8d9093a7a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892730"
---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Azure Feature Pack para Integration Services (SSIS)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Feature Pack de SQL Server Integration Services (SSIS) para Azure es una extensión que proporciona los componentes que se muestran en esta página para que SSIS se conecte a los servicios de Azure, para transferir datos entre Azure y orígenes de datos locales, y para procesar los datos almacenados en Azure.

[![Descargar Feature Pack de SSIS para Azure](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/download/details.aspx?id=54798) **Descargar**

- Para SQL Server 2017 - [Feature Pack de Microsoft SQL Server 2017 Integration Services para Azure](https://www.microsoft.com/download/details.aspx?id=54798)
- Para SQL Server 2016 - [Feature Pack de Microsoft SQL Server 2016 Integration Services para Azure](https://www.microsoft.com/download/details.aspx?id=49492)
- Para SQL Server 2014 - [Feature Pack de Microsoft SQL Server 2014 Integration Services para Azure](https://www.microsoft.com/download/details.aspx?id=47366)
- Para SQL Server 2012 - [Feature Pack de Microsoft SQL Server 2012 Integration Services para Azure](https://www.microsoft.com/download/details.aspx?id=47367)

En las páginas de descarga también se incluye información sobre los requisitos previos. Asegúrese de instalar SQL Server antes de instalar el Feature Pack de Azure en un servidor o es posible que los componentes del Feature Pack no estén disponibles al implementar los paquetes en la base de datos de catálogo de SSIS, SSISDB, en el servidor.

## <a name="components-in-the-feature-pack"></a>Componentes de Feature Pack
-   Administradores de conexión

    -   [Administrador de conexiones de Azure Data Lake Analytics](connection-manager/azure-data-lake-analytics-connection-manager.md)

    -   [Administrador de conexiones de Azure Data Lake Store](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Administrador de conexiones de Azure HDInsight](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

    -   [Administrador de conexiones de Azure Resource Manager](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Administrador de conexiones de almacenamiento de Azure](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Administrador de conexiones de suscripciones de Azure](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
-   Tareas

    -   [Tarea de descarga de blobs de Azure](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Tarea de carga de blobs de Azure](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Tarea de Azure Data Lake Analytics](control-flow/azure-data-lake-analytics-task.md)

    -   [Tarea Sistema de archivos de Azure Data Lake Store](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

    -   [Tarea de creación de clúster de HDInsight de Azure](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Tarea de eliminación de clúster de HDInsight de Azure](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Tarea de Hive de HDInsight de Azure](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Tarea de Pig de Azure HDInsight](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Tarea de carga de Azure SQL DW](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [Tarea de archivo flexible](../integration-services/control-flow/flexible-file-task.md)

-   Componentes de flujo de datos

    -   [Origen de blobs de Azure](../integration-services/data-flow/azure-blob-source.md)

    -   [Destino de blobs de Azure](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Origen de Azure Data Lake Store](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Destino de Azure Data Lake Store](../integration-services/data-flow/azure-data-lake-store-destination.md)

    -   [Origen de archivo flexible](../integration-services/data-flow/flexible-file-source.md)

    -   [Destino de archivo flexible](../integration-services/data-flow/flexible-file-destination.md)

-   Enumerador de archivos para Blob de Azure, Azure Data Lake Store y Data Lake Storage Gen2. Consultar [Contenedor de bucles Para cada uno](../integration-services/control-flow/foreach-loop-container.md)

## <a name="use-tls-12"></a>Uso de TLS 1.2

La versión de TLS que usa Azure Feature Pack sigue la configuración de .NET Framework del sistema.
Para usar TLS 1.2, agregue un valor `REG_DWORD` denominado `SchUseStrongCrypto` con datos `1` en las dos claves del Registro siguientes.

1. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319`

## <a name="dependency-on-java"></a>Dependencia en Java

Se necesita Java para usar determinadas características.
La arquitectura (32 o 64 bits) de la compilación de Java debe coincidir con la del runtime de SSIS que se va a usar.
Se han probado las siguientes compilaciones de Java.

- [OpenJDK 8u192 de Zulu](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Java SE Runtime Environment 8u192 de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>Configurar OpenJDK de Zulu

1. Descargue y extraiga el paquete ZIP de instalación.
2. Desde el símbolo del sistema, ejecute `sysdm.cpl`.
3. En la pestaña **Avanzadas**, haga clic en **Variables de entorno**.
4. En la sección **Variables del sistema**, haga clic en **Nueva**.
5. Escriba `JAVA_HOME` para el **Nombre de variable**.
6. Seleccione **Examinar directorio**, vaya a la carpeta extraída y seleccione la subcarpeta `jre`.
   Luego seleccione **Aceptar** y el campo **Valor de la variable** se rellena de forma automática.
7. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Nueva variable del sistema**.
8. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Variables de entorno**.
9. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades del sistema**.

### <a name="set-up-zulus-openjdk-on-azure-ssis-integration-runtime"></a>Configuración de OpenJDK de Zulú en Azure-SSIS Integration Runtime

Esto debe hacerse a través de la [interfaz de instalación personalizada](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup) para Azure-SSIS Integration Runtime.
Supongamos que se usa `zulu8.33.0.1-jdk8.0.192-win_x64.zip`.
El contenedor de blobs se puede organizar de la manera siguiente:

~~~
main.cmd
install_openjdk.ps1
zulu8.33.0.1-jdk8.0.192-win_x64.zip
~~~

Como punto de entrada, `main.cmd` desencadena la ejecución del script `install_openjdk.ps1` de PowerShell que, a su vez, extrae `zulu8.33.0.1-jdk8.0.192-win_x64.zip` y establece `JAVA_HOME` en consecuencia.

**main.cmd**

~~~
powershell.exe -file install_openjdk.ps1
~~~

**install_openjdk.ps1**

~~~
Expand-Archive zulu8.33.0.1-jdk8.0.192-win_x64.zip -DestinationPath C:\
[Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\zulu8.33.0.1-jdk8.0.192-win_x64\jre", "Machine")
~~~

### <a name="set-up-oracles-java-se-runtime-environment"></a>Configurar Java SE Runtime Environment de Oracle

1. Descargue y ejecute el instalador .exe.
2. Siga las instrucciones del programa de instalación para completar la instalación.

## <a name="scenario-processing-big-data"></a>Escenario: Procesamiento de macrodatos
 Use el Conector Azure para completar el trabajo de procesamiento de macrodatos siguiente:

1.  Utilice la tarea de carga de blobs de Azure para cargar datos de entrada en el almacenamiento de blobs de Azure.

2.  Utilice la tarea de creación de clúster de HDInsight de Azure para crear un clúster de HDInsight de Azure. Este paso es opcional si quiere utilizar su propio clúster.

3.  Utilice la tarea de Hive de HDInsight de Azure o la tarea de Pig de HDInsight de Azure para invocar un trabajo de Pig o Hive en el clúster de HDInsight de Azure.

4.  Utilice la tarea de eliminación de clúster de HDInsight de Azure para eliminar el clúster de HDInsight tras su uso si creó un clúster de HDInsight a petición en el paso 2.

5.  Utilice la tarea de descarga de blobs de HDInsight de Azure para descargar los datos de salida de Pig o Hive del almacenamiento de blobs de Azure.

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>Escenario: Administración de datos en la nube
 Use el destino de blobs de Azure en un paquete de SSIS para escribir los datos de salida en Almacenamiento de blobs de Azure o para utilizar el origen de blobs de Azure para leer datos desde un Almacenamiento de blobs de Azure.

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 Utilice el contenedor de bucles Foreach con el enumerador de blobs de Azure para procesar los datos de varios archivos de blob.

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)
  
