---
title: Implementación sin conexión
titleSuffix: SQL Server big data clusters
description: Aprenda a realizar una implementación sin conexión de un clúster de macrodatos de SQL Server.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd8b3128fc11037a5ade494813611d473c995f8f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419369"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Realización de una implementación sin conexión de un clúster de macrodatos de SQL Server

En este artículo se explica cómo realizar una implementación sin conexión de un clúster de macrodatos de SQL Server 2019 (versión preliminar). Los clústeres de macrodatos deben tener acceso a un repositorio de Docker desde el que extraer imágenes de contenedor. Una instalación sin conexión es aquella en la que las imágenes necesarias se encuentran en un repositorio privado de Docker. Ese repositorio privado se usa como origen de imágenes de una nueva implementación.

## <a name="prerequisites"></a>Prerequisites

- Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Cargar imágenes en un repositorio privado

En los pasos siguientes se explica cómo extraer las imágenes de contenedor de clúster de macrodatos del repositorio de Microsoft y luego insertarlas en el repositorio privado.

> [!TIP]
> En los pasos siguientes se explica el proceso. Pero para simplificar la tarea, puede usar el [script automatizado](#automated) en lugar de ejecutar estos comandos manualmente.

1. Extraiga las imágenes de contenedor de clúster de macrodatos mediante la repetición del siguiente comando. Reemplace `<SOURCE_IMAGE_NAME>` por cada [nombre de imagen](#images). Reemplace `<SOURCE_DOCKER_TAG>` por la etiqueta de la versión del clúster de macrodatos, como **2019-CTP3.2-ubuntu**.  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Inicie sesión en el registro de Docker privado de destino.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. Etiquete las imágenes locales con el siguiente comando para cada imagen:

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Inserte las imágenes locales en el repositorio privado de Docker:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> Imágenes de contenedor de clúster de macrodatos

Las siguientes imágenes de contenedor de clúster de macrodatos son necesarias para una instalación sin conexión:

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**
 - **mssql-mleap-serving-runtime**
 - **mssql-security-support**

## <a id="automated"></a> Script automatizado

Puede usar un script de Python automatizado que extraiga automáticamente todas las imágenes de contenedor necesarias y las inserte en un repositorio privado.

> [!NOTE]
> Python es un requisito previo para usar el script. Para obtener más información sobre cómo instalar Python, vea la [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. En Bash o PowerShell, descargue el script con **curl**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. Luego ejecute el script con uno de los siguientes comandos:

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux:**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. Siga los mensajes para especificar la información del repositorio de Microsoft y el repositorio privado. Una vez completado el script, todas las imágenes necesarias deben encontrarse en el repositorio privado.

## <a name="install-tools-offline"></a>Instalación de herramientas sin conexión

Las implementaciones de clústeres de macrodatos requieren varias herramientas, como **Python**, **azdata** y **kubectl**. Siga estos pasos para instalar estas herramientas en un servidor sin conexión.

### <a id="python"></a> Instalación de Python sin conexión

1. En un equipo con acceso a Internet, descargue uno de los siguientes archivos comprimidos que contienen Python:

   | Sistema operativo | Descargar |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie el archivo comprimido en el equipo de destino y extráigalo en una carpeta de su elección.

1. Solo para Windows, ejecute `installLocalPythonPackages.bat` desde esa carpeta y pase la ruta de acceso completa a la misma carpeta como un parámetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="azdata"></a> Instalación de azdata sin conexión

1. En un equipo con acceso a Internet y [Python](https://wiki.python.org/moin/BeginnersGuide/Download), ejecute el siguiente comando para descargar todos los paquetes de **azdata** en la carpeta actual.

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. Copie los paquetes descargados y el archivo **requirements.txt** en el equipo de destino.

1. Ejecute el siguiente comando en el equipo de destino y especifique la carpeta en la que ha copiado los archivos anteriores.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> Instalación de kubectl sin conexión

Para instalar **kubectl** en un equipo sin conexión, siga estos pasos.

1. Use **curl** para descargar **kubectl** en la carpeta que prefiera. Para obtener más información, vea [Instalación del binario de kubectl mediante curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl).

1. Copie la carpeta en el equipo de destino.

## <a name="deploy-from-private-repository"></a>Implementación desde un repositorio privado

Para implementar desde el repositorio privado, siga los pasos de la [guía de implementación](deployment-guidance.md), pero use un archivo de configuración de implementación personalizado que especifique la información del repositorio privado de Docker. Los siguientes comandos de **azdata** muestran cómo cambiar la configuración de Docker de un archivo de configuración de implementación personalizado denominado **control.json**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

La implementación pide el nombre de usuario y la contraseña de Docker, o bien puede especificarlos en las variables de entorno **DOCKER_USERNAME** y **DOCKER_PASSWORD**.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre las implementaciones de clústeres de macrodatos, vea [Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md).
