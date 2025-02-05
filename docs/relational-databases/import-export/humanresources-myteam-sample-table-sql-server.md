---
title: Tabla de ejemplo HumanResources.myTeam (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- myTeam sample table [SQL Server]
- bulk importing [SQL Server], examples
- bulk exporting [SQL Server], examples
ms.assetid: 27da45a0-c1f4-4bf4-ab24-6196e80d3834
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a95168f9c932b187a77d0d8e97511fd0070ea8ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035684"
---
# <a name="humanresourcesmyteam-sample-table-sql-server"></a>Tabla de ejemplo HumanResources.myTeam (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Muchos de los ejemplos de código de [Importar y exportar datos masivos](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) requieren una tabla de prueba especial llamada **myTeam**. Antes de poder ejecutar los ejemplos, debe crear la tabla **myTeam** en el esquema **HumanResources** de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] es una de las bases de datos de ejemplo de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 La tabla **myTeam** contiene las columnas siguientes.  
  
|columna|Tipo de datos|Nulabilidad|Descripción|  
|------------|---------------|-----------------|-----------------|  
|**EmployeeID**|**smallint**|No NULL|Clave principal para las filas. Identificador de empleado de un miembro de mi equipo.|  
|**Nombre**|**nvarchar(50)**|No NULL|Nombre de un miembro de mi equipo.|  
|**Title**|**nvarchar(50)**|Admisión de valores NULL|Cargo que tiene el empleado en mi equipo.|  
|**Información previa**|**nvarchar(50)**|No NULL|Fecha y hora de la última actualización de la fila. (Es el valor predeterminado).|  
  
**Para crear HumanResources.myTeam**  
  
-   Utilice las siguientes instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```sql
    --Create HumanResources.MyTeam:   
    USE AdventureWorks;  
    GO  
    CREATE TABLE HumanResources.myTeam   
    (EmployeeID smallint NOT NULL,  
    Name nvarchar(50) NOT NULL,  
    Title nvarchar(50) NULL,  
    Background nvarchar(50) NOT NULL DEFAULT ''  
    );  
    GO  
    ```  
  
**Para rellenar HumanResources.myTeam**  
  
-   Ejecute las siguientes instrucciones `INSERT` para rellenar la tabla con dos filas:  
  
    ```sql
    USE AdventureWorks;  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(77,'Mia Doppleganger','Administrative Assistant','Microsoft Office');  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(49,'Hirum Mollicat','I.T. Specialist','Report Writing and Data Mining');  
    GO  
    ```  
  
    > [!NOTE]  
    >  Estas instrucciones omiten la cuarta columna, `Background`. Tiene un valor predeterminado. Omitir esta columna hace que esta instrucción `INSERT` deje la columna en blanco.  
  
## <a name="see-also"></a>Consulte también  
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
