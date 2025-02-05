---
title: Guardar seguimientos y plantillas de seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- exporting trace templates
- importing trace templates
- SQL Server Profiler, templates
ms.assetid: 957e6bf8-e7a3-4a59-a1cd-0a41538a8158
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4baca63080a3f67c1f9e54a8a0aa955a27029df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267430"
---
# <a name="save-traces-and-trace-templates"></a>Guardar seguimientos y plantillas de seguimiento
  Es importante distinguir entre guardar archivos de seguimiento y guardar plantillas de seguimiento. Guardar un archivo de seguimiento implica guardar los datos de eventos capturados en un lugar especificado. Guardar una plantilla de seguimiento implica guardar la definición del seguimiento, como las columnas de datos, las clases de eventos o los filtros especificados.  
  
## <a name="saving-traces"></a>guardar seguimientos  
 Guarde los datos de los eventos capturados en un archivo o una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando necesite analizar o reproducir los datos capturados más adelante. Utilice un archivo de seguimiento para lo siguiente:  
  
-   Utilice un archivo de seguimiento o una tabla de seguimiento para crear una carga de trabajo a fin de utilizarla como entrada para el Asistente para la optimización de motor de base de datos.  
  
-   Utilice un archivo de seguimiento para capturar eventos y enviar el archivo de seguimiento a un proveedor de asistencia técnica para su análisis.  
  
-   Utilice las herramientas de procesamiento de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tener acceso a los datos o verlos en el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Solo pueden tener acceso directo a la tabla de seguimiento los miembros del rol fijo de servidor **sysadmin** o el creador de la tabla.  
  
> [!NOTE]  
>  La captura de datos de seguimiento en una tabla resulta una operación más lenta que la captura de datos de seguimiento en un archivo. Una alternativa es capturar los datos de seguimiento en un archivo, abrir el archivo de seguimiento y, después, guardar el seguimiento como una tabla de seguimiento.  
  
 Cuando use un archivo de seguimiento, el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] guardará los datos de eventos capturados (no las definiciones de seguimiento) en un archivo de seguimiento ( [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .trc) del\*. La extensión se agrega automáticamente al final del archivo al guardarlo, independientemente de si se ha especificado otra extensión. Por ejemplo, si especifica un archivo de seguimiento denominado **Seguimiento.dat**, el nombre del archivo creado será **Seguimiento.dat.trc**.  
  
> [!IMPORTANT]  
>  Los usuarios que tienen el permiso SHOWPLAN, ALTER TRACE o VIEW SERVER STATE pueden ver consultas capturadas en la salida del plan de presentación. Estas consultas pueden contener información confidencial, como contraseñas. Por consiguiente, se recomienda conceder estos permisos solo a los usuarios que tengan autorización para ver información confidencial, como los miembros del rol fijo de base de datos **db_owner** o los miembros del rol fijo de servidor **sysadmin** . Además, se recomienda guardar solo los archivos del plan de presentación o los archivos de seguimiento que contengan eventos relacionados con el plan de presentación en una ubicación que utilice el sistema de archivos NTFS, así como restringir el acceso a los usuarios que tengan autorización para ver información confidencial.  
  
## <a name="saving-templates"></a>Guardar plantillas  
 La definición de la plantilla de un seguimiento incluye las clases de eventos, columnas de datos, filtros y todas las demás propiedades (excepto los datos de eventos capturados) que se utilizan para crear un seguimiento. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] proporciona plantillas del sistema predefinidas para las tareas de seguimiento comunes y para tareas específicas, como crear una carga de trabajo que el Asistente para la optimización de motor de base de datos pueda utilizar para ajustar el diseño físico de la base de datos. También se pueden crear y guardar plantillas definidas por el usuario.  
  
### <a name="importing-and-exporting-templates"></a>Importar y exportar plantillas  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] permite importar y exportar plantillas de un servidor a otro. Al exportar una plantilla se mueve una copia de una plantilla existente al directorio especificado. Al importar una plantilla se realiza una copia de una plantilla especificada. Cuando estas plantillas se ven en el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], se pueden distinguir de las plantillas del sistema por el término "(usuario)" que sigue al nombre de la plantilla. Las plantillas del sistema predefinidas no se pueden sobrescribir ni modificar directamente.  
  
### <a name="analyzing-performance-with-templates"></a>Analizar el rendimiento con plantillas  
 Si supervisa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]con frecuencia, utilice plantillas para analizar el rendimiento. Las plantillas capturan los mismos datos de eventos cada vez y utilizan la misma definición de seguimiento para supervisar los mismos eventos. No tendrá que definir las clases de eventos y las columnas de datos cada vez que cree un seguimiento. Además, se puede proporcionar una plantilla a otro usuario para supervisar eventos específicos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por ejemplo, un proveedor de asistencia técnica puede proporcionar una plantilla a un cliente. El cliente puede utilizar la plantilla para capturar los datos de eventos necesarios, que posteriormente enviará al proveedor de asistencia técnica para que los analice.  
  
 **Para guardar un seguimiento en un archivo**  
  
 [Guardar los resultados de un seguimiento en un archivo &#40;SQL Server Profiler&#41;](save-trace-results-to-a-file-sql-server-profiler.md)  
  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)  
  
## <a name="see-also"></a>Vea también  
 [Guardar los resultados de un seguimiento en una tabla &#40;SQL Server Profiler&#41;](save-trace-results-to-a-table-sql-server-profiler.md)   
 [Crear una plantilla de seguimiento &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)   
 [Derivar una plantilla a partir de un seguimiento en ejecución &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Derivar una plantilla a partir de un archivo o tabla de seguimiento &#40;SQL Server Profiler&#41;](derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [Exportar una plantilla de seguimiento &#40;SQL Server Profiler&#41;](export-a-trace-template-sql-server-profiler.md)   
 [Importar una plantilla de seguimiento &#40;SQL Server Profiler&#41;](import-a-trace-template-sql-server-profiler.md)  
  
  
