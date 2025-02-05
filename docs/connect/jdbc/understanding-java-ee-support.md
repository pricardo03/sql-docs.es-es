---
title: Descripción de la compatibilidad con Java EE | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a9448b80-b7a3-49cf-8bb4-322c73676005
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 318800db7335a47226e75a4e05a4493c366507f9
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892311"
---
# <a name="understanding-java-ee-support"></a>Descripción de la compatibilidad con Java EE

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En las secciones siguientes se documenta cómo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona compatibilidad con las características de las API opcionales de Java Platform, Enterprise Edition (Java EE) y JDBC 3.0. Los ejemplos del código fuente que se proporcionan en este sistema de Ayuda proporcionan una referencia adecuada para comenzar a usar estas características.  
  
Primero, asegúrese de que el entorno de Java (JDK, JRE) incluye el paquete javax.sql. Es un paquete necesario para cualquier aplicación JDBC que utilice la API opcional. JDK 1.5 y las versiones posteriores ya contienen este paquete, por lo que no tiene que instalarlo por separado.  
  
## <a name="driver-name"></a>Nombre del controlador

El nombre de clase del controlador es **com.microsoft.sqlserver.jdbc.SQLServerDriver**. Para JDBC Driver 4.1, 4.2 y 6.0, el controlador se encuentra en el archivo **sqljdbc.jar**, **sqljdbc4.jar**, **sqljdbc41.jar** o **sqljdbc42.jar**.

Para el controlador JDBC Driver 6.2, el controlador se encuentra en **mssql-jdbc-6.2.2.jre7.jar** o **mssql-jdbc-6.2.2.jre8.jar**.

Para el controlador JDBC Driver 6.4, el controlador se encuentra en **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** o **mssql-jdbc-6.4.0.jre9.jar**.

Para el controlador JDBC Driver 7.0, el controlador se encuentra en **mssql-jdbc-7.0.0.jre8.jar** o **mssql-jdbc-7.0.0.jre10.jar**.

Para el controlador JDBC Driver 7.2, el controlador se encuentra en **mssql-jdbc-7.2.2.jre8.jar** o **mssql-jdbc-7.2.2.jre11.jar**.

Para el controlador JDBC Driver 7.4, el controlador se encuentra en **mssql-jdbc-7.4.1.jre8.jar**, **mssql-jdbc-7.4.1.jre11.jar** o **mssql-jdbc-7.4.1.jre12.jar**.
  
El nombre de clase se usa siempre que se carga el controlador con la clase DriverManager de JDBC y siempre que se especifica el nombre de clase del controlador en cualquier configuración de controlador. Por ejemplo, configurar un origen de datos dentro de un servidor de aplicaciones de Java EE podría requerir que se escribiera el nombre de clase del controlador.  
  
## <a name="data-sources"></a>Orígenes de datos

El controlador JDBC proporciona compatibilidad con los orígenes de datos de Java EE / JDBC 3.0. La clase [SQLServerXADataSource ](../../connect/jdbc/reference/sqlserverxadatasource-class.md) del controlador JDBC Driver se implementa por `com.microsoft.sqlserver.jdbc.SQLServerXADataSource`.  
  
### <a name="datasource-names"></a>Nombre de los orígenes de datos

Puede realizar conexiones a bases de datos mediante orígenes de datos. Los orígenes de datos disponibles con el controlador JDBC se describen en la tabla siguiente:  
  
|Tipo de origen de datos|Nombre de clase y descripción|  
|---------------|--------------------------|  
|DataSource|`com.microsoft.sqlserver.jdbc.SQLServerDataSource` <br/> <br/> Origen de datos que no es un grupo.|  
|ConnectionPoolDataSource|`com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource` <br/> <br/> Origen de datos para configurar los grupos de conexiones de servidor de aplicaciones de JAVA EE. Normalmente se usa cuando la aplicación se ejecuta dentro de un servidor de aplicaciones de JAVA EE.|  
|XADataSource|`com.microsoft.sqlserver.jdbc.SQLServerXADataSource` <br/> <br/> Origen de datos para configurar orígenes de datos de JAVA EE XA. Normalmente se usa cuando la aplicación se ejecuta dentro de un servidor de aplicaciones de JAVA EE y un administrador de transacciones de XA.|  
  
### <a name="data-source-properties"></a>Propiedades de origen de datos

Todos los orígenes de datos permiten establecer y obtener cualquier propiedad que esté asociada al conjunto de propiedades del controlador subyacente.  
  
Ejemplos:  
  
`setServerName("localhost");`  
`setDatabaseName("AdventureWorks");`  
  
A continuación se muestra cómo se conecta una aplicación mediante un origen de datos:  

```java
//initialize JNDI ..  
Context ctx = new InitialContext(System.getProperties());
...
DataSource ds = (DataSource) ctx.lookup("MyDataSource");
Connection c = ds.getConnection("user", "pwd");  
```

Para obtener más información acerca de las propiedades del origen de datos, vea [Establecer las propiedades de los orígenes de datos](../../connect/jdbc/setting-the-data-source-properties.md).  
  
## <a name="see-also"></a>Consulte también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
