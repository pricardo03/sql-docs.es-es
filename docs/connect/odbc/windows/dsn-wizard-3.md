---
title: Pantalla del Asistente para orígenes de datos (controlador ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 63391969f378fdefbfa9547c079dcce4ff259e22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936547"
---
# <a name="data-source-wizard-screen-3"></a>Pantalla del Asistente para orígenes de datos 3

Especifique la base de datos predeterminada, diversas opciones de ANSI que va a usar el controlador y el nombre de un servidor reflejado.

## <a name="options"></a>Opciones

### <a name="change-the-default-database-to"></a>Establecer la siguiente base de datos como predeterminada

Especifica el nombre de la base de datos predeterminada para cualquier conexión establecida utilizando este origen de datos. Cuando este cuadro está desactivado, las conexiones utilizan la base de datos predeterminada definida para el identificador de inicio de sesión en el servidor. Cuando este cuadro está activado, la base de datos denominada en el cuadro invalida la base de datos predeterminada definida para el identificador de inicio de sesión. Si el cuadro **Adjuntar nombre del archivo de la base de datos** tiene el nombre de un archivo principal, la base de datos descrita por el archivo principal se asocia como una base de datos utilizando el nombre especificado en el cuadro **Establecer la siguiente base de datos como predeterminada**.

Utilizar la base de datos predeterminada para el identificador de inicio de sesión es más eficaz que especificar una base de datos predeterminada en el origen de datos ODBC.

### <a name="mirror-server"></a>Servidor reflejado

Especifica el nombre del asociado de conmutación por error de la base de datos que se va a reflejar. Si no aparece un nombre de base de datos en el cuadro **Establecer la siguiente base de datos como predeterminada** o el nombre mostrado es la base de datos predeterminada, la opción **Servidor reflejado** está deshabilitada.

Si lo desea, puede especificar un nombre principal de servicio (SPN) para el servidor reflejado. El SPN para el servidor reflejado se utiliza para la autenticación mutua entre cliente y servidor.

### <a name="attach-database-filename"></a>Adjuntar nombre del archivo de la base de datos

Especifica el nombre del archivo principal de una base de datos que se puede adjuntar. Esta base de datos se adjunta y se utiliza como predeterminada para el origen de datos. Especifique la ruta de acceso completa y el nombre del archivo principal. El nombre de la base de datos especificado en el cuadro **Establecer la siguiente base de datos como predeterminada** se utiliza como nombre para la base de datos adjuntada.

### <a name="use-ansi-quoted-identifiers"></a>Usar identificadores entrecomillados ANSI

Especifica que QUOTED_IDENTIFIERS se active cuando el controlador ODBC de SQL Server se conecte. Cuando esta casilla está activada, SQL Server exige las reglas ANSI con respecto a las comillas. Las comillas dobles solo se pueden utilizar para los identificadores, por ejemplo en los nombres de columna y de tabla. Las cadenas de caracteres se deben incluir entre comillas simples:

```
SELECT "LastName"
FROM "Person.Contact"
WHERE "LastName" = 'O''Brien'
```

Cuando esta casilla está desactivada, las aplicaciones que utilizan identificadores entrecomillados, como la utilidad Microsoft Query que se incluye con Microsoft Excel, encuentran errores al generar instrucciones SQL con identificadores entrecomillados.

### <a name="use-ansi-nulls-paddings-and-warnings"></a>Usar nulos, rellenos y advertencias ANSI

Especifica que se activen las opciones ANSI_NULLS, ANSI_WARNINGS y ANSI_PADDINGS cuando el controlador ODBC de SQL Server se conecte.

Si la opción ANSI_NULLS está activada, el servidor exige las reglas ANSI relativas a la comparación de las columnas para NULL. La sintaxis de ANSI "IS NULL" o "IS NOT NULL" se debe utilizar para todas las comparaciones de NULL. La sintaxis de Transact-SQL "=NULL" no se admite.

Si la opción ANSI_WARNINGS está activada, SQL Server emite mensajes de advertencia para las condiciones que infringen las reglas ANSI pero que no infringen las reglas de Transact-SQL. Algunos ejemplos de tales errores son el truncamiento de datos en la ejecución de una instrucción UPDATE o INSERT, o encontrar un valor NULL durante una función de agregado. 

Si la opción ANSI_PADDING está activada, los espacios en blanco situados al final de los valores **varchar** y los ceros situados al final de los valores **varbinary** no se recortan automáticamente.

### <a name="application-intent"></a>Application Intent

Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.

### <a name="multi-subnet-failover"></a>Conmutación por error de múltiples subredes.

Si la aplicación se está conectando a un grupo de disponibilidad (AG) de recuperación ante desastres (Grupos de disponibilidad AlwaysOn) de alta disponibilidad en distintas subredes, lo que permite **la conmutación por error de múltiples** subredes. configura el controlador ODBC para SQL Server para proporcionar una detección del servidor activo y una conexión con él más rápidas.

### <a name="transparent-network-ip-resolution"></a>Resolución de IP de red transparente.

Modifica el comportamiento de la **conmutación por error de varias subredes** para permitir una reconexión más rápida durante la conmutación por error. Para obtener más información, vea [Uso de resolución de IP de red transparente](../../../connect/odbc/using-transparent-network-ip-resolution.md).

### <a name="column-encryption"></a>Cifrado de columnas.

Habilita el descifrado y el cifrado automáticos de las transferencias de datos a y desde columnas cifradas con la característica [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) disponible en SQL Server 2016 y versiones posteriores.

### <a name="use-fmtonly-metadata-discovery"></a>Usar la detección de metadatos de FMTONLY:

Use el método de detección de metadatos SET FMTONLY heredado al conectarse a SQL Server 2012 o una versión más reciente. Habilítelo solo cuando se usan consultas no admitidas por [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md), como las que contienen tablas temporales. 

### <a name="next"></a>Siguiente

Avanza a la siguiente pantalla del asistente.

### <a name="back"></a>Atrás

Vuelve a la pantalla anterior del asistente.

## <a name="next-steps"></a>Pasos siguientes

[Pantalla del Asistente para orígenes de datos 2](../../../connect/odbc/windows/dsn-wizard-2.md)

[Pantalla del Asistente para orígenes de datos 4](../../../connect/odbc/windows/dsn-wizard-4.md)
