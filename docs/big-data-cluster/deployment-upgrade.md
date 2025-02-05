---
title: Actualización a una nueva versión
titleSuffix: SQL Server big data clusters
description: Aprenda a actualizar clústeres de macrodatos de SQL Server 2019 (versión preliminar) a una nueva versión.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 29bdd3996112154b222ffb7d43390050c9af2d02
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731089"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>Cómo actualizar clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se proporcionan instrucciones para actualizar un clúster de macrodatos de SQL Server a una nueva versión. Los pasos de este artículo se aplican específicamente a la actualización entre versiones preliminares.

## <a name="backup-and-delete-the-old-cluster"></a>Copia de seguridad del clúster anterior y eliminación

Actualmente, la única manera de actualizar un clúster de macrodatos a una nueva versión es quitarlo manualmente y volver a crearlo. Cada versión tiene una versión única de **azdata** que no es compatible con la versión anterior. Además, si un clúster anterior tuviera que descargar una imagen en un nodo nuevo, es posible que la imagen más reciente no fuera compatible con las imágenes anteriores del clúster. Para actualizar a la versión más reciente, siga estos pasos:

1. Antes de eliminar el clúster anterior, realice una copia de seguridad de los datos en la instancia maestra de SQL Server y en HDFS. En la instancia maestra de SQL Server, puede usar [Copia de seguridad y restauración de SQL Server](data-ingestion-restore-database.md). En HDFS, [puede copiar los datos con **curl**](data-ingestion-curl.md).

1. Elimine el clúster anterior con el comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use la versión de **azdata** que coincida con el clúster. No elimine un clúster anterior con la versión más reciente de **azdata**.

1. Antes de CTP 3.2, el nombre de **azdata** era **mssqlctl**. Si tiene instaladas versiones anteriores de **mssqlctl** o **azdata**, es importante desinstalar antes de instalar la versión más reciente de **azdata**.

   En CTP 2.3 o superior, ejecute el siguiente comando. Reemplace `ctp3.1` en el comando por la versión de **mssqlctl** que está desinstalando. Si la versión es anterior a CTP 3.1, agregue un guión antes del número de versión (por ejemplo, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Instale la última versión de **azdata**. Los siguientes comandos instalan **azdata** para CTP 3.2:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > La ruta de acceso a **azdata** cambia en cada versión. Aunque haya instalado anteriormente **azdata** o **mssqlctl**, debe volver a instalar desde la ruta de acceso más reciente antes de crear el nuevo clúster.

## <a id="azdataversion"></a> Comprobar la versión de azdata

Antes de implementar un nuevo clúster de macrodatos, compruebe que está usando la versión más reciente de **azdata** con el parámetro `--version`:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Instalar la nueva versión

Después de quitar el clúster de macrodatos anterior e instalar la versión de **azdata** más reciente, implemente el nuevo clúster de macrodatos con las instrucciones de implementación actuales. Para obtener más información, vea [Cómo implementar clústeres de macrodatos SQL Server en Kubernetes](deployment-guidance.md). Luego, restaure las bases de datos o los archivos necesarios.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos, vea [¿Qué son los clústeres de macrodatos de SQL Server?](big-data-cluster-overview.md)
