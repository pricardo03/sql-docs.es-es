---
title: Usar metadatos de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fbe290c558dd8c64605bad0a977657904582c696
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916260"
---
# <a name="using-database-metadata"></a>Usar metadatos de una base de datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar en una base de datos información sobre compatibilidad, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la clase [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). Esta clase contiene numerosos métodos que devuelven información en forma de un solo valor o de conjunto de resultados.

Para crear un objeto SQLServerDatabaseMetaData, puede usar el método [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) para obtener información sobre la base de datos a la que está conectado.

En el ejemplo siguiente, se pasa una conexión abierta [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la base de datos de ejemplo a la función, el método GetMetadata de la clase SQLServerConnection se usa para devolver un objeto SQLServerDatabaseMetadata y, a continuación, varios métodos de la El objeto SQLServerDatabaseMetaData se usa para mostrar información sobre el controlador, la versión del controlador, el nombre de la base de datos y la versión de la base de datos.

[!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]

## <a name="see-also"></a>Consulte también

[Controlar metadatos con el controlador JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
