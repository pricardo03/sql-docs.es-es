---
title: Ver el registro de errores del Agente SQL Server (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- viewing SQL Server Agent error logs
- displaying SQL Server Agent error logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: de920425-fa44-469f-b83d-49e3f97e97f4
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d4e5b42cb1d38ed771bde353d8df5f18dbeca1c4
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266981"
---
# <a name="view-sql-server-agent-error-log-sql-server-management-studio"></a>View SQL Server Agent Error Log (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe el modo de ver el registro de errores del Agente  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
El Visor de archivos de registro muestra información de registro de muchos componentes diferentes. Cuando el Visor del archivo de registros esté abierto, utilice el panel **Seleccionar registros** para seleccionar los registros que desea que se muestren. Cada registro muestra las columnas apropiadas a ese tipo de registro. La disponibilidad de los registros dependerá del modo en que se abra el Visor del archivo de registros.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   [Para ver el registro de errores del Agente SQL Server utilizando SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se tiene permiso para usarlo.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-view-the-includessnoversionincludesssnoversion-mdmd-agent-error-log"></a>Para ver el registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene el registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyo nombre desea ver.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Registros de errores** .  
  
4.  Haga clic con el botón derecho en el registro de errores que desea ver y seleccione **Ver registro del agente**.  
  
    Las opciones siguientes están disponibles en el cuadro de diálogo **Visor de archivos de registro -** _nombre_de_servidor_:  
  
    **Cargar registro**  
    Abre un cuadro de diálogo donde puede especificar un archivo de registro para cargar.  
  
    **Exportar**  
    Abre un cuadro de diálogo que permite exportar la información que se muestra en la cuadrícula **Resumen de archivos de registro** a un archivo de texto.  
  
    **Actualizar**  
    Actualice la vista de los registros seleccionados. El botón **Actualizar** hace que se vuelvan a leer los registros seleccionados del servidor de destino al tiempo que se aplica una configuración de filtro.  
  
    **Filtro**  
    Abre un cuadro de diálogo que permite especificar la configuración que se usa para filtrar el archivo de registro, como **Conexión**, **Fecha**u otros criterios de filtro de **General** .  
  
    **Buscar**  
    Permite buscar texto específico en el archivo de registro. No se admite la búsqueda con caracteres comodín.  
  
    **Detener**  
    Detiene la carga de las entradas del archivo de registro. Por ejemplo, puede utilizar esta opción si la carga de un archivo de registro remoto o sin conexión tarda mucho tiempo y solo desea ver las entradas más recientes.  
  
    **Resumen de archivos de registro**  
    Este panel de información muestra un resumen del filtro del archivo de registro. Si no se ha filtrado el archivo, se mostrará el siguiente texto: **No se aplicó ningún filtro**. Si se aplicó un filtro al registro, se mostrará el texto **Filtrar entradas del registro en:** <filter criteria>.  
  
    **Detalles de las filas seleccionadas**  
    Seleccione una fila para mostrar detalles adicionales sobre la fila de evento seleccionada en la parte inferior de la página. Puede ordenar de nuevo las columnas arrastrándolas a nuevas ubicaciones de la cuadrícula. Puede modificar el tamaño de las columnas arrastrando las barras de separación de las columnas del encabezado de la cuadrícula hacia la izquierda o hacia la derecha. Haga doble clic en las barras de separación de las columnas del encabezado de la cuadrícula para ajustar automáticamente el tamaño de la columna al ancho del contenido.  
  
    **Instancia**  
    Nombre de la instancia en que se produjo el evento. Esto se muestra como *nombre de equipo*\\*nombre de instancia*.  
  
    **Date**  
    Muestra la fecha del evento.  
  
    **Source**  
    Muestra la característica de origen desde la que se crea el evento, como el nombre del servicio (MSSQLSERVER, por ejemplo). No aparece para todos los tipos de registro.  
  
    **de mensaje**  
    Muestra todos los mensajes asociados al evento.  
  
    **Tipo de registro**  
    Muestra el tipo de registro al que pertenece el evento. Todos los registros seleccionados aparecen en la ventana de resumen del archivo de registro.  
  
    **Origen del registro**  
    Muestra una descripción del registro de origen en el que se captura el evento.  
  
5.  Cuando termine, haga clic en **Cerrar**.  
  
