---
title: Eliminar uno o más trabajos | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, deleting
- dropping jobs
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 67dcdad0-57b2-431c-b77f-4ffc926af93d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e777fc76a49e7d4ec645133808787e25a702348f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62523513"
---
# <a name="delete-one-or-more-jobs"></a>Eliminar uno o más trabajos
  En este tema se describe cómo eliminar trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server.  
  
 
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
 Solo podrá eliminar los trabajos que posea, a menos que sea miembro del rol fijo de servidor **sysadmin** .  
  
 
  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
  
#### <a name="to-delete-a-job"></a>Para eliminar un trabajo  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Expanda **Agente SQL Server**, expanda **Trabajos**, haga clic con el botón derecho en el trabajo que desee eliminar y haga clic en **Eliminar**.  
  
3.  En el cuadro de diálogo **Eliminar objeto** , confirme que el trabajo que desea eliminar está seleccionado.  
  
4.  Haga clic en **Aceptar**.  
  
#### <a name="to-delete-multiple-jobs"></a>Para eliminar varios trabajos  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Expanda **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en **Monitor de actividad de trabajo**y haga clic en **Ver actividad de trabajo**.  
  
4.  En Monitor de actividad de trabajo, seleccione los trabajos que desee eliminar, haga clic con el botón derecho en la selección y, luego, elija **Eliminar trabajos**.  
  

  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-delete-a-job"></a>Para eliminar un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_job  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_delete_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql).  
  

  
##  <a name="SMO"></a> Usar objetos de administración de SQL Server  
 **Para eliminar varios trabajos**  
  
 Utilice la clase `JobCollection` mediante un lenguaje de programación que elija, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  

  
  
