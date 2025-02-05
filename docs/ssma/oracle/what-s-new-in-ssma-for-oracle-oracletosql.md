---
title: Novedades de SSMA para Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/31/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: da0a047b0ae20fbc191a61e1c9eb96660eac035e
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811451"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Novedades de SSMA para Oracle (OracleToSQL)
En este artículo se enumeran los cambios SQL Server Migration Assistant (SSMA) para Oracle en cada versión.

## <a name="ssma-v83"></a>SSMA v 8.3

El lanzamiento de la versión 8.3 de SSMA para Oracle se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión de SSMA para Oracle proporciona correcciones que:

* Solucionar problemas de accesibilidad
* Agregar compatibilidad básica para el tipo ' hierarchyid ' en SQL Server
* Solucionar un problema con un tipo de valor devuelto desconocido para una función llamada a través del sinónimo
* Actualizar ODP.NET a v 19.3

> [!IMPORTANT]
> Con SSMA v 7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v82"></a>SSMA v 8.2

La versión v 8.2 de SSMA para Oracle se ha mejorado para:

* Agregar compatibilidad para DBMS_OUTPUT. HABILITAR O DESHABILITAR.
* Quite CAST como FLOAT para las columnas BINARY_FLOAT y BINARY_DOUBLE en la consulta de migración de datos predeterminada.
* Corregir secuencias actualizar si el valor actual ha cambiado.
* Corregir el error relacionado con la interpretación incorrecta de las pseudo columnas (ROWNUM, etc.) si existe una columna con el mismo nombre.
* Se ha corregido un bloqueo que se produce al convertir los bucles FOR con un identificador sin resolver ambiguo.

Además, esta versión incluye un conjunto de correcciones de destino diseñado para mejorar la calidad y las métricas de conversión, así como las correcciones para:

* Un problema con los índices no clúster deshabilitados después de la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir un error en una actualización de SSMA v 8.1 a v 8.2. Si se produce este error, descargue la nueva versión e instálela manualmente.

> [!IMPORTANT]
> Con SSMA v 7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v81"></a>SSMA v 8.1

La versión v 8.1 de SSMA para Oracle se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir un error en una actualización de SSMA v 8.0 a v 8.1. Si se produce este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v80"></a>SSMA v 8.0

La versión v 8.0 de SSMA para Oracle se ha mejorado con las correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **instancia administrada de Azure SQL Database** como destino. Ahora puede crear nuevos proyectos que tengan como destino Instancia administrada de Azure SQL Database:

  ![Proyecto de MI de base de SQL](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > SSMA para Oracle Extension Pack también se actualizó para permitir instalaciones remotas en Instancia administrada de Azure SQL Database:
  >
  > ![SSMA para Oracle Extension Pack](../media/ssma-oracle-ext-pack.png)

  Algunas características, como el evaluador y la migración de datos del lado servidor, no se admiten al establecer como destino Instancia administrada de Azure SQL Database. Obtenga más información [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/).

* **Asesor de corrección**posterior a la conversión. Obtenga más información [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección preliminar de base de datos/esquema.

  Al conectarse al origen, el usuario puede seleccionar las bases de datos o los esquemas de interés. Si selecciona solo los esquemas que va a migrar, se ahorrará tiempo durante la conexión inicial y se mejorará el rendimiento global de SSMA.

  ![SSMA (objetos de filtro)](../media/ssma-filter-objects.png)

* La capacidad de usar el controlador de red oficial administrado para conectarse a Oracle. El controlador OCI ya no es un requisito previo para usar SQL Server Migration Assistant para Oracle.

* La capacidad de asignar ROWID y UROWID a VARCHAR de forma predeterminada. Cambiado de ' uniqueidentifier ' para dar cabida a la migración de datos para columnas ROWID explícitas.

## <a name="ssma-v710"></a>SSMA v 7.10

La versión v 7.10 de SSMA para Oracle contiene los siguientes cambios:

* Soluciones de destino diseñadas para proporcionar seguridad adicional y protección de la privacidad para satisfacer los cambios en los requisitos globales.
* Mejora de la conversión relacionada con las consultas jerárquicas.

## <a name="ssma-v79"></a>SSMA v 7.9

La versión v 7.9 de SSMA para Oracle contiene los siguientes cambios:

* Correcciones dirigidas que mejoran las métricas de calidad y conversión.
* Compatibilidad para migrar instrucciones "Continue" desde Oracle a SQL Server.
* Compatibilidad en la línea de comandos de SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Compatibilidad para la migración de datos con SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante el uso de una opción del menú contextual.
* También se ha modificado el cuadro de diálogo de conexión Azure SQL Database en SSMA para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo Azure SQL Database tenía que mencionarse explícitamente dentro de la configuración de los proyectos.

## <a name="ssma-v78"></a>SSMA v 7.8

La versión v 7.8 de SSMA para Oracle contiene los siguientes cambios:

* Compatibilidad con:
  * Expresión de fila de la cláusula IN.
  * Conversiones de tipos implícitas.
  * Conversión de UID para Azure SQL Database.
* Cambiar la asignación de tipos resaltada en la configuración del proyecto.
* La capacidad de los usuarios de deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v 7.7

La versión v 7.7 de SSMA para Oracle contiene los siguientes cambios:

* SSMA para Oracle se ha mejorado con correcciones dirigidas que mejoran las métricas de calidad y conversión.
* En función de la demanda popular, la versión de 32 bits de SSMA para Oracle vuelve a ser. En comparación con la implementación anterior (antes de v 7.4), hay dos paquetes de instalador, pero no se pueden instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tenga. Siempre es preferible usar la versión de 64 bits, si es posible.
* La compatibilidad con SQL Server 2017 es ahora oficial con el paquete de extensiones de Oracle admitido en Linux también (nueva opción de instalación remota). Tenga en cuenta que la funcionalidad del paquete de extensiones está limitada cuando se instala en Linux, ya que no se admiten las características de migración de datos del lado servidor y el evaluador.
* SSMA para Oracle permite migrar las vistas materializadas como tablas normales (se pueden configurar a través de los valores de configuración del **proyecto** -> **sincronizar** -> **detectar tablas de respaldo para vistas materializadas**).

## <a name="ssma-v76"></a>SSMA v 7.6

La versión v 7.6 de SSMA para Oracle se ha mejorado con correcciones específicas que mejoran las métricas de calidad y conversión y admiten SQL Server 2017 (versión preliminar pública). La compatibilidad con SQL Server 2017 en Windows y Linux está en versión preliminar pública y no debe usarse para migraciones de producción.

## <a name="ssma-v75"></a>SSMA v 7.5

La versión v 7.5 de SSMA para Oracle contiene los siguientes cambios:

* Mejorado con varias mejoras para garantizar una mayor accesibilidad para las personas con discapacidades.
* Se actualizó para mejorar la calidad y la métrica de conversión con correcciones específicas, como el control mejorado de los tipos de datos de fecha y flota durante la migración de datos, en función de los comentarios de los clientes.

## <a name="ssma-v74"></a>SSMA v 7.4

La versión v 7.4 de SSMA para Oracle contiene los siguientes cambios:

* SSMA para Oracle ahora admite Azure SQL Data Warehouse como plataforma de destino para la migración.

  ![Ventana nuevo proyecto](../media/new-project.png)
  * Admite las opciones de almacenamiento del almacenamiento de datos como se muestra en la siguiente imagen:

  ![Opciones de almacenamiento para el almacenamiento de datos](../media/storage-options_red.png)
  * Admite las opciones de distribución de datos como se muestra en la siguiente imagen:

  ![distribución de datos para el almacenamiento de datos](../media/data-distribution_red.png)

* La opción **tiempo de espera de consulta** ahora está disponible durante la detección de objetos de esquema en el origen y el destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

* La métrica de calidad y conversión se ha mejorado con las correcciones de destino, en función de los comentarios de los clientes.

> [!IMPORTANT]
> .Net 4.5.2 es un requisito previo para instalar SSMA v 7.4. Además, a partir de v 7.4, se suspende la versión de 32 bits de SSMA.

## <a name="ssma-v73"></a>SSMA v 7.3

La versión v 7.3 de SSMA para Oracle contiene los siguientes cambios:

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

La versión v 7.2 de SSMA para Oracle contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones de destino basadas en los comentarios de los clientes.
* Mejoras en la telemetría para proporcionar mejores puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v 7.1

La versión v 7.1 de SSMA para Oracle contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 es ahora una plataforma de destino admitida para la migración. Esta característica se encuentra en Technical Preview y permite el movimiento de datos y esquemas a los servidores SQL Server de destino.
* SSMA admite ahora las actualizaciones automáticas para descargar la versión más reciente de SSMA en cuanto esté disponible.
* Los binarios instalables de SSMA se entregan ahora a través de los archivos de paquete de Windows Installer (. msi).

## <a name="may-2016"></a>2016 de mayo

La versión de mayo de 2016 de SSMA para Oracle contiene los siguientes cambios:  

* Compatibilidad agregada para SQL Server 2016.
* Se ha agregado la conversión de tablas de archivo Oracle Flashback a SQL Server tablas temporales.

  > [!NOTE]
  > SSMA no copia los datos de historial de las tablas de archivo de datos de Oracle Flashback. Como resultado, los datos del historial se deben copiar manualmente durante el proceso de migración. Además, aunque SSMA no muestra la tabla de historial en el explorador de metadatos de SQL Server porque se trata como una tabla del sistema, puede ver la tabla de historial en SQL Server Management Studio.
  >
  > SQL Server 2016 no admite varias características de Oracle Flashback, entre las que se incluyen:
  >
  > * Consulta de transacciones de Oracle Flashback
  > * Paquete DBMS_FLASHBACK
  > * Transacción flashback
  > * Archivo de datos Flashback
  > * Tabla flashback
  > * Drop de flashback
  > * Base de datos Flashback
* Conversión agregada de la Directiva de VPD de Oracle a SQL Server objetos de directiva (Seguridad de nivel de fila para Oracle).
* Menor tiempo de carga inicial para Oracle.
* Se ha mejorado el analizador y la resolución.
* Se quitó la comprobación del instalador para .net 2,0.
* Dependencia del paquete de extensiones actualizada de .net 3,5 a .net 4,0.
* Se han corregido los comandos "guardar proyecto" y "Abrir proyecto" para la consola de SSMA.
* Se corrigió el comando "securepassword" para la consola de SSMA.
* Recuento fijo de objetos para la carga inicial.
* Se ha corregido la conversión de tipos de datos de caracteres para Oracle.
* Se corrigió el error en la configuración global.
  
## <a name="march-2016"></a>2016 de marzo

La versión de vista previa de marzo de 2016 de SSMA para Oracle agregó compatibilidad con:  
  
* Migración a SQL Server 2016.  
* Migración de Seguridad de nivel de fila de Oracle (con algunas limitaciones).  
* Migrar las tablas de Oracle en memoria a SQL Server almacén de columnas.  
  
## <a name="january-2016"></a>2016 de enero

La versión de mantenimiento de enero de 2014 de SSMA para Oracle contiene los siguientes cambios:  
  
* Compatibilidad agregada para los índices clúster.  
* Se han corregido las consultas lentas de esquema de Oracle (RFC 5076207).  
* Se corrigió la conexión a Azure desde la consola.  
* Se ha agregado el elemento de menú Ver registro a SSMA (RFC 5706203). 
* Telemetría agregada.
  
## <a name="july-2014"></a>2014 de julio

La versión 2014 de julio de SSMA para Oracle contiene los siguientes cambios:  
  
* Se ha agregado compatibilidad con Azure SQL DB.
* Funcionalidad del paquete de extensión que se ha migrado al esquema para admitir Azure SQL DB.
* Compatibilidad agregada para las vistas materializadas de Oracle.  
* Se ha agregado compatibilidad con las tablas con optimización para memoria de SQL Server 2014.  
* Se han incluido mejoras de rendimiento probadas para bases de datos con más de 10 000 objetos.  
* Se han agregado mejoras de la interfaz de usuario para tratar con un gran número de objetos.  
* Se ha agregado el resaltado de esquemas LOB "conocidos".  
* Mejoras en la velocidad de conversión incluida.  
* Compatibilidad agregada para mostrar los recuentos de objetos en la interfaz de usuario.  
* Menor tamaño de informe en más del 25%.
* Mensajes de error mejorados para construcciones sin analizar.  
  
## <a name="april-2014"></a>2014 de abril

La versión de abril de 2014 de SSMA para Oracle contiene los siguientes cambios:  
  
* Compatibilidad agregada de MS SQL Server 2014.  
* Se ha agregado compatibilidad con Oracle 12 y la optimización de consultas.  
* Se corrigieron los errores relacionados con la conversión a Azure.  
* Se han corregido errores relacionados con las páginas del informe invisibles en IE 10.  
  
## <a name="january-2012"></a>2012 de enero

La versión 2012 de enero de SSMA para Oracle agrega compatibilidad con los parámetros de entrada de RowType y RecordType de forma predeterminada en NULL.  
  
## <a name="july-2011"></a>2011 de julio

La versión 2011 de julio de SSMA para Oracle contiene los siguientes cambios:  
  
* Se ha agregado compatibilidad para la conversión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la secuencia de Oracle en el generador de secuencias de "Denali".
* Informes de errores mejorados durante la migración de datos.  
* Conversión mejorada de la instrucción mediante palabras reservadas.  
* Conversión implícita mejorada del valor de fecha en una función.  
  
## <a name="april-2011"></a>2011 de abril

La versión de abril de 2011 de SSMA para Oracle contiene los siguientes cambios:  
  
* Producto "SSMA para Oracle" consolidado, que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y "Denali".
* Se ha agregado compatibilidad para conectar y migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Motor de migración de datos del lado cliente mejorado, que admite la migración en paralelo de datos.  
* Rendimiento mejorado de la migración de datos con modelos de recuperación simples y de registro masivo.  
* Compatibilidad agregada para la compatibilidad con versiones anteriores de los proyectos creados con versiones anteriores de SSMA (v 4.0 y v 4.2).  
* Se ha agregado la posibilidad de instalar SSMA para el producto Oracle v 5.0 en paralelo (SxS) con versiones anteriores de SSMA (v 4.0 y v 4.2).
* Compatibilidad agregada para informes de tipos definidos por el usuario (incluye subtipo, VARRAY, tabla ANIDAda, tabla de objetos y vista de objetos) y sus usos en bloques PL/SQL con mensajes de error especiales.  

## <a name="july-2010"></a>2010 de julio

Se ha agregado la versión 2010 de julio de SSMA para Oracle:

* Compatibilidad para migrar a SQL Server 2008 R2.  
* Una nueva aplicación de consola SSMA para la ejecución de la línea de comandos.  
* Compatibilidad con la migración de datos mediante motores de migración de datos del lado cliente y del lado servidor.  
* Compatibilidad con la instrucción SELECT personalizada en la migración de datos.  
* Compatibilidad con la migración desde Oracle 11g R2.  
  
## <a name="june-2008"></a>2008 de junio

La versión 2008 de junio de SSMA para Oracle contiene los siguientes cambios:  
  
* Se han agregado mejoras en el informe de evaluación, incluida información adicional para los sinónimos, el origen sin formato para los objetos que se deben analizar, los paneles y el SQL Server la eliminación del logotipo y la persistencia del diseño.  
* Mejoras agregadas en la conversión de objetos:  
  * Packages DBMS_LOB, se ha agregado la conversión DBMS_SQL.  
  * Se ha revisado la conversión.  
  * Modificación de la conversión de colecciones y registros; ahora, la conversión de registros en casos simples se libera a través de variables independientes para cada campo.  
  * Mejoras en la implementación de registros y colecciones.  
  * Funciones de agregación de ventanas agregadas.  
  * Cláusula ROLLUP/CUBE agregada.  
  * Mejora de NEXTVAL/CURVAl.  
  * Se han agregado la agrupación de columnas en la cláusula SET, los conjuntos de agrupación y el ID. de agrupación.  
  * Instrucción MERGE agregada.  
  * Compatibilidad con los nuevos tipos de fecha y hora y la conversión de registros y colecciones a medida que se agregan tipos de datos CLR.  
* Se han agregado nuevas características de evaluador. Ahora, las tablas se pueden probar como objetos mediante el evaluador, se puede modificar un orden de llamada de varios objetos que se pueden comprobar en el caso de prueba, el usuario puede probar procedimientos y funciones con registros y colecciones como parámetros y valores devueltos, y se ha agregado un analizador de dependencias para comprobar solo las tablas usadas.  
  
## <a name="august-2007"></a>2007 de agosto

Se ha agregado la versión 2007 de agosto de SSMA para Oracle:

* Un nuevo componente de EVALUAdor permite crear, administrar y ejecutar casos de prueba para comprobar el código SQL convertido.  
* Se ha agregado compatibilidad con la conversión de los subtipos, las colecciones y los módulos locales de Oracle en el convertidor de SQL.  
* Una nueva característica de sincronización le permite sincronizar objetos específicos con SQL Server base de datos.  
* Nuevas opciones de conversión.  
  
## <a name="april-2007"></a>2007 de abril

La versión de abril de 2007 de SSMA para Oracle fue la versión inicial.
