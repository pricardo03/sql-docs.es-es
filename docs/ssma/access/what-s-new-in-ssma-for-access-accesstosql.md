---
title: Novedades de SSMA para Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/31/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 39f8d7da95fc8e2102d1208216a2eb43bb038fea
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "68632070"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Novedades de SSMA para Access (AccessToSQL)

En este artículo se enumeran SQL Server Migration Assistant (SSMA) para obtener acceso a los cambios en cada versión.  

## <a name="ssma-v83"></a>SSMA v 8.3

La publicación v 8.3 de SSMA para el acceso se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión de SSMA para Access proporciona correcciones que:

* Solucionar problemas de accesibilidad
* Agregar compatibilidad básica para el tipo ' hierarchyid ' en SQL Server

> [!IMPORTANT]
> Con SSMA v 7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v82"></a>SSMA v 8.2

La versión v 8.2 de SSMA para Access se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir un error en una actualización de SSMA v 8.1 a v 8.2. Si se produce este error, descargue la nueva versión e instálela manualmente.

> [!IMPORTANT]
> Con SSMA v 7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v81"></a>SSMA v 8.1

La versión v 8.1 de SSMA para Access se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir un error en una actualización de SSMA v 8.0 a v 8.1. Si se produce este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v80"></a>SSMA v 8.0

La versión v 8.0 de SSMA para Access se ha mejorado con las correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **instancia administrada de Azure SQL Database** como destino. Ahora puede crear nuevos proyectos que tengan como destino Instancia administrada de Azure SQL Database:

  ![Proyecto de MI de base de SQL](../media/ssma-newproject-sqldbmi.png)

* **Asesor de corrección**posterior a la conversión. Obtenga más información [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección preliminar de base de datos/esquema.

    Al conectarse al origen, el usuario puede seleccionar las bases de datos o los esquemas de interés. Si selecciona solo los esquemas que va a migrar, se ahorrará tiempo durante la conexión inicial y se mejorará el rendimiento global de SSMA.

   ![SSMA (objetos de filtro)](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

La versión v 7.10 de SSMA para Access se ha mejorado con las correcciones de destino diseñadas para proporcionar protección adicional de seguridad y privacidad para satisfacer los cambios en los requisitos globales.

## <a name="ssma-v79"></a>SSMA v 7.9

La versión v 7.9 de SSMA para Access contiene los siguientes cambios:

* Correcciones dirigidas que mejoran las métricas de calidad y conversión.
* Compatibilidad en la línea de comandos de SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* También se ha modificado el cuadro de diálogo de conexión Azure SQL Database en SSMA para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo Azure SQL Database tenía que mencionarse explícitamente dentro de la configuración de los proyectos.

## <a name="ssma-v78"></a>SSMA v 7.8

La versión v 7.8 de SSMA para Access contiene los cambios siguientes:

* Cambiar la asignación de tipos resaltada en la configuración del proyecto.
* La capacidad de los usuarios de deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v 7.7

La versión v 7.7 de SSMA para Access contiene los siguientes cambios:

* Correcciones dirigidas que mejoran las métricas de calidad y conversión.
* En función de la demanda popular, se vuelve a la versión de 32 bits de SSMA para Access. En comparación con la implementación anterior (antes de v 7.4), hay dos paquetes de instalador, pero no se pueden instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tenga. Siempre es preferible usar la versión de 64 bits, si es posible.

## <a name="ssma-v76"></a>SSMA v 7.6

La versión v 7.6 de SSMA para Access se ha mejorado con correcciones de destino que mejoran las métricas de calidad y conversión y admiten SQL Server 2017 (versión preliminar pública). La compatibilidad con SQL Server 2017 en Windows y Linux está en versión preliminar pública y no debe usarse para migraciones de producción.

## <a name="ssma-v75"></a>SSMA v 7.5

La versión v 7.5 de SSMA para Access se ha mejorado con varias mejoras para garantizar una mayor accesibilidad para las personas con discapacidades.

## <a name="ssma-v74"></a>SSMA v 7.4

La versión v 7.4 de SSMA para Access contiene los siguientes cambios:

* La opción **tiempo de espera de consulta** ahora está disponible durante la detección de objetos de esquema en el origen y el destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

* La métrica de calidad y conversión se ha mejorado con las correcciones de destino, en función de los comentarios de los clientes.

  > [!IMPORTANT]
  > .Net 4.5.2 es un requisito previo para instalar SSMA v 7.4. Además, a partir de v 7.4, se ha interrumpido la versión de 32 bits de SSMA.

## <a name="ssma-v73"></a>SSMA v 7.3

La versión v 7.3 de SSMA para Access contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones de destino basadas en los comentarios de los clientes.
* El marco de extensibilidad de SSMA expuesto a través de los siguientes elementos:
  * Exportar funcionalidad a un proyecto SQL Server Data Tools (SSDT).
    * Ahora puede exportar scripts de esquema de SSMA a un proyecto de SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicionales e implementar la base de datos.

        ![Comando Guardar como proyecto de SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que puede usar SSMA para realizar conversiones personalizadas.
    * Ahora puede construir código que pueda controlar las conversiones de sintaxis personalizadas y las conversiones que no se administraron previamente mediante SSMA.
      * En esta entrada de blog se ofrecen instrucciones sobre cómo construir un convertidor personalizado, que amplían las [capacidades de conversión de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Descargue un proyecto de ejemplo para la conversión de esta [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v 7.2

La versión v 7.2 de SSMA para Access contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones de destino basadas en los comentarios de los clientes.
* Mejoras en la telemetría para proporcionar mejores puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v 7.1

La versión v 7.1 de SSMA para Access contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 es ahora una plataforma de destino admitida para la migración. Esta característica se encuentra en Technical Preview y admite el movimiento de datos y esquemas para los servidores SQL Server de destino.
* SSMA admite ahora las actualizaciones automáticas para descargar la versión más reciente de SSMA en cuanto esté disponible.
* Los binarios instalables de SSMA se entregan ahora a través de los archivos de paquete de Windows Installer (. msi).

## <a name="may-2016"></a>2016 de mayo

La versión de mayo de 2016 de SSMA para Access contiene los siguientes cambios:  
  
* Compatibilidad oficial agregada para SQL Server 2016
* Se quitó la comprobación del instalador para .net 2,0.
* Se han corregido los comandos "guardar proyecto" y "Abrir proyecto" para la consola de SSMA.
* Se corrigió el comando "securepassword" para la consola de SSMA.
* Recuento fijo de objetos para la carga inicial.
* Carga de datos de tablas fijas para pestañas de interfaz de usuario para el acceso.
* Se corrigió el error en la configuración global. 

## <a name="march-2016"></a>2016 de marzo

La versión de vista previa de marzo de 2016 de SSMA para Access agrega compatibilidad para la migración a SQL Server 2016.  

## <a name="january-2016"></a>2016 de enero

La versión de mantenimiento de enero de 2016 de SSMA para Access contiene los cambios siguientes:  
  
* Función no válida corregida para el valor predeterminado de un campo GUID (RFC 3894811).  
* Se corrigió el bloqueo en la importación de registros a SQL Database (Azure) (RFC 4919573).  
* Se ha agregado el elemento de menú Ver registro a SSMA (RFC 5706203).  
* Telemetría agregada.
  
## <a name="july-2014"></a>2014 de julio

La versión 2014 de julio de SSMA para Access contiene los cambios siguientes:  
  
* Conversión de código de Azure SQL DB mejorada.  
* Se ha cambiado la funcionalidad del paquete de extensiones al esquema para admitir Azure SQL DB.  
* Mejoras en el rendimiento de las bases de datos con más de 10 000 objetos.  
* Se han agregado mejoras de la interfaz de usuario para tratar con un gran número de objetos.  
* Se ha agregado compatibilidad con el resaltado de esquemas LOB "conocidos" (por lo que se pueden omitir en la conversión).  
* Mejoras en la velocidad de conversión agregada.
* Compatibilidad agregada para mostrar los recuentos de objetos en la interfaz de usuario.
* Menor tamaño de informe en más del 25%.
* Mensajes de error mejorados para construcciones sin analizar.  
  
## <a name="april-2014"></a>2014 de abril

La versión de abril de 2014 de SSMA para Access contiene los siguientes cambios:  
  
* Compatibilidad agregada para MS SQL Server 2014.
* Se corrigieron los errores relacionados con la conversión a Azure.  
* Se han corregido errores relacionados con las páginas del informe invisibles en IE 10.  
  
## <a name="january-2012"></a>2012 de enero

La versión 2012 de enero de SSMA para Access contiene los cambios siguientes:  
  
* Se proporciona la opción de no conservar el nombre de usuario y la contraseña para las tablas vinculadas de MS Access después de la migración.  
* Establezca acciones en cascada para las referencias circulares en ninguna acción.  
* Se proporcionan mensajes adecuados que indican que las acciones en cascada para las referencias circulares se han establecido en ninguna acción.  
  
## <a name="july-2011"></a>2011 de julio

La versión 2011 de julio de SSMA para Access agrega informes de errores mejorados durante la migración de datos.  
  
## <a name="april-2011"></a>2011 de abril

La versión de abril de 2011 de SSMA para Access contiene los siguientes cambios:  
  
* Se ha agregado una única instalación de "SSMA para Access", que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , "Denali" y Azure SQL.  
* Se ha agregado la capacidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de conectar "Denali".  
* Se ha agregado la compatibilidad con la versión de la consola de SSMA para la compatibilidad con versiones anteriores. Puede abrir los proyectos creados por versiones anteriores a SSMA v 5.0.
* Se ha agregado la capacidad de instalar el producto SSMA v 5.0 en paralelo (SxS) con versiones anteriores del producto SSMA.  
  
## <a name="july-2010"></a>2010 de julio  
La versión 2010 de julio de SSMA para Access contiene los cambios siguientes:  
  
* Compatibilidad agregada para migrar a SQL Server 2008 R2 y Azure SQL.
* Se ha agregado una conexión segura a SQL Server y Azure SQL.  
* Se ha agregado compatibilidad con las bases de datos de Access 2010.
* Se ha agregado una nueva aplicación de consola SSMA para la ejecución de la línea de comandos.
* Se ha agregado compatibilidad con el tipo de datos SQL Server DateTime2.
  
## <a name="june-2008"></a>2008 de junio

La versión 2008 de junio de SSMA para Access agrega compatibilidad con las bases de datos de Access 2007.  
  
## <a name="may-2007"></a>2007 de mayo

La versión de mayo de 2007 de SSMA para Access contiene los siguientes cambios:  
  
* Se ha agregado compatibilidad con las bases de datos de Access que usan directivas de grupo de trabajo.  
* Proporciona la capacidad de eliminar objetos convertidos desde el explorador de metadatos de SQL Server.  
* Se ha agregado compatibilidad con los comentarios escritos por el usuario en el modo SQL con formato SQL Server.  
* Mejoras agregadas en la conversión de objetos.  
  
## <a name="november-2006"></a>2006 de noviembre

La versión de noviembre de 2006 de SSMA para Access contiene los siguientes cambios:  
  
* Se ha agregado un nuevo Asistente para migración de bases de datos que le guía a través de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]migración de una única base de datos desde el acceso a.  
* Se ha agregado un nuevo comando Convert, Load y Migrate que convierte las bases de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos de Access, carga los objetos convertidos en y migra los datos en un solo paso.  
* Migración de consulta mejorada. LA migración de consultas ahora convierte más consultas SELECT en vistas. Para obtener más información, vea [convertir objetos de base de datos de Access](converting-access-database-objects-accesstosql.md).  
* Se ha agregado la capacidad de editar las propiedades de tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e índice en la pestaña **tabla** .  
* Nueva configuración global agregada:
  * Puede optar por mostrar los números de línea en las ventanas del editor.  
  * Puede configurar SSMA para que solicite reemplazar objetos duplicados, o siempre o nunca reemplazar objetos duplicados durante la conversión del esquema.  
* Se ha agregado una nueva opción de conversión que le permite especificar si SSMA muestra una advertencia cuando una consulta compleja contiene un carácter comodín.  
  
## <a name="july-2006"></a>2006 de julio

La versión de julio de 2006 de SSMA para Access fue la versión inicial.
