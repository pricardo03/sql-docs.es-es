---
title: Notas de la versión
titleSuffix: Azure Data Studio
description: Notas de la versión de Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 07/11/2019
ms.openlocfilehash: 3e2b75282c9babf876d0daec033a435d75c2e2f1
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731057"
---
# <a name="release-notes-for-azure-data-studio"></a>Notas de la versión de Azure Data Studio

**[Descargue e instale la versión más reciente](download.md)** .

## <a name="july-2019"></a>Julio de 2019

11 de julio de 2019 &nbsp; / &nbsp; versión: 1.9.0 

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Publicación de la extensión SentryOne Plan Explorer | Nuestro apreciado partner de Microsoft, SentryOne, publicará su [extensión SentryOne Plan Explorer para Azure Data Studio](https://www.sentryone.com/products/sentryone-plan-explorer-extension-azure-data-studio). <br> Se trata de una extensión gratuita que proporciona diagramas de plan mejorados para las consultas que se ejecutan en Azure Data Studio, con algoritmos de diseño optimizados y codificación de colores intuitiva que ayudan a identificar rápidamente los operadores más caros que afectan al rendimiento de las consultas. Para obtener más información sobre la extensión, consulte [aquí](https://sqlperformance.com/2019/07/sentryone/plan-explorer-extension-azure-data-studio) la publicación del blog de SentryOne. |
| Nuevas características que se incorporarán a Comparación de esquemas | &bull; &nbsp; Compatibilidad con archivos de Comparación de esquemas (.SCMP). <br/>&bull; &nbsp; Compatibilidad con cancelación de Comparación de esquemas. <br/>&bull; &nbsp; Puede ver los cambios completos [aquí](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A%22July+2019+Release%22+label%3A%22Area%3A+Schema+Compare%22+is%3Aclosed+).|
| Mejoras de Notebook | &bull; &nbsp; Compatibilidad con Plotly Python. <br/>&bull; &nbsp; Apertura de Notebook desde el explorador. <br/> &bull; &nbsp; Cuadro de diálogo Administración de paquetes de Python. <br/> &bull; &nbsp; Mejoras de rendimiento y de Markdown. <br/> &bull; &nbsp; Actualización de los métodos abreviados de teclado. <br/>  &bull; &nbsp; Puede encontrar las correcciones de errores y las características secundarias [aquí](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A%22July+2019+Release%22+is%3Aclosed+label%3A%22Area%3A+Notebooks%22+). |
| Compatibilidad con SQL Server 2019 |  Esta versión incluye compatibilidad con otras características del clúster de macrodatos de SQL Server 2019: <br/> &bull; &nbsp; Tabla de puntos de conexión de servicio en el panel de administración que enumera todos los servicios clave del clúster. <br/> &bull; &nbsp; El cuaderno Estado del clúster muestra cómo puede consultar el estado del clúster en todos los servicios y pods, y ofrece soluciones a los posibles problemas.| 
| Paquetes de idioma actualizados disponibles| Ahora hay 10 paquetes de idioma disponibles en el Marketplace de Administrador de extensiones. Tan solo hay que buscar el idioma específico con el Marketplace de extensiones e instalarlo. Una vez instalado el idioma seleccionado, Azure Data Studio le pedirá que reinicie con el nuevo idioma. |
| Actualización de SQL Server Profiler | La extensión Perfil de SQL Server se ha actualizado para incluir nuevas características, entre las que se incluyen: <br/> &bull; &nbsp; Filtrado por nombre de base de datos. <br/> &bull; &nbsp; Compatibilidad con copiar y pegar. <br/> &bull; &nbsp; Filtro Guardar/Cargar. <br/>[Aquí](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aclosed+milestone%3A%22July+2019+Release%22+label%3A%22Area%3A+SQL+Profiler%22+) encontrará una lista completa de las mejoras de la extensión SQL Server Profiler.  |
| Combinación de versión de mayo de Visual Studio Code 1.35 | [Aquí](https://code.visualstudio.com/updates/v1_35) encontrará las mejoras más recientes. |
| Problemas y errores resueltos | En las versiones anteriores de Azure Data Studio, si se seleccionaba una base de datos de usuario al conectarse desde el cuadro de diálogo de conexión, la entrada resultante del Explorador de objetos estaba enfocada por completo a esa única base de datos. A partir de esta versión, ese comportamiento se está cambiando para que las propiedades de nivel de servidor también se muestren en el Explorador de objetos. <br/> Para obtener una la lista completa de las correcciones, vea [Correcciones y problemas en GitHub](https://github.com/microsoft/azuredatastudio/milestone/35?closed=1). |
| &nbsp; | &nbsp; |


## <a name="june-2019"></a>Junio de 2019

6 de junio de 2019 &nbsp; / &nbsp; versión: 1.8.0 

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Publicación de la extensión Servidores de administración central (CMS) de SQL Server | La extensión Servidores de administración central almacena una lista de instancias de SQL Server que se organizan en uno o varios grupos de este tipo de servidores. Los usuarios pueden conectarse a sus propios servidores CMS existentes y administrarlos, por ejemplo, para agregar y quitar servidores. [Aquí](https://docs.microsoft.com/sql/relational-databases/administer-multiple-servers-using-central-management-servers) puede obtener más información. |
| Publicación de las extensiones de la herramienta de administración de bases de datos para Windows | Esta extensión inicia dos de las experiencias más usadas en SQL Server Management Studio desde Azure Data Studio. Los usuarios pueden hacer clic con el botón derecho en una gran variedad de objetos diferentes (como bases de datos, tablas, columnas, vistas, etc.) y seleccionar Propiedades para ver el cuadro de diálogo de propiedades de SSMS correspondiente ese objeto. Además, los usuarios pueden hacer clic con el botón derecho en una base de datos y seleccionar Generar scripts para iniciar el ya conocido asistente de generación de scripts de SSMS. 
| Mejoras en la Comparación de esquemas | &bull; &nbsp; Se han agregado opciones de exclusión e inclusión. <br/>&bull; &nbsp; Generar script abre el script tras generarlo. <br/>&bull; &nbsp; Se han quitado las barras de desplazamiento doble.  <br/>&bull; &nbsp; Mejoras de formato y diseño. <br/>&bull; &nbsp; [Aquí](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+label%3A%22Area%3A+Schema+Compare%22+is%3Aclosed) puede ver los cambios completos.|
| Sección Mensajes movida a su propia pestaña | Cuando los usuarios ejecutaban consultas SQL, los resultados y los mensajes se encontraban en paneles apilados. Ahora se encuentran en pestañas independientes en un panel como en SSMS. |
| Mejoras de SQL Notebook | &bull; &nbsp; Los usuarios ahora pueden optar por usar sus propias instalaciones de Python 3 o Anaconda en los cuadernos. <br/>&bull; &nbsp; Varias correcciones de estabilidad y ajuste. <br/> &bull; &nbsp; [Aquí](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+is%3Aclosed+label%3A%22Area%3A+Notebooks%22) puede ver la lista completa de mejoras.|
| Combinación de versión de mayo de Visual Studio Code 1.34 | [Aquí](https://code.visualstudio.com/updates/v1_34) encontrará las mejoras más recientes. |
| Problemas y errores resueltos. | Consulte [Errores y problemas en GitHub](https://github.com/microsoft/azuredatastudio/milestone/32?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conocidos
- Extensiones de la herramienta de administración de bases de datos para Windows
    - No se pueden iniciar propiedades desde un nodo de servidor desconectado.
    - No se pueden iniciar las propiedades de los servidores de Azure.
    - No todos los objetos tienen cuadros de diálogo de propiedades.
    - Los diálogos tardan mucho tiempo en iniciarse.
    - Errores al iniciar servidores con algunos tipos de conexiones (como AAD).
- Cuaderno
    - [5838](https://github.com/microsoft/azuredatastudio/issues/5838) Permitir a los usuarios utilizar el sistema Python para los cuadernos.
- Comparación de esquemas
    - [5804](https://github.com/microsoft/azuredatastudio/issues/5804) Las tareas de Comparación de esquemas muestran el menú contextual Cancelar predeterminado, que no hace nada.

## <a name="may-2019"></a>Mayo de 2019

8 de mayo de 2019 &nbsp; / &nbsp; versión: 1.7.0 

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Publicación de la extensión Comparación de esquemas | Comparación de esquemas es una característica ya conocida en SQL Server Data Tools (SSDT), y su caso de uso principal es comparar y visualizar las diferencias entre las bases de datos y archivos .dacpac, y ejecutar acciones para que sean iguales. |
| Vista de tareas movida a la ventana de salida | Los usuarios ahora pueden ver el estado de las tareas de larga duración (como copia de seguridad, restauración y comparación de esquemas) de la vista de tareas en la ventana de salida.
| Página de bienvenida agregada | &bull; &nbsp; Vínculos a acciones comunes como Nueva consulta, Nuevo archivo, Nuevo bloc de notas. <br/>&bull; &nbsp; Vínculos a documentación y GitHub. |
| Mejoras en SQL Notebook | &bull; &nbsp; Mejoras en la representación de Markdown, incluida una mayor compatibilidad con notas y tablas. <br/>&bull; &nbsp; Mejoras de facilidad de uso en la barra de herramientas. <br/>&bull; &nbsp; Los vínculos de Markdown para cuadernos de confianza ya no requieren Cmd/Ctrl + clic y se puede hacer clic en ellos directamente. <br/>&bull; &nbsp; Mejoras en la limpieza de procesos de Jupyter después de cerrar cuadernos y reducción de errores al iniciar varios cuadernos simultáneamente. <br/>&bull; &nbsp; Mejoras en las conexiones de cuadernos de SQL para evitar errores al ejecutar 2 cuadernos en la misma base de datos. <br/>&bull; &nbsp; Mejoras en el desplazamiento automático de cuadernos a la celda que se está ejecutando actualmente al hacer clic en el botón Ejecutar celdas de la barra de herramientas. <br/>&bull; &nbsp; Mejoras generales en estabilidad y rendimiento. |
| Problemas y errores resueltos. | Consulte [Errores y problemas en GitHub](https://github.com/microsoft/azuredatastudio/milestone/31?closed=1). |
| &nbsp; | &nbsp; |

## <a name="april-2019"></a>April de 2019

18 de abril de 2019 &nbsp; / &nbsp; versión: 1.6.0 

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Nombre de la pestaña **Servidores** cambiado a **Conexiones** | |
| Migración de Azure Resource Explorer como viewlet de Azure a Conexiones | Los usuarios ahora pueden ver sus instancias de Azure SQL a través de un viewlet de Azure en la vista Conexiones, y expandir para ver los objetos de cada servidor o base de datos.|
| Mejoras en SQL Notebook | &bull; &nbsp; Botón agregado en la barra de herramientas para borrar la salida de todas las celdas. <br/>&bull; &nbsp; Botón agregado en la barra de herramientas para ejecutar todas las celdas. <br/>&bull; &nbsp; Nombre fijo de la conexión en lugar del nombre del servidor (si se establece) en la lista desplegable Anexar a. <br/>&bull; &nbsp; Corrección de imágenes en Markdown que no se representaban al usar rutas de acceso de imagen relativas. <br/>&bull; &nbsp; Funcionalidad mejorada en las cuadrículas de cuadernos con la adición de un cambio de tamaño de columna automático mediante doble clic, y mejora de la compatibilidad con la rueda del mouse. <br/>&bull; &nbsp; Mejoras en el control de errores y la resistencia de instalación de Python al instalar Python a través de cuadernos. <br/>&bull; &nbsp; Mejoras en la funcionalidad "seleccionar todo" al seleccionar las celdas del cuaderno. <br/>&bull; &nbsp; Mejoras en las conexiones de cuadernos para evitar cerrar un cuaderno y afectar a la conexión del explorador de objetos. <br/>&bull; &nbsp; Experiencia de cuadernos mejorada para mostrar un mensaje al usuario cuando el cuaderno está desconectado y necesita una conexión para ejecutar las celdas.<br/>&bull; &nbsp; Compatibilidad mejorada con cuadernos no guardados para rehidratar en ADS cuando se inicia de nuevo ADS. |
| Problemas y errores resueltos | Consulte [Errores y problemas en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/26?closed=1). |
| &nbsp; | &nbsp; |

## <a name="march-2019-hotfix"></a>Marzo de 2019 (revisión)

22 de marzo de 2019 &nbsp; / &nbsp; versión: 1.5.2 &nbsp; / &nbsp; Versión de revisión

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Corrección de algunos problemas detectados en 1.5.1 | Consulte [Publicación de revisión de marzo en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/28).<br/> <br/>&bull; &nbsp; Se corrigió un problema por el que el usuario no podía cerrar un cuaderno abierto desde la tarea "Abrir un bloc de notas" en el panel. <br/>&bull; &nbsp; Se corrigió un problema en el que el JSON del Notebook tenía un signo } adicional después de guardar. <br/>&bull; &nbsp; Se corrigió un problema por el que las cuadrículas de cuaderno no respondían a los cambios de tema. <br/>&bull; &nbsp; Se corrigió un problema en el que se mostraba la ruta completa del cuaderno en el encabezado de pestaña. Ahora solo se muestra el nombre de archivo. |
| &nbsp; | &nbsp; |

## <a name="march-2019"></a>Marzo de 2019

18 de marzo de 2019 &nbsp; / &nbsp; versión: 1.5.1

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| [Extensión PostgreSQL para Azure Data Studio](postgres-extension.md) agregada | Características admitidas: <br/>&bull; &nbsp; Cuadro de diálogo de conexión <br/>&bull; &nbsp; Explorador de objetos <br/>&bull; &nbsp; Editor de consultas <br/>&bull; &nbsp; Gráficos <br/>&bull; &nbsp; Paneles <br/>&bull; &nbsp; Fragmentos de código <br/>&bull; &nbsp; Editar datos <br/>&bull; &nbsp; Cuadernos |
| Cuadernos de SQL agregados | Se ha agregado compatibilidad con el kernel de SQL al visor de Notebook integrado: <br/>&bull; &nbsp; Admite T-SQL <br/>&bull; &nbsp; Admite T-SQL |
| Extensión de PowerShell agregada  | Ofrece la experiencia de la [extensión de PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) de VS Code.  |
| Extensión dacpac de SQL Server agregada  | Quita el asistente para aplicación de capa de datos de la extensión de importación de SQL Server y la agrega a una nueva extensión.  |
| Extensión de Community QueryPlan.show agregada | Integra compatibilidad para visualizar planes de consulta.  |
| Extensión de SQL Server 2019, versión preliminar, agregada | &bull; &nbsp; La compatibilidad con Jupyter Notebook (en concreto, con los kernels de Python3 y Spark) se ha pasado a la herramienta básica de Azure Data Studio. <br/>&bull; &nbsp; Corrección de errores en el asistente para datos externos  |
| Problemas y errores resueltos | Consulte [Errores y problemas en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/25?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conocidos
- [#4427](https://github.com/Microsoft/azuredatastudio/issues/4427): si se hace clic en ejecutar en la celda antes de que el kernel esté listo para Spark, se produce un error fatal. **Solución alternativa:** espere a que se carguen los kernels antes de ejecutar las celdas.
- [#4493](https://github.com/Microsoft/azuredatastudio/issues/4493): ADS iniciado desde SSMS mediante autenticación de SQL: se pide al usuario la contraseña. **Solución alternativa:** use la autenticación de Windows por ahora. 
- [#4494](https://github.com/Microsoft/azuredatastudio/issues/4494): no se puede instalar la característica de cuadernos de SQL. <br/>
**Solución alternativa:** Siga [aquí](https://github.com/Microsoft/azuredatastudio/issues/4494#issuecomment-473043832) los pasos de solución de errores. 
- [#4503](https://github.com/Microsoft/azuredatastudio/issues/4503): Azure Data Studio no se pueden abrir directamente desde la carpeta de descargas (Mac). <br />
**Solución alternativa:** reinicie el equipo después de descomprimir la aplicación. Pendiente de investigación. 
- [#4539](https://github.com/Microsoft/azuredatastudio/issues/4539):  la característica Guardar como de Notebook pierde el contexto de conexión. <br />
**Solución alternativa:** Se corregirá en la próxima versión. 
- [#4458](https://github.com/Microsoft/azuredatastudio/issues/4458): la extracción de dacpac bloquea SqlToolsService si se usa una versión no válida. <br/>
**Solución alternativa:** reinicie Azure Data Studio y asegúrese de que se usa la versión correcta.
- Se pierden los iconos de Nuevo cuaderno y Abrir cuaderno. <br/>
**Solución alternativa:** el tipo de conexión heredado está en desuso. Se recomienda conectarse al punto de conexión de SQL Server para obtener todas las acciones previstas (nuevo cuaderno, trabajo de Spark). 

## <a name="february-2019"></a>Febrero de 2019

13 de febrero de 2019 &nbsp; / &nbsp; versión: 1.4.5

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Paquete de extensión **Admin Pack PARA SQL Server** agregado. | Esto facilita la instalación de extensiones relacionadas con la administración de SQL Server. Esto incluye:<br/>&bull; &nbsp; [Agente SQL Server](sql-server-agent-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [SQL Server Profiler](https://docs.microsoft.com/sql/azure-data-studio/sql-server-profiler-extension)<br/>&bull; &nbsp; [Importación de SQL Server](sql-server-import-extension.md?view=sql-server-2017) |
| Se ha agregado compatibilidad con eventos extendidos de filtrado en la extensión de Profiler. | &nbsp; |
| Se ha agregado la característica Guardar como XML que puede guardar los resultados de T-SQL como XML. | &nbsp; |
| Se han agregado mejoras en el Asistente para importar aplicaciones de capa de datos. | &bull; &nbsp; Se ha agregado el botón Generar script.<br/>&bull; &nbsp; Se ha agregado la vista para proporcionar advertencias de posibles pérdidas de datos durante la implementación. |
| Actualizaciones en la versión preliminar de SQL Server 2019. | Vea [Extensión de SQL Server 2019, versión preliminar](sql-server-2019-extension.md?view=sql-server-ver15). |
| Streaming de resultados habilitado de forma predeterminada para las consultas de larga duración. | &nbsp; |
| Problemas y errores resueltos | Consulte [Errores y problemas en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/23?closed=1). |
| &nbsp; | &nbsp; |

## <a name="january-2019-hotfix"></a>Enero de 2019 (revisión)

16 de enero de 2019 &nbsp; / &nbsp; versión: 1.3.9 &nbsp; / &nbsp; Versión de revisión

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Corrección de algunos problemas detectados en 1.3.8. | Consulte [Publicación de revisión de enero en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1).<br/><br/>Para obtener información detallada, vea:<br/>&bull; &nbsp; [Registro de cambios en GitHub](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).<br/>&bull; &nbsp; [Versiones en GitHub](https://github.com/Microsoft/azuredatastudio/releases). |
| &nbsp; | &nbsp; |

## <a name="january-2019"></a>Enero de 2019

9 de enero de 2019 &nbsp; / &nbsp; versión: 1.3.8

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Se ha agregado un nuevo instalador de usuario para Windows. | A diferencia del instalador de sistema existente, el nuevo instalador de usuario no requiere privilegios de administrador. Esto también permite una experiencia de actualización más sencilla para los usuarios que no son administradores. |
| Se ha agregado compatibilidad con la autenticación de Azure Active Directory. | &nbsp; |
| Presentación de Idera SQL DM Performance Insights, versión preliminar. | &nbsp; |
| Compatibilidad con el Asistente para aplicaciones de capa de datos en la extensión Importación de SQL Server. | &nbsp; |
| Actualización de la extensión de SQL Server 2019, versión preliminar. | Vea [Extensión de SQL Server 2019, versión preliminar](sql-server-2019-extension.md?view=sql-server-ver15). |
| Mejoras en SQL Server Profiler. | &nbsp; |
| Streaming de resultados para consultas de gran tamaño (vista previa). | &nbsp; |
| Extensiones de la comunidad: sp_executesql para SQL y Nueva base de datos. | &nbsp; |
| Problemas y errores resueltos | Consulte [Errores y problemas en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1). |
| &nbsp; | &nbsp; |

## <a name="november-2018"></a>Noviembre de 2018

6 de noviembre de 2018 &nbsp; / &nbsp; versión: 1.2.4

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Actualización de la extensión de SQL Server 2019, versión preliminar. | Vea [Extensión de SQL Server 2019, versión preliminar](sql-server-2019-extension.md?view=sql-server-ver15). |
| Introducción de la extensión Paste the Plan (Pegado del plan). | &nbsp; |
| Introducción de la extensión de consultas High color (Color alto), incluido el tema del editor de SSMS. | &nbsp; |
| Correcciones en las extensiones Agente SQL Server, Profiler e Importación. | &nbsp; |
| Corrección del problema de .Net Core Socket KeepAlive que produce conexiones inactivas en macOS. | &nbsp; |
| Actualización de SQL Tools Service a .Net Core 2.2, versión preliminar 3 (para compatibilidad eventual con AAD). | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-november-2018"></a>Correcciones de errores, noviembre de 2018

- Corrección del [problema #2933](https://github.com/Microsoft/azuredatastudio/issues/2933): Conexión perdida a Azure SQL DB.
- Corrección del [problema #2914](https://github.com/Microsoft/azuredatastudio/issues/2914): Excepción "Argumento no válido" al expandir el nodo de base de datos OE.
- Corrección del [problema #2935](https://github.com/Microsoft/azuredatastudio/pull/2935): Visualización correcta de mensajes de varias líneas en los resultados de la consulta.
- Corrección del [problema #2906](https://github.com/Microsoft/azuredatastudio/pull/2906): Corrección del nombre del documento de Editar datos cuando el nombre de la tabla contiene caracteres especiales.
- Corrección del [problema #2929](https://github.com/Microsoft/azuredatastudio/issues/2929): El registro de cambios de extensión integrado indica que se comprueben los cambios en las notas de la versión de VSCode.
- Corrección del [problema #2719](https://github.com/Microsoft/azuredatastudio/issues/2719): Iconos dobles o triples de tema de contraste alto.
- Corrección del [problema #3047](https://github.com/Microsoft/azuredatastudio/pull/3047): Adición de una interfaz de línea de comandos para conectarse a un SQL Server.
- Corrección del [problema #3031](https://github.com/Microsoft/azuredatastudio/pull/3031): Adición de compatibilidad con el tema del plan de consulta.

## <a name="october-2018"></a>Octubre de 2018

29 de octubre de 2018&nbsp; / &nbsp; versión: 1.1.4

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Introducción de Azure Resource Explorer para examinar las bases de datos de Azure SQL. | &nbsp; |
| Mejora de la solidez de la conexión del Explorador de objetos y del Editor de consultas. | &nbsp; |
| Mejoras en las extensiones del Agente SQL. | &nbsp; |
| Actualización de la extensión de SQL Server 2019, versión preliminar. | Vea [Extensión de SQL Server 2019, versión preliminar](sql-server-2019-extension.md?view=sql-server-ver15). |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-october-2018"></a>Correcciones de errores, octubre de 2018

- Corrección del [problema #2717](https://github.com/Microsoft/azuredatastudio/issues/2717): Formato con clic de los resultados de la columna XML.
- Corrección del [problema #2993](https://github.com/Microsoft/azuredatastudio/issues/2993): Ancho de ventanas de resultados incompleto.
- Corrección del [problema #2999](https://github.com/Microsoft/azuredatastudio/issues/2999): No se pudo cargar el archivo System.Diagnostics.Tracing en Mac al conectarse a la base de datos.
- Corrección del [problema #2851](https://github.com/Microsoft/azuredatastudio/issues/2851): El gráfico TimeSeries no se representa correctamente.
- Corrección del [problema #2996](https://github.com/Microsoft/azuredatastudio/issues/2996): Pérdida de tabla Temp debido a un cambio de sesión repentino.

Para obtener información detallada, vea [Registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md) y [Versiones](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="september-2018-ga-release"></a>Septiembre de 2018 (versión GA)

24 de septiembre de 2018 &nbsp; / &nbsp; versión: 1.0 &nbsp; / &nbsp; versión GA

Versión de disponibilidad general de Azure Data Studio (anteriormente SQL Operations Studio).

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Mejoras en el rendimiento de la cuadrícula de resultados de la consulta y la experiencia del usuario para un gran número de conjuntos de resultados. | &nbsp; |
| El código fuente de Visual Studio Code se actualiza de la versión 1.23 a la versión 1.26.1 con diseño de cuadrícula y mejora del editor de configuración (versión preliminar). | &nbsp; |
| Mejoras de accesibilidad para el lector de pantalla, la navegación con el teclado y el contraste alto. | &nbsp; |
| Se ha agregado la opción `Connection name` para proporcionar un nombre para mostrar alternativo en el viewlet de servidores. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="announcing-the-sql-server-2019-preview-extension"></a>Anuncio de la extensión de SQL Server 2019, versión preliminar

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Compatibilidad con características en vista previa de SQL Server 2019, incluido el [clúster de macrodatos](../big-data-cluster/big-data-cluster-overview.md) | Conéctese a la puerta de enlace HDFS/Spark incluida con la versión preliminar de SQL Server 2019.<br/><br/>Examine HDFS, cargue y guarde archivos, e inicie acciones prácticas como analizar en Notebook para archivos CSV.<br/><br/>Envíe trabajos de Spark desde el panel o haga clic con el botón derecho en una conexión de HDFS/Spark en el Explorador de objetos. |
| Azure Data Studio Notebooks | Cree o abra cuadernos con un visor de Notebook integrado. En esta versión, el visor de Notebook solo admite la conexión a kernels locales y al clúster de macrodatos de SQL Server 2019.<br/><br/>Use las bibliotecas del acelerador de código PROSE en Notebook para obtener información sobre el formato de archivo y los tipos de datos para la preparación rápida de los datos. |
| Azure Resource Explorer | La vista de Azure Resource Explorer permite examinar los puntos de conexión relacionados con los datos de las cuentas de Azure y crear conexiones con ellos en el Explorador de objetos. En esta versión se admiten los servidores y las bases de datos Azure SQL. |
| Asistente para crear tablas externas de SQL Server PolyBase | Cree una tabla externa y sus estructuras de metadatos auxiliares con un asistente fácil de usar. En esta versión, se admiten los servidores remotos SQL Server y Oracle. |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-september-2018"></a>Correcciones de errores, septiembre de 2018

- Corrección del [problema #2647](https://github.com/Microsoft/azuredatastudio/issues/143): Los gráficos dieron un gran paso atrás.
- Corrección del [problema #2648](https://github.com/Microsoft/azuredatastudio/issues/143): SELECT que devuelve JSON con hipervínculos en toda la columna.

Para obtener información detallada, vea [Registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md) y [Versiones](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="august-2018"></a>Agosto de 2018

30 de agosto de 2018 &nbsp; / &nbsp; versión: 0.32.8 &nbsp; / &nbsp; Versión preliminar pública

La *versión preliminar pública de agosto* se centra en las correcciones de errores, la estabilización del producto y el llenado de huecos en escenarios existentes.

_0.32.8 contiene correcciones para un par de regresiones encontradas en 0.32.7 ([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971), [#2372](https://github.com/Microsoft/azuredatastudio/issues/2372))_

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Anuncio de la extensión de importación de SQL Server | &nbsp; |
| Administración de sesiones de SQL Server Profiler | &nbsp; |
| Compatibilidad con la plantilla de sesiones de SQL Server Profiler | &nbsp; |
| Mejoras en el Agente SQL Server | &nbsp; |
| Nueva extensión de la comunidad: Kit de primer respondedor | &nbsp; |
| Mejoras en la calidad de la vida: Cadenas de conexión | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-august-2018"></a>Correcciones de errores, agosto de 2018

- Analizar SQL en una ventana del Editor de consultas mediante el comando `Parse Syntax`.
- Corrección del [problema #143](https://github.com/Microsoft/azuredatastudio/issues/143): Hacer doble clic no selecciona @ en el nombre de variable.
- Corrección del [problema #387](https://github.com/Microsoft/azuredatastudio/issues/387): El icono de la base de datos de la pestaña de SQL está en rojo.
- Corrección del [problema #825](https://github.com/Microsoft/azuredatastudio/issues/825): Solicitud: Conectar automáticamente al servidor actual después de Script como... 
- Corrección del [problema #1278](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [entrada de escritorio] - valor redundante para Nombre y comentario.
- Corrección del [problema #1285](https://github.com/Microsoft/azuredatastudio/issues/1285): La actualización hace que el icono de la aplicación se quite o se reemplace en Windows.
- Corrección del [problema #1317](https://github.com/Microsoft/azuredatastudio/issues/1317): Corrija el separador decimal.
- Corrección del [problema #1474](https://github.com/Microsoft/azuredatastudio/issues/1474): Cancelar el cambio de conexión desconecta la conexión actual.
- Corrección del [problema #1497](https://github.com/Microsoft/azuredatastudio/issues/1497): Las opciones de Ver como gráfico se cortan en la parte inferior.
- Corrección del [problema #1524](https://github.com/Microsoft/azuredatastudio/issues/1524): Shell/Panel: Los iconos principales del viewlet son arrastrables y pueden bloquear la aplicación.
- Corrección del [problema #1578](https://github.com/Microsoft/azuredatastudio/issues/1578): No se puede expandir ni contraer la carpeta del explorador de archivos remotos haciendo clic en el nombre.
- Corrección del [problema #1620](https://github.com/Microsoft/azuredatastudio/issues/1620): Sugerencia de característica: Obtener la cadena de conexión para la conexión existente.
- Corrección del [problema #1624](https://github.com/Microsoft/azuredatastudio/issues/1624): SelectBox no cambia de color cuando se deshabilita.
- Corrección del [problema #1728](https://github.com/Microsoft/azuredatastudio/issues/1728): Guardar como JSON/EXCEL/CSV no funciona.
- Corrección del [problema #1744](https://github.com/Microsoft/azuredatastudio/issues/1744): El panel de resultados pierde las posiciones de desplazamiento al cambiar de pestaña.
- Corrección del [problema #1748](https://github.com/Microsoft/azuredatastudio/issues/1748): Mensaje de error al guardar el archivo de Excel una segunda vez (y en veces posteriores).
- Corrección del [problema #1782](https://github.com/Microsoft/azuredatastudio/issues/1782): Al editar datos, la celda no vuelve al valor original al presionar la tecla Escape.
- Corrección del [problema #1836](https://github.com/Microsoft/azuredatastudio/issues/1836): Archivos .sql no asociados con SQL Operations Studio.
- Corrección del [problema #1850](https://github.com/Microsoft/azuredatastudio/issues/1850): Al escribir N'', se completa automáticamente a N'''.
- Corrección del [problema #1985](https://github.com/Microsoft/azuredatastudio/issues/1985): Desfase de1 columna al copiar desde la cuadrícula de resultados de la consulta.
- Corrección del [problema #1998](htpts://github.com/Microsoft/azuredatastudio/pull/1998): Adición de la versión de VS Code al cuadro de diálogo Acerca de.
- Corrección del [problema #2042](https://github.com/Microsoft/azuredatastudio/pull/2042): : Botón habilitado para importar consultas de archivos SQL.
- Corrección del [problema #2091](https://github.com/Microsoft/azuredatastudio/issues/2091): No se puede usar el método abreviado CTRL + C para copiar desde el panel de resultados.
- Corrección del [problema #2099](https://github.com/Microsoft/azuredatastudio/pull/2099): Se han agregado más opciones de saveAsCsv.
- Corrección del [problema #2107](https://github.com/Microsoft/azuredatastudio/issues/2107): Actualización del icono de los documentos del Panel y de Profiler.
- Corrección del [problema #2129](https://github.com/Microsoft/azuredatastudio/pull/2129): Guardar los datos de edición desplaza la posición al cambiar de pestaña.
- Corrección del [problema #2152](https://github.com/Microsoft/azuredatastudio/issues/2152): El indicador de fila de cuadrícula de resultados se basa en cero.

### <a name="known-issues-august-2018"></a>Problemas conocidos, agosto de 2018

- [Problema #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Guardar como Excel solo guarda la primera fila de datos.
- [Problema #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): No se puede conectar en Ubuntu 16.04 a SQL en un contenedor.

## <a name="july-2018"></a>Julio de 2018

19 de julio de 2018&nbsp; / &nbsp; versión: 0.31.4 &nbsp; / &nbsp; Versión preliminar pública

La *versión preliminar pública* de julio se centra en los siguientes elementos:

- La versión inicial de los escenarios de configuración del Agente SQL Server.
- Mejoras en la plantilla de vista y sesión de SQL Server Profiler.
- Correcciones de errores continuadas para problemas notificados por los clientes en GitHub.

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Mejoras en la [Extensión Agente SQL Server para SQL Operations Studio](sql-server-agent-extension.md). | Se ha agregado la vista de alertas, operadores, proxies e iconos en el panel izquierdo.<br/><br/>Se han agregado los cuadros de diálogo Nuevo trabajo, Nuevo paso de trabajo, Nueva alerta y Nuevo operador.<br/><br/>Se ha agregado Eliminar trabajo, Eliminar alerta y Eliminar operador (clic con el botón derecho).<br/><br/>Se ha agregado la visualización de ejecuciones anteriores.<br/><br/>Se han agregado filtros para cada nombre de columna. |
| Mejoras en la [extensión SQL Server Profiler para SQL Operations Studio](sql-server-profiler-extension.md). | Se han agregado 5 plantillas predeterminadas para ver Eventos extendidos.<br/><br/>Se ha agregado el nombre de conexión de Servidor/Base de datos.<br/><br/>Se ha agregado compatibilidad para instancias de Azure SQL Database.<br/><br/>Se ha agregado una sugerencia para salir de Profiler cuando se cierra la pestaña y Profiler todavía se está ejecutando. |
| Versión de la extensión de combinación de scripts. | &nbsp; |
| Se han agregado puntos de extensibilidad de cuadros de diálogo y asistentes para los autores de extensiones. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-july-2018"></a>Correcciones de errores, julio de 2018

- Corrección del [problema 728](https://github.com/Microsoft/azuredatastudio/issues/728): No hay respuesta para Agregar conexión en macOS.
- Corrección del [problema 1612](https://github.com/Microsoft/azuredatastudio/issues/1612): La presentación del texto de la cuadrícula de resultados está desordenada con caracteres internacionales.
- Corrección del [problema 1693](https://github.com/Microsoft/azuredatastudio/issues/1693): Cuadro de diálogo de copia de seguridad - La interfaz de usuario del explorador de archivos está dañada.
- Corrección del [problema 1713](https://github.com/Microsoft/azuredatastudio/issues/1713): Número de filas afectadas.
- Corrección del [problema 1718](https://github.com/Microsoft/azuredatastudio/issues/1718): No se puede conectar con ningún origen de datos.
- Corrección del [problema 1719](https://github.com/Microsoft/azuredatastudio/issues/1719): TypeError al conectar con el servidor.
- Corrección del [problema 1724](https://github.com/Microsoft/azuredatastudio/issues/1724): Los cuadros de diálogo de extensiones han dejado de funcionar.
- Corrección del [problema 1749](https://github.com/Microsoft/azuredatastudio/issues/1749): ERROR - Se interpretan los datos HTML en una columna.
- Corrección del [problema 1789](https://github.com/Microsoft/azuredatastudio/issues/1789): Extensibilidad - Si agrega un proveedor de conexión, la desinstalación nunca lo quitará de la lista.
- Corrección del [problema 1791](https://github.com/Microsoft/azuredatastudio/issues/1791): Extensiones de Sqlops - queryeditor.connect() se conecta a la base de datos de destino, pero la interfaz de usuario no muestra que el editor está conectado.
- Corrección del [problema 1799](https://github.com/Microsoft/azuredatastudio/issues/1799): El gráfico con las 10 bases de datos principales por tamaño no funciona en instancias con distinción de mayúsculas y minúsculas.
- Corrección del [problema 1814](https://github.com/Microsoft/azuredatastudio/issues/1814): error tipográfico de sqlops.d.ts que causa la definición de tipo "any" implícita.
- Corrección del [problema 1817](https://github.com/Microsoft/azuredatastudio/issues/1817): Error de ortografía.
- Corrección del [problema 1830](https://github.com/Microsoft/azuredatastudio/issues/1830): Establecer iconPath en ButtonComponent después de llamar a component() no cambia el icono.
- Corrección del [problema 1843](https://github.com/Microsoft/azuredatastudio/issues/1843): Mejor organización de tablas.

## <a name="june-2018"></a>Junio de 2018

20 de junio de 2018 &nbsp; / &nbsp; versión: 0.30.6 &nbsp; / &nbsp; Versión preliminar pública

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Publicación inicial de la extensión **SQL Server Profiler para SQL Operations Studio, _versión preliminar_** . | &nbsp; |
| La nueva extensión **SQL Data Warehouse** incluye sofisticados widgets de panel personalizables que exponen información al almacenamiento de datos. | Esto desbloquea escenarios clave en torno a la administración y el ajuste del almacenamiento de datos para asegurarse de que está optimizado para un rendimiento coherente. |
| Compatibilidad con **"Filtrar y ordenar" de Editar datos**. | &nbsp; |
| Mejoras de la extensión **Agente SQL Server para SQL Operations Studio _, versión preliminar_** , para las vistas Trabajos e Historial de trabajos. | &nbsp; |
| Se han mejorado las API de extensibilidad del **asistente y del marco de trabajo del generador de interfaz de usuario**. | &nbsp; |
| Actualización del código fuente de la plataforma VS Code. | Se han integrado las siguientes versiones:<br/>&bull; &nbsp; [Marzo de 2018 (1.22)](https://code.visualstudio.com/updates/v1_22)<br/>&bull; &nbsp; [Abril de 2018 (1.23)](https://code.visualstudio.com/updates/v1_23) |
| &nbsp; | &nbsp; |

### <a name="github-issues-fixes-june-2018"></a>Correcciones de problemas de GitHub, junio de 2018

- Solicitud de característica ([problema 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): Hacer que la cuadrícula de resultados ajuste automáticamente el ancho de columna a los datos y recordar los cambios manuales si se vuelve a ejecutar la misma consulta.
- Corrección del [problema 1398](https://github.com/Microsoft/azuredatastudio/issues/1398): Se debería mostrar el botón Agregar mensaje y Agregar cuenta cuando la cuenta vinculada está vacía.
- Corrección del [problema 1399](https://github.com/Microsoft/azuredatastudio/issues/1399): La pestaña de cuenta vinculada queda dañada cuando se contrae la vista.
- Corrección del [problema 1374](https://github.com/Microsoft/azuredatastudio/issues/1374): El servicio de herramientas de SQL se bloquea al abrir el archivo .sql desde el disco.
- Corrección del [problema 1372](https://github.com/Microsoft/azuredatastudio/issues/1372): Falta la palabra clave de SQL "BETWEEN".
- Corrección del [problema 1395](https://github.com/Microsoft/azuredatastudio/issues/1395): La palabra clave "MATCH" bloquea el servicio de herramientas de SQL.
- Corrección del [problema 1496](https://github.com/Microsoft/azuredatastudio/issues/1496): La opción del menú contextual de nuevo generador de perfiles en el Explorador de objetos no hace nada.
- Corrección del [problema 1495](https://github.com/Microsoft/azuredatastudio/issues/1495): El plan de consulta "Explicar" del editor de consultas está dañado.

## <a name="may-2018"></a>Mayo de 2018

7 de mayo de 2018 &nbsp; / &nbsp; versión: 0.29.3 &nbsp; / &nbsp; Versión preliminar pública

La *versión preliminar pública de mayo* se centra en la estabilización y la corrección de errores.

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Presentación de la extensión Búsqueda de SQL de Redgate disponible en el administrador de extensiones. | &nbsp; |
| Localización de la comunidad disponible para 10 idiomas. | Alemán, español, francés, italiano, japonés, coreano, portugués, ruso, chino simplificado y chino tradicional. |
| Cambios en la colección de telemetría. | &bull; &nbsp; Colección de telemetría reducida.<br/>&bull; &nbsp; Experiencia de exclusión mejorada.<br/>&bull; &nbsp; Vínculos en productos a la declaración de privacidad. |
| El administrador de extensiones ha mejorado la experiencia de Marketplace. | Detección más fácil de las extensiones de la comunidad. |
| Extensión de Agente SQL. | &bull; &nbsp; Trabajos.<br/>&bull; &nbsp; Mejora de la vista del historial de trabajos. |
| Actualizaciones para las extensiones de whoisactive y Server Reports. | &nbsp; |
| Desplazamiento mejorado de la administración de las propiedades del panel. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues"></a>Corrección de problemas de GitHub

- Corrección del [problema 703](https://github.com/Microsoft/azuredatastudio/issues/703): La escritura de texto similar a HTML en Editar datos hace que el valor se muestre incorrectamente hasta que se actualiza.
- Corrección del [problema 821](https://github.com/Microsoft/azuredatastudio/issues/821): Dependencia del paquete azuredatastudio.deb.
- Corrección del [problema 1260](https://github.com/Microsoft/azuredatastudio/issues/1260): Palabra clave "Distinct" no resaltada.
- Corrección del [problema 1332](https://github.com/Microsoft/azuredatastudio/issues/1332): La reversión de la fila en "Editar datos" no funciona.
- Corrección del [problema 1215](https://github.com/Microsoft/azuredatastudio/issues/1215): Extensión del Agente SQL y la barra de estado.
- Corrección del [problema 1316](https://github.com/Microsoft/azuredatastudio/issues/1316): Agente SQL no cambia de tamaño después de cambiar el tamaño de las ventanas.

## <a name="april-2018"></a>Abril de 2018

25 de abril de 2018 &nbsp; / &nbsp; versión: 0.28.6 &nbsp; / &nbsp; Versión preliminar pública

La *versión preliminar pública de abril* contiene correcciones de errores y mejoras.

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Mejoras en la extensión de la versión preliminar del Agente SQL: | &nbsp; |
| &nbsp; &nbsp; &nbsp; Compatibilidad mejorada con archivos. | &bull; &nbsp; Archivos grandes.<br/>&bull; &nbsp; Archivos protegidos para guardar los protegidos por el administrador.<br/>&bull; &nbsp; Almacenamiento de \>256M en SQL Operations Studio. |
| &nbsp; &nbsp; &nbsp; División de terminal integrado. | Trabajo simultáneo con varios terminales abiertos. |
| &nbsp; &nbsp; &nbsp; Mayor velocidad de instalación y tiempo de inicio. | Se ha reducido la huella del número de archivos en disco dejada por la instalación. |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues-april-2018"></a>Corrección de problemas de GitHub, abril de 2018

- Corrección del [problema 37](https://github.com/Microsoft/azuredatastudio/issues/37): Cuando el visor de gráficos genera un error, se produce un comportamiento inesperado.
- Corrección del [problema 462](https://github.com/Microsoft/azuredatastudio/issues/462): Solicitud de característica - Opción para que los grupos de servidores se expandan de forma predeterminada.
- Corrección del [problema 606](https://github.com/Microsoft/azuredatastudio/issues/606): Intellisense - Sugerencia incorrecta para el comando "update".
- Corrección del [problema 967](https://github.com/Microsoft/azuredatastudio/issues/967): Se espera un plan de consulta cuando se selecciona el plan de presentación XML en la cuadrícula de resultados.
- Corrección del [problema 1023](https://github.com/Microsoft/azuredatastudio/issues/1023): Adición de corchetes para la llamada ms_foreachdb desde flyfishingdba.
- Corrección del [problema 1048](https://github.com/Microsoft/azuredatastudio/issues/1048): Error de protocolo de enlace SSL/TLS previo al inicio de sesión.
- Corrección del [problema 1050](https://github.com/Microsoft/azuredatastudio/issues/1050): Borrar la vista de información antes de mostrar el error.
- Corrección del [problema 1057](https://github.com/Microsoft/azuredatastudio/issues/1057): Las acciones restaurar y nueva consulta en el widget de explorador están dañadas.
- Corrección del [problema 1068](https://github.com/Microsoft/azuredatastudio/issues/1068): Aparecen ventanas de salida del panel con un mensaje de error para Azure SQL Database.
- Corrección del [problema 1069](https://github.com/Microsoft/azuredatastudio/issues/1069): El cuadro de diálogo de conexión muestra el error Servidor obligatorio cuando se muestra inicialmente.
- Corrección del [problema 1070](https://github.com/Microsoft/azuredatastudio/issues/1070): Grupos de servidores ahora requieren un doble clic para expandirse.
- Corrección del [problema 1072](https://github.com/Microsoft/azuredatastudio/issues/1072): El fondo del control Seleccionar es semitransparente.
- Corrección del [problema 1115](https://github.com/Microsoft/azuredatastudio/issues/1115): Corrección de todos los problemas de accesibilidad de contraste alto en SQL Operations Studio.
- Corrección del [problema 1101](https://github.com/Microsoft/azuredatastudio/issues/1101): La extensión no puede actualizar el vínculo "Descargar manualmente"; se dirige a una ubicación incorrecta.
- Corrección del [problema 1103](https://github.com/Microsoft/azuredatastudio/issues/1103): El desplazamiento V no funciona en la pestaña Inicio.
- Corrección del [problema 1104](https://github.com/Microsoft/azuredatastudio/issues/1104): Las pestañas de la extensión de SQL dejaban de funcionar.

### <a name="visual-studio-code-121-platform"></a>Plataforma Visual Studio Code 1.21

Un aspecto destacado de la versión preliminar pública de abril es la actualización del código fuente de la plataforma Visual Studio Code 1.21. Incluye varias actualizaciones en el editor principal y el área de trabajo con respecto al punto de sincronización 1.19 anterior. A continuación se muestran algunos ejemplos:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| [Nueva interfaz de usuario de notificaciones](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui). | Administre y revise fácilmente las notificaciones de SQL Operations Studio. |
| [División de terminal integrado](https://code.visualstudio.com/updates/v1_21#_split-terminals). | Trabajo simultáneo con varios terminales abiertos. |
| [Guardar archivos grandes y protegidos](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges). | Guardar archivos protegidos por el administrador y \>256M archivos en SQL Operations Studio. |
| [Compatibilidad mejorada con archivos grandes](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements). | Optimizaciones del búfer de texto para archivos grandes. |
| [Búsqueda de configuración mejorada](https://code.visualstudio.com/updates/v1_20#_settings-search). | Detección fácil de la configuración adecuada con búsqueda en lenguaje natural. |
| [Fragmentos de código globales](https://code.visualstudio.com/updates/v1_20#_global-snippets). | Creación de fragmentos de código que pueden usarse en todos los tipos de archivo. |
| [Selección múltiple en el explorador](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer). | Posibilidad de realizar acciones en varios archivos a la vez. |
| [Errores y advertencias en el explorador](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer). | Navegación rápida a los errores en el código base. |
| [Arrastrar y colocar, copiar y pegar entre ventanas](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support). | Movimiento de archivos entre ventanas abiertas de SQL Operations Studio. |
| [Compatibilidad con submódulos de Git](https://code.visualstudio.com/updates/v1_20#_git-submodules). | Posibilidad de realizar operaciones de Git en repositorios de Git anidados. |
| [Compatibilidad con el lector de pantalla de terminal](https://code.visualstudio.com/updates/v1_20#_screen-reader-support). | El terminal integrado ahora tiene un modo **optimizado para lector de pantalla**. |
| [Diseño del editor centrado](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout). | Maximización del espacio real de la pantalla de visualización de código. |
| [Resultados de búsqueda en horizontal (versión preliminar)](https://code.visualstudio.com/updates/v1_21#_horizontal-search). | Ahora puede ver los resultados de la búsqueda en un panel horizontal. |
| &nbsp; | &nbsp; |

Para obtener más información, consulte las [notas de la versión de Visual Studio Code de febrero](https://code.visualstudio.com/updates/v1_21) y las [notas de la versión de Visual Studio Code de enero](https://code.visualstudio.com/updates/v1_20).

Para más información, vea [Registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).

## <a name="march-2018"></a>Marzo de 2018

28 de marzo de 2018 &nbsp; / &nbsp; versión: 0.27.3 &nbsp; / &nbsp; Versión preliminar pública

La *versión preliminar pública de marzo* continúa solucionando los principales problemas de GitHub y se centra en mejorar nuestro historial de extensibilidad. En concreto, se habilita el administrador de extensiones, se mejora la administración de paneles y se proporcionan extensiones del Agente SQL y de Insights. Esta versión ofrece las siguientes mejoras:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Mejora del modelo de extensibilidad de paneles para admitir los paneles de configuración y la información con pestañas. | El administrador de extensiones permite la adquisición simple de extensiones.<br/><br/>Extensiones de panel para sp\_whoisactive de [whoisactive.com](http://www.whoisactive.com).<br/><br/>Para obtener más detalles, vea [Ampliación de la funcionalidad de SQL Operations Studio](extensions.md). |
| Agregue otras [API de extensibilidad para la administración de conexiones y del explorador de objetos](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API). | &nbsp; |
| Corrección continua de [problemas de GitHub](https://github.com/Microsoft/azuredatastudio/issues) importantes que afectan a los clientes. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="february-2018"></a>Febrero de 2018

15 de febrero de 2018 &nbsp; / &nbsp; versión: 0.26.7 &nbsp; / &nbsp; Versión preliminar pública

La *versión preliminar pública de febrero* incluye algunas sugerencias de características y correcciones de errores de alta prioridad. Esta versión ofrece las siguientes mejoras:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Introducción de la instalación de actualización automática, que proporciona una notificación cuando hay una nueva versión disponible para descargar. | &nbsp; |
| El campo **Base de datos** del cuadro de diálogo de conexión es ahora una lista desplegable rellenada dinámicamente que contiene una lista de bases de datos que se han rellenado desde el servidor especificado. | &nbsp; |
| Introducción de la API de extensibilidad de conexiones. | &nbsp; |
| Integración del editor de VS Code 1.19. | &nbsp; |
| Actualización del componente JustinPealing/html-query-plan para obtener varias mejoras del visor del plan de consulta. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixed-issues-february-2018"></a>Problemas corregidos, febrero de 2018

- Corrección del [problema 6](https://github.com/Microsoft/azuredatastudio/issues/6): Mantener la conexión y la base de datos seleccionada al abrir nuevas pestañas de consulta.
- Corrección del [problema 22](https://github.com/Microsoft/azuredatastudio/issues/22): "Nombre de servidor" y "Nombre de base de datos": ¿pueden listas desplegables en lugar de cuadros de texto?
- Corrección del [problema 549](https://github.com/Microsoft/azuredatastudio/issues/549): Tras una instalación silenciosa o muy silenciosa, se abre la aplicación.
- Corrección del [problema 481](https://github.com/Microsoft/azuredatastudio/issues/481): Agregar la opción "Buscar actualizaciones".
- Corrección de la coloración y finalización automática del Editor de SQL:
  - Corrección del [problema 584](https://github.com/Microsoft/azuredatastudio/issues/584): Palabra clave "FULL" no resaltada por IntelliSense.
  - Corrección del [problema 345](https://github.com/Microsoft/azuredatastudio/issues/345): Colorear funciones SQL en el editor.
  - Corrección del [problema 300](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] latest "]" mostrará el color verde.
  - Corrección del [problema 225](https://github.com/Microsoft/azuredatastudio/issues/225): Error de coincidencia de color de palabra clave.
  - Corrección del [problema 60](https://github.com/Microsoft/azuredatastudio/issues/60): Resaltado no válido del color de la sintaxis de SQL al usar una tabla temporal INNER en la cláusula.

## <a name="january-2018"></a>Enero de 2018

17 de enero de 2018 &nbsp; / &nbsp; versión: 0.25.4 &nbsp; / &nbsp; Versión preliminar pública

La *versión preliminar pública de enero* incluye algunas sugerencias de características y correcciones de errores de alta prioridad. Esta versión ofrece las siguientes mejoras:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Las conexiones de servidor guardadas están disponibles en el cuadro de diálogo de conexión. | &nbsp; |
| Habilitar la salida rápida. La salida rápida está desactivada de forma predeterminada; para habilitarla, vea [Salida rápida](settings.md#hot-exit). | &nbsp; |
| Color de pestañas basado en Grupo de servidores. El color de las pestañas está desactivado de forma predeterminada; para habilitarlo, vea [Color de las pestañas](settings.md#tab-color). | &nbsp; |
| *Nombre del servidor* ha cambiado a *Servidor* en el cuadro de diálogo de conexión. | &nbsp; |
| Corrección del comando interrumpido de *ejecución de consulta actual*. | &nbsp; |
| Corrección del error de scripting de interrupción de arrastre y colocación. | &nbsp; |
| Corrección del icono del menú Inicio anclado incorrectamente. | &nbsp; |
| Corrección de la ausencia del icono de personalización de marca de cuenta de Azure. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="december-2017"></a>Diciembre de 2017

19 de diciembre de 2017 &nbsp; / &nbsp; versión: 0.24.1 &nbsp; / &nbsp; Versión preliminar pública

La *versión preliminar pública de diciembre* incluye varias correcciones de errores en todas las áreas de características, así como las siguientes mejoras:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| El cuadro de diálogo Crear regla de firewall ahora está disponible para ayudarle a conectarse a Azure SQL Database y Azure SQL Data Warehouse. | &nbsp; |
| Se ha agregado el programa de instalación de Windows y los paquetes de instalación de Linux DEB y RPM. | &nbsp; |
| Administración del editor de objetos visuales del panel. | &nbsp; |
| Comandos *Crear script como ALTER* y *Script como ejecutar*. | &nbsp; |
| Comando *Ejecutar consulta actual con plan real*. | &nbsp; |
| Integración de la plataforma del editor de VS Code 1.18.1. | &nbsp; |
| Habilitación de la instalación de prueba de archivos de extensión VSIX. | &nbsp; |
| Admite la sintaxis de iteración por lotes "GO N". | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="november-2017"></a>Noviembre de 2017

15 de noviembre de 2017 &nbsp; / &nbsp; versión: 0.23.6

- Versión inicial de [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="next-steps"></a>Next Steps

Para empezar, vea una de las siguientes guías de inicio rápido:

- [Conectar y consultar SQL Server](quickstart-sql-server.md)
- [Conectar y consultar Azure SQL Database](quickstart-sql-database.md)
- [Conectar y consultar Azure SQL Data Warehouse](quickstart-sql-dw.md)

Contribuya a [!INCLUDE[name-sos](../includes/name-sos-short.md)]:

- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
