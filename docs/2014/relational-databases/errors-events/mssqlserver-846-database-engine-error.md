---
title: MSSQLSERVER_846 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 846 (Database Engine error)
ms.assetid: ccf367eb-06b0-42b8-b4d6-2b88f4a502d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 840898cb41274a1871e5d087e2be1d2ab9e39e23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913192"
---
# <a name="mssqlserver846"></a>MSSQLSERVER_846
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|846|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|N/D|  
|Texto del mensaje|Tiempo de espera agotado mientras se esperaba el bloqueo temporal del búfer -- tipo %d, bp %p, página %d:%d, stat %#x, id. de base de datos: %d, id. de unidad de asignación: %I64d%ls, tarea 0x%p : %d, tiempo de espera %d, marcas 0x%I64x, tarea propietaria 0x%p. No se continúa la espera.|  
  
## <a name="explanation"></a>Explicación  
 Es posible que un equipo deje de responder o que se agote el tiempo de espera o se produzca alguna otra interrupción de las operaciones normales al mismo tiempo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escribe errores de bloqueos temporales de búfer en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si el campo de estado del mensaje tiene activado el valor 0x04, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estará esperando una operación de E/S. También puede recibir el mensaje [MSSQLSERVER_833](mssqlserver-833-database-engine-error.md) en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si el campo de estado del mensaje tiene desactivado el valor 0x04, habrá una contención intensa en una página. Si el objeto es una página de datos, esto puede deberse a un diseño de código ineficaz. Si la página no es de datos, el error puede producirse por cuellos de botella del servidor, como recursos de hardware insuficientes.  
  
## <a name="user-action"></a>Acción del usuario  
 Para solucionar este problema, según el entorno, puede seguir uno o varios de estos pasos para reducir o eliminar los mensajes de error:  
  
-   Determine si tiene algún cuello de botella de hardware. Si es necesario, actualice el hardware para que sea compatible con los requisitos de configuración, consulta y carga del entorno. Para obtener más información sobre los cuellos de botella, vea [Identificar los cuellos de botella](../performance/identify-bottlenecks.md).  
  
-   Compruebe si hay algún error registrado y ejecute los diagnósticos suministrados por el proveedor de hardware.  
  
-   Asegúrese de que las unidades de disco no estén comprimidas. No se admite el almacenamiento de datos ni archivos de registro en unidades comprimidas. Para obtener más información sobre los archivos físicos, vea [Archivos y grupos de archivos de base de datos](../databases/database-files-and-filegroups.md).  
  
-   Observe si los mensajes de error desaparecen al desactivar las siguientes opciones:  
  
    -   Opción de configuración de aumento de prioridad de SQL Server  
  
    -   Opción de agrupación ligera (modo de fibra)  
  
    -   Opción "set working set size"  
  
    > [!NOTE]  
    >  A menudo, las opciones de configuración anteriores pueden ser contraproducentes si modifica su valor predeterminado desactivado. Para obtener más información, vea [Opciones de configuración del servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
-   Optimice las consultas para reducir los recursos utilizados en el sistema. La optimización del rendimiento ayudará a reducir la demanda en un sistema y a mejorar el tiempo de respuesta de las consultas individuales.  
  
-   Establezca la opción AUTO_SHRINK en OFF para reducir la sobrecarga de los cambios de tamaño de la base de datos.  
  
-   Asegúrese de establecer la opción FILEGROWTH en incrementos lo suficientemente grandes como para ser infrecuentes. Programe un trabajo para comprobar el espacio disponible en las bases de datos y, a continuación, aumente el tamaño de la base de datos durante las horas de menor actividad.  
  
  
