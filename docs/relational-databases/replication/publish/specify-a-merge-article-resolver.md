---
title: Especificar un solucionador de artículos de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
- merge replication conflict resolution [SQL Server replication], merge article resolvers
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 69daa9fd9420298bb69439ae629fb6391d0f0c10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073485"
---
# <a name="specify-a-merge-article-resolver"></a>Especificar un solucionador de artículos de mezcla
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo especificar un solucionador de artículos de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  

  
##  <a name="recommendations"></a>Recomendaciones  
  
-   La replicación de mezcla admite los siguientes tipos de solucionadores de artículos:  
  
    -   El solucionador predeterminado. El comportamiento del solucionador predeterminado depende de si se trata de una suscripción de cliente o de servidor. Para más información sobre cómo especificar el tipo de suscripción, vea [Specify a Merge Subscription Type and Conflict Resolution Priority &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md) (Especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos &#40;SQL Server Management Studio&#41;).  
  
    -   Un solucionador personalizado, escrito por el usuario, que puede ser un controlador de lógica de negocios (escrito en código administrado) o un solucionador personalizado basado en COM. Para más información, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md). Si necesita implementar lógica personalizada que se ejecute para cada fila replicada, no solo para filas con conflictos, vea [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Un solucionador estándar basado en COM, incluido con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Para utilizar un solucionador distinto del predeterminado, debe copiarlo en el equipo en el que se ejecuta el Agente de mezcla y registrarlo (si utiliza un controlador de lógica de negocios, también debe registrarlo en el publicador). El Agente de mezcla se ejecuta en:  
  
    -   El distribuidor, para una suscripción de inserción.  
  
    -   El suscriptor, para una suscripción de extracción.  
  
    -   El servidor con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS), para una suscripción de extracción que utilice la sincronización web.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Una vez registrado el solucionador, especifique que un artículo debe utilizar el solucionador en la pestaña **Resolución** del cuadro de diálogo **Propiedades del artículo: \<artículo>** , que está disponible en el Asistente para nueva publicación y el cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md) (Crear una publicación) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-resolver"></a>Para especificar un solucionador  
  
1.  En la página **Artículos** del Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación: \<publicación>** , seleccione una tabla.  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
3.  En la página **Propiedades del artículo: \<artículo>** , haga clic en la pestaña **Resolución**.  
  
4.  Seleccione **Usar un solucionador personalizado (registrado en el distribuidor)** y después, en la lista, haga clic en el solucionador.  
  
5.  Si el solucionador requiere una entrada (por ejemplo, un nombre de columna), especifíquela en el cuadro de texto **Especifique la información necesaria para el solucionador** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Repita este proceso para cada artículo que necesite un solucionador.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-register-a-custom-conflict-resolver"></a>Para registrar un solucionador de conflictos personalizado  
  
1.  Si piensa registrar su propio solucionador de conflictos personalizado, cree uno de los tipos siguientes:  
  
    -   Solucionador basado en código administrado como un controlador de lógica de negocios. Para más información, consulte [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Solucionador basado en procedimientos almacenados y solucionador basado en COM. Para más información, consulte [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
2.  Para determinar si el solucionador deseado ya está registrado, ejecute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) en el publicador en cualquier base de datos. Esto muestra una descripción del solucionador personalizado así como del identificador de clase (CLSID) de cada solucionador basado en COM registrado en el distribuidor o información sobre el ensamblado administrado de cada controlador de lógica de negocios registrado en el distribuidor.  
  
3.  Si el solucionador personalizado aún no está registrado, ejecute [sp_registercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) en el distribuidor. Especifique un nombre para el solucionador en **@article_resolver** ; para un controlador de lógica de negocios, éste es el nombre descriptivo del ensamblado. Para los solucionadores basados en COM, especifique el CLSID de la DLL para **@resolver_clsid** y para un controlador de lógica de negocios, especifique el valor **true** para **@is_dotnet_assembly** , el nombre del ensamblado para **@dotnet_assembly_name** y el nombre completo de la clase que invalida <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para **@dotnet_class_name** .  
  
    > [!NOTE]  
    >  Si no hay implementado un ensamblado de controlador de lógica de negocios en el mismo directorio que la aplicación ejecutable de Combinación Agente, en el mismo directorio que la aplicación que inicia el Agente de mezcla de forma sincrónica, o en la caché de ensamblados global (GAC), debe especificar la ruta de acceso completa con el nombre del ensamblado para **@dotnet_assembly_name** .  
  
4.  Si el solucionador es un solucionador basado en COM:  
  
    -   Copie la DLL del solucionador personalizado en el distribuidor para la suscripción de inserción o en el suscriptor para las suscripciones de extracción.  
  
        > [!NOTE]  
        >  Los solucionadores personalizados de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] se encuentran en el directorio [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
    -   Utilice regsvr32.exe para registrar la DLL del solucionador personalizado con el sistema operativo. Por ejemplo, al ejecutar lo siguiente desde el símbolo del sistema se registra el solucionador de conflictos de suma de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  Si el solucionador es un controlador de lógica de negocios, implemente el ensamblado en la misma carpeta que la aplicación ejecutable del Agente de mezcla (replmerg.exe), en la misma carpeta que la aplicación que invoca el Agente de mezcla o en la carpeta especificada para el parámetro **@dotnet_assembly_name** del paso 3.  
  
    > [!NOTE]  
    >  La ubicación de instalación predeterminada de la aplicación ejecutable de Agente de mezcla es [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
## <a name="specify-a-custom-resolver-when-defining-a-merge-article"></a>Especificación de un solucionador personalizado al definir un artículo de mezcla  
  
1.  Si tiene previsto utilizar un solucionador de conflictos personalizado, cree y registre el solucionador mediante el procedimiento anterior.  
  
2.  En el publicador, ejecute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) y tenga en cuenta el nombre del solucionador personalizado deseado en el campo **value** del conjunto de resultados.  
  
3.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique el nombre del solucionador del paso 2 para **@article_resolver** y cualquier entrada necesaria para el solucionador personalizado utilizando el parámetro **@resolver_info** . Para los solucionadores personalizados basados en un procedimiento almacenado, **@resolver_info** es el nombre del procedimiento almacenado. Para más información sobre la entrada requerida por solucionadores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)], vea [Solucionadores basados en Microsoft COM](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
## <a name="specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>Especificación o cambio de un solucionador personalizado para un artículo de mezcla existente  
  
1.  Para determinar si se ha definido un solucionador personalizado para un artículo u obtener el nombre del solucionador, ejecute [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Si hay un solucionador personalizado definido para el artículo, su nombre se mostrará en el campo **article_resolver** . Cualquier entrada proporcionada al solucionador se mostrará en el campo **resolver_info** del conjunto de resultados.  
  
2.  En el publicador, ejecute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) y tenga en cuenta el nombre del solucionador personalizado deseado en el campo **value** del conjunto de resultados.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique el valor **article_resolver**, incluso la ruta de acceso completa para los controladores de lógica de negocios, para **@property** y el nombre del solucionador personalizado deseado del paso 2 para **@value** .  
  
4.  Para cambiar alguna entrada necesaria para el solucionador personalizado, ejecute de nuevo [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique el valor **resolver_info** para **@property** y cualquier entrada necesaria para el solucionador personalizado para **@value** . Para los solucionadores personalizados basados en un procedimiento almacenado, **@resolver_info** es el nombre del procedimiento almacenado. Para más información sobre la entrada requerida, vea [Solucionadores basados en Microsoft COM](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
## <a name="unregister-a-custom-conflict-resolver"></a>Eliminación del registro de un solucionador de conflictos personalizado  
  
1.  En el publicador, ejecute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) y tenga en cuenta el nombre del solucionador personalizado para quitar en el campo **value** del conjunto de resultados.  
  
2.  Ejecute [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) en el distribuidor. Especifique el nombre completo del solucionador personalizado del paso 1 para **@article_resolver** .  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 En este ejemplo se crea un nuevo artículo y se especifica que se utilice el Solucionador de conflictos de cálculo de media de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para calcular la media de la columna **UnitPrice** cuando se produzcan conflictos.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 Este ejemplo cambia un artículo para especificar que se use el Solucionador de conflictos de suma de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el fin de calcular la suma de la columna **UnitsOnOrder** cuando se produzcan conflictos.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## <a name="see-also"></a>Consulte también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
