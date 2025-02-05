---
title: 'SQL Server Management Studio: datos de uso y diagnóstico (SSMS) | Microsoft Docs'
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c79a2c3da9ee7f877c3d13bf17ca7912117df883
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264698"
---
# <a name="local-audit-for-ssms-usage-and-diagnostic-data-collection"></a>Auditoría local para la recopilación de datos de uso y diagnóstico de SSMS
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server Management Studio (SSMS) contiene características habilitadas para Internet que pueden recopilar y enviar datos anónimos sobre el uso de características a Microsoft. SSMS puede recopilar información estándar del equipo e información sobre el uso y el rendimiento que se podría transmitir a Microsoft y analizarse a fin de mejorar la calidad, la seguridad y la confiabilidad de SSMS. No recopilamos su nombre, dirección ni otra información de contacto. Para más información, consulte [Declaración de privacidad de Microsoft](https://privacy.microsoft.com/privacystatement) y [Complemento de privacidad de SQL Server](https://go.microsoft.com/fwlink/?LinkID=868444).

## <a name="audit-feature-usage-and-diagnostic-data"></a>Auditoría de datos de diagnóstico y uso de características

Para ver los datos de uso de características recopilados mediante SSMS, realice los pasos siguientes:

1.  Inicie SSMS.
2.  Haga clic en **Ver** y en **Salida** en el menú principal para mostrar la ventana **Salida**. 
3.  Cuando aparezca la ventana **Salida**, seleccione **Telemetría** en el menú **Mostrar salida de:** .

Mientras use SSMS para interactuar con las bases de datos, la ventana **Salida** mostrará los datos que se recopilen.

## <a name="enable-or-disable-usage-and-diagnostic-data-collection-in-ssms"></a>Habilitación o deshabilitación de colecciones de datos de uso y diagnóstico en SSMS

Para optar por recibir o no recibir la recopilación de datos de uso de SSMS:

- Para SQL Server Management Studio 17:

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\14.0`

  Nombre de RegEntry = `UserFeedbackOptIn`

  Tipo de entrada `DWORD`: `0` es dejar optar por no recibir; `1` es optar por recibir

  Además, SSMS 17.x se basa en el shell de Visual Studio 2015 y la instalación de Visual Studio admite los comentarios de los clientes de forma predeterminada.  

  Para configurar Visual Studio para deshabilitar los comentarios de los clientes en equipos específicos, cambie el valor de la siguiente subclave del Registro por la cadena `0`: `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn`

  Por ejemplo, modifique la subclave así:  
  `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn `=` 0`

  La recopilación de datos de uso y diagnóstico de SQL Server 2017 respeta la directiva de grupo basada en el Registro sobre estas subclaves del Registro.

- Para SQL Server Management Studio 18:

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\18.0_IsoShell`

  Nombre de RegEntry = `UserFeedbackOptIn`

  Tipo de entrada `DWORD`: `0` es dejar optar por no recibir; `1` es optar por recibir

## <a name="see-also"></a>Vea también

- [Configuración de la recopilación de datos de uso y diagnóstico para SQL Server](../sql-server/usage-and-diagnostic-data-configuration-for-sql-server.md)
- [Auditoría local para la recopilación de datos de uso y diagnóstico de SQL Server](http://msdn.microsoft.com/library/mt743085.aspx)