---
title: Preguntas más frecuentes (P+F) sobre el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 17032e4d1bd6487edc0b0b41b7f808c27ab995ee
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892373"
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>Preguntas más frecuentes (P+F) sobre el controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En esta página se ofrecen respuestas a las preguntas más frecuentes sobre Microsoft JDBC Driver for SQL Server.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**¿Cómo puedo ayudar a mejorar el controlador JDBC Driver?**  
El controlador JDBC Driver es de código abierto, y el código fuente puede encontrarse en [GitHub](https://github.com/microsoft/mssql-jdbc). Puede ayudar a mejorar el controlador notificando problemas y contribuyendo a la base del código.

**¿Qué versiones de SQL Server y Java admite el controlador?**  
Consulte la página [Microsoft JDBC Driver for SQL Server Support Matrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) para más información.

**¿Cuál es la diferencia entre los paquetes del controlador JDBC Driver disponibles en el Centro de descarga de Microsoft y el controlador JDBC Driver disponible en GitHub?**  
Los archivos del controlador JDBC Driver disponibles en el repositorio GitHub para el controlador JDBC Driver de Microsoft son el núcleo del controlador JDBC Driver y están bajo la licencia de código abierto que se encuentra en el repositorio. Los paquetes del controlador del Centro de descarga de Microsoft incluyen bibliotecas adicionales para la autenticación integrada de Windows y la habilitación de transacciones XA con el controlador JDBC Driver. Esas bibliotecas adicionales están bajo la licencia incluida con el paquete descargable.

**¿Qué debo saber al actualizar el controlador?**
El controlador Microsoft JDBC Driver 7.4 admite especificaciones de JDBC 4.2 y 4.3 (parcialmente) e incluye tres bibliotecas de clases de archivo JAR en el paquete de instalación, tal y como se muestra a continuación:

| JAR                        | Especificación de JDBC            | Versión JDK |
| -------------------------- | ----------------------------- | ----------- |
| MSSQL-JDBC-7.4.1. jre12. jar | JDBC 4.3 (parcialmente) y 4.2 | JDK 12.0    |
| MSSQL-JDBC-7.4.1. jre11. jar | JDBC 4.3 (parcialmente) y 4.2 | JDK 11.0    |
| MSSQL-JDBC-7.4.1. jre8. jar  | JDBC 4.2                      | JDK 8.0     |

 El controlador Microsoft JDBC Driver 7.2 admite especificaciones de JDBC 4.2 y 4.3 (parcialmente) e incluye dos bibliotecas de clases de archivo JAR en el paquete de instalación, tal y como se muestra a continuación:

| JAR                        | Especificación de JDBC            | Versión JDK |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.2.2.jre11.jar | JDBC 4.3 (parcialmente) y 4.2 | JDK 11.0    |
| mssql-jdbc-7.2.2.jre8.jar  | JDBC 4.2                      | JDK 8.0     |

 El controlador Microsoft JDBC Driver 7.0 admite especificaciones de JDBC 4.2 y 4.3 (parcialmente) e incluye dos bibliotecas de clases de archivo JAR en el paquete de instalación, tal y como se muestra a continuación:

| JAR                        | Especificación de JDBC            | Versión JDK |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.0.0.jre10.jar | JDBC 4.3 (parcialmente) y 4.2 | JDK 10.0    |
| mssql-jdbc-7.0.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |

El controlador Microsoft JDBC Driver 6.4 admite especificaciones de JDBC 4.1, 4.2 y 4.3 (parcialmente) e incluye tres bibliotecas de clases de archivo JAR en el paquete de instalación, tal y como se muestra a continuación:

| JAR                       | Especificación de JDBC                 | Versión JDK |
| ------------------------- | ---------------------------------- | ----------- |
| mssql-jdbc-6.4.0.jre9.jar | JDBC 4.3 (parcialmente), 4.2 y 4.1 | JDK 9.0     |
| mssql-jdbc-6.4.0.jre8.jar | JDBC 4.2 y 4.1                  | JDK 8.0     |
| mssql-jdbc-6.4.0.jre7.jar | JDBC 4.1                           | JDK 7.0     |

El controlador Microsoft JDBC Driver 6.2 admite especificaciones de JDBC 4.0, 4.1 y 4.2 e incluye dos bibliotecas de clases de archivo JAR en el paquete de instalación, tal y como se muestra a continuación:

| JAR                       | Especificación de JDBC     | Versión JDK |
| ------------------------- | ---------------------- | ----------- |
| mssql-jdbc-6.2.2.jre8.jar | JDBC 4.0, 4.1 y 4.2 | JDK 8.0     |
| mssql-jdbc-6.2.2.jre7.jar | JDBC 4.1 y 4.0       | JDK 7.0     |

Los controladores Microsoft JDBC Driver 6.0 y 4.2 para SQL Server admiten especificaciones de JDBC 4.0, 4.1 y 4.2 e incluyen dos bibliotecas de clases de archivo JAR en el paquete de instalación, tal y como se muestra a continuación:

| JAR           | Especificación de JDBC     | Versión JDK |
| ------------- | ---------------------- | ----------- |
| sqljdbc42.jar | JDBC 4.0, 4.1 y 4.2 | JDK 8.0     |
| sqljdbc41.jar | JDBC 4.1 y 4.0       | JDK 7.0     |

El controlador Microsoft JDBC Driver 4.1 para SQL Server admite la especificación de JDBC 4.0 e incluye una biblioteca de clases de archivo JAR en el paquete de instalación, tal y como se muestra a continuación:

| JAR           | Especificación de JDBC | Versión JDK     |
| ------------- | ------------------ | --------------- |
| sqljdbc41.jar | JDBC 4.0           | JDK 7.0 y 6.0 |

**¿Necesito realizar cambios de código en mi aplicación para poder usar el controlador más reciente con la versión de SQL Server que tengo actualmente?**  
Por lo general, el controlador se diseña para que sea compatible con versiones anteriores, así que no es necesario cambiar las aplicaciones existentes al actualizar el controlador. En caso de que una nueva versión del controlador presente un cambio importante, puede consultar la sección [Notas de la versión para el controlador JDBC de Microsoft](../../connect/jdbc/release-notes-for-the-jdbc-driver.md) para saber con claridad qué cambios se han realizado y el impacto que tendrán en las aplicaciones existentes. Además, puede consultar las notas de la versión incluidas con el controlador para obtener una lista de errores corregidos en esa versión y problemas conocidos.

**¿Cuánto cuesta el controlador?**  
Microsoft JDBC Driver for SQL Server está disponible sin ningún coste adicional.

**¿Se puede redistribuir el controlador?**
Los controladores JDBC Driver 4.1, 4.2, 6.0, 6.2, 6.4 y 7.0 son redistribuibles. Revise la cláusula "Código distribuible" en los contratos de licencia.

**¿Puedo usar el controlador para acceder a Microsoft SQL Server desde un equipo Linux?**
Sí. Puede utilizar el controlador para acceder a SQL Server desde otras plataformas distintas de Windows, Unix y Linux. Para obtener más información, consulte [Matriz de compatibilidad de Microsoft JDBC Driver para SQL Server](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md).

**¿El controlador admite el cifrado de Capa de sockets seguros (SSL)?**
A partir de la versión 1.2, el controlador admite el cifrado de capa de sockets seguros (SSL). Para más información, consulte [Usar el cifrado SSL](../../connect/jdbc/using-ssl-encryption.md).

**¿Qué tipos de autenticación admite Microsoft JDBC Driver para SQL Server?**  
En la tabla siguiente se muestran las opciones de autenticación disponibles. La autenticación Kerberos pura de Java está disponible a partir de la versión 4.0 del controlador.

|             |                                       |
| ----------- | ------------------------------------- |
| Plataforma    | Autenticación                        |
| Distinta de Windows | Kerberos pura de Java                    |
| Distinta de Windows | SQL Server                            |
| Distinta de Windows | Autenticación de Azure Active Directory |
| Windows     | Kerberos pura de Java                    |
| Windows     | SQL Server                            |
| Windows     | Kerberos con copia de seguridad NTLM             |
| Windows     | NTLM                                  |
| Windows     | Autenticación de Azure Active Directory |

**¿El controlador es compatible con las direcciones de la versión 6 del protocolo de Internet (IPv6)?**  
Sí. El controlador admite el uso de direcciones IPv6. Use la colección de las propiedades de conexión y la propiedad de la cadena de conexión serverName. Para más información, consulte [Generar URL de conexión](../../connect/jdbc/building-the-connection-url.md).

**¿Qué es el almacenamiento en búfer adaptable?**  
El almacenamiento en búfer adaptable se introdujo a partir de la versión 1.2 del controlador JDBC Driver de Microsoft SQL Server 2005. Se diseña para recuperar cualquier tipo de datos de valores grandes sin sufrir la sobrecarga de los cursores de servidor. La característica de almacenamiento en búfer adaptable de Microsoft SQL Server JDBC Driver proporciona una propiedad de cadena de conexión, responseBuffering, cuyos valores puede establecerse en "adaptive" o "full". En la versión 1.2, el modo del almacenamiento en búfer es "full" de manera predeterminada y la aplicación debe establecer el modo de almacenamiento en búfer adaptable explícitamente. A partir de Microsoft JDBC Driver 2.0, el comportamiento predeterminado del controlador es "adaptive". Por tanto, la aplicación no tiene que solicitar explícitamente el comportamiento adaptable para obtener dicho comportamiento. Para obtener más información, vea [Usar el almacenamiento en búfer adaptable](../../connect/jdbc/using-adaptive-buffering.md) y la entrada de blog [What is adaptive response buffering and why should I use it?](https://go.microsoft.com/fwlink/?LinkId=111575) (¿Qué es el almacenamiento en búfer adaptable y por qué se debe usar?).

**¿El controlador es compatible con la agrupación de conexiones?**  
El controlador proporciona compatibilidad con la agrupación de conexiones de Java Platform, Enterprise Edition 5 (Java EE 5). El controlador implementa las interfaces necesarias de JDBC 3.0 para que pueda participar en la implementación de la agrupación de conexiones de los proveedores de servidores de aplicaciones de software intermedio. El controlador participa en las conexiones agrupadas en estos entornos. Para obtener más información, consulte [Using Connection Pooling](../../connect/jdbc/using-connection-pooling.md). El controlador no proporciona su propia implementación de agrupación, sino que se basa en servidores de aplicaciones Java de terceros.

**¿Hay servicios de soporte disponibles para el controlador?**  
Existen varias opciones de soporte. Puede publicar su pregunta o problema en nuestro [repositorio de GitHub](https://github.com/microsoft/mssql-jdbc), que supervisa Microsoft. Los [foros](https://go.microsoft.com/fwlink/?LinkID=246673) se supervisan por Microsoft, los MVP y la comunidad. También puede ponerse en contacto con el equipo de asistencia al cliente de Microsoft. El equipo de desarrollo puede pedirle que reproduzca el problema fuera de los servidores de aplicaciones de terceros. Si el problema no se puede reproducir fuera del entorno de contenedor host de Java, tendrá que ponerse en contacto con el tercero relacionado para que el equipo pueda seguir ayudándolo. También puede que el equipo le pida que reproduzca el problema en un sistema operativo concreto, como Windows, para que podamos ofrecerle la mejor ayuda posible.

**¿Está el controlador certificado para usarse con servidores de aplicaciones de terceros?**
El controlador se ha probado con los principales servidores de aplicaciones, incluidos IBM WebSphere y SAP NetWeaver.

**¿Cómo se habilita el seguimiento?**  
El controlador admite el uso del seguimiento (o registro) para ayudar a solucionar problemas con Microsoft JDBC Driver cuando se esté utilizando en su aplicación. Para habilitar el uso de seguimiento de archivos JAR del lado cliente, Microsoft JDBC Driver utiliza las API de registro de java.util.logging. Para obtener más información, vea [Hacer un seguimiento del funcionamiento del controlador](../../connect/jdbc/tracing-driver-operation.md). Para el seguimiento de archivos XA del lado servidor, consulte [Data Access Tracing in SQL Server](https://go.microsoft.com/fwlink/?LinkId=248705)(Seguimiento de datos de acceso en SQL Server).

**¿Dónde puedo descargar las versiones anteriores del controlador como Microsoft JDBC Driver para SQL Server 2000 o 2005, o las versiones 1.0, 1.1 o 1.2?**  
Estas versiones del controlador no están disponibles para descargarse debido a que ya no son compatibles. Estamos trabajando continuamente para mejorar la compatibilidad con la conectividad de Java. Por tanto, se recomienda encarecidamente trabajar con la versión más reciente de Microsoft JDBC Driver.

**Uso JRE 1.4. ¿Qué controlador es compatible con JRE 1.4?**  
Los clientes que utilizan productos SAP y requieren compatibilidad con JRE 1.4, pueden ponerse en contacto con [SAPService Marketplace](https://service.sap.com/) para obtener Microsoft JDBC driver 1.2.

**¿Puede el controlador comunicarse mediante algoritmos aprobados en FIPS?**  
Microsoft JDBC Driver no contiene algoritmos criptográficos. Si un cliente utiliza algoritmos de sistemas operativos, aplicaciones y JVM que el estándar federal de procesamiento de información (FIPS) considera aceptables y configura el controlador para usar esos algoritmos, el controlador usa solo los designados para la comunicación.

## <a name="see-also"></a>Vea también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)
