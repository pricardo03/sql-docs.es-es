---
title: Requisitos del sistema para el controlador JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5b317b3483d24087df203eb14fdabe7b12f2539
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893972"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>Requisitos del sistema para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para acceder a los datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] mediante [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], debe tener los siguientes componentes instalados en el equipo:

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ([descargar](download-microsoft-jdbc-driver-for-sql-server.md))
- Java Runtime Environment

## <a name="java-runtime-environment-requirements"></a>Requisitos de Java Runtime Environment  

 A partir de Microsoft JDBC Driver 7.4 para SQL Server, se admiten Java Development Kit (JDK) 12.0 y Java Runtime Environment (JRE) 12.0.

 A partir de Microsoft JDBC Driver 7.2 para SQL Server, se admiten Java Development Kit (JDK) 11.0 y Java Runtime Environment (JRE) 11.0.
 
 A partir de Microsoft JDBC Driver 7.0 para SQL Server, se admiten Java Development Kit (JDK) 10.0 y Java Runtime Environment (JRE) 10.0.

 A partir de Microsoft JDBC Driver 6.4 para SQL Server, se admiten Java Development Kit (JDK) 9.0 y Java Runtime Environment (JRE) 9.0.

 A partir de Microsoft JDBC Driver 4.2 para SQL Server, se admiten Java Development Kit (JDK) 8.0 y Java Runtime Environment (JRE) 8.0. La compatibilidad con API de Java Database Connectivity (JDBC) Spec se ha ampliado para incluir la API de JDBC 4.1 y 4.2.
  
 A partir de Microsoft JDBC Driver 4.1 para SQL Server, se admiten Java Development Kit (JDK) 7.0 y Java Runtime Environment (JRE) 7.0.
  
 A partir de [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], la compatibilidad del controlador JDBC con la API de especificaciones de Java Database Connectivity (JDBC) se ha ampliado para incluir la API de JDBC 4.0. La API de JDBC 4.0 se presentó como parte de Java Development Kit (JDK) 6.0 y de Java Runtime Environment (JRE) 6.0. JDBC 4.0 es un superconjunto de la API de JDBC 3.0.
  
 Cuando se implementa [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] en sistemas operativos Windows y UNIX, se deben usar los paquetes de instalación, *sqljdbc_\<versión>_enu.exe* y *sqljdbc_\<versión>_enu.tar.gz*, respectivamente. Para obtener más información acerca de cómo implementar el controlador JDBC, vea el tema [Implementar el controlador JDBC](../../connect/jdbc/deploying-the-jdbc-driver.md).  

**Microsoft JDBC Driver 7.4 para SQL Server:**  

  JDBC Driver 7.4 incluye tres bibliotecas de clases JAR en cada paquete de instalación: **mssql-jdbc-7.4.1.jre8.jar**, **mssql-jdbc-7.4.1.jre11.jar** y **mssql-jdbc-7.4.1.jre12.jar**.

  JDBC Driver 7.4 está diseñado para funcionar con todas las máquinas virtuales de Java y ser compatible con ellas, aunque solo se ha probado en OpenJDK 1.8, OpenJDK 11.0, OpenJDK 12.0, Azul Zulu JRE 1.8, Azul Zulu JRE 11.0 y Azul Zulu JRE 12.0.
  
  A continuación se resume la compatibilidad que ofrecen los dos archivos JAR incluidos en Microsoft JDBC Driver 7.4 para SQL Server:  
  
  |JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|   
|MSSQL-JDBC-7.4.1. jre8. jar|4.2|8|Requiere la versión 1.8 de Java Runtime Environment (JRE). El uso de JRE 1.7 o anterior lanza una excepción.<br /><br /> Las nuevas características de 7,4 incluyen: compatibilidad con JDK 12, autenticación NTLM y useFmtOnly. |    
|MSSQL-JDBC-7.4.1. jre11. jar|4.3|11|Requiere Java Runtime Environment (JRE) 11.0. El uso de JRE 10.0 o anterior lanza una excepción.<br /><br /> Las nuevas características de 7,4 incluyen: compatibilidad con JDK 12, autenticación NTLM y useFmtOnly. |  
|MSSQL-JDBC-7.4.1. jre12. jar|4.3|12|Requiere la versión 12.0 de Java Runtime Environment (JRE). El uso de JRE 11.0 o anterior lanza una excepción.<br /><br /> Las nuevas características de 7,4 incluyen: compatibilidad con JDK 12, autenticación NTLM y useFmtOnly. |   


  El controlador JDBC Driver 7.4 también está disponible en el repositorio central de Maven y se puede agregar a un proyecto de Maven agregando el siguiente código en POM.XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
</dependency>
```

**Microsoft JDBC Driver 7.2 para SQL Server:**  

  JDBC Driver 7.2 incluye dos bibliotecas de clases JAR en cada paquete de instalación: **mssql-jdbc-7.2.2.jre8.jar** y **mssql-jdbc-7.2.2.jre11.jar**.

  JDBC Driver 7.2 está diseñado para funcionar con todas las máquinas virtuales de Java y ser compatible con ellas, aunque solo se ha probado en OpenJDK 8.0, OpenJDK 11.0, Azul Zulu JRE 8.0 y Azul Zulu JRE 11.0.
  
  A continuación se resume la compatibilidad que ofrecen los dos archivos JAR incluidos en Microsoft JDBC Driver 7.2 para SQL Server:  
  
  |JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.2.2.jre8.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanza una excepción.<br /><br /> Las nuevas características en 7.2 incluyen compatibilidad con JDK 11, autenticación de Managed Service Identity (MSI) de Active Directory, compatibilidad con OSGi, API de SQLServerError. |    
|mssql-jdbc-7.2.2.jre11.jar|4.3|10|Requiere Java Runtime Environment (JRE) 11.0. El uso de JRE 10.0 o anterior lanza una excepción.<br /><br /> Las nuevas características en 7.2 incluyen compatibilidad con JDK 11, autenticación de Managed Service Identity (MSI) de Active Directory, compatibilidad con OSGi, API de SQLServerError. |    


  El controlador JDBC Driver 7.2 también está disponible en el repositorio central de Maven y se puede agregar a un proyecto de Maven agregando el siguiente código en el POM.XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.2.jre11</version>
</dependency>
```
 
**Microsoft JDBC Driver 7.0 para SQL Server**  

  JDBC Driver 7.0 incluye dos bibliotecas de clases JAR en cada paquete de instalación: **mssql-jdbc-7.0.0.jre8.jar** y **mssql-jdbc-7.0.0.jre10.jar**.

  JDBC Driver 7.0 está diseñado para funcionar con todas las máquinas virtuales de Java y ser compatible con ellas, aunque solo se ha probado en OpenJDK 8.0 y 10.0.
  
  A continuación se resume la compatibilidad que ofrecen los dos archivos JAR incluidos en Microsoft JDBC Driver 7.0 para SQL Server:  
  
  |JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanza una excepción.<br /><br /> Las nuevas características en 7.0 incluyen compatibilidad con JDK 10, nivel de cumplimiento predeterminado actualizado a las especificaciones JDBC 4.2, compatibilidad con tipos de datos espaciales, propiedad de conexión cancelQueryTimeout, métodos de límite de solicitud, propiedad de conexión useBulkCopyForBatchInsert, información sobre detección y clasificación de datos, extensión de características UTF-8 y compatibilidad con CityHash. |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|Requiere Java Runtime Environment (JRE) 10.0. El uso de JRE 9.0 o anterior lanza una excepción.<br /><br /> Las nuevas características en 7.0 incluyen compatibilidad con JDK 10, nivel de cumplimiento predeterminado actualizado a las especificaciones JDBC 4.2, compatibilidad con tipos de datos espaciales, propiedad de conexión cancelQueryTimeout, métodos de límite de solicitud, propiedad de conexión useBulkCopyForBatchInsert, información sobre detección y clasificación de datos, extensión de características UTF-8 y compatibilidad con CityHash. |    


  El controlador JDBC Driver 7.0 también está disponible en el repositorio central de Maven y se puede agregar a un proyecto de Maven agregando el siguiente código en el POM.XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```
  
**Microsoft JDBC Driver 6.4 para SQL Server:**  

  JDBC Driver 6.4 incluye tres bibliotecas de clases JAR en cada paquete de instalación: **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** y **mssql-jdbc-6.4.0.jre9.jar**.

  JDBC Driver 6.4 está diseñado para funcionar con todas las máquinas virtuales de Java y ser compatible con ellas, aunque solo se ha probado en OpenJDK 7.0, 8.0 y 9.0.
  
  A continuación se resume la compatibilidad que ofrecen los tres archivos JAR incluidos en Microsoft JDBC Driver 6.4 para SQL Server:  
  
  |JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|Requiere la versión 7.0 de Java Runtime Environment (JRE). El uso de JRE 6.0 o anterior lanza una excepción.<br /><br /> Las nuevas características en 6.4 incluyen autenticación de Azure AD para Linux, método de entidad de seguridad y contraseña para Kerberos, detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, tiempo de expiración de consultas, tiempo de expiración de socket y reutilización del controlador de la declaración preparada. |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanza una excepción.<br /><br /> Las nuevas características en 6.4 incluyen autenticación de Azure AD para Linux, método de entidad de seguridad y contraseña para Kerberos, detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, tiempo de expiración de consultas, tiempo de expiración de socket y reutilización del controlador de la declaración preparada. |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|Requiere Java Runtime Environment (JRE) 9.0. El uso de JRE 8.0 o anterior lanza una excepción.<br /><br /> Las nuevas características en 6.4 incluyen autenticación de Azure AD para Linux, método de entidad de seguridad y contraseña para Kerberos, detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, tiempo de expiración de consultas, tiempo de expiración de socket y reutilización del controlador de la declaración preparada. |

El controlador JDBC Driver 6.4 también está disponible en el repositorio central de Maven y se puede agregar a un proyecto de Maven agregando el siguiente código en el POM.XML 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**Microsoft JDBC Driver 6.2 para SQL Server:**  
  
  JDBC Driver 6.2 incluye dos bibliotecas de clases JAR en cada paquete de instalación: **mssql-jdbc-6.2.2.jre7.jar** y **mssql-jdbc-6.2.2.jre8.jar**. 
  
 JDBC Driver 6.2 está diseñado para funcionar con todas las máquinas virtuales de Java y ser compatible con ellas, aunque solo se ha probado en Sun JRE 5.0, 6.0, 7.0 y 8.0.
  
 A continuación se resume la compatibilidad que ofrecen los dos archivos JAR incluidos en Microsoft JDBC Driver 6.0 y 4.2 para SQL Server:  
  
|JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|
|mssql-jdbc-6.2.2.jre7.jar|4.1|7|Requiere la versión 7.0 de Java Runtime Environment (JRE). El uso de JRE 6.0 o anterior lanza una excepción.<br /><br /> Las nuevas características en 6.2 incluyen autenticación de Azure AD para Linux, método de entidad de seguridad y contraseña para Kerberos, detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, tiempo de expiración de consultas, tiempo de expiración de socket y reutilización del controlador de la declaración preparada. |  
|mssql-jdbc-6.2.3.jre8.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanza una excepción.<br /><br /> Las nuevas características en 6.2 incluyen autenticación de Azure AD para Linux, método de entidad de seguridad y contraseña para Kerberos, detección automática de REALM en SPN para la autenticación entre dominios, delegación restringida de Kerberos, tiempo de expiración de consultas, tiempo de expiración de socket y reutilización del controlador de la declaración preparada|    

  El controlador JDBC Driver 6.2 también está disponible en el repositorio central de Maven y se puede agregar a un proyecto de Maven agregando el siguiente código en el POM.XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 y 4.2 para SQL Server:**  
  
  Los controladores JDBC Driver 6.0 y 4.2 incluyen dos bibliotecas de clases JAR en cada paquete de instalación: **sqljdbc41.jar** y **sqljdbc42.jar**. 
  
 JDBC Driver 6.0 y 4.2 están diseñados para funcionar con todas las máquinas virtuales de Java y ser compatible con ellas, aunque solo se ha probado en Sun JRE 5.0, 6.0, 7.0 y 8.0.
  
 A continuación se resume la compatibilidad que ofrecen los dos archivos JAR incluidos en Microsoft JDBC Driver 6.0 y 4.2 para SQL Server:  
  
|JAR|Cumplimiento con la versión JDBC|Versión de Java recomendada|Descripción|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Requiere la versión 7.0 de Java Runtime Environment (JRE). El uso de JRE 6.0 o anterior lanza una excepción.<br /><br /> Las nuevas características de los paquetes 6.0 y 4.2 incluyen JBC 4.1 Compliance y Bulk Copy<br /><br /> Además, las nuevas características de solo el paquete 6.0 incluyen Always Encrypted, parámetros con valores de tabla, autenticación de Azure Active Directory, conexiones transparentes a los grupos de disponibilidad Always On, mejora en la recuperación de metadatos de parámetros para consultas preparadas y nombre de dominio internacionalizado (IDN)|  
|sqljdbc42.jar|4.2|8|Requiere la versión 8.0 de Java Runtime Environment (JRE). El uso de JRE 7.0 o anterior lanza una excepción.<br /><br /> Las nuevas características de los paquetes 6.0 y 4.2 incluyen JDBC 4.1 Compliance, JDBC 4.2 Compliance y Bulk Copy<br /><br /> Además, las nuevas características de solo el paquete 6.0 incluyen Always Encrypted, parámetros con valores de tabla, autenticación de Azure Active Directory, conexiones transparentes a los grupos de disponibilidad Always On, mejora en la recuperación de metadatos de parámetros para consultas preparadas y nombre de dominio internacionalizado (IDN)|  
  
 **Microsoft JDBC Driver 4.1 para SQL Server:**  
  
 El controlador JDBC Driver 4.1 incluye una biblioteca de clases JAR en cada paquete de instalación: **sqljdbc41.jar**.  
    
|JAR|Descripción|  
|---------|-----------------|  
|sqljdbc41.jar|La biblioteca de clases **sqljdbc41.jar** proporciona compatibilidad con la API de JDBC 4.0. Incluye todas las características de JDBC 4.0 y los métodos de la API de JDBC 4.0. JDBC 4.1 no es compatible (se produce la excepción "SQLFeatureNotSupportedException").<br /><br /> La biblioteca de clases **sqljdbc41.jar** requiere Java Runtime Environment (JRE) 7.0. El uso de **sqljdbc41.jar** en JRE 6.0 y 5.0 lanza una excepción.<br /><br /> 
  
 JDBC Driver está diseñado para funcionar con todas las máquinas virtuales de Java y ser compatible con ellas, aunque se ha probado en Sun JRE 5.0, 6.0 y 7.0.
  
 A continuación se resume la compatibilidad que ofrece el archivo JAR incluido en Microsoft JDBC Driver 4.1 para SQL Server.  
  
|JAR|Versión de JDBC|JRE (puede ejecutarse)|JDK (puede compilar)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>Requisitos de SQL Server  
 El controlador JDBC admite conexiones a Azure SQL Database y SQL Server. Para Microsoft JDBC Driver 4.2 y 4.1 para SQL Server, la compatibilidad comienza a partir de SQL Server 2008.
  
## <a name="operating-system-requirements"></a>Requisitos de sistema operativo  
 El controlador JDBC se ha diseñado para funcionar en cualquier sistema operativo que admita el uso de una máquina virtual Java (JVM). No obstante, solo se han probado oficialmente los sistemas operativos Sun Solaris, SUSE Linux y Windows.  
  
## <a name="supported-languages"></a>Idiomas admitidos  
 El controlador JDBC es compatible con todas las intercalaciones de columnas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información acerca de las intercalaciones compatibles con el controlador JDBC, consulte [Características internacionales del controlador JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md).  
  
 Para obtener más información sobre las intercalaciones, vea "Trabajar con intercalaciones" en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
