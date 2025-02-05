---
title: Conexión y recuperación de datos | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c7e642879c095dd4d9dca4f51a936ab72c523e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956883"
---
# <a name="connecting-and-retrieving-data"></a>Conectar y recuperar datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Cuando se trabaja con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], hay dos métodos principales para establecer una conexión con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uno de estos métodos establece las propiedades de conexión en la URL de conexión y, a continuación, llama al método getConnection de la clase DriverManager para devolver un objeto [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
> [!NOTE]  
> Para obtener una lista de las propiedades de conexión compatibles con el controlador JDBC, vea [establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
El segundo método implica el establecimiento de las propiedades de conexión mediante los métodos establecedores de la clase [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) y, a continuación, la llamada al método [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) para devolver un objeto SQLServerDataSource.  
  
En los temas de esta sección se describen los distintos modos en que puede conectarse a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se muestran las distintas técnicas para recuperar datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
| Tema                                                                | Descripción                                                                                                                                                   |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Ejemplo de URL de conexión](../../connect/jdbc/connection-url-sample.md) | Describe cómo usar una URL de conexión para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usar una instrucción SQL para recuperar datos. |
| [Ejemplo de origen de datos](../../connect/jdbc/data-source-sample.md)       | Describe cómo usar un origen de datos para conectarse a SQL y usar un procedimiento almacenado para recuperar datos.                                                 |
  
## <a name="see-also"></a>Consulte también

[Aplicaciones del controlador JDBC de ejemplo](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
