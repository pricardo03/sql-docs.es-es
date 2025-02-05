---
title: Usar metadatos del conjunto de resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86e41f52ed8296c46cfd7b167407b10fc9f0b285
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005943"
---
# <a name="using-result-set-metadata"></a>Usar metadatos del conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para consultar información sobre las columnas que contiene un conjunto de resultados, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementa la clase [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). Esta clase contiene varios métodos que devuelven información como un solo valor.

Para crear un objeto SQLServerResultSetMetaData, puede utilizar el método [GetMetadata](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) .

En el ejemplo siguiente, se pasa una conexión abierta [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la base de datos de ejemplo a la función, el método GetMetadata de la clase SQLServerResultSet se usa para devolver un objeto SQLServerResultSetMetaData y, a continuación, varios métodos de la El objeto SQLServerResultSetMetaData se usa para mostrar información sobre el nombre y el tipo de datos de las columnas contenidas en el conjunto de resultados.

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>Consulte también

[Controlar metadatos con el controlador JDBC](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
