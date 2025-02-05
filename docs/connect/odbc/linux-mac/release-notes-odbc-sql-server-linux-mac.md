---
title: Notas de la versión de ODBC en Linux y macOS | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: MightyPen
ms.technology: connectivity
ms.topic: conceptual
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 5d2587a6150807841edc9773478f1b798ee60d84
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742810"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-to-sql-server-on-linux-and-macos"></a>Notas de la versión de Microsoft ODBC Driver para SQL Server en Linux y macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este artículo se enumeran y describen las novedades en los lanzamientos de versiones del controlador ODBC de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS.

<!--
Going forward, please use the new 2-column markdown table for each new H2 version section.
And we are keeping the H2 titles much shorter, partly by removing redundant or obvious info.
We want to track the Month YYYY each new version H2 section is added, at the end of the H2 title.
This is the new standard format for Release Notes article content.

OLD     FILE NAME:    linux-mac/release-notes.md
NOW NEW FILE NAME:    linux-mac/release-notes-odbc-sql-server-linux-mac.md

Thank you.
GeneMi.  2019/04/03.
-->
## <a name="174-august-2019"></a>17,4, 2019 de agosto

| Característica agregada | Detalles |
| :------------ | :------ |
| Always Encrypted con enclaves seguros. | Consulte [Uso de Always Encrypted con ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md). |
| Carga dinámica de OpenSSL | Consulte [Instrucciones de programación ](programming-guidelines.md#bkmk-openssl). |
| Configuración de mantenimiento de conexión TCP configurable. | Consulte [Conectarse a SQL Server](connection-string-keywords-and-data-source-names-dsns.md). |
| Correcciones de errores. | Vea [Correcciones de errores](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="173-february-2019"></a>17.3, febrero de 2019

| Nuevo elemento | Detalles |
| :------- | :------ |
| Nuevas distribuciones compatibles. | &bull; &nbsp; &nbsp; SuSE 15<br/>&bull; &nbsp; &nbsp; Ubuntu 18.10<br/>&bull; &nbsp; &nbsp; macOS 10.14 |
| Modo de autenticación de Azure Active Directory Managed Service Identity (del sistema y asignado por el usuario). | Consulte [Uso de Azure Active Directory con el controlador ODBC](../using-azure-active-directory.md). |
| Capacidad de transmitir en secuencias los parámetros de entrada con columnas Always Encrypted. | Para obtener más información, vea [Limitations of the ODBC driver when using Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted) (Limitaciones del controlador ODBC al usar Always Encrypted). |
| Transacciones distribuidas XA. | Vea [Uso de las transacciones XA](../use-xa-with-dtc.md).<br/><br/>"XA" son las siglas de _eXtended Architecture (arquitectura ampliada)_ , que es un estándar para la ejecución de una transacción global que accede a más de un sistema de almacenamiento de datos del servidor. |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2, julio de 2018

| Nuevo elemento | Detalles |
| :------- | :------ |
| Nuevas distribuciones compatibles. | &bull; &nbsp; &nbsp; Ubuntu 18.04 |
| Clasificación de datos para Azure SQL Database y SQL Server. | Vea [Clasificación de datos](../data-classification.md). |
| Admite la codificación de servidor UTF-8. | &nbsp; |
| `SQLBrowseConnect` | &nbsp; |
| Dependencia dinámica en `libcurl`. | A partir de esta versión, el paquete `libcurl` no es una dependencia explícita.<br/>El paquete `libcurl` de OpenSSL o NSS es necesario cuando se usa la autenticación de Azure Active Directory o Azure Key Vault.<br/>Si detecta un error con respecto a `libcurl`, asegúrese de que está instalado. |
| Resistencia de conexión inactiva con palabras clave de ConnectRetryCount y ConnectRetryInterval en la cadena de conexión. | &bull; &nbsp; &nbsp; Use `SQL_COPT_SS_CONNECT_RETRY_COUNT` (solo lectura) para recuperar el número de reintentos de conexión.<br/><br/>&bull; &nbsp; &nbsp; Use `SQL_COPT_SS_CONNECT_RETRY_INTERVAL` (solo lectura) para recuperar la duración del intervalo de reintentos de conexión.<br/><br/>Vea [Resistencia de conexión en el controlador Windows ODBC](../windows/connection-resiliency-in-the-windows-odbc-driver.md). |
| Correcciones de errores. | [Correcciones de errores](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1, marzo de 2018

| Nuevo elemento | Detalles |
| :------- | :------ |
| Compatibilidad con atributos de conexión de `SQL_COPT_SS_CEKCACHETTL` y `SQL_COPT_SS_TRUSTEDCMKPATHS`. | &bull; &nbsp; &nbsp; `SQL_COPT_SS_CEKCACHETTL` permite controlar el momento en que existe la memoria caché local de las claves de cifrado de columna, así como vaciarla.<br/><br/>&bull; &nbsp; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS` permite que la aplicación restrinja las operaciones de Always Encrypted para que solo usen la lista especificada de claves maestras de columna.<br/><br/>Vea [Using Always Encrypted with the ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md) (Uso de Always Encrypted con el controlador ODBC para SQL Server). |
| Compatibilidad para cargar `.rll` desde la ubicación predeterminada. | Vea la sección [Carga del archivo de recursos](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading) en el documento de instalación. |
| Correcciones de errores. | [Correcciones de errores](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="17"></a>17

**Nuevas distribuciones compatibles**: macOS High Sierra y Ubuntu 17.10 

**Mejoras de rendimiento**: el rendimiento se multiplica por más de 10 cuando el controlador convierte a o desde UTF-8/16.

**Características agregadas**:

Compatibilidad con Always Encrypted para la API de BCP

El nuevo atributo de cadena de conexión UseFMTOnly hace que el controlador use metadatos heredados en casos especiales que requieren tablas temporales.

Compatibilidad con Instancia administrada de Azure SQL (versión preliminar privada ampliada). 
> [!NOTE]
> Hay varias diferencias cuando se usa Instancia administrada:
> -   No se admite FILESTREAM. 
> -   No se admite el acceso al sistema de archivos local, pero es necesario para algunas cosas como los archivos de seguimiento. 
> -   No es posible crear el UDT desde la ruta de acceso local. 
> -   No se admite la Autenticación integrada de Windows. 
> -   DTC no se admite 
> -   La cuenta "sa" no está presente (la cuenta predeterminada se llama "cloudSA").
> -   El ERROR de token TDS (0xAA) devuelve un nombre de servidor incorrecto.
> -   No se admiten caracteres especiales en el nombre de la base de datos. 
> -   No se admite ALTER DATABASE [dbname1] MODIFY NAME = [dbname2].
> -   Los mensajes de error siempre se muestran en inglés, independientemente de la configuración de idioma (igual que Azure). 

## <a name="131-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos-may-2017"></a>13.1, para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS, mayo de 2017

La versión 13.1 del controlador ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agrega compatibilidad con Always Encrypted y Azure Active Directory cuando se usa junto con Microsoft SQL Server 2016.

**Nuevas distribuciones compatibles**: OS X 10.11 y macOS 10.12 se admiten en la primera versión del controlador ODBC en macOS. También ya se admite Ubuntu 16.10, junto con Red Hat 6, 7 y SUSE 12. Cada plataforma tiene un paquete de plataforma correspondiente (RPM o DEB) para facilitar la instalación y configuración.  Vea [Instalación del controlador](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para obtener instrucciones de instalación.

**Cambios de compatibilidad con el Administrador de controladores unixODBC 2.3.1**: el controlador ODBC ya no depende del empaquetado personalizado para el administrador de controladores unixODBC (excepto en RedHat 6) y en su lugar se basa en el administrador de paquetes de distribución para resolver la dependencia de UnixODBC desde los repositorios de distribución.

**Compatibilidad con la API de BCP**: el controlador ODBC de Linux y macOS ahora admite el uso de la [funciones de la API de BCP (**bcp_init**, etc.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="130-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>13.0, para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux

Con Microsoft ODBC Driver 13.0 para SQL Server, ahora también se admiten SQL Server 2014 y SQL Server 2016.  

**Nuevas distribuciones compatibles**:

Junto con Red Hat y SUSE, ahora también se ofrece compatibilidad con Ubuntu. Cada plataforma tiene un paquete de plataforma correspondiente (RPM o DEB) para facilitar la instalación y configuración.  Vea [Instalación del controlador](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para obtener instrucciones de instalación.

**Compatibilidad con el Administrador de controladores unixODBC 2.3.1**: además de un administrador de controladores más reciente, también hay un paquete para la instalación de esta dependencia que facilita la instalación y la configuración.  

**Resolución de IP de red transparente**: la resolución de IP de red transparente es una revisión de la característica existente de conmutación por error de múltiples subredes que afecta a la secuencia de conexión del controlador en el caso donde la primera IP resuelta del nombre de host no responde y hay varias direcciones IP asociadas con el nombre de host.

**Compatibilidad con TLS 1.2**: Microsoft ODBC Driver 13.0 para SQL Server en Linux ahora es compatible con TLS 1.2, cuando se usan comunicaciones seguras con SQL Server.

## <a name="11-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>11, para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux

El controlador ODBC en SUSE Linux (Preview) es compatible con SUSE Linux Enterprise 11 Service Pack 2 de 64 bits. Para obtener más información, consulte [System Requirements](../../../connect/odbc/linux-mac/system-requirements.md).  

El controlador ODBC en Linux es compatible con [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obtener más información, vea [Compatibilidad del controlador ODBC con alta disponibilidad y recuperación ante desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  

El controlador ODBC en Linux es compatible con conexiones a Base de datos SQL de Microsoft Azure. Para obtener más información, consulte [How to: Connect to Windows Azure SQL Database Using ODBC](https://msdn.microsoft.com/library/hh974312.aspx)(Cómo conectarse a Base de datos SQL de Windows Azure con ODBC).  

La opción `-l` (tiempo de expiración del inicio de sesión) se ha agregad para `bcp`. Para obtener más información, vea [Conexión con **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md).
