---
title: Propiedades de la tabla | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.tableproperties.storage.f1
- sql12.SWB.SELECTCOLUMNS.F1
- sql12.swb.tableproperties.filetable.f1
- sql12.swb.tableproperties.general.f1
- sql12.swb.tableproperties.changetracking.f1
ms.assetid: ad8a2fd4-f092-4c0f-be85-54ce8b9d725a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b07f157294700b3b3b7958ce4cdc6f1589bff864
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196714"
---
# <a name="table-properties"></a>Propiedades de tabla
  En este tema se describen las propiedades de la tabla que se muestran en el cuadro de diálogo Propiedades de tabla en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información sobre cómo mostrar estas propiedades, vea [Ver la definición de tabla](view-the-table-definition.md).  
  
 **En este tema**  
  
1.  [Página General](#GeneralPage)  
  
2.  [Página Seguimiento de cambios](#ChangeTracking)  
  
3.  [Página FileTable](#FileTable)  
  
4.  [Página Almacenamiento](#Storage)  
  
##  <a name="GeneralPage"></a> Página General  
 **Base de datos**  
 Nombre de la base de datos que contiene esta tabla.  
  
 **Server**  
 Nombre de la instancia de servidor actual.  
  
 **Usuario**  
 Nombre del usuario de esta conexión.  
  
 **Fecha de creación**  
 Fecha y hora de creación de la tabla.  
  
 **Name**  
 El nombre de la tabla.  
  
 **Esquema**  
 Esquema al que pertenece la tabla.  
  
 **Objeto de sistema**  
 Indica que esta tabla es una tabla de sistema, utilizada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para incluir información interna. Los usuarios no deben cambiar ni hacer referencia directamente a las tablas de sistema.  
  
 **Valores NULL ANSI**  
 Indica si el objeto se ha creado con la opción ANSI NULL establecida en ON. Para obtener más información, vea [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql).  
  
 **Identificador entre comillas**  
 Indica si el objeto se ha creado con la opción de identificador entre comillas establecida en ON. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).  
  
 **Extensión de bloqueo**  
 Indica la granularidad de la extensión de bloqueo de la tabla. Para obtener más información acerca del bloqueo del motor de base de datos, vea [Guía de las versiones de fila y el bloqueo de transacciones de SQL Server](https://msdn.microsoft.com/library/jj856598.aspx). Los valores posibles son:  
  
 AUTO  
 Esta opción permite al [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] seleccionar la granularidad de la escala de bloqueo que sea adecuada para el esquema de tabla.  
  
-   Si la tabla tiene particiones, se permitirá la extensión de bloqueo en la granularidad de árbol b (HoBT) o montón. Una vez realizada la extensión del bloqueo hasta el nivel de HoBT, el bloqueo no se extenderá a la granularidad de TABLE más adelante.  
  
-   Si la tabla no tiene particiones, la extensión del bloqueo se aplicará a la granularidad de TABLE.  
  
 TABLE  
 La extensión de bloqueo se aplicará a la granularidad de nivel de tabla, independientemente de que la tabla tenga o no particiones. TABLE es el valor predeterminado.  
  
 DISABLE  
 Evita la extensión de bloqueo en la mayoría de los casos. No siempre se evitan los bloqueos de nivel de la tabla. Por ejemplo, si está examinando una tabla que no tiene ningún índice clúster en el nivel de aislamiento serializable, [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe realizar un bloqueo de la tabla para proteger la integridad de los datos.  
  
 **Tabla replicada**  
 Indica si se ha replicado la tabla en otra base de datos mediante la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los valores posibles son `True` o `False`.  
  
##  <a name="ChangeTracking"></a> Página Seguimiento de cambios  
 **Seguimiento de los cambios**  
 Indica si el seguimiento de cambios está habilitado para la tabla. El valor predeterminado es `False`.  
  
 Esta opción solo está disponible cuando el seguimiento de cambios está habilitado para la base de datos.  
  
 Para habilitar el seguimiento de cambios, deberá contar con permisos para modificar la tabla y ésta deberá tener una clave principal. Puede configurar el seguimiento de cambios mediante [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql).  
  
 **Seguimiento de columnas actualizadas**  
 Indica si el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] hace un seguimiento de qué columnas se actualizaron.  
  
 Para obtener más información sobre el seguimiento de cambios, vea [Acerca del seguimiento de cambios &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md).  
  
##  <a name="FileTable"></a> Página FileTable  
 Muestra las propiedades de la tabla relacionada con las tablas FileTable. Para obtener más información, vea [FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md).  
  
 **Intercalación de la columna Nombre de una tabla FileTable**  
 La intercalación que se aplica a la columna **Nombre** de FileTable. La columna **Nombre** contiene nombres de archivo y de directorio.  
  
 **Nombre del directorio de FileTable**  
 La carpeta raíz para la tabla FileTable.  
  
 **Espacio de nombres de FileTable habilitado**  
 Si es `True`, este valor indica que la tabla es una tabla FileTable. Si cambia este valor a `False`, cambiará la tabla FileTable a una tabla de usuario ordinaria. Si posteriormente desea cambiar la tabla a una tabla FileTable, la tabla tiene que pasar una comprobación de coherencia de FileTable antes de que la conversión se realice correctamente.  
  
##  <a name="Storage"></a> Página Almacenamiento  
 Muestra las propiedades relacionadas con el almacenamiento de la tabla seleccionada.  
  
### <a name="compression"></a>Compresión  
 **Tipo de compresión**  
 El tipo de compresión de la tabla. Esta propiedad solo está disponible para tablas que no tienen particiones. Para obtener más información, consulte [Data Compression](../data-compression/data-compression.md).  
  
 **Particiones que utilizan la compresión de página**  
 El número de particiones que están utilizando la compresión de página. Esta propiedad solo está disponible para tablas con particiones.  
  
 **Particiones no comprimidas**  
 El número de particiones que no se comprimen. Esta propiedad solo está disponible para tablas con particiones.  
  
 **Particiones que utilizan la compresión de fila**  
 El número de particiones que están utilizando la compresión de fila. Esta propiedad solo está disponible para tablas con particiones.  
  
### <a name="filegroup"></a>Grupo de archivos  
 **Grupo de archivos de texto**  
 Nombre del grupo de archivos que contiene los datos de texto de la tabla.  
  
 **Grupo de archivos**  
 El nombre del grupo de archivos que contiene la tabla.  
  
 **La tabla tiene particiones**  
 Los valores posibles son `True` y `False`.  
  
 **Grupo de archivos de flujo de archivos**  
 Especifique el nombre del grupo de archivos de datos FILESTREAM si la tabla tiene una columna `varbinary(max)` con el atributo FILESTREAM. El valor predeterminado es el grupo de archivos de datos de FILESTREAM predeterminado.  
  
 Si la tabla no contiene datos de FILESTREAM, el campo estará en blanco.  
  
### <a name="general"></a>General  
 **El formato de almacenamiento Vardecimal está habilitado**  
 Cuando `True`, este valor de solo lectura indica que `decimal` y `numeric` tipos de datos se almacenan con el formato de almacenamiento vardecimal. Para cambiar esta opción, utilice el `vardecimal storage format` opción de [sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql). El formato de almacenamiento Vardecimal está en desuso. En su lugar, use la compresión de fila.  
  
 **Espacio de índice**  
 La cantidad de espacio en megabytes que ocupan los índices en la tabla. Este valor no incluye el uso del espacio del índice XML en la tabla. Si los índices XML pertenecen a la tabla, use [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) en su lugar.  
  
 **Recuento de filas**  
 Número de filas de la tabla.  
  
 **Espacio de datos**  
 La cantidad de espacio en megabytes que ocupan los datos en la tabla.  
  
### <a name="partitioning"></a>Creación de particiones  
 Esta sección solo está disponible si la tabla tiene particiones. Para obtener más información, vea [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).  
  
 **Columna de partición**  
 El nombre de la columna en la que la tabla tiene una partición.  
  
 **Esquema de partición**  
 Nombre del esquema de partición si la tabla tiene particiones. Si no tiene particiones, el campo está en blanco.  
  
 **Número de particiones**  
 El número de particiones de la tabla.  
  
 **Esquema de partición de FILESTREAM**  
 Nombre del esquema de partición de FILESTREAM si la tabla tiene particiones. Si no tiene particiones, el campo está en blanco.  
  
 El esquema de partición FILESTREAM debe ser simétrico al esquema especificado en la opción **Esquema de partición** .  
  
## <a name="see-also"></a>Vea también  
 [Ver la definición de tabla](view-the-table-definition.md)   
 [Modificar columnas &#40;motor de base de datos&#41;](../tables/modify-columns-database-engine.md)  
  
  
