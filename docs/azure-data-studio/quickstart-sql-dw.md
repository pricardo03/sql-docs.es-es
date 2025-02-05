---
title: 'Inicio rápido: conectarse a una instancia de Azure SQL Data Warehouse y realizar consultas'
titleSuffix: Azure Data Studio
description: En este inicio rápido, se muestra cómo usar Azure Data Studio para conectarse a una instancia de Azure SQL Data Warehouse y ejecutar una consulta.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.openlocfilehash: 810d03ab97fd584e1ddaab45e06a21377b81685d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959403"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>Inicio rápido: usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse y consultar datos en Azure SQL Data Warehouse

En este inicio rápido, se muestra cómo usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse a Azure SQL Data Warehouse y, después, usar instrucciones Transact-SQL para crear, insertar y seleccionar datos. 

## <a name="prerequisites"></a>Prerequisites
Para completar este inicio rápido, necesita [!INCLUDE[name-sos](../includes/name-sos-short.md)] y una instancia de Azure SQL Data Warehouse.

- [Instale [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md).

Si aún no tiene una instancia de SQL Data Warehouse, vea [Crear una instancia de SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Recuerde el nombre del servidor y las credenciales de inicio de sesión.


## <a name="connect-to-your-data-warehouse"></a>Conectarse a un almacenamiento de datos

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para establecer una conexión con su instancia del servidor de Azure SQL Data Warehouse.

1. La primera vez que ejecute [!INCLUDE[name-sos](../includes/name-sos-short.md)], se abrirá la página **Conexión**. Si no ve la página **Conexión**, haga clic en **Agregar conexión**, o bien en el icono de **Nueva conexión** en la barra lateral **SERVIDORES**:
   
   ![Icono de Nueva conexión](media/quickstart-sql-dw/new-connection-icon.png)

2. En este artículo, se usa el *inicio de sesión de SQL*, pero se admite la *autenticación de Windows*. Rellene los campos como se indica a continuación con el nombre del servidor, el nombre de usuario y la contraseña de *su instancia* de Azure SQL Server:

   | Configuración       | Valor sugerido | Descripción |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Nombre completo del servidor | El nombre tiene que ser similar a este: **sqldwsample.database.windows.net** |
   | **Autenticación** | Inicio de sesión de SQL| En este tutorial, se usa la autenticación de SQL. |
   | **User name** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña (inicio de sesión de SQL)** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |
   | **¿Desea guardar la contraseña?** | Sí o no | Si no quiere escribir la contraseña cada vez, seleccione Sí. |
   | **Nombre de la base de datos** | *dejar en blanco* | Nombre de la base de datos a la que se va a conectar. |
   | **Grupo de servidores** | Seleccione <Default>. | Si ha creado un grupo de servidores, puede establecerlo en un grupo de servidores específico. | 

   ![Icono de Nueva conexión](media/quickstart-sql-dw/new-connection-screen.png) 

3. Si el servidor no tiene una regla de firewall que permita a Azure Data Studio conectarse, se abrirá el formulario **Crear nueva regla de firewall**. Rellene el formulario para crear una nueva regla de firewall. Para obtener detalles, vea [Reglas de firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nueva regla de firewall](media/quickstart-sql-dw/firewall.png)  

4. Después de conectarse correctamente, el servidor se abre en la barra lateral *SERVIDORES*.

## <a name="create-the-tutorial-data-warehouse"></a>Crear el almacenamiento de datos del tutorial
1. Haga clic con el botón derecho en el servidor (en el Explorador de objetos) y seleccione **Nueva consulta**.

1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **Ejecutar**:

   ```sql
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB] (EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
    GO  
    
    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
   ```


## <a name="create-a-table"></a>Creación de una tabla

El editor de consultas aún está conectado a la base de datos *maestra*, pero lo que queremos es crear una tabla en la base de datos *TutorialDB*. 

1. Cambie el contexto de conexión a **TutorialDB**:

   ![Cambiar el contexto](media/quickstart-sql-database/change-context.png)


1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **Ejecutar**:

   > [!NOTE]
   > Puede anexar esto, o bien puede sobrescribir la consulta anterior en el editor. Al hacer clic en **Ejecutar**, solo se ejecuta la consulta seleccionada. Si hay ninguna opción seleccionada, al hacer clic en **Ejecutar**, se ejecutarán todas las consultas en el editor.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>Insertar filas

1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **Ejecutar**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```


## <a name="view-the-result"></a>Ver el resultado
1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **Ejecutar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Se muestran los resultados de la consulta:

   ![Seleccionar los resultados](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>Limpiar recursos

Otros artículos de esta colección se basan en este inicio rápido. Si tiene previsto continuar trabajando con otras guías de inicio rápido posteriores, no elimine los recursos creados en este inicio rápido. Si no tiene previsto continuar, siga este procedimiento para eliminar los recursos creados por este inicio rápido en Azure Portal.
Para limpiar los recursos, elimine los grupos de recursos que ya no necesite. Para obtener más información, vea [Limpieza de recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Pasos siguientes

Ahora que ya se ha conectado correctamente a una instancia de Azure SQL Data Warehouse y ha ejecutado una consulta, pruebe el [Tutorial del editor de código](tutorial-sql-editor.md).
