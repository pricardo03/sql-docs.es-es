---
title: Entradas del registro de orígenes de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b9d101395a3276f92f3ccf49e36effc65420f7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093877"
---
# <a name="registry-entries-for-data-sources"></a>Entradas del registro para los orígenes de datos
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 El archivo DLL de instalador mantiene información en el registro de cada origen de datos. En Microsoft Windows NT o Windows 2000 y Microsoft Windows 95/98, esta información se almacena en las subclaves de una de las dos claves del registro siguientes:  
  
 HKEY_LOCAL_MACHINE  
  
 SOFTWARE  
  
 ODBC  
  
 ODBC.ini  
  
 HKEY_CURRENT_USER  
  
 SOFTWARE  
  
 ODBC  
  
 ODBC.ini  
  
 Clave que se usa depende de si el origen de datos es un *origen de datos del sistema,* que está disponible para todos los usuarios, o un *origen de datos de usuario,* que solo está disponible para el usuario actual. Orígenes de datos del sistema se almacenan en el árbol HKEY_LOCAL_MACHINE y orígenes de datos de usuario se almacenan en el árbol de HKEY_CURRENT_USER. En todos los demás aspectos, los orígenes de datos del sistema y los orígenes de datos de usuario son idénticos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Subclave de orígenes de datos de ODBC](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [Subclaves de la especificación del origen de datos](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [Subclave predeterminada](../../../odbc/reference/install/default-subkey.md)  
  
-   [Subclave ODBC](../../../odbc/reference/install/odbc-subkey.md)
