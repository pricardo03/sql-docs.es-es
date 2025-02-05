---
title: Suscribir una base de datos a una categoría de directiva o anular la suscripción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.groupsubscription.f1
ms.assetid: d2c31769-7098-428e-ad9c-ef56541b7c52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d0139376adc28b07877389a023b19310b06417ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68212134"
---
# <a name="subscribe-or-unsubscribe-a-database--to-a-policy-category"></a>Suscribir una base de datos a una categoría de directiva o anular la suscripción
  En este tema se describe cómo se suscribe una base de datos a una categoría de directiva o se cancela la suscripción en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para suscribir una base de datos a una categoría de directiva o anular la suscripción con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere pertenencia al rol fijo de base de datos db_owner.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-subscribe-or-unsubscribe-a-database-to-a-policy-category"></a>Para suscribir una base de datos a una categoría de directiva o anular la suscripción  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la base de datos en la que se encuentran las suscripciones de categorías que desea administrar.  
  
2.  Haga clic en el signo más para expandir la carpeta **Bases de datos** .  
  
3.  Haga clic con el botón derecho en la base de datos que contiene las suscripciones que quiera administrar, seleccione **Directivas**y, después, seleccione **Categorías**.  
  
     En el cuadro de diálogo **Categorías** están disponibles las siguientes opciones:  
  
     Expandir columna  
     Haga clic para expandir una categoría de directiva. De este modo se muestra una lista de todas las directivas que están incluidas en la categoría.  
  
     **Name**  
     Nombre de la categoría de directiva.  
  
     **Suscrito**  
     Indica si el destino se ha suscrito a la categoría de directiva. Si esta casilla está deshabilitada, la categoría de directiva está establecida para **Suscripciones de base de datos de mandatos**. Esto significa que la categoría de directiva se aplica a todas las bases de datos en el servidor.  
  
     **Directiva**  
     Cuando se expanden los grupos de directivas, muestra las directivas de la categoría de directiva.  
  
     **Enabled**  
     Indica si las directivas están habilitadas o deshabilitadas.  
  
     **Modo de ejecución**  
     Muestra el modo de ejecución de la directiva.  
  
     **Historial**  
     Haga clic en el hipervínculo Ver historial para abrir el Visor del archivo de registros para ver el historial de directiva.  
  
4.  Para suscribirse a una categoría de administración basada en directivas, active la casilla de la categoría en la columna **Subscribed** . Para anular la suscripción de una categoría, desactive la casilla.  
  
5.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-subscribe-a-database-to-a-policy-category"></a>Para suscribir una base de datos a una categoría de directiva  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    -- Adds a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_subscribe_to_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 Para obtener más información, vea [sp_syspolicy_subscribe_to_policy_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql).  
  
#### <a name="to-unsubscribe-a-database-to-a-policy-category"></a>Para anular la suscripción de una base de datos a una categoría de directiva  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    -- Deletes a subscription to the 'Finance' policy category for the AdventureWorks2012 database.  
    EXEC sys.sp_syspolicy_unsubscribe_from_policy_category @policy_category = N'Finance';  
    GO  
    ```  
  
 Para obtener más información, vea [sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql).  
  
  
