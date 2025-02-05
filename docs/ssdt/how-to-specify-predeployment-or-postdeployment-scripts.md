---
title: 'Procedimientos: Especificar scripts anteriores o posteriores a la implementación | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 7f78f517-f13d-4f4b-84b9-e804cb490b2c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a1531bffd50bb14838e74b5315c30a870563f86f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035009"
---
# <a name="how-to-specify-predeployment-or-postdeployment-scripts"></a>Procedimientos: Especificación de scripts anteriores o posteriores a la implementación
Los scripts anteriores y posteriores a la implementación ejecutan instrucciones de Transact\-SQL antes y después del script de implementación principal, que se genera a partir del proyecto de base de datos. Un proyecto solo puede tener un script anterior a la implementación y un script posterior a la implementación. Estos scritps se pueden usar para muchos propósitos. Por ejemplo:  
  
-   Un script anterior a la implementación puede copiar datos de una tabla que se vaya a convertir en una tabla temporal antes de volver a dar formato a los datos y aplicarlos a la tabla modificada en un script posterior a la implementación.  
  
-   Puede insertar datos de referencia que deban figurar en una tabla en un script posterior a la implementación. Antes de insertar los datos, puede probar si la tabla ya contiene datos. Si la tabla no está vacía, debe borrar los datos existentes o especificar que desea volver a crear siempre la base de datos antes de implementarla. Puede agregar una instrucción como la siguiente en el script posterior a la implementación:  
  
```  
IF (EXISTS(SELECT * FROM [dbo].[MyReferenceTable]))  
BEGIN  
    DELETE FROM [dbo].[MyReferenceTable]  
END  
```  
  
## <a name="to-add-and-modify-a-pre--or-post-deployment-script"></a>Para agregar un script anterior o posterior a la implementación  
  
1.  En el **Explorador de soluciones**, expanda el proyecto de base de datos para mostrar la carpeta Scripts.  
  
2.  Haga clic con el botón secundario del mouse en la carpeta Scripts y seleccione Agregar.  
  
3.  Seleccione Scripts en el menú contextual.  
  
4.  Seleccione un script anterior o posterior a la implementación. Si lo desea, especifique un nombre distinto del predeterminado. Haga clic en Agregar para finalizar.  
  
5.  Haga doble clic en el archivo en la carpeta Scripts.  
  
    Se abre el editor de Transact\-SQL en el que se muestra el contenido del archivo.  
  
Puede usar sintaxis SQLCMD y variables en sus scripts y establecer estas variables en las propiedades del proyecto de base de datos. Por ejemplo:  
  
-   Puede utilizar sintaxis SQLCMD para incluir el contenido de un archivo en un script anterior o posterior a la implementación. Los archivos se incluyen y se ejecutan en el orden en que se definen: `:r .\myfile.sql`  
  
-   Puede usar sintaxis SQLCMD para hacer referencia a una variable en el script posterior a la implementación. Puede establecer la variable SQLCMD en las propiedades del proyecto o en un perfil de publicación:  
  
    ```  
    :setvar TableName MyTable  
    SELECT * FROM [$(TableName)]  
    ```  
  
Para obtener más información acerca del uso de SQLCMD en scripts, vea [Configuración del proyecto de base de datos](../ssdt/database-project-settings.md).  
  
## <a name="see-also"></a>Consulte también  
[Desarrollo de bases de datos sin conexión orientado a proyectos](../ssdt/project-oriented-offline-database-development.md)  
  
