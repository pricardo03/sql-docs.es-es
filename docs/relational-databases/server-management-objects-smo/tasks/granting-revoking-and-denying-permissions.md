---
title: Conceder, revocar y denegar permisos | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- granting permissions [SMO]
- denying permissions [SMO]
- permissions [SMO]
- revoking permissions [SMO]
ms.assetid: b0eb0f60-3e56-4880-b645-138832b38a1e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8db1acd2f2ef408f1e9bed70949444bda5a1ef3d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111480"
---
# <a name="granting-revoking-and-denying-permissions"></a>Conceder, revocar y denegar permisos
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  El objeto <xref:Microsoft.SqlServer.Management.Smo.ServerPermission> se utiliza para asignar un conjunto de permisos o un permiso de servidor individual al objeto <xref:Microsoft.SqlServer.Management.Smo.ServerPermissionSet>. Para los permisos en el nivel de servidor, el cesionario hace referencia a un inicio de sesión. Se hace una lista de los inicios de sesión autenticados por Windows como nombres de usuario de Windows. Cuando este ejemplo de código se ejecuta, revoca el permiso del cesionario y comprueba se ha quitado con el método <xref:Microsoft.SqlServer.Management.Smo.Server.EnumServerPermissions%2A>.  
  
 Los permisos de bases de datos y permisos de objetos de bases de datos pueden asignarse de igual forma utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.DatabasePermissionSet> y el objeto <xref:Microsoft.SqlServer.Management.Smo.ObjectPermissionSet>.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="granting-server-permissions-in-visual-basic"></a>Conceder permisos de servidor en Visual Basic  
 En este ejemplo de código se conceden los permisos Crear extremo y Modificar cualquier extremo al inicio de sesión especificado y, a continuación, se enumeran y se muestran los permisos. Se revoca uno de los permisos y se enumeran los permisos de nuevo a continuación. En este ejemplo se supone que el inicio de sesión especificado tiene los permisos especificados para comenzar.  
  
```VBNET  
' compile with: /r:Microsoft.SqlServer.Smo.dll /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll /r:Microsoft.SqlServer.SqlEnum.dll  
Imports Microsoft.SqlServer.Management.Smo  
  
Public Class A  
   Public Shared Sub Main()  
      Dim svr As New Server()  
  
      ' Creating the logins (Grantee)  
      Dim vGrantee As [String] = "Grantee1"  
      Dim login As New Login(svr, vGrantee)  
      login.LoginType = LoginType.SqlLogin  
      login.Create("password@1")  
  
      Dim vGrantee2 As [String] = "Grantee2"  
      Dim login2 As New Login(svr, vGrantee2)  
      login2.LoginType = LoginType.SqlLogin  
      login2.Create("password@2")  
  
      ' Define a ServerPermissionSet that contains permission to Create Endpoint and Alter Any Endpoint.   
      Dim sps As New ServerPermissionSet(ServerPermission.CreateEndpoint)  
      sps.Add(ServerPermission.AlterAnyEndpoint)  
  
      ' Grant Create Endpoint and Alter Any Endpoint permissions to Grantee  
      svr.Grant(sps, vGrantee)  
      svr.Grant(sps, vGrantee2)  
  
      ' Enumerate and display the server permissions in the set for the grantee specified in the vGrantee string variable.   
      Dim spis As ServerPermissionInfo() = svr.EnumServerPermissions(vGrantee, sps)  
      'enumerates all server permissions for the Grantee from the specified permission set  
      Console.WriteLine("====Before revoke===========")  
      For Each spi As ServerPermissionInfo In spis  
         Console.WriteLine(spi.Grantee + " has " & spi.PermissionType.ToString() & " permission.")  
      Next  
      Console.WriteLine(" ")  
  
      ' Revoke the create endpoint permission from the grantee.   
      svr.Revoke(New ServerPermissionSet(ServerPermission.CreateEndpoint), vGrantee)  
  
      ' Enumerate and display the server permissions in the set for the grantee specified in the vGrantee string variable.   
      spis = svr.EnumServerPermissions(vGrantee, sps)  
  
      Console.WriteLine("==After revoke=========")  
      For Each spi As ServerPermissionInfo In spis  
         Console.WriteLine(spi.Grantee + " has " & spi.PermissionType.ToString() & " permission.")  
      Next  
      Console.WriteLine(" ")  
  
      ' Grant the Create Server Role permission to the grantee.   
      svr.Grant(New ServerPermissionSet(ServerPermission.ViewAnyDatabase), vGrantee)  
      ' Enumerate and display the server permissions for the grantee specified in the vGrantee string variable.   
  
      ' enumerates all server permissions for the Grantee  
      spis = svr.EnumServerPermissions(vGrantee)  
  
      Console.WriteLine("==After grant========")  
  
      For Each spi As ServerPermissionInfo In spis  
         Console.WriteLine(spi.Grantee + " has " & spi.PermissionType.ToString() & " permission.")  
      Next  
      Console.WriteLine("")  
  
      ' Enumerate and display the server permissions in the set for all logins.   
      spis = svr.EnumServerPermissions(sps)  
      'enumerates all server permissions in the set for all logins  
      Console.WriteLine("==After grant========")  
  
      For Each spi As ServerPermissionInfo In spis  
         Console.WriteLine(spi.Grantee + " has " & spi.PermissionType.ToString() & " permission.")  
      Next  
      Console.WriteLine("")  
   End Sub  
End Class  
```  
  
## <a name="granting-server-permissions-in-visual-c"></a>Conceder permisos de servidor en Visual C#  
 En este ejemplo de código se conceden los permisos Crear extremo y Modificar cualquier extremo al inicio de sesión especificado y, a continuación, se enumeran y se muestran los permisos. Se revoca uno de los permisos y se enumeran los permisos de nuevo a continuación. En este ejemplo se supone que el inicio de sesión especificado tiene los permisos especificados para comenzar.  
  
```csharp  
// compile with: /r:Microsoft.SqlServer.Smo.dll /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll /r:Microsoft.SqlServer.SqlEnum.dll  
using System;  
using Microsoft.SqlServer.Management.Smo;  
  
public class A {  
   public static void Main() {  
      Server svr = new Server();  
  
      // Creating the logins (Grantee)  
      String vGrantee = "Grantee1";  
      Login login = new Login(svr, vGrantee);  
      login.LoginType = LoginType.SqlLogin;  
      login.Create("password@1");  
  
      String vGrantee2 = "Grantee2";  
      Login login2 = new Login(svr, vGrantee2);  
      login2.LoginType = LoginType.SqlLogin;  
      login2.Create("password@2");  
  
      // Define a ServerPermissionSet that contains permission to Create Endpoint and Alter Any Endpoint.   
      ServerPermissionSet sps = new ServerPermissionSet(ServerPermission.CreateEndpoint);  
      sps.Add(ServerPermission.AlterAnyEndpoint);  
  
      // Grant Create Endpoint and Alter Any Endpoint permissions to Grantee  
      svr.Grant(sps, vGrantee);  
      svr.Grant(sps, vGrantee2);  
  
      // Enumerate and display the server permissions in the set for the grantee specified in the vGrantee string variable.   
      ServerPermissionInfo[] spis = svr.EnumServerPermissions(vGrantee, sps); //enumerates all server permissions for the Grantee from the specified permission set  
  
      Console.WriteLine("====Before revoke===========");  
      foreach (ServerPermissionInfo spi in spis) {  
         Console.WriteLine(spi.Grantee + " has " + spi.PermissionType.ToString() + " permission.");  
      }  
      Console.WriteLine(" ");  
  
      // Revoke the create endpoint permission from the grantee.   
      svr.Revoke(new ServerPermissionSet(ServerPermission.CreateEndpoint), vGrantee);  
  
      // Enumerate and display the server permissions in the set for the grantee specified in the vGrantee string variable.   
      spis = svr.EnumServerPermissions(vGrantee, sps);  
  
      Console.WriteLine("==After revoke=========");  
      foreach (ServerPermissionInfo spi in spis) {  
         Console.WriteLine(spi.Grantee + " has " + spi.PermissionType.ToString() + " permission.");  
      }  
      Console.WriteLine(" ");  
  
      // Grant the Create Server Role permission to the grantee.   
      svr.Grant(new ServerPermissionSet(ServerPermission.ViewAnyDatabase), vGrantee);  
      // Enumerate and display the server permissions for the grantee specified in the vGrantee string variable.   
  
      // enumerates all server permissions for the Grantee  
      spis = svr.EnumServerPermissions(vGrantee);   
  
      Console.WriteLine("==After grant========");  
  
      foreach (ServerPermissionInfo spi in spis) {  
         Console.WriteLine(spi.Grantee + " has " + spi.PermissionType.ToString() + " permission.");  
      }  
      Console.WriteLine("");  
  
      // Enumerate and display the server permissions in the set for all logins.   
      spis = svr.EnumServerPermissions(sps); //enumerates all server permissions in the set for all logins  
  
      Console.WriteLine("==After grant========");  
  
      foreach (ServerPermissionInfo spi in spis) {  
         Console.WriteLine(spi.Grantee + " has " + spi.PermissionType.ToString() + " permission.");  
      }  
      Console.WriteLine("");  
   }  
}  
```  
  
## <a name="granting-server-permissions-in-powershell"></a>Conceder permisos de servidor en PowerShell  
 En este ejemplo de código se conceden los permisos Crear extremo y Modificar cualquier extremo al inicio de sesión especificado y, a continuación, se enumeran y se muestran los permisos. Se revoca uno de los permisos y se enumeran los permisos de nuevo a continuación. En este ejemplo se supone que el inicio de sesión especificado tiene los permisos especificados para comenzar.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#The subject login:  
# "Place Login Name here - has permission to Create Endpoints"  
$vGrantee = "LoginName"  
  
#This sample assumes that the grantee already has permission to Create Endpoints.   
  
$sps  =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.ServerPermissionSet  
  
$sps.CreateEndpoint = $true  
$sps.AlterAnyEndpoint = $true  
  
#This sample assumes that the grantee already has permission to Create Endpoints.   
  
#Enumerate and display the server permissions in the set for the grantee specified  
# in the vGrantee string variable.  
$spis = $srv.EnumServerPermissions($vGrantee)  
  
"===Before revoke============="  
foreach ( $spi in $spis)  
{  
    $spi.Grantee + " has " + $spi.PermissionType + " permission."  
}  
""  
#remove perission to create an endpoint  
$sps.CreateEndpoint = $false  
$srv.Revoke($sps, $vGrantee)  
  
#Enumerate and display the server permissions in the set for the grantee specified  
# in the vGrantee string variable.  
$spis = $srv.EnumServerPermissions($vGrantee)  
  
"===After revoke============="  
foreach ( $spi in $spis)  
{  
    $spi.Grantee + " has " + $spi.PermissionType + " permission."  
}  
""  
#Grant the revoked permissions back  
$sps.CreateEndpoint = $true  
$sps.AlterAnyEndpoint = $true  
$srv.Grant($sps, $vGrantee)  
  
#Enumerate and display the server permissions in the set for the grantee specified  
# in the vGrantee string variable.  
$spis = $srv.EnumServerPermissions($vGrantee)  
  
"===After grant============="  
foreach ( $spi in $spis)  
{  
    $spi.Grantee + " has " + $spi.PermissionType + " permission."  
}  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Jerarquía de permisos &#40;motor de base de datos&#41;](../../../relational-databases/security/permissions-hierarchy-database-engine.md)  
  
  
