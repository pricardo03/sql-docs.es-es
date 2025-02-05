---
title: sp_configure (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fb4aeced22755ff2b8012e5eeff7c27ec2f73374
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476011"
---
# <a name="spconfigure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-pdw-md.md)]

  Muestra o cambia las opciones de configuración global del servidor actual.

> [!NOTE]  
>  Para las opciones de configuración de nivel de base de datos, vea [ALTER DATABASE scoped &#40;Configuration Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Para configurar Soft-NUMA, consulte [SQL Server &#40;&#41;de Numa de software](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
sp_configure [ [ @configname = ] 'option_name'   
    [ , [ @configvalue = ] 'value' ] ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- List all of the configuration options  
sp_configure  
[;]  
  
-- Configure Hadoop connectivity  
sp_configure [ @configname= ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @configname = ] 'option_name'`Es el nombre de una opción de configuración. *option_name* es **varchar(35)** y su valor predeterminado es NULL. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] reconoce cualquier cadena única que forme parte del nombre de configuración. Si no se especifica, se devuelve la lista completa de opciones.  
  
 Para obtener información sobre las opciones de configuración disponibles y su configuración, consulte [opciones &#40;de&#41;configuración del servidor SQL Server](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
`[ @configvalue = ] 'value'`Es el nuevo valor de configuración. *value* es de tipo **int**y su valor predeterminado es NULL. El valor máximo depende de la opción individual.  
  
 Para ver el valor máximo de cada opción, vea la columna **Maximum** de la vista de catálogo **Sys.** Configurations.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Cuando se ejecuta sin parámetros, **sp_configure** devuelve un conjunto de resultados con cinco columnas y ordena las opciones alfabéticamente en orden ascendente, tal como se muestra en la tabla siguiente.  
  
 Los valores de **config_value** y **run_value** no son equivalentes automáticamente. Después de actualizar una opción de configuración mediante **sp_configure**, el administrador del sistema debe actualizar el valor de configuración en ejecución mediante reconfigure o reconfigure with override. Para obtener más información, vea la sección Comentarios.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|Nombre de la opción de configuración.|  
|**Mínimo**|**int**|Valor mínimo de la opción de configuración.|  
|**Máximo**|**int**|Valor máximo de la opción de configuración.|  
|**config_value**|**int**|Valor en el que se estableció la opción de configuración mediante **sp_configure** (valor en sys. Configurations **. Value**). Para obtener más información sobre estas opciones, vea [opciones &#40;de configuración&#41; del servidor SQL Server](../../database-engine/configure-windows/server-configuration-options-sql-server.md) y sys. Configurations [de &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
|**run_value**|**int**|Valor que se está ejecutando actualmente de la opción de configuración (valor en sys. Configurations **. value_in_use**).<br /><br /> Para obtener más información, vea [Sys. &#40;Configurations&#41;de Transact-SQL](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
  
## <a name="remarks"></a>Comentarios  
 Utilice **sp_configure** para mostrar o cambiar la configuración de nivel de servidor. Para cambiar la configuración de la base de datos, utilice ALTER DATABASE. Para cambiar la configuración que afecta solo a la sesión de usuario actual, utilice la instrucción SET.  
  
## <a name="updating-the-running-configuration-value"></a>Actualizar el valor de configuración actual  
 Cuando se especifica un nuevo *valor* para una *opción*, el conjunto de resultados muestra este valor en la columna **config_value** . Inicialmente, este valor difiere del valor de la columna **run_value** , que muestra el valor de configuración que se está ejecutando actualmente. Para actualizar el valor de configuración en ejecución en la columna **run_value** , el administrador del sistema debe ejecutar reconfigure o reconfigure with override.  
  
 RECONFIGURE y RECONFIGURE WITH OVERRIDE funcionan con todas las opciones de configuración. No obstante, la instrucción RECONFIGURE básica rechaza cualquier valor de opción que esté fuera de un intervalo razonable o que pueda ocasionar conflictos entre las opciones. Por ejemplo, reconfigure genera un error si el valor del **intervalo de recuperación** es superior a 60 minutos o si el valor de la **máscara de afinidad** se superpone con el valor de máscara de **afinidad de e/s** . RECONFIGURE WITH OVERRIDE, por el contrario, admite cualquier valor de opción que contenga el tipo de datos correcto y obliga a realizar la reconfiguración con el valor especificado.  
  
> [!CAUTION]  
>  Un valor de opción inapropiado puede afectar negativamente a la configuración de la instancia de servidor. Utilice RECONFIGURE WITH OVERRIDE con precaución.  
  
 La instrucción RECONFIGURE actualiza algunas opciones dinámicamente; para otras opciones es necesario detener y reiniciar el servidor. Por ejemplo, las opciones de memoria de servidor **min Server** Memory y **Max Server Memory** se actualizan dinámicamente en el [!INCLUDE[ssDE](../../includes/ssde-md.md)]; por lo tanto, puede cambiarlas sin necesidad de reiniciar el servidor. Por el contrario, para volver a configurar el valor de ejecución de la opción de **factor** de [!INCLUDE[ssDE](../../includes/ssde-md.md)]relleno, es necesario reiniciar el.  
  
 Después de ejecutar reconfigure en una opción de configuración, puede ver si la opción se ha actualizado dinámicamente ejecutando **sp_configure '***nombredeopción***'** . Los valores de las columnas **run_value** y **config_value** deben coincidir para una opción actualizada dinámicamente. También puede comprobar qué opciones son dinámicas examinando la columna **is_dynamic** de la vista de catálogo **Sys.** Configurations.  
 
 El cambio también se escribe en el registro de errores de SQL Server.
  
> [!NOTE]  
>  Si un *valor* especificado es demasiado alto para una opción, la columna **run_value** refleja el [!INCLUDE[ssDE](../../includes/ssde-md.md)] hecho de que tiene como valor predeterminado memoria dinámica en lugar de usar una configuración que no es válida.  
  
 Para obtener más información, vea reconfigure [ &#40;Transact&#41;-SQL](../../t-sql/language-elements/reconfigure-transact-sql.md).  
  
## <a name="advanced-options"></a>Opciones avanzadas  
 Algunas opciones de configuración, como **affinity mask** y **Recovery Interval**, se designan como opciones avanzadas. De forma predeterminada, estas opciones no están disponibles para verlas o modificarlas. Para que estén disponibles, establezca la opción de configuración **ShowAdvancedOptions** en 1.  
  
 Para obtener más información sobre las opciones de configuración y sus valores, consulte [opciones &#40;de&#41;configuración del servidor SQL Server](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros para cambiar una opción de configuración o ejecutar la instrucción RECONFIGURE, debe tener el permiso ALTER Settings de nivel de servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. Enumerar las opciones de configuración avanzadas  
 En este ejemplo se muestra cómo establecer y enumerar todas las opciones de configuración. Para ver las opciones de configuración avanzadas, primero hay que establecer en `show advanced option` el valor de `1`. A continuación, si se ejecuta `sp_configure` sin parámetros, se mostrarán todas las opciones de configuración.  
  
```  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 Este es el mensaje: "Opción de configuración" Mostrar opciones avanzadas "cambió de 0 a 1. Ejecute la instrucción RECONFIGURE para instalar".  
  
 Ejecute `RECONFIGURE` y muestre todas las opciones de configuración:  
  
```  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>b. Cambiar una opción de configuración  
 En el siguiente ejemplo se establece el `recovery interval` (intervalo de recuperación) del sistema en `3` minutos.  
  
```  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>C. Lista de todas las opciones de configuración disponibles  
 En este ejemplo se muestra cómo enumerar todas las opciones de configuración.  
  
```  
EXEC sp_configure;  
```  
  
 El resultado devuelve el nombre de opción seguido por los valores mínimo y máximo de la opción. **Config_value** es el valor que [!INCLUDE[ssDW](../../includes/ssdw-md.md)] se usará cuando se complete la reconfiguración. El valor **run_value** es el valor que se está usando actualmente. Los valores **config_value** y **run_value** son normalmente los mismos, a menos que el valor se esté modificando.  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. Lista de las opciones de configuración para un nombre de configuración  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. Establecer la conectividad de Hadoop  
 La configuración de la conectividad de Hadoop requiere algunos pasos más además de ejecutar sp_configure. Para obtener el procedimiento completo, vea [Create external Data &#40;Source Transact-&#41;SQL](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
