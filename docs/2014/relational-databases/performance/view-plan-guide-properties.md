---
title: Ver propiedades de la guía de plan | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.planguideprop.general.f1
helpviewer_keywords:
- plan guides [SQL Server], view plan guide properties
- viewing plan guide properties
ms.assetid: 8c0d2f39-59c1-4168-a649-65473f6a771b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b49b24db5dfa3c9b522247024e0cbb8dbd1a81d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151266"
---
# <a name="view-plan-guide-properties"></a>Ver propiedades de la guía de plan
  Puede ver las propiedades de las guías de plan en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver las propiedades de las guías de plan, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o para los que el usuario tiene algún permiso.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>Para ver las propiedades de una guía de plan  
  
1.  Haga clic en el signo más para expandir la base de datos en la que desea ver las propiedades de una guía de plan y haga clic en el signo más para expandir la carpeta **Programación** .  
  
2.  Haga clic en el signo más para expandir la carpeta **Guías de plan** .  
  
3.  Haga clic con el botón derecho en la guía de plan cuyas propiedades quiere ver y seleccione **Propiedades**.  
  
     Las propiedades siguientes se muestran en el cuadro de diálogo **Propiedades de la guía de plan** .  
  
     **Sugerencias**  
     Muestra las sugerencias de consulta o el plan de consulta que se va a aplicar a la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] . Cuando un plan de consulta se especifica como una sugerencia, se mostrará la salida del Plan de presentación XML.  
  
     **Está deshabilitado**  
     Muestra el estado de la guía de plan. Los valores posibles son **True** o **False**.  
  
     **Name**  
     Muestra el nombre de la guía de plan.  
  
     **Parámetros**  
     Cuando el tipo de ámbito es SQL o TEMPLATE, muestra el nombre y el tipo de dato de todos los parámetros incorporados en la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
     **Lote del ámbito**  
     Muestra el texto del lote en el que aparece la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
     **Nombre de objeto del ámbito**  
     Si el tipo de ámbito es OBJECT, muestra el nombre del procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] , función escalar definida por el usuario, función con valores de tabla de múltiples instrucciones o desencadenador DML en que aparece la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
     **Nombre de esquema del ámbito**  
     Si el tipo de ámbito es OBJECT, muestra el nombre del esquema en el que está contenido el objeto.  
  
     **Tipo de ámbito**  
     Muestra el tipo de entidad en la que aparece la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Así se especifica el contexto para hacer coincidir la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] con la guía de plan. Los valores posibles son **OBJECT**, **SQL**y **TEMPLATE**.  
  
     **Estamento**  
     Muestra la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] frente a la que se aplicará la guía de plan.  
  
4.  Haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>Para ver las propiedades de una guía de plan  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- If a plan guide named "Guide1" already exists in the AdventureWorks2012 database, delete it.  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID(N'Guide1') IS NOT NULL  
       EXEC sp_control_plan_guide N'DROP', N'Guide1';  
    GO  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
    GO  
    -- Gets the name, created date, and all other relevant property information on the plan guide created above.   
    SELECT name AS plan_guide_name,  
       create_date,  
       query_text,  
       scope_type_desc,  
       OBJECT_NAME(scope_object_id) AS scope_object_name,  
       scope_batch,  
       parameters,  
       hints,  
       is_disabled  
    FROM sys.plan_guides  
    WHERE name = N'Guide1';  
    GO  
    ```  
  
 Para obtener más información, vea [sys.plan_guides &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-plan-guides-transact-sql).  
  
  
