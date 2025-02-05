---
title: Secuencias de comandos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- dependencies [SMO]
- scripts [SMO]
ms.assetid: 13a35511-3987-426b-a3b7-3b2e83900dc7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f10289e099a0c3b6400b71d972c6f749ffb76ff8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63158784"
---
# <a name="scripting"></a>Scripting
  El objeto <xref:Microsoft.SqlServer.Management.Smo.Scripter> y sus objetos secundarios o el método `Script` en objetos individuales controlan el scripting en SMO. El <xref:Microsoft.SqlServer.Management.Smo.Scripter> objeto controla la asignación de relaciones de dependencia para objetos en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 La generación avanzada de script utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.Scripter> y sus objetos secundarios es un proceso de tres fases:  
  
1.  Detección  
  
2.  Generación de lista  
  
3.  Generación de script  
  
 La fase de detección utiliza el objeto <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker>. Dada una lista de URN de objetos, el método <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.DiscoverDependencies%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker> devuelve un objeto <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> para los objetos en la lista URN. El valor booleano *fParents* parámetro se utiliza para seleccionar si los elementos primarios o secundarios del objeto especificado son para su detección. El árbol de dependencia se puede modificar en esta fase.  
  
 En la fase de generación de lista, el árbol se pasa y se devuelve la lista resultante. Esta lista de objetos aparece en orden de scripting y se puede manipular.  
  
 La fase de generación de la lista utiliza el método <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.WalkDependencies%2A> para devolver <xref:Microsoft.SqlServer.Management.Smo.DependencyTree>. <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> se puede modificar en esta fase.  
  
 En la tercera y última fase, se genera un script con la lista especificada y las opciones de scripting. El resultado se devuelve como un objeto de sistema <xref:System.Collections.Specialized.StringCollection>. En esta fase los nombres de objeto dependientes se extraen a continuación de la colección Elementos del objeto <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> y de propiedades como <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.NumberOfSiblings%2A> y <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.FirstChild%2A>.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
 Este ejemplo de código requiere una instrucción `Imports` para el espacio de nombres System.Collections.Specialized. Inserte esto con las otras instrucciones Imports, antes de cualquier declaración en la aplicación.  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
Imports System.Collections.Specialized  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-basic"></a>Generar script de las dependencias de una base de datos en Visual Basic  
 En este ejemplo de código se muestra cómo detectar las dependencias y cómo recorrer en iteración la lista para mostrar los resultados.  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
  
Public Class A  
   Public Shared Sub Main()  
      ' database name  
      Dim dbName As [String] = "AdventureWorksLT2012"   ' database name  
  
      ' Connect to the local, default instance of SQL Server.   
      Dim srv As New Server()  
  
      ' Reference the database.    
      Dim db As Database = srv.Databases(dbName)  
  
      ' Define a Scripter object and set the required scripting options.   
      Dim scrp As New Scripter(srv)  
      scrp.Options.ScriptDrops = False  
      scrp.Options.WithDependencies = True  
      scrp.Options.Indexes = True   ' To include indexes  
      scrp.Options.DriAllConstraints = True   ' to include referential constraints in the script  
  
      ' Iterate through the tables in database and script each one. Display the script.  
      For Each tb As Table In db.Tables  
         ' check if the table is not a system table  
         If tb.IsSystemObject = False Then  
            Console.WriteLine("-- Scripting for table " + tb.Name)  
  
            ' Generating script for table tb  
            Dim sc As System.Collections.Specialized.StringCollection = scrp.Script(New Urn() {tb.Urn})  
            For Each st As String In sc  
               Console.WriteLine(st)  
            Next  
            Console.WriteLine("--")  
         End If  
      Next  
   End Sub  
End Class  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-c"></a>Generar script de las dependencias de una base de datos en Visual C#  
 En este ejemplo de código se muestra cómo detectar las dependencias y cómo recorrer en iteración la lista para mostrar los resultados.  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
  
public class A {  
   public static void Main() {   
      String dbName = "AdventureWorksLT2012"; // database name  
  
      // Connect to the local, default instance of SQL Server.   
      Server srv = new Server();  
  
      // Reference the database.    
      Database db = srv.Databases[dbName];  
  
      // Define a Scripter object and set the required scripting options.   
      Scripter scrp = new Scripter(srv);  
      scrp.Options.ScriptDrops = false;  
      scrp.Options.WithDependencies = true;  
      scrp.Options.Indexes = true;   // To include indexes  
      scrp.Options.DriAllConstraints = true;   // to include referential constraints in the script  
  
      // Iterate through the tables in database and script each one. Display the script.     
      foreach (Table tb in db.Tables) {   
         // check if the table is not a system table  
         if (tb.IsSystemObject == false) {  
            Console.WriteLine("-- Scripting for table " + tb.Name);  
  
            // Generating script for table tb  
            System.Collections.Specialized.StringCollection sc = scrp.Script(new Urn[]{tb.Urn});  
            foreach (string st in sc) {  
               Console.WriteLine(st);  
            }  
            Console.WriteLine("--");  
         }  
      }   
   }  
}  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-powershell"></a>Scripting de las dependencias de una base de datos en PowerShell  
 En este ejemplo de código se muestra cómo detectar las dependencias y cómo recorrer en iteración la lista para mostrar los resultados.  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
# Create a Scripter object and set the required scripting options.  
$scrp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Scripter -ArgumentList (Get-Item .)  
$scrp.Options.ScriptDrops = $false  
$scrp.Options.WithDependencies = $true  
$scrp.Options.IncludeIfNotExists = $true  
  
# Set the path context to the tables in AdventureWorks2012.  
  
CD Databases\AdventureWorks2012\Tables  
  
foreach ($Item in Get-ChildItem)  
 {    
 $scrp.Script($Item)  
 }  
```  
  
  
