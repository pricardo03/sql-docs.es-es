---
title: Actualizar credenciales en orígenes de datos de informe desde un sitio de SharePoint | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a9908e340dadeb1108e68ca10f466276c14df23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575434"
---
# <a name="update-credentials-in-report-data-sources-from-a-sharepoint-site"></a>Actualizar credenciales en orígenes de datos de informe desde un sitio de SharePoint
  En este tema se describe cómo actualizar los orígenes de datos incrustados en informes y los orígenes de datos compartidos en una biblioteca de documentos de SharePoint.  
  
 Muchos de sus informes pueden incluir orígenes de datos o utilizar orígenes de datos compartidos configurados para usar la autenticación de Windows. En algunas circunstancias, como cuando crea alertas de datos para informes guardados en una biblioteca de documentos de SharePoint, tendrá que actualizar las credenciales del origen de datos a las credenciales almacenadas o no requerir ninguna credencial.  
  
 Para utilizar credenciales almacenadas en informes, puede decidir crear y usar un nuevo inicio de sesión de SQL Server. Para obtener más información, vea [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md).  
  
### <a name="to-update-an-embedded-data-source-to-use-stored-credentials"></a>Para actualizar un origen de datos incrustado de modo que use credenciales almacenadas  
  
1.  Vaya a la biblioteca de documentos de SharePoint donde guardó el informe.  
  
2.  Haga clic en el icono para expandir el menú desplegable del informe y, después, haga clic en **Administrar orígenes de datos**.  
  
     Se abre la página Administrar orígenes de datos.  
  
3.  En la columna **Nombre** , haga clic en el origen de datos.  
  
4.  Para **Tipo de conexión** , compruebe que la opción **Origen de datos personalizado** esté seleccionada.  
  
     Esta opción indica que el origen de datos está incrustado en el informe.  
  
5.  Deje las opciones **Tipo de origen de datos** y **Cadena de conexión** tal como están, a menos que desee que el informe se conecte a un tipo diferente de origen de datos, a un servidor diferente o a un almacén de datos.  
  
6.  Para **Credenciales**, seleccione **Credenciales almacenadas**. Esta opción solo funciona si el origen de datos no acepta credenciales o si se pasan credenciales de otra manera.  
  
     En algunas circunstancias se puede usar también la opción **No se necesitan credenciales** .  
  
     En algunos tipos de orígenes de datos, se debe configurar una cuenta de ejecución desatendida en el servidor de informes. Para más información, vea el tema del tipo de origen de datos correspondiente en [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) y [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
7.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquelo con este formato: \<dominio>\\<cuenta\> y seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**.  
  
    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de base de datos admite la suplantación o la delegación, puede seleccionar **Establecer contexto de ejecución en esta cuenta**.  
  
8.  Para comprobar que el origen de datos se puede conectar usando las credenciales actualizadas, haga clic en **Probar conexión**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>Para actualizar un origen de datos compartido de modo que use credenciales almacenadas  
  
1.  Vaya a la biblioteca de documentos de SharePoint donde guardó el origen de datos compartido.  
  
2.  Haga clic en el icono para expandir el menú desplegable del origen de datos compartido y, después, haga clic en **Editar definición de origen de datos**.  
  
     Se abre la página Origen de datos.  
  
3.  Deje las opciones **Tipo de origen de datos** y **Cadena de conexión** tal como están, a menos que desee que el origen de datos compartido se conecte a un tipo diferente de origen de datos, a un servidor diferente o a un almacén de datos.  
  
4.  Para **Credenciales**, seleccione **Credenciales almacenadas**.  
  
     En algunas circunstancias se puede usar también la opción **No se necesitan credenciales** . Esta opción solo funciona si el origen de datos no acepta credenciales o si se pasan credenciales de otra manera.  
  
     En algunos tipos de orígenes de datos, se debe configurar una cuenta de ejecución desatendida en el servidor de informes. Para más información, vea el tema del tipo de origen de datos correspondiente en [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) y [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
5.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquelo con este formato: \<dominio>\\<cuenta\> y seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**.  
  
    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de base de datos admite la suplantación o la delegación, puede seleccionar **Establecer contexto de ejecución en esta cuenta**.  
  
6.  Para comprobar que el origen de datos se puede conectar usando las credenciales actualizadas, haga clic en **Probar conexión**.  
  
7.  Compruebe que la opción Habilitar este origen de datos está seleccionada.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Cargar documentos en una biblioteca de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  
