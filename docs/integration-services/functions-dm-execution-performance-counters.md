---
title: dm_execution_performance_counters (base de datos SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 1b38e8e3-c560-4b6e-b60e-bfd7cfcd4fdf
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 820d4b3dae7643db7f03f4e761b63208f20263e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102790"
---
# <a name="functions---dmexecutionperformancecounters"></a>Funciones - dm_execution_performance_counters

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Devuelve las estadísticas de rendimiento de una ejecución en el servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
dm_execution_performance_counters [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id = ] *execution_id*  
 El identificador único de la ejecución que contiene uno o más paquetes. Los paquetes que se ejecutan con la tarea Ejecutar paquete se ejecutan en la misma instancia que el paquete primario.  
  
 Si no se especifica un identificador de ejecución, se devuelven estadísticas de rendimiento de varias ejecuciones. Si es miembro del rol de base de datos **ssis_admin** , se devuelven las estadísticas de rendimiento de todas las ejecuciones actuales.  Si no es miembro del rol de base de datos **ssis_admin** , se devuelven las estadísticas de rendimiento de las ejecuciones actuales para las que tiene permisos de lectura. *execution_id* es **BigInt**.  
  
## <a name="remarks"></a>Notas  
 En la tabla siguiente se muestran los valores de nombre de contador devueltos por la función dm_execution_performance_counter.  
  
|Nombre de contador|Descripción|  
|------------------|-----------------|  
|Bytes BLOB leídos|Número de bytes de datos de objetos binarios grandes (BLOB) que el motor de flujo de datos lee de todos los orígenes.|  
|Bytes BLOB escritos|Número de bytes de datos BLOB que el motor de flujo de datos escribe en todos los destinos.|  
|Archivos BLOB en uso|Número de archivos BLOB que el motor de flujo de datos está usando para la puesta en cola.|  
|Memoria de búfer|Cantidad de memoria usada por los búferes de Integration Services, incluida la memoria física y virtual.|  
|Búferes en uso|Número de objetos de búfer, de cualquier tipo, que están usando todos los componentes de flujo de datos y el motor de flujo de datos.|  
|Búferes puestos en cola|Número de búferes escritos en el disco.|  
|Memoria de búfer plano|Cantidad de memoria, en bytes, usada por todos los búferes planos. Los búferes planos son bloques de memoria que un componente usa para almacenar datos.|  
|Búferes planos en uso|Número de búferes planos que usa el motor de flujo de datos. Todos los búferes planos son privados.|  
|Memoria de búfer privado|Cantidad de memoria en uso por todos los búferes privados. Un búfer privado es un búfer que una transformación usa para realizar trabajo temporal.<br /><br /> Un búfer no es privado si el motor de flujo de datos lo crea para admitir el flujo de datos.|  
|Búferes privados en uso|Número de búferes que las transformaciones usan para realizar trabajo temporal.|  
|Filas leídas|Número total de filas listas para su ejecución.|  
|Filas escritas|Número total de filas escritas por la ejecución.|  
  
## <a name="return"></a>Devolución  
 La función dm_execution_performance_counters devuelve una tabla con las columnas siguientes para una ejecución en curso. La información devuelta corresponde a todos los paquetes contenidos en la ejecución. Si no hay ninguna ejecución en curso, se devuelve una tabla vacía.  
  
|Nombre de la columna|Tipo de columna|Descripción|Notas|  
|-----------------|-----------------|-----------------|-------------|  
|execution_id|**BigInt**<br /><br /> **NULL** no es un valor válido.|Identificador único para la ejecución que contiene el paquete.||  
|counter_name|**nvarchar(128)**|Nombre del contador.|Vea la sección **Comentarios** de los valores.|  
|counter_value|**BigInt**|Valor devuelto por el contador.||  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, la función devuelve estadísticas para la ejecución actual con el identificador 34.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, la función devuelve estadísticas para todas las ejecuciones actuales en el servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], según sus permisos.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
## <a name="permissions"></a>Permisos  
 Esta función necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en la instancia de ejecución  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen las condiciones que hacen que la función genere un error.  
  
-   El usuario no tiene permisos MODIFY para la ejecución especificada.  
  
-   El identificador de ejecución especificado no es válido.  
  
  
