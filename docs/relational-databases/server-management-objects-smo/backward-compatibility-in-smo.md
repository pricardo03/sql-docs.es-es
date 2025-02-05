---
title: Compatibilidad con versiones anteriores en SMO | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 2f986436-aaf2-4eaf-9809-df849d97d4fb
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7a002b4f5d4b678171fc5dd396152d155779f78b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126771"
---
# <a name="backward-compatibility-in-smo"></a>Compatibilidad con versiones anteriores en SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Las aplicaciones de SMO que se escribieron utilizando versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden volver a compilar utilizando SMO en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="migrating-smo-applications"></a>Migrar aplicaciones de SMO  
 Se deben quitar las referencias a archivos dll de SMO en las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se deben incluir las referencias a los nuevos archivos dll de SMO proporcionados con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 Como mínimo, debe hacer referencia a lo siguiente:  
  
-   Microsoft.SqlServer.ConnectionInfo  
  
-   Microsoft.SqlServer.Smo  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc  
  
 Estos archivos son necesarios para las clases de conexión, las clases de utilidad SMO y las clases de fundación.  
  
> [!NOTE]  
>  Se ha eliminado SmoEnum.dll por lo que deben eliminarse las referencias a esta dll del proyecto [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de SMO.  
  
 Los espacios de nombres también han cambiado; puede usar los siguientes:  
  
##### <a name="for-visual-c"></a>Para Visual C#  
  
```  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
```  
  
##### <a name="for-visual-basic"></a>Para Visual Basic  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
```  
  
 Si el código usa la funcionalidad Urn como **Server.GetSqlSmoObject(Urn)** , debe efectuar un vínculo al espacio de nombres Microsoft.SqlServer.Management.Sdk.Sfc.  
  
 Si el código usa el objeto Transfer directamente, tendrá que efectuar un vínculo al espacio de nombres Microsoft.SqlServer.Management.SmoExtended.  
  
 Al migrar código, es posible que tenga que modificarlo. Esto ocurre porque varias características de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] se han quedado en desuso en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información acerca de las características en desuso, consulte [en desuso las características de motor de base de datos en SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md) en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] libros en pantalla.  
  
  
