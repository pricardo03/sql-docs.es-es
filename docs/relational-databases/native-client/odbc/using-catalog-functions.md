---
title: Utilizar funciones de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQLLinkedCatalogs function
- SQL Server Native Client ODBC driver, catalog functions
- SQLLinkedServers function
- catalog functions [ODBC]
- functions [ODBC]
ms.assetid: 7773fb2e-06b5-4c4b-88e9-0ad9132ad273
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c24e98f15793820df59bf372a73e42204814fb19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913070"
---
# <a name="using-catalog-functions"></a>Utilizar funciones de catálogo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Todas las bases de datos tienen una estructura que contiene los datos almacenados en la base de datos. Una definición de esta estructura, junto con otra información como permisos, está almacenada en un catálogo (se implementa como un conjunto de tablas del sistema), también conocido como diccionario de datos.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client permite que una aplicación determinar la estructura de base de datos a través de llamadas a funciones de catálogo ODBC. Las funciones de catálogo devuelven información en conjuntos de resultados y se implementan utilizando procedimientos almacenados de catálogo para consultar las tablas del sistema en el catálogo. Por ejemplo, una aplicación puede solicitar un conjunto de resultados que contenga información sobre todas las tablas del sistema o todas las columnas de una tabla determinada. Las funciones de catálogo estándar de ODBC se utilizan para obtener información de catálogo del servidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al que está conectada la aplicación.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite consultas distribuidas en las que se tiene acceso a datos de varios orígenes de datos OLE DB heterogéneos en una única consulta. Uno de los métodos para tener acceso a un origen de datos OLE DB remoto consiste en definir el origen de datos como un servidor vinculado. Esto puede hacerse mediante el uso de [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Una vez definido el servidor vinculado, se puede hacer referencia a los objetos de ese servidor en instrucciones Transact-SQL utilizando un nombre con cuatro partes:  
  
 *linked_server_name.catalog.schema.object_name*.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite dos funciones específicas del controlador que ayudan a obtener información de catálogo de los servidores vinculados:  
  
-   **SQLLinkedServers**  
  
     Devuelve una lista de los servidores vinculados definidos para el servidor local.  
  
-   **SQLLinkedCatalogs**  
  
     Devuelve una lista de los catálogos incluidos en un servidor vinculado.  
  
 Una vez que tenga un nombre de servidor vinculado y un nombre de catálogo, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client permite obtener información desde el catálogo con un nombre de dos partes de _linked_server_name_ **.** _catálogo_ para *CatalogName* funciones de catálogo de ODBC siguiente:  
  
-   **SQLColumnPrivileges**  
  
-   **SQLColumns**  
  
-   **SQLPrimaryKeys**  
  
-   **SQLStatistics**  
  
-   **SQLTablePrivileges**  
  
-   **SQLTables**  
  
 Las dos partes _linked_server_name_ **.** _catálogo_ también es compatible con *FKCatalogName* y *PKCatalogName* en [SQLForeignKeys](../../../relational-databases/native-client-odbc-api/sqlforeignkeys.md).  
  
 Para utilizar SQLLinkedServers y SQLLinkedCatalogs hacen falta los siguientes archivos:  
  
-   sqlncli.h  
  
     Incluye prototipos de función y definiciones de constante para las funciones de catálogo del servidor vinculado. Se debe haber incluido sqlncli.h en la aplicación ODBC y ha de estar en la ruta de inclusión cuando se compile la aplicación.  
  
-   sqlncli11.lib  
  
     Debe estar en la ruta de acceso de la biblioteca del vinculador y estar especificado como un archivo que se va a vincular. sqlncli11.lib se distribuye con el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   sqlncli11.dll  
  
     Debe estar presente en el momento de la ejecución. sqlncli11.dll se distribuye con el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLColumnPrivileges](../../../relational-databases/native-client-odbc-api/sqlcolumnprivileges.md)   
 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)   
 [SQLPrimaryKeys](../../../relational-databases/native-client-odbc-api/sqlprimarykeys.md)   
 [SQLTablePrivileges](../../../relational-databases/native-client-odbc-api/sqltableprivileges.md)   
 [SQLTables](../../../relational-databases/native-client-odbc-api/sqltables.md)   
 [SQLStatistics](../../../relational-databases/native-client-odbc-api/sqlstatistics.md)  
  
  
