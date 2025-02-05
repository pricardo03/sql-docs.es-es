---
title: Dependencias de características de Microsoft JDBC Driver para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26395c7a925906e7b27d4e47098164019e56f31d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893950"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Dependencias de características de Microsoft JDBC Driver para SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se enumeran las bibliotecas en las que se basa el controlador JDBC Driver de Microsoft para SQL Server. El proyecto presenta las siguientes dependencias.

## <a name="compile-time"></a>Tiempo de compilación

 - `com.microsoft.azure:azure-keyvault`: proveedor de Azure Key Vault para la característica Always Encrypted Azure Key Vault (opcional)
 - `com.microsoft.azure:adal4j`: biblioteca Azure Active Directory para Java para la característica de autenticación de Azure Active Directory y la característica Azure Key Vault (opcional)
 - `com.microsoft.rest:client-runtime`: biblioteca Azure Active Directory para Java para la característica de autenticación de Azure Active Directory y la característica Azure Key Vault (opcional)
 - `org.antlr:antlr4-runtime`: ANTLR 4 Runtime para la característica useFmtOnly (opcional)
 - `org.osgi:org.osgi.core`: biblioteca OSGi Core para la compatibilidad de OSGi Framework.
 - `org.osgi:org.osgi.compendium`: biblioteca OSGi Compendium para la compatibilidad de OSGi Framework.

## <a name="test-time"></a>Tiempo de prueba

Los proyectos específicos que requieren cualquiera de las características anteriores deben declarar explícitamente las dependencias respectivas en su archivo POM.

**Por ejemplo:** cuando usa la característica de autenticación de Azure Active Directory, deberá volver a declarar la dependencia `adal4j` en el archivo POM del proyecto. Vea el siguiente fragmento:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>
```

**Por ejemplo:** cuando esté utilizando la característica Azure Key Vault, debe volver a declarar la dependencia `azure-keyvault` y la dependencia `adal4j` en el archivo POM del proyecto. Vea el siguiente fragmento:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.1</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>Requisitos de dependencias para JDBC Driver

### <a name="working-with-the-azure-key-vault-provider"></a>Uso del proveedor de Azure Key Vault:

- Versión del controlador JDBC Driver 7.4.1 - versiones de dependencia: Azure-Keyvault (versión 1.2.1), Adal4j (versión 1.6.4), Client-Runtime-for-AutoRest (1.6.10) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- Versión del controlador JDBC Driver 7.2.2 - versiones de dependencia: Azure-Keyvault (versión 1.2.0), Azure-Keyvault-Webkey (versión 1.2.0), Adal4j (versión 1.6.3), Client-Runtime-for-AutoRest (1.6.5) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- Versión del controlador JDBC Driver 7.0.0 - versiones de dependencia: Azure-Keyvault (versión 1.0.0), Adal4j (versión 1.6.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- Versión del controlador JDBC Driver 6.4.0 - versiones de dependencia: Azure-Keyvault (versión 1.0.0), Adal4j (versión 1.4.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Versión del controlador JDBC Driver 6.2.2 - versiones de dependencia: Azure-Keyvault (versión 1.0.0), Adal4j (versión 1.4.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Versión del controlador JDBC Driver 6.0.0 - versiones de dependencia: Azure-Keyvault (version 0.9.7), Adal4j (version 1.3.0) y sus dependencias ([aplicación de ejemplo](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> Con las versiones de controlador 6.2.2 y 6.4.0, la dependencia azure-keyvault-java se ha actualizado a la versión 1.0.0. Sin embargo, la nueva versión no era compatible con la versión anterior (0.9.7) e interrumpe la implementación existente en el controlador. La nueva implementación en el controlador requirió cambios en la API, lo cual a su vez interrumpe los programas cliente que usan el proveedor de Azure Key Vault.
>
> Este problema se resuelve con las versiones más recientes del controlador (de la 7.0.0 en adelante). El constructor quitado que utilizaba el mecanismo de devolución de llamada de autenticación se agrega de nuevo al proveedor de Azure Key Vault para permitir la compatibilidad con versiones anteriores.

### <a name="working-with-azure-active-directory-authentication"></a>Uso de la autenticación de Azure Active Directory:

- Versión del controlador JDBC Driver 7.4.1 - versiones de dependencia: Adal4j (version 1.6.4), Client-Runtime-for-AutoRest (1.6.10) y sus dependencias
- Versión del controlador JDBC Driver 7.2.2 - versiones de dependencia: Adal4j (version 1.6.3), Client-Runtime-for-AutoRest (1.6.5) y sus dependencias
- Versión del controlador JDBC Driver 7.0.0 - versiones de dependencia: Adal4j (versión 1.6.0) y sus dependencias
- Versión del controlador JDBC Driver 6.4.0 - versiones de dependencia: Adal4j (versión 1.4.0) y sus dependencias
- Versión del controlador JDBC Driver 6.2.2 - versiones de dependencia: Adal4j (versión 1.4.0) y sus dependencias
- Versión del controlador JDBC Driver 6.0.0 - versiones de dependencia: Adal4j (versión 1.3.0) y sus dependencias En esta versión del controlador, puede conectarse mediante el modo de autenticación de _ActiveDirectoryIntegrated_ solo en un sistema operativo de Windows y mediante sqljdbc_auth.dll y la Biblioteca de autenticación de Active Directory para SQL Server (ADALSQL.DLL).

Desde la versión del controlador 6.4.0, las aplicaciones no necesariamente requieren el uso de ADALSQL.DLL en sistemas operativos Windows. En el caso de *sistemas operativos que no sean Windows*, el controlador requiere un vale de Kerberos para funcionar con la autenticación de ActiveDirectoryIntegrated. Para obtener más información sobre cómo conectarse a Active Directory mediante el uso de Kerberos, vea [Establecer el vale de Kerberos en Windows, Linux y Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac).

En el caso de *sistemas operativos Windows*, el controlador busca sqljdbc_auth.dll de forma predeterminada y no requiere la instalación de un vale de Kerberos ni dependencias de la biblioteca de Azure. Si sqljdbc_auth.dll no está disponible, el controlador busca el vale de Kerberos para autenticarse en Active Directory como en otros sistemas operativos.

Puede obtener una [aplicación de ejemplo](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) que usa esta característica.

## <a name="see-also"></a>Vea también

[JDBC Driver GitHub repository](https://github.com/microsoft/mssql-jdbc) (Repositorio de GitHub del controlador JDBC Driver)  
[Referencia de API de JDBC Driver](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
