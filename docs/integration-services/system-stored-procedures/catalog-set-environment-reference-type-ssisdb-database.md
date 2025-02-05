---
title: catalog.set_environment_reference_type (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b79e3a06-22c0-40e5-8933-1b3414db3329
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d50cef16424f5524429c6b4285af0ae8568391be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038698"
---
# <a name="catalogsetenvironmentreferencetype-ssisdb-database"></a>catalog.set_environment_reference_type (base de datos SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece el tipo de referencia y el nombre del entorno asociados con una referencia de entorno existente para un proyecto en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_environment_reference_location [ @reference_id = reference_id  
    , [ @reference_type = ] reference_type  
 [  , [ @environment_folder_name = ] environment_folder_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @reference_id = ] *reference_id*  
 Identificador único de la referencia de entorno que se va a actualizar. *reference_id* es **bigint**.  
  
 [ @reference_type = ] *reference_type*  
 Indica si el entorno se puede encontrar en la misma carpeta que el proyecto (referencia relativa) o en una carpeta diferente (referencia absoluta). Utilice el valor `R` para indicar una referencia relativa. Utilice el valor `A` para indicar una referencia absoluta. El parámetro *reference_type* es **char(1)** .  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 La carpeta en que se encuentra el entorno. Este valor se requiere para las referencias absolutas. El parámetro *environment_folder_name* es **nvarchar(128)** .  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Los permisos de lectura y modificación en el proyecto, y el permiso de lectura en el entorno  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El nombre de la carpeta, el nombre del entorno o el identificador de referencia no es válido  
  
-   El usuario no tiene los permisos apropiados  
  
-   Una referencia absoluta se especifica mediante el carácter `A` en el parámetro *reference_location*, pero el nombre de la carpeta no se especificó con el parámetro *environment_folder_name*.  
  
## <a name="remarks"></a>Notas  
 Un proyecto puede tener referencias de entorno absolutas o relativas. Las referencias relativas se refieren al entorno por nombre y requieren que resida en la misma carpeta que el proyecto. Las referencias absolutas hacen referencia al entorno por nombre y carpeta, y pueden hacer referencia a los entornos que residen en una carpeta diferente que el proyecto. Un proyecto puede hacer referencia a varios entornos.  
  
> [!IMPORTANT]  
>  Si se especifica una referencia relativa, el valor del parámetro *environment_folder_name* no se utiliza y el nombre de la carpeta del entorno se establece automáticamente en **NULL**. Si se especifica una referencia absoluta, el nombre de la carpeta de entorno se debe proporcionar en el parámetro *environment_folder_name*.  
  
  
