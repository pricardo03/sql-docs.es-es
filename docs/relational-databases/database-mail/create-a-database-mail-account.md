---
title: Creación de una nueva cuenta de Correo electrónico de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], accounts
- accounts [Database Mail]
ms.assetid: c07abbc6-fc6a-470b-8fa3-532f2e06b16a
author: stevestein
ms.author: sstein
ms.openlocfilehash: a31f23d4de02bd4554d997364a3a5aa26b3d4ef3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134491"
---
# <a name="create-a-database-mail-account"></a>Crear una nueva cuenta de Correo electrónico de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use el **Asistente para configuración de Correo electrónico de base de datos** o [!INCLUDE[tsql](../../includes/tsql-md.md)] para crear una cuenta de Correo electrónico de base de datos.  
  
-   **Antes de empezar:**  [Requisitos previos](#Prerequisites)  
  
-   **Para crear una cuenta de Correo electrónico de base de datos, mediante:**  [Asistente para configuración de Correo electrónico de base de datos](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [pasos siguientes para configurar el Correo electrónico de base de datos](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Determine el nombre y el número de puerto del servidor de Protocolo simple de transferencia de correo (SMTP) que usa para enviar correo electrónico. Si el SMTP precisa autenticación, determine el nombre de usuario y la contraseña para el servidor SMTP.  
  
-   Opcionalmente, también puede especificar el tipo de servidor y el número de puerto del servidor. El tipo de servidor siempre es 'SMTP' para el correo saliente. La mayoría de los servidores SMTP usan el puerto 25, es decir, el puerto predeterminado.  
  
##  <a name="SSMSProcedure"></a> Usar el asistente para configuración del Correo electrónico de base de datos  
 **Para crear una cuenta de Correo electrónico de base de datos mediante un asistente**  
  
-   En el explorador de objetos, conecte a la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que quiera configurar el Correo electrónico de base de datos y expanda el árbol del servidor.  
  
-   Expanda el nodo **Administración** .  
  
-   Haga doble clic en el Correo electrónico de base de datos para abrir el asistente de configuración del Correo electrónico de base de datos.  
  
-   En la página de **Seleccionar tarea de configuración** , seleccione **Administrar cuentas y perfiles de Correo electrónico de base de datos**, haga clic en **Siguiente**.  
  
-   En la página de **Administrar perfiles y cuentas** , seleccione **Crear una nueva cuenta** y haga clic **Siguiente**.  
  
-   En la página de **Nueva cuenta** , especifique el nombre de cuenta, la descripción, la información del servidor de correo, y el tipo de autenticación. Haga clic en **Siguiente**.  
  
-   En la página de **Finalización del asistente** , revise las acciones que realizará y haga clic en **Finalizar** para completar crear la nueva cuenta.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para crear una cuenta de Correo electrónico de base de datos mediante Transact-SQL**  
  
 Ejecute el procedimiento almacenado **msdb.dbo.sysmail_add_account_sp** para crear la cuenta, especificando:  
  
-   El nombre de la cuenta que va a crear.  
  
-   Una descripción opcional de la cuenta.  
  
-   La dirección de correo electrónico que se muestra en los mensajes de correo electrónico salientes.  
  
-   El nombre para mostrar que se muestra en los mensajes de correo electrónico salientes.  
  
-   El nombre de servidor del servidor SMTP.  
  
-   El nombre de usuario que se utiliza para iniciar sesión en el servidor SMTP, si el servidor SMTP requiere autenticación.  
  
-   La contraseña que se usa para iniciar sesión en el servidor SMTP, si el servidor SMTP requiere autenticación.  
  
 En el ejemplo siguiente se crea una nueva cuenta de Correo electrónico de base de datos.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
##  <a name="FollowUp"></a> Seguimiento: pasos siguientes para configurar el Correo electrónico de base de datos  
  
-   [Crear un perfil de Correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-profile.md)  
  
  
