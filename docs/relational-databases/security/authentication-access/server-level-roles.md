---
title: Roles de nivel de servidor | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.Security.NT_AUTHORITY.SYSTEM
- sql13.Security.BUILTIN.administrators
helpviewer_keywords:
- roles [SQL Server], server-level
- principals [SQL Server], server-level
- CONTROL SERVER permission
- fixed server roles [SQL Server]
- credentials [SQL Server], roles
- sysadmin fixed server role
- server-level roles [SQL Server]
- authentication [SQL Server], roles
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 239e2d3f2475738044e4c3644f734fdbb6a0eafb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116788"
---
# <a name="server-level-roles"></a>Roles de nivel de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md](../../../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona roles de nivel de servidor para ayudarle a administrar los permisos de un servidor. Estos roles son entidades de seguridad que agrupan otras entidades de seguridad. Los roles de nivel de servidor se aplican a todo el servidor en lo que respecta a su ámbito de permisos. (Los*roles* son como los *grupos* del sistema operativo Windows).  
  
 Los roles fijos de servidor se proporcionan por comodidad y compatibilidad con versiones anteriores. Siempre que sea posible, asigne permisos más específicos.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona nueve roles fijos de servidor. Los permisos que se conceden a los roles fijos de servidor (a excepción de **public**) no se pueden modificar. A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], puede crear roles de servidor definidos por el usuario y agregarles permisos de nivel de servidor.  
  
 Puede agregar entidades de seguridad de nivel de servidor (inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], cuentas de Windows y grupos de Windows) a los roles de nivel de servidor. Cada miembro de un rol fijo de servidor puede agregar otros inicios de sesión a ese mismo rol. Los miembros de roles de servidor definidos por el usuario no pueden agregar otras entidades de seguridad de servidor al rol.  
> [!NOTE]
>  Los permisos de nivel de servidor no están disponible en SQL Database ni en SQL Data Warehouse. Para más información sobre SQL Database, vea [Control y concesión de acceso a bases de datos](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).
  
## <a name="fixed-server-level-roles"></a>Roles fijos de nivel de servidor  
 En la tabla siguiente se muestran los roles fijos de nivel de servidor y sus capacidades.  
  
|Rol fijo de nivel de servidor|Descripción|  
|------------------------------|-----------------|  
|**sysadmin**|Los miembros del rol fijo de servidor **sysadmin** pueden realizar cualquier actividad en el servidor.|  
|**serveradmin**|Los miembros del rol fijo de servidor **serveradmin** pueden cambiar opciones de configuración en el servidor y cerrar el servidor.|  
|**securityadmin**|Los miembros del rol fijo de servidor **securityadmin** administran los inicios de sesión y sus propiedades. Pueden administrar los permisos de nivel de servidor `GRANT`, `DENY`, y `REVOKE`. También pueden administrar los permisos de nivel de base de datos `GRANT`, `DENY` y `REVOKE` si tienen acceso a una base de datos. Asimismo, pueden restablecer contraseñas para inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> **IMPORTANTE:** La capacidad de conceder acceso a [!INCLUDE[ssDE](../../../includes/ssde-md.md)] y configurar los permisos de usuario permite que el administrador de seguridad asigne la mayoría de los permisos de servidor. El rol **securityadmin** se debe tratar como equivalente al rol **sysadmin** .|  
|**processadmin**|Los miembros del rol fijo de servidor **processadmin** pueden finalizar los procesos que se ejecutan en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**setupadmin**|Los miembros del rol fijo de servidor **setupadmin** pueden agregar y quitar servidores vinculados mediante instrucciones de [!INCLUDE[tsql](../../../includes/tsql-md.md)]. (Es necesaria la pertenencia a **sysadmin** cuando se usa [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]).|  
|**bulkadmin**|Los miembros del rol fijo de servidor **bulkadmin** pueden ejecutar la instrucción `BULK INSERT`.|  
|**diskadmin**|El rol fijo de servidor **diskadmin** se usa para administrar archivos de disco.|  
|**dbcreator**|Los miembros del rol fijo de servidor **dbcreator** pueden crear, modificar, quitar y restaurar cualquier base de datos.|  
|**public**|Cada inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pertenece al rol de servidor **public**. Cuando a una entidad de seguridad de servidor no se le han concedido ni denegado permisos específicos para un objeto protegible, el usuario hereda los permisos concedidos al rol pública para ese elemento. Solo asigne los permisos públicos en cualquier objeto cuando desee que el objeto esté disponible para todos los usuarios. No puede cambiar la pertenencia en public.<br /><br /> **Nota:** El rol **public** se implementa de manera diferente que otros roles y los permisos se pueden conceder, denegar o revocar de los roles fijos de servidor públicos.|  
  
## <a name="permissions-of-fixed-server-roles"></a>Permisos de los roles fijos de servidor  
 Cada rol fijo de servidor cuenta con diversos permisos asignados. El gráfico siguiente muestra los permisos asignados a los roles de servidor.   
![fixed_server_role_permissions](../../../relational-databases/security/authentication-access/media/permissions-of-server-roles.png)   
  
> [!IMPORTANT]  
>  El permiso **CONTROL SERVER** es similar, pero no idéntico al rol fijo de servidor **sysadmin** . Los permisos no conllevan la pertenencia a los roles y la pertenencia a los roles no otorga permisos. (Por ejemplo, **CONTROL SERVER** no implica la pertenencia al rol fijo de servidor. **sysadmin**). Sin embargo, en ocasiones, es posible hacer suplantaciones entre roles y permisos equivalentes. La mayoría de los comandos **DBCC** y muchos procedimientos del sistema necesitan pertenencia al rol fijo de servidor **sysadmin** . Para obtener una lista de 171 procedimientos almacenados del sistema que requieren la pertenencia a **sysadmin** , vea la siguiente publicación del blog de Andreas Wolter [CONTROL SERVER vs. sysadmin/sa: permissions, system procedures, DBCC, automatic schema creation and privilege escalation - caveats (CONTROL SERVER frente a administradores del sistema: permisos, procedimientos del sistema, DBCC, creación automática de esquemas y escalación de privilegios - advertencias)](http://andreas-wolter.com/en/control-server-vs-sysadmin-sa/).  
  
## <a name="server-level-permissions"></a>Permisos de nivel de servidor  
 Solo se pueden agregar a los roles de servidor definidos por el usuario los permisos de nivel de servidor. Para obtener una lista de los permisos en el nivel de servidor, ejecute la siguiente instrucción: Los permisos en el nivel de servidor son:  
  
```  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 Para obtener más información sobre los permisos, vea [Permisos &#40;motor de base de datos&#41;](../../../relational-databases/security/permissions-database-engine.md) y [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md).  
  
## <a name="working-with-server-level-roles"></a>Trabajar con roles de nivel de servidor  
 En la tabla siguiente se explican los comandos, las vistas y las funciones que se pueden utilizar para trabajar con roles de nivel de servidor.  
  
|Característica|Tipo|Descripción|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)|Metadatos|Devuelve una lista de roles de nivel de servidor.|  
|[sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)|Metadatos|Devuelve información acerca de los miembros de un rol de nivel de servidor.|  
|[sp_srvrolepermission &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)|Metadatos|Muestra los permisos de un rol de nivel de servidor.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|Metadatos|Indica si un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es miembro del rol de nivel de servidor especificado.|  
|[sys.server_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)|Metadatos|Devuelve una fila por cada miembro de cada rol de nivel de servidor.|  
|[sp_addsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)|Comando|Agrega un inicio de sesión como miembro de un rol de nivel de servidor. Obsoleto. Utilice [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md) en su lugar.|  
|[sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)|Comando|Quita un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o un usuario o grupo de Windows de un rol de nivel de servidor. Obsoleto. Utilice [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md) en su lugar.|  
|[CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-role-transact-sql.md)|Comando|Crea un rol de servidor definido por el usuario.|  
|[ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md)|Comando|Cambia la pertenencia de un rol de servidor o cambia el nombre de un rol de servidor definido por el usuario.|  
|[DROP SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-role-transact-sql.md)|Comando|Quita un rol de servidor definido por el usuario.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|Función|Determina la pertenencia del rol de servidor.|  
  
## <a name="see-also"></a>Consulte también  
 [Roles de nivel de base de datos](../../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)   
 [Proteger SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [GRANT &#40;permisos de entidad de seguridad de servidor de Transact-SQL&#41;](../../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [REVOKE &#40;permisos de entidad de seguridad de servidor de Transact-SQL&#41;](../../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [DENY &#40;permisos de entidad de seguridad de servidor de Transact-SQL&#41;](../../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [Crear un rol de servidor](../../../relational-databases/security/authentication-access/create-a-server-role.md)  
  
  
