---
title: Configurar registros de errores de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a4da039e1fcc41570fcead275bbe4b2cb0be5797
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731099"
---
# <a name="scm-services---configure-sql-server-error-logs"></a>Servicios SCM - Configurar registros de errores de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo ver o modificar la forma en que se reciclan los registros de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>Para abrir el cuadro de diálogo Configurar registros de errores de SQL Server  

1. En el Explorador de objetos, expanda la instancia de SQL Server, expanda **Administración**, haga clic con el botón derecho en **Registros de SQL Server**y después haga clic en **Configurar**.

2. En el cuadro de diálogo **Configurar registros de errores de SQL Server** , elija una de las siguientes opciones.

    A. Número de archivos de registro

      **Limitar el número de archivos de registro de error antes de reciclarlos**

      Actívela para limitar el número de registros de error que se deben crear antes de que se reciclen. Se crea un nuevo registro de errores cada vez que se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva copias de seguridad de los seis registros anteriores, a menos que se active esta opción y se especifique un número máximo de archivos de registro de errores diferente a continuación.  
  
      **Número máximo de archivos de registro de errores**

      Especifica el número máximo de archivos de registro de errores que se pueden crear antes de reciclarse. El valor predeterminado es 6, que es el número de registros de copia de seguridad anteriores que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva antes de reciclarlos.

    B. Tamaño de archivo de registro

      **Tamaño máximo del archivo de registro de errores en KB**

      Puede establecer la cantidad de tamaño de cada archivo en KB. Si lo deja en 0, el tamaño del registro es ilimitado.
