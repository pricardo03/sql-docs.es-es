---
title: Configurar o cambiar la intercalación del servidor | Microsoft Docs
ms.custom: ''
ms.date: 01/22/2019
ms.prod: sql
ms.reviewer: carlrab
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 81a776a0bece59f98042fec6cbf7b191ec82be1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140836"
---
# <a name="set-or-change-the-server-collation"></a>Configurar o cambiar la intercalación del servidor

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  La intercalación de servidor actúa como intercalación predeterminada para todas las bases de datos del sistema que se han instalado con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como las bases de datos de usuario recién creadas. Debe elegir cuidadosamente la intercalación de nivel de servidor porque afecta a:
 - Las reglas de ordenación y comparación en `=`, `JOIN`, `ORDER BY` y otros operadores que comparan datos textuales.
 - La intercalación de las columnas `CHAR`, `VARCHAR`, `NCHAR` y `NVARCHAR` en vistas del sistema, funciones del sistema y los objetos en TempDB (por ejemplo, las tablas temporales).
 - Los nombres de variables, cursores y etiquetas `GOTO`. Las variables @pi y @PI se consideran diferentes si la intercalación de nivel de servidor distingue entre mayúsculas y minúsculas, y se consideran iguales si la intercalación de nivel de servidor no distingue entre mayúsculas y minúsculas.
  
## <a name="setting-the-server-collation-in-sql-server"></a>Configuración de la intercalación del servidor en SQL Server

  La intercalación de servidor se especifica durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La intercalación de nivel de servidor predeterminada es **SQL_Latin1_General_CP1_CI_AS**. No se pueden especificar intercalaciones exclusivas de Unicode como intercalación de nivel de servidor. Para más información, consulte [Compatibilidad con la intercalación y Unicode](collation-and-unicode-support.md).
  
## <a name="changing-the-server-collation-in-sql-server"></a>Cambio de la intercalación del servidor en SQL Server

 El cambio de la intercalación predeterminada para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ser una operación compleja que incluye los siguientes pasos:  
  
- Asegurarse de que se dispone de toda la información o scripts necesarios para volver a crear las bases de datos de usuario y todos los objetos contenidos en ellas.  
  
- Exportar todos los datos mediante una herramienta como [bcp Utility](../../tools/bcp-utility.md). Para obtener más información, vea [Importar y exportar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
- Quitar todas las bases de datos de usuario.  
  
- Vuelva a generar la base de datos maestra al especificar la nueva intercalación en la propiedad SQLCOLLATION del comando **setup** . Por ejemplo:  
  
    ```sql  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]
    /SQLCOLLATION=CollationName  
    ```  
  
     Para obtener más información, vea [Volver a generar bases de datos del sistema](../../relational-databases/databases/rebuild-system-databases.md).  
  
- Crear todas las bases de datos y todos los objetos contenidos en ellas.  
  
- Importar todos los datos.  
  
> [!NOTE]  
> En lugar de cambiar la intercalación predeterminada de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede especificar una intercalación predeterminada para cada nueva base de datos que cree.  
  
## <a name="setting-the-server-collation-in-managed-instance"></a>Configuración de la intercalación del servidor en Instancia administrada

La intercalación de nivel de servidor en Instancia administrada de Azure SQL se puede especificar al crear la instancia y no se puede cambiar posteriormente. Puede establecer la intercalación de nivel de servidor a través de [Azure Portal](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started#create-a-managed-instance) o [PowerShell y la plantilla de Resource Manager](https://docs.microsoft.com/azure/sql-database/scripts/sql-managed-instance-create-powershell-azure-resource-manager-template) mientras crea la instancia. La intercalación de nivel de servidor predeterminada es **SQL_Latin1_General_CP1_CI_AS**. No se pueden especificar intercalaciones UTF-8 ni exclusivas de Unicode la intercalación como nivel de servidor.
Si va a migrar bases de datos de SQL Server a Instancia administrada, compruebe la intercalación del servidor en la instancia de SQL Server de origen mediante la función `SERVERPROPERTY(N'Collation')` y cree una Instancia administrada que coincida con la intercalación de SQL Server. Es posible que la migración de una base de datos de SQL Server a Instancia administrada con intercalaciones de nivel de servidor que no coinciden produzca varios errores inesperados en las consultas. No se puede cambiar la intercalación de nivel de servidor en la Instancia administrada existente.

## <a name="see-also"></a>Consulte también

 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)   
 [Establecer o cambiar la intercalación de base de datos](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [Establecer o cambiar la intercalación de columnas](../../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Volver a generar bases de datos del sistema](../../relational-databases/databases/rebuild-system-databases.md)  
 
