---
title: Creación de una auditoría de servidor y una especificación de auditoría de servidor, utilizando | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.SQLAUDIT.FILTER.F1
- sql12.swb.sqlaudit.srvaudit.general.f1
- sql12.swb.sqlaudit.general.f1
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
ms.assetid: 6624b1ab-7ec8-44ce-8292-397edf644394
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ec1c7205597224e5fca27942ca25ad4e197ec0d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198413"
---
# <a name="create-a-server-audit-and-server-audit-specification"></a>Crear una auditoría de servidor y una especificación de auditoría de servidor
  En este tema se describe cómo crear una auditoría de servidor y una especificación de auditoría de servidor en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. La*auditoría* de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] implica el seguimiento y registro de los eventos que se producen en el sistema. El objeto *SQL Server Audit* recopila una única instancia de acciones y grupos de acciones de nivel de servidor o de base de datos para su supervisión. La auditoría se realiza en el nivel de instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Es posible tener varias auditorías por cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . El objeto *Especificación de auditoría de servidor* pertenece a una auditoría. Puede crear una especificación de auditoría de servidor por cada auditoría, ya que ambos se crean en el ámbito de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](sql-server-audit-database-engine.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear una auditoría de servidor y una especificación de auditoría de servidor, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Para poder crear una especificación de auditoría de servidor, debe existir la auditoría. Cuando se crea una especificación de auditoría de servidor, está en estado deshabilitado.  
  
-   La instrucción CREATE SERVER AUDIT está en el ámbito de una transacción. Si se revierte la transacción, también se revierte la instrucción.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
  
-   Para crear, modificar o quitar una auditoría de servidor, las entidades de seguridad deben tener el permiso ALTER ANY SERVER AUDIT o CONTROL SERVER.  
  
-   Los usuarios con el permiso ALTER ANY SERVER AUDIT pueden crear especificaciones de auditoría de servidor y enlazarlas a cualquier auditoría.  
  
-   Una vez creada una especificación de auditoría de servidor, las entidades de seguridad que cuenten con los permisos CONTROL SERVER o ALTER ANY SERVER AUDIT, así como la cuenta sysadmin, o las entidades de seguridad que tengan acceso explícito a la auditoría podrán ver dicha especificación.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>Para crear una auditoría de servidor  
  
1.  En el Explorador de objetos, expanda la carpeta **Seguridad** .  
  
2.  Haga clic con el botón derecho en la carpeta **Auditorías** y, después, seleccione **Nueva auditoría...** .  
  
     Las siguientes opciones están disponibles en la página **General** del cuadro de diálogo **Crear auditoría** .  
  
     **Nombre de auditoría**  
     Nombre de la auditoría. Se genera automáticamente al crear una nueva auditoría, pero se puede modificar.  
  
     **Retardo de cola (en milisegundos)**  
     Especifica la cantidad de tiempo, en milisegundos, que puede transcurrir antes de exigir que se procesen las acciones de auditoría.  El valor 0 indica la entrega sincrónica. El valor mínimo predeterminado es **1000** (1 segundo). El máximo es 2.147.483.647 (2.147.483,647 segundos, o 24 días, 20 horas, 31 minutos y 23,647 segundos).  
  
     **Si hay un error de registro de auditoría:**  
     **Continuar**  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Las operaciones de  continúan. Los registros de auditoría no se conservan. La auditoría continúa intentando el registro de eventos y se reanudará si se resuelve la condición de error. La selección de la opción **Continuar** puede permitir que una actividad no se audite, con lo que se infringirían las directivas de seguridad. Seleccione esta opción cuando la operación de continuación del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] sea más importante que el mantenimiento de una auditoría completa. Esta es la selección predeterminada.  
  
     **Apagar el servidor**  
     Fuerza el apagado del servidor cuando la instancia de servidor que escribe en el destino no puede escribir datos en el destino de la auditoría. Para poder usarlo, es preciso utilizar un inicio de sesión con el permiso `SHUTDOWN`. Si el inicio de sesión no tiene dicho permiso, la función generará un error y se mostrará un mensaje de error. No se producirán eventos auditados. Seleccione esta opción si un error de auditoría puede poner en peligro la seguridad o la integridad del sistema.  
  
     **Error en la operación**  
     En los casos en que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit no puede escribir en el registro de auditoría, esta opción haría que las acciones de base de datos produjesen un error si generasen eventos auditados. No se producirán eventos auditados. Las acciones que no producen eventos auditados pueden continuar. La auditoría continúa intentando el registro de eventos y se reanudará si se resuelve la condición de error. Seleccione esta opción si el mantenimiento de una auditoría completa es más importante que el acceso total al [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
    > [!IMPORTANT]  
    >  Cuando la auditoría está en un estado de error, la conexión de administrador dedicada puede seguir realizando eventos auditados.  
  
     Lista**Destino de auditoría**  
     Especifica el destino de los datos de la auditoría. Las opciones disponibles son un archivo binario, el registro de aplicación Windows o el registro de seguridad de Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no puede escribir en el registro de seguridad de Windows sin configurar valores adicionales en Windows. Para obtener más información, vea [Escribir eventos de auditoría de SQL Server en el registro de seguridad](write-sql-server-audit-events-to-the-security-log.md).  
  
     **Ruta del archivo**  
     Especifica la ubicación de la carpeta donde se escriben los datos de la auditoría si se ha especificado un archivo **Destino de auditoría** .  
  
     **Puntos suspensivos (...)**  
     Se abre el **Buscar carpeta -** _nombre_servidor_ cuadro de diálogo para especificar una ruta de acceso de archivo o crear una carpeta donde se escribirá el archivo de auditoría.  
  
     **Límite máximo del archivo de auditoría:**  
     **Máximo de archivos de sustitución incremental**  
     Especifica que, si se alcanza el número máximo de archivos de auditoría, el contenido de los nuevos archivos reemplazará a los archivos de auditoría más antiguos.  
  
     **Número máximo de archivos**  
     Especifica que, si se alcanza el número máximo de archivos de auditoría, cualquier acción que ocasione la generación de eventos de auditoría adicionales producirá un error y se mostrará un mensaje.  
  
     Casilla**Ilimitado**  
     Cuando se activa la casilla **Ilimitado** en **Máximo de archivos de sustitución incremental** , no se impone ningún límite en cuanto al número de archivos de auditoría que se crearán. La casilla **Ilimitado** está activada de forma predeterminada y se aplica a las selecciones de **Máximo de archivos de sustitución incremental** y **Máximo de archivos** .  
  
     Casilla**Número de archivos**  
     Especifica el número de archivos de auditoría que se crearán, hasta 2.147.483.647. Esta opción solo está disponible si se desactiva la casilla **Ilimitado** .  
  
     **Tamaño máximo del archivo**  
     Especifica el tamaño máximo de un archivo de auditoría en megabytes (MB), gigabytes (GB) o terabytes (TB). Puede especificar entre 1024 MB y 2.147.483.647 TB. La activación de la casilla **Ilimitado** no pone un límite en el tamaño del archivo. La especificación de un valor inferior a 1024 MB producirá y devolverá un error. La casilla **Ilimitado** está activada de forma predeterminada.  
  
     Casilla**Reservar espacio en disco**  
     Especifica que se debe preasignar una cantidad de espacio en disco igual al tamaño máximo de archivo especificado. Este valor solo se puede utilizar si la casilla **Ilimitado** en **Tamaño máximo del archivo** no está activada. Esta casilla no está activada de forma predeterminada.  
  
3.  Opcionalmente, en la página **Filtrar** , escriba un predicado, o la cláusula `WHERE` , para la auditoría de servidor de modo que se especifiquen opciones adicionales no disponibles en la página **General** . Encierre el predicado entre paréntesis; por ejemplo: `(object_name = 'EmployeesTable')`.  
  
4.  Cuando termine de seleccionar opciones, haga clic en **Aceptar**.  
  
#### <a name="to-create-a-server-audit-specification"></a>Para crear una especificación de auditoría de servidor  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la carpeta **Seguridad** .  
  
2.  Haga clic con el botón derecho en la carpeta **Especificaciones de auditoría de servidor** y seleccione **Nueva especificación de auditoría de base de servidor...** .  
  
     Las siguientes opciones están disponibles en el cuadro de diálogo **Crear especificación de auditoría de servidor** .  
  
     **Name**  
     El nombre de la especificación de auditoría de servidor. Se genera automáticamente al crear una nueva especificación de auditoría de servidor, pero se puede modificar.  
  
     **Auditar**  
     Nombre de una auditoría de servidor existente. Escriba el nombre de la auditoría o selecciónelo en la lista.  
  
     **Tipo de acción de auditoría**  
     Especifica los grupos de acciones de auditoría y las acciones de auditoría en el nivel de servidor que se desea capturar. Para obtener la lista de grupos de acciones de auditoría y de acciones de auditoría de nivel de servidor, así como una descripción de los eventos que contienen, vea [Grupos de acciones y acciones de SQL Server Audit](sql-server-audit-action-groups-and-actions.md).  
  
     **Esquema de objeto**  
     Muestra el esquema para el **Nombre de objeto**especificado.  
  
     **Nombre de objeto**  
     Nombre del objeto que se va a auditar. Este valor solo está disponible para las acciones de auditoría, no se aplica a los grupos de auditoría.  
  
     **Puntos suspensivos (...)**  
     Abre el cuadro de diálogo **Seleccionar objetos** para buscar y seleccionar un objeto disponible, basándose en el **Tipo de acción de auditoría**especificado.  
  
     **Nombre de la entidad**  
     La cuenta por la que se va filtrar la auditoría para el objeto que se va a auditar.  
  
     **Puntos suspensivos (...)**  
     Abre el cuadro de diálogo **Seleccionar objetos** para buscar y seleccionar un objeto disponible, basándose en el **Nombre de objeto**especificado.  
  
3.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>Para crear una auditoría de servidor  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Creates a server audit called "HIPAA_Audit" with a binary file as the target and no options.  
    CREATE SERVER AUDIT HIPAA_Audit  
        TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
    ```  
  
#### <a name="to-create-a-server-audit-specification"></a>Para crear una especificación de auditoría de servidor  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    /*Creates a server audit specification called "HIPAA_Audit_Specification" that audits failed logins for the SQL Server audit "HIPAA_Audit" created above.  
    */  
  
    CREATE SERVER AUDIT SPECIFICATION HIPAA_Audit_Specification  
    FOR SERVER AUDIT HIPAA_Audit  
        ADD (FAILED_LOGIN_GROUP);  
    GO  
    -- Enables the audit.   
  
    ALTER SERVER AUDIT HIPAA_Audit  
    WITH (STATE = ON);  
    GO  
    ```  
  
 Para obtener más información, vea [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql) y [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-specification-transact-sql).  
  
  
