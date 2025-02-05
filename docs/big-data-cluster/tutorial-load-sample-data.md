---
title: Carga de datos de muestra
titleSuffix: SQL Server big data clusters
description: En este tutorial se muestra cómo cargar datos de ejemplo en un clúster de macrodatos de SQL Server. En los datos de ejemplo se incluyen datos relacionales en la instancia maestra de SQL Server. También se incluyen datos de HDFS en el bloque de almacenamiento. Estos datos son compatibles con otros tutoriales de esta sección.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b35eccece4df47cb483932386cf6a38e45d2dc8
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419280"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>Tutorial: Carga de datos de ejemplo en un clúster de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este tutorial se explica cómo usar un script para cargar datos de ejemplo en un clúster de macrodatos de SQL Server 2019 (versión preliminar). Muchos de los otros tutoriales de la documentación usan estos datos de ejemplo.

> [!TIP]
> Puede encontrar más ejemplos para el clúster de macrodatos de SQL Server 2019 (versión preliminar) en el repositorio de GitHub [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster). Se encuentran en la ruta de acceso **sql-server-samples/samples/features/sql-big-data-cluster/** .

## <a name="prerequisites"></a>Prerequisites

- [Un clúster de macrodatos implementado](deployment-guidance.md)
- [Herramientas de macrodatos](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a> Carga de los datos de ejemplo

En los pasos siguientes se usa un script de arranque para descargar una copia de seguridad de base de datos de SQL Server y cargar los datos en el clúster de macrodatos. Para facilitar su uso, estos pasos se han dividido en las secciones de [Windows](#windows) y [Linux](#linux).

## <a id="windows"></a> Windows

En los pasos siguientes se describe cómo usar un cliente Windows para cargar los datos de ejemplo en el clúster de macrodatos.

1. Abra un nuevo símbolo del sistema de Windows.

   > [!IMPORTANT]
   > No use Windows PowerShell para realizar estos pasos. En PowerShell, el script producirá un error, ya que usará la versión de PowerShell de **curl**.

1. Use **curl** para descargar el script de arranque de los datos de ejemplo.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Descargue el script de Transact-SQL **bootstrap-sample-db.sql**. El script de arranque llama a este script.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. El script de arranque requiere los siguientes parámetros posicionales para el clúster de macrodatos:

   | Parámetro | Descripción |
   |---|---|
   | <CLUSTER_NAMESPACE> | Nombre que ha asignado al clúster de macrodatos. |
   | <SQL_MASTER_IP> | Dirección IP de la instancia maestra. |
   | <SQL_MASTER_SA_PASSWORD> | Contraseña de administrador del sistema de la instancia maestra. |
   | <KNOX_IP> | Dirección IP de la puerta de enlace de HDFS/Spark. |
   | <KNOX_PASSWORD> | Contraseña de la puerta de enlace de HDFS/Spark. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para buscar las direcciones IP de la instancia maestra de SQL Server y Knox. Ejecute `kubectl get svc -n <your-big-data-cluster-name>` y busque la instancia maestra (**master-svc-external**) y Knox (**gateway-svc-external**) en las direcciones de EXTERNAL-IP. El nombre predeterminado de un clúster es **mssql-cluster**.

1. Ejecute el script de arranque.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

En los pasos siguientes se describe cómo usar un cliente Linux para cargar los datos de ejemplo en el clúster de macrodatos.

1. Descargue el script de arranque y asígnele permisos de ejecutable.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Descargue el script de Transact-SQL **bootstrap-sample-db.sql**. El script de arranque llama a este script.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. El script de arranque requiere los siguientes parámetros posicionales para el clúster de macrodatos:

   | Parámetro | Descripción |
   |---|---|
   | <CLUSTER_NAMESPACE> | Nombre que ha asignado al clúster de macrodatos. |
   | <SQL_MASTER_IP> | Dirección IP de la instancia maestra. |
   | <SQL_MASTER_SA_PASSWORD> | Contraseña de administrador del sistema de la instancia maestra. |
   | <KNOX_IP> | Dirección IP de la puerta de enlace de HDFS/Spark. |
   | <KNOX_PASSWORD> | Contraseña de la puerta de enlace de HDFS/Spark. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) para buscar las direcciones IP de la instancia maestra de SQL Server y Knox. Ejecute `kubectl get svc -n <your-big-data-cluster-name>` y busque la instancia maestra (**master-svc-external**) y Knox (**gateway-svc-external**) en las direcciones de EXTERNAL-IP. El nombre predeterminado de un clúster es **mssql-cluster**.

1. Ejecute el script de arranque.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>Pasos siguientes

Una vez que se ejecute el script de arranque, el clúster de macrodatos tiene las bases de datos de ejemplo y los datos de HDFS. En los siguientes tutoriales se usan los datos de ejemplo para mostrar las capacidades de los clústeres de macrodatos:

Virtualización de datos:

- [Tutorial: Consulta de HDFS en un clúster de macrodatos de SQL Server](tutorial-query-hdfs-storage-pool.md)
- [Tutorial: Consulta de Oracle desde un clúster de macrodatos de SQL Server](tutorial-query-oracle.md)

Ingesta de datos:

- [Tutorial: ingerir datos en un grupo de datos de SQL Server con Transact-SQL](tutorial-data-pool-ingest-sql.md)
- [Tutorial: Introducir datos en un grupo de datos de SQL Server con trabajos de Spark](tutorial-data-pool-ingest-spark.md)

Cuadernos:

- [Tutorial: Ejecutar un cuaderno de ejemplo en un clúster de macrodatos de SQL Server 2019](tutorial-notebook-spark.md)