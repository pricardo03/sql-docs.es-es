---
title: Creación de desencadenadores DML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], DML triggers
- deferred name resolution, DML triggers
- WITH ENCRYPTION clause
- IF UPDATE
- SET statement, DML triggers
- DML triggers, programming
- testing column changes
- results [SQL Server], DML triggers
ms.assetid: b2b52258-642b-462e-8e0f-18c09d2eccf4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3fa03aae36fd7de30f8efd88742b1e3a73907a0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676440"
---
# <a name="create-dml-triggers"></a>Crear desencadenadores DML
  En este tema se describe cómo crear un desencadenador DML de [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y usando la instrucción CREATE TRIGGER de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
##  <a name="Top"></a> Antes de comenzar  
  
### <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Para obtener una lista de las limitaciones y restricciones relacionadas con la creación de desencadenadores DML, vea [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
###  <a name="Permissions"></a> Permisos  
 Es necesario contar con permiso ALTER sobre la tabla o vista en la que se crea el desencadenador.  
  
##  <a name="Procedures"></a> Cómo crear un desencadenador DML  
 Puede usar cualquiera de los siguientes medios:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Databases**, expanda la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , expanda **Tablas** y a continuación expanda la tabla **Purchasing.PurchaseOrderHeader**.  
  
3.  Haga clic con el botón derecho en **Desencadenadores**y, después, seleccione **Nuevo desencadenador**.  
  
4.  En el menú **Consulta** , haga clic en **Especificar valores para parámetros de plantilla**. También puede pulsar (Ctrl+Mayús+M) para abrir el cuadro de diálogo **Especificar valores para parámetros de plantilla** .  
  
5.  En el cuadro de diálogo **Especificar valores para parámetros de plantilla** , especifique los siguientes valores para los parámetros mostrados.  
  
    |Parámetro|Valor|  
    |---------------|-----------|  
    |Autor|*Su nombre.*|  
    |Create Date|*La fecha de hoy.*|  
    |Descripción|Comprueba la solvencia del proveedor antes de permitir que se inserte un nuevo pedido de compra con el proveedor.|  
    |Schema_Name|Purchasing|  
    |Trigger_Name|NewPODetail2|  
    |Table_Name|PurchaseOrderDetail|  
    |Data_Modification_Statement|Quite UPDATE y DELETE de la lista.|  
  
6.  Haga clic en **Aceptar**.  
  
7.  En el **Editor de consultas**, reemplace el comentario `-- Insert statements for trigger here` con la instrucción siguiente:  
  
    ```sql  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
8.  Para comprobar que la sintaxis es válida, en el menú **Consulta** , haga clic en **Analizar**. Si se devuelve un mensaje de error, compare la instrucción con la información anterior y corrija lo que sea necesario y repita este paso.  
  
9. Para crear el desencadenador DML, en el menú **Consulta** , haga clic en **Ejecutar**. El desencadenador DML se crea como un objeto de la base de datos.  
  
10. Para ver el desencadenador DML que aparece en el Explorador de objetos, haga clic con el botón derecho en **Desencadenadores** y seleccione **Actualizar**.  
  
 [Antes de comenzar](#Top)  
  
###  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] y expándala.  
  
2.  En el menú **Archivo** , haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo crea el mismo desencadenador DML almacenado que antes.  
  
    ```  
    -- Trigger valid for multirow and single row inserts  
    -- and optimal for single row inserts.  
    USE AdventureWorks2012;  
    GO  
    CREATE TRIGGER NewPODetail3  
    ON Purchasing.PurchaseOrderDetail  
    FOR INSERT AS  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
##  <a name="PowerShellProcedure"></a> [Antes de comenzar](#Top)  
  
  
