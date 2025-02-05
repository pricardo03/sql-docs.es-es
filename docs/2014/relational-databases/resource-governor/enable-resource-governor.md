---
title: Habilitar el regulador de recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, enabling
ms.assetid: 4d17af53-cf11-4ce4-aab4-deda94a49836
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5ef8d77de1df31387d33e6577fe84bd5ef9fa680
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63216026"
---
# <a name="enable-resource-governor"></a>Habilitar el regulador de recursos
  El regulador de recursos está desactivado de forma predeterminada. Puede habilitar el regulador de recursos utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o Transact-SQL.  
  
-   **Antes de empezar:**  [Limitaciones y restricciones](#LimitationsRestrictions), [Permisos](#Permissions)  
  
-   **Para habilitar Resource Governor, mediante:**  [Explorador de objetos](#RGOnObjEx), [propiedades de Resource Governor](#RGOnProp), [Transact-SQL](#RGOnTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
 Habilitar el regulador de recursos tiene como consecuencia lo siguiente:  
  
-   La función clasificadora se ejecuta para las nuevas conexiones, de forma que se pueden asignar sus cargas de trabajo a los grupos de cargas de trabajo.  
  
-   Se respetan y se aplican los límites de los recursos especificados en la configuración del regulador de recursos.  
  
-   Las solicitudes que existieran antes de habilitar el regulador de recursos resultarán afectadas por cualquier cambio realizado en la configuración en el momento de deshabilitar el regulador de recursos.  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 No puede utilizar la instrucción `ALTER RESOURCE GOVERNOR` para habilitar el regulador de recursos durante una transacción del usuario.  
  
###  <a name="Permissions"></a> Permisos  
 Habilitar el regulador de recursos requiere el permiso CONTROL SERVER.  
  
##  <a name="RGOnObjEx"></a> Habilitar el regulador de recursos mediante el Explorador de objetos  
 **Para habilitar el regulador de recursos utilizando el Explorador de objetos**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra el Explorador de objetos y expanda de forma recursiva el nodo **Administración** hasta el nodo **Regulador de recursos**.  
  
2.  Haga clic con el botón derecho en **Regulador de recursos**y luego haga clic en **Habilitar**.  
  
##  <a name="RGOnProp"></a> Habilitar el regulador de recursos mediante Propiedades del regulador de recursos  
 **Para habilitar el regulador de recursos mediante la página Propiedades del regulador de recursos**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra el Explorador de objetos y expanda de forma recursiva el nodo **Administración** hasta el nodo **Regulador de recursos**.  
  
2.  Haga clic con el botón derecho en **Regulador de recursos** y luego haga clic en **Propiedades**. De este modo se abre la página **Propiedades del regulador de recursos** .  
  
3.  Haga clic en la casilla **Habilitar regulador de recursos** y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="RGOnTSQL"></a> Habilitar el regulador de recursos mediante Transact-SQL  
 **Para habilitar el regulador de recursos mediante Transact-SQL**  
  
1.  Ejecute la instrucción **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Ejemplo (Transact-SQL)  
 En el ejemplo siguiente se habilita el regulador de recursos.  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Regulador de recursos](resource-governor.md)   
 [Deshabilitar el regulador de recursos](disable-resource-governor.md)   
 [Grupo de recursos de servidor del regulador de recursos](resource-governor-resource-pool.md)   
 [Grupos de cargas de trabajo del regulador de recursos](resource-governor-workload-group.md)   
 [Función clasificadora del regulador de recursos](resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
