---
title: MSSQLSERVER_2515 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2515 (Database Engine error)
ms.assetid: af93aa29-70c9-4923-90af-aafadb20c1c6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e531a2d916cfc464c18aab931c268197fbf5982
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915032"
---
# <a name="mssqlserver2515"></a>MSSQLSERVER_2515
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2515|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_DIFF_MAP_OUT_OF_SYNC|  
|Texto del mensaje|Página P_ID, Id. de objeto O_ID, Id. de índice I_ID, Id. de partición PN_ID, Id. de unidad de asignación A_ID (tipo TYPE): se ha modificado, pero no está marcada como modificada en el mapa de bits de la copia de seguridad diferencial.|  
  
## <a name="explanation"></a>Explicación  
 La página especificada tiene un número de secuencia de registro (LSN) mayor que el LSN de referencia diferencial del BackupManager de la base de datos o el LSN de base diferencial del bloque de control de archivos del archivo, el que sea más reciente. Sin embargo, la página no está marcada como modificada en el mapa de bits de la copia de seguridad diferencial.  
  
 Solo se incluirá una página por base de datos en el informe, ya que esta comprobación se realiza únicamente cuando se sabe que el mapa de bits diferencial está libre de errores.  
  
## <a name="user-action"></a>Acción del usuario  
  
### <a name="look-for-hardware-failure"></a>Busque un error de hardware  
 Ejecute un diagnóstico de hardware y corrija cualquier problema. Examine también los registros del sistema y de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows así como el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ver si el error se produjo como resultado de un error de hardware. Arregle cualquier problema relacionado con el hardware que encuentre en estos registros.  
  
 Si sigue teniendo problemas de datos dañados, intente intercambiar diferentes componentes de hardware para aislar el problema. Asegúrese de que el sistema no tiene habilitada la memoria caché de escritura en el controlador de disco. Si cree que el problema se debe a la caché de escritura, póngase en contacto con su proveedor de hardware.  
  
 Finalmente, puede resultarle útil cambiar a un nuevo sistema de hardware. Este cambio puede incluir volver a formatear las unidades de disco y volver a instalar el sistema operativo.  
  
### <a name="restore-from-backup"></a>Restaure mediante la copia de seguridad  
 Si el problema no está relacionado con el hardware y tiene una copia de seguridad limpia disponible, úsela para restaurar la base de datos.  
  
### <a name="run-dbcc-checkdb"></a>Ejecute DBCC CHECKDB  
 Si no tiene disponible una copia de seguridad limpia, ejecute DBCC CHECKDB sin una cláusula REPAIR para determinar el alcance de los daños. DBCC CHECKDB recomendará el uso de una cláusula REPAIR. A continuación, ejecute DBCC CHECKDB con la cláusula REPAIR apropiada para reparar el problema.  
  
> [!CAUTION]  
>  Si no está seguro del efecto que tendrá DBCC CHECKDB con una cláusula REPAIR en los datos, póngase en contacto con su proveedor principal de soporte antes de ejecutar esta instrucción.  
  
 Si ejecuta DBCC CHECKDB con una de las cláusulas REPAIR y no se soluciona el problema, póngase en contacto con su proveedor principal de soporte.  
  
### <a name="results-of-running-repair-options"></a>Resultados de ejecutar opciones REPAIR  
 La ejecución de REPAIR invalidará el mapa de bits diferencial. No se puede realizar una copia de seguridad diferencial hasta que se lleve a cabo una copia de seguridad completa de la base de datos. La copia de seguridad completa de la base de datos proporciona una línea base para la regeneración del mapa de bits diferencial.  
  
## <a name="see-also"></a>Vea también  
 [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)   
 [MSSQLSERVER_2516](mssqlserver-2516-database-engine-error.md)  
  
  
