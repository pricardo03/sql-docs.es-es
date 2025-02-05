---
title: Implementación con un script de Python
titleSuffix: SQL Server big data clusters
description: Aprenda a usar un script de implementación para implementar clústeres de macrodatos de SQL Server 2019 (versión preliminar) en Azure Kubernetes Service (AKS).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: dee1c8669e6496553c367b4d1078d1e6a7f26497
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470721"
---
# <a name="use-a-python-script-to-deploy-a-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Uso de un script de Python para implementar un clúster de macrodatos de SQL Server en Azure Kubernetes Service (AKS)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este tutorial, usará un script de implementación de Python de muestra para implementar un clúster de macrodatos de SQL Server 2019 (versión preliminar) en Azure Kubernetes Service (AKS).

> [!TIP]
> AKS es solo una opción para hospedar Kubernetes para el clúster de macrodatos. Para obtener información sobre otras opciones de implementación, así como sobre cómo personalizar las opciones de implementación, consulte [Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md).

La implementación del clúster de macrodatos predeterminada que se usa aquí consta de una instancia maestra de SQL, una instancia de grupo de proceso, dos instancias de grupo de datos y dos instancias de grupo de almacenamiento. Los datos se conservan con volúmenes persistentes de Kubernetes que usan las clases de almacenamiento predeterminadas de AKS. La configuración predeterminada que se usa en este tutorial es adecuada para entornos de desarrollo y pruebas.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Prerequisites

- Suscripción a Azure.
- [Herramientas de macrodatos](deploy-big-data-tools.md):
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **CLI de Azure**

## <a name="log-in-to-your-azure-account"></a>Iniciar sesión en su cuenta

El script usa la CLI de Azure para automatizar la creación de un clúster de AKS. Antes de ejecutar el script, debe iniciar sesión en su cuenta de Azure con la CLI de Azure al menos una vez. Ejecute el siguiente comando desde el símbolo del sistema.

```
az login
```

## <a name="download-the-deployment-script"></a>Descargue el script de implementación

En este tutorial se automatiza la creación del clúster de macrodatos en AKS con un script de Python: **deploy-sql-big-data-aks.py**. Si ya ha instalado Python para **azdata**, debería poder ejecutar el script correctamente en este tutorial. 

En un símbolo del sistema de Windows PowerShell o Bash de Linux, ejecute el siguiente comando para descargar el script de implementación de GitHub.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>Ejecute el script de implementación

Siga estos pasos para ejecutar el script de implementación. Este script creará un servicio AKS en Azure y, a continuación, implementará un clúster de macrodatos de SQL Server 2019 en AKS. También puede modificar el script con otras [variables de entorno](deployment-guidance.md#configfile) para crear una implementación personalizada.

1. Ejecute el script con el siguiente comando:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > Si tiene python3 y python2 en el equipo cliente y en la ruta de acceso, tiene que ejecutar el comando con python3: `python3 deploy-sql-big-data-aks.py`.

1. Cuando se le solicite, escriba la siguiente información:

   | Valor | Descripción |
   |---|---|
   | **Id. de suscripción a Azure** | Identificador de suscripción de Azure que se usará para AKS. Puede enumerar todas las suscripciones y sus identificadores ejecutando `az account list` desde otra línea de comandos. |
   | **Grupo de recursos de Azure** | Nombre del grupo de recursos de Azure que se va a crear para el clúster de AKS. |
   | **Región de Azure** | La región de Azure del nuevo clúster de AKS (**westus** de forma predeterminada). |
   | **Tamaño de la máquina** | El [tamaño de la máquina](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) que se va a usar para los nodos del clúster de AKS (**Standard_L8s** de forma predeterminada). |
   | **Nodos de trabajo** | El número de nodos de trabajo en el clúster de AKS (valor predeterminado **1**). |
   | **Nombre del clúster** | El nombre del clúster de AKS y del clúster de macrodatos. El nombre del clúster de macrodatos debe estar formado solo por caracteres alfanuméricos en minúsculas y sin espacios (valor predeterminado**sqlbigdata**). |
   | **Contraseña** | Contraseña del controlador, puerta de enlace de HDFS/Spark e instancia maestra (valor predeterminado **MySQLBigData2019**). |
   | **Usuario del controlador** | Nombre de usuario del controlador (valor predeterminado: **admin**). |

Los siguientes parámetros eran necesarios para los participantes en el programa de usuarios pioneros del clúster de macrodatos de SQL Server 2019: **nombre de usuario de Docker** y **contraseña de Docker**. A partir de la versión CTP 3.2 ya no son necesarios.

   > [!IMPORTANT]
   > Es posible que el tamaño de máquina predeterminado **Standard_L8s** no esté disponible en todas las regiones de Azure. Si selecciona un tamaño de máquina diferente, asegúrese de que el número total de discos que se pueden conectar a través de los nodos del clúster es mayor o igual que 24. Cada notificación de volumen persistente en el clúster requiere un disco conectado. Actualmente, el clúster de macrodatos requiere 24 notificaciones de volumen persistentes. Por ejemplo, el tamaño de la máquina [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series) admite 32 discos conectados, por lo que puede evaluar los clústeres de macrodatos con un solo nodo de este tamaño de máquina.

   > [!NOTE]
   > La cuenta `sa` es un administrador del sistema en la instancia maestra de SQL Server que se crea durante la instalación. Después de crear la implementación, la variable de entorno `MSSQL_SA_PASSWORD` es reconocible al ejecutar `echo $MSSQL_SA_PASSWORD` en el contenedor de la instancia maestra. Por motivos de seguridad, cambie la contraseña `sa` en la instancia maestra después de la implementación. Para obtener más información, consulte [Cambio de la contraseña de administrador del sistema](../linux/quickstart-install-connect-docker.md#sapassword).

1. El script se iniciará mediante la creación de un clúster de AKS con los parámetros especificados. Este paso tarda varios minutos.

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>Supervisar el estado

Después de que el script cree el clúster de AKS, continúa para establecer las variables de entorno necesarias con la configuración que ha especificado anteriormente. A continuación, llame a **azdata** para implementar el clúster de macrodatos en AKS.

La ventana de comandos de cliente generará el estado de implementación. Durante el proceso de implementación, debería ver una serie de mensajes en los que está esperando el pod del controlador:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Después de 10 o 20 minutos, se le notificará que el pod del controlador se está ejecutando:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> La implementación completa puede tardar mucho tiempo debido al tiempo necesario para descargar las imágenes de contenedor de los componentes del clúster de macrodatos. Pero no debería tardar muchas horas. Si tiene problemas con la implementación, consulte [Supervisión y solución de problemas de clústeres de macrodatos de SQL Server](cluster-troubleshooting-commands.md).

## <a name="inspect-the-cluster"></a>Inspeccionar el clúster

En cualquier momento durante la implementación, puede usar **kubectl** o **azdata** para inspeccionar el estado y los detalles sobre el clúster de macrodatos en ejecución.

### <a name="use-kubectl"></a>Usar kubectl

Abra una nueva ventana de comandos para usar **kubectl** durante el proceso de implementación.

1. Ejecute el siguiente comando para obtener un resumen del estado de todo el clúster:

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Si no ha cambiado el nombre del clúster de macrodatos, el valor predeterminado del script es **sqlbigdata**.

1. Inspeccione los servicios de Kubernetes y sus puntos de conexión internos y externos con el siguiente comando de **kubectl**:

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. También puede inspeccionar el estado de los pods de Kubernetes con el siguiente comando:

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. Obtenga más información sobre un pod específico con el siguiente comando:

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> Para más información sobre cómo supervisar y solucionar problemas de una implementación, consulte [Supervisión y solución de problemas de clústeres de macrodatos de SQL Server](cluster-troubleshooting-commands.md).

## <a name="connect-to-the-cluster"></a>Conexión al clúster

Cuando finalice el script de implementación, la salida le notificará que se ha realizado correctamente:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

El clúster de macrodatos de SQL Server ahora está implementado en AKS. Ahora puede usar Azure Data Studio para conectarse al clúster. Para más información, consulte [Conexión a un clúster de macrodatos de SQL Server con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="clean-up"></a>Limpieza

Si está probando los clústeres de macrodatos de SQL Server en Azure, debe eliminar el clúster de AKS cuando termine para evitar cargos inesperados. No quite el clúster si desea seguir utilizándolo.

> [!WARNING]
> En los pasos siguientes se anula el clúster de AKS, que también quita el clúster de macrodatos de SQL Server. Si tiene bases de datos o datos de HDFS que desea conservar, haga una copia de seguridad de los datos antes de eliminar el clúster.

Ejecute el siguiente comando de la CLI de Azure para quitar el clúster de macrodatos y el servicio AKS en Azure (reemplace `<resource group name>` por el **grupo de recursos de Azure** que ha especificado en el script de implementación):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>Pasos siguientes

El script de implementación ha configurado Azure Kubernetes Service y también ha implementado un clúster de macrodatos de SQL Server 2019. También puede optar por personalizar las implementaciones futuras a través de instalaciones manuales. Para obtener más información sobre cómo se implementan los clústeres de macrodatos, así como sobre cómo personalizar las implementaciones, consulte [Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md).

Ahora que el clúster de macrodatos de SQL Server está implementado, puede cargar los datos de ejemplo y explorar los tutoriales:

> [!div class="nextstepaction"]
> [Tutorial: Cargar datos de ejemplo en un clúster de macrodatos de SQL Server 2019](tutorial-load-sample-data.md)