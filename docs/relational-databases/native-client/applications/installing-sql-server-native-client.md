---
title: Instalar SQL Server Native Client | Documentos de Microsoft
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
author: MightyPen
ms.author: genemi
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, uninstalling
- SQLNCLI, installing
- SQLNCLI, uninstalling
- Setup [SQL Server Native Client]
- uninstalling SQL Server Native Client
- data access [SQL Server Native Client], uninstalling SQL Server Native Client
- installing SQL Server Native Client
- SQL Server Native Client, installing
- data access [SQL Server Native Client], installing SQL Server Native Client
- removing SQL Server Native Client
ms.assetid: c6abeab2-0052-49c9-be79-cfbc50bff5c1
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dee5cebb97ff491595ca5e875c3adfc08c82bf2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987585"
---
# <a name="installing-sql-server-native-client"></a>Instalar SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 se instala a la vez que [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]. 
 
 No hay ningún cliente nativo de SQL Server 2016. Para obtener más información, consulte [SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client.md). 
 
También puede obtener sqlncli.msi de la página web de SQL Server 2012 Feature Pack. Para descargar la versión más reciente de SQL Server Native Client, vaya a [Microsoft® SQL Server® 2012 Feature Pack](https://www.microsoft.com/download/confirmation.aspx?id=29065). Si una versión anterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client anterior a SQL Server 2012 también está instalado en el equipo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 estarán instalados en paralelo con la versión anterior.  
  
 Los archivos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli11.dll, sqlnclir11.rll y s11ch_sqlncli.chm) se instalan en la siguiente ubicación:  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  Todos los valores del Registro adecuados para el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se crean como parte del proceso de instalación.  
  
 Los archivos de encabezado y biblioteca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h y sqlncli11.lib) se instalan en la siguiente ubicación:  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 Además de instalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como parte de la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], hay también un programa de instalación redistribuible denominado sqlncli.msi, que se puede encontrar en el disco de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la ubicación siguiente: `%CD%\Setup\`.  
  
 Puede distribuir [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a través de sqlncli.msi. Es posible que tenga que instalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client al implementar una aplicación. Una manera de instalar varios paquetes en lo que al usuario le parece ser una instalación única es usar tecnología de encadenador y arranque. Para obtener más información, vea [Authoring a Custom Bootstrapper Package for Visual Studio 2005](https://go.microsoft.com/fwlink/?LinkId=115667) (Crear un paquete de arranque personalizado para Visual Studio 2005) y [Adding Custom Prerequisites](https://go.microsoft.com/fwlink/?LinkId=115668) (Agregar requisitos previos personalizados).  
  
 Las versiones x64 e Itanium de sqlncli.msi también instalan las versiones de 32 bits de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Si su aplicación está diseñada para una plataforma distinta de aquella en la que se desarrolló, puede descargar versiones de sqlncli.msi para x64, Itanium y x86 en el Centro de descarga de Microsoft.  
  
 Cuando se llama a sqlncli.msi, solo se instalan los componentes de cliente de forma predeterminada. Los componentes de cliente son archivos que admiten la ejecución de una aplicación que se desarrolló con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Para instalar también los componentes SDK, especifique `ADDLOCAL=All` en la línea de comandos. Por ejemplo:  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>Instalación silenciosa  
 Si usa la opción /passive, /qn, /qb o /qr con msiexec, también debe especificar IACCEPTSQLNCLILICENSETERMS=YES, para indicar explícitamente que acepta los términos de la licencia de usuario final. Esta opción se debe especificar con todas las letras mayúsculas.  
  
## <a name="uninstalling-sql-server-native-client"></a>Desinstalar SQL Server Native Client  
 Dado que aplicaciones como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server y el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dependen de las herramientas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, es importante no desinstalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client hasta que se desinstalen todas las aplicaciones dependientes. Para usuarios con una advertencia de que la aplicación depende del proveedor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, utilice la opción de instalación APPGUID en su MSI, como se indica a continuación:  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 El valor pasado a APPGUID es su código de producto específico. Se debe crear un código de producto al usar Microsoft Installer para empaquetar su programa de instalación de la aplicación.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)   
 [Temas de procedimientos de instalación](https://msdn.microsoft.com/library/59de41e7-557f-462a-8914-53ec35496baa)  
  
  
