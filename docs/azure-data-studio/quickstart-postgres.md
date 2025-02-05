---
title: 'Inicio rápido: Conexión a PostgreSQL y consulta'
titleSuffix: Azure Data Studio
description: En este inicio rápido se muestra cómo usar Azure Data Studio para conectarse a PostgreSQL y ejecutar una consulta
ms.custom: seodec18
ms.date: 03/19/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
ms.openlocfilehash: 9dcbbe621ab237eeceff55cd5f931d7d650dd3b4
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959468"
---
# <a name="quickstart-connect-and-query-postgresql-using-includename-sosincludesname-sos-shortmd"></a>Inicio rápido: Conexión a PostgreSQL y consulta con [!INCLUDE[name-sos](../includes/name-sos-short.md)]
En este inicio rápido se muestra cómo usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse a Postgres y luego usar instrucciones SQL para crear la base de datos *tutorialdb* y consultarla.

## <a name="prerequisites"></a>Prerequisites

Para completar este inicio rápido, necesitará [!INCLUDE[name-sos](../includes/name-sos-short.md)], la extensión PostgreSQL para [!INCLUDE[name-sos](../includes/name-sos-short.md) y acceder a un servidor PostgreSQL.

- [Instale [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md).
- [Instale la extensión PostgreSQL para Azure Data Studio](postgres-extension.md).
- [Instale PostgreSQL](https://www.postgresql.org/download/). (También puede crear una base de datos de Postgres en la nube mediante [az postgres up](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli)). 

## <a name="connect-to-postgresql"></a>Conexión con PostgreSQL

1. Inicie **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** .

2. La primera vez que se inicia [!INCLUDE[name-sos](../includes/name-sos-short.md)], se abre el cuadro de diálogo **Conexión**. Si el cuadro de diálogo **Conexión** no se abre, haga clic en el icono **Nueva conexión** en la página **SERVIDORES**:

   ![Icono Nueva conexión](media/quickstart-postgresql/new-connection-icon.png)

3. En el formulario que aparece, vaya a **Tipo de conexión** y seleccione **PostgreSQL** en el menú desplegable.


4. Rellene los campos restantes con el nombre del servidor, el nombre del usuario y la contraseña del servidor PostgreSQL. 

   ![Pantalla Nueva conexión](media/quickstart-postgresql/new-connection-screen.png)  

   | Configuración       | Valor de ejemplo | Descripción |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | localhost | Nombre completo del servidor |
   | **User name** | postgres | Nombre de usuario con el que quiere iniciar sesión. |
   | **Contraseña (inicio de sesión de SQL)** | *password* | Contraseña de la cuenta con la que inicia sesión. |
   | **Contraseña** | *Comprobación* | Active esta casilla si no quiere escribir la contraseña cada vez que se conecte. |
   | **Nombre de la base de datos** | \<Default\> | Rellene esta opción si quiere que la conexión especifique una base de datos. |
   | **Grupo del servidor** | \<Default\> | Esta opción le permite asignar esta conexión a un grupo de servidores específico que cree. | 
   | **Nombre (opcional)** | *dejar en blanco* | Esta opción permite especificar un nombre descriptivo para el servidor. | 

5. Seleccione **Conectar**. 

Después de conectarse correctamente, el servidor se abre en la barra lateral **SERVIDORES**.


## <a name="create-a-database"></a>Crear una base de datos

En los pasos siguientes se crea una base de datos denominada **tutorialdb**:

1. Haga clic con el botón derecho en el servidor PostgreSQL en la barra lateral **SERVIDORES** y seleccione **Nueva consulta**.

2. Pegue esta instrucción SQL en el editor de consultas que se abre.

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. En la barra de herramientas, seleccione **Ejecutar** para ejecutar la consulta. Aparecen notificaciones en el panel **MENSAJES** que muestran el progreso de la consulta.

>[!TIP]
> Puede usar **F5** en el teclado para ejecutar la instrucción en lugar de utilizar **Ejecutar**.

Una vez finalizada la consulta, haga clic con el botón derecho en **Bases de datos** y seleccione **Actualizar** para ver **tutorialdb** en la lista del nodo **Bases de datos**.


## <a name="create-a-table"></a>Creación de una tabla

 En los pasos siguientes se crea una tabla en la **tutorialdb**:

1. Cambie el contexto de la conexión a **tutorialdb** con la lista desplegable del editor de consultas. 

   ![Cambio de contexto](media/quickstart-postgresql/change-context.png)

2. Pegue la siguiente instrucción SQL en el editor de consultas y haga clic en **Ejecutar**. 

   > [!NOTE]
   > Puede anexarla o sobrescribir la consulta existente en el editor. Tenga en cuenta que al hacer clic en **Ejecutar** solo se ejecuta la consulta resaltada. Si no hay nada resaltado, al hacer clic en **Ejecutar** se ejecutan todas las consultas en el editor.

   ```sql
   -- Drop the table if it already exists
   DROP TABLE IF EXISTS customers;
   -- Create a new table called 'customers'
   CREATE TABLE customers(
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR (50) NOT NULL,
       location VARCHAR (50) NOT NULL,
       email VARCHAR (50) NOT NULL
   );
   ```

## <a name="insert-rows"></a>Insertar filas

Pegue el siguiente fragmento de código en la ventana de consulta y haga clic en **Ejecutar**:

   ```sql
   -- Insert rows into table 'customers'
   INSERT INTO customers
       (customer_id, name, location, email)
    VALUES
      ( 1, 'Orlando', 'Australia', ''),
      ( 2, 'Keith', 'India', 'keith0@adventure-works.com'),
      ( 3, 'Donna', 'Germany', 'donna0@adventure-works.com'),
      ( 4, 'Janet', 'United States','janet1@adventure-works.com');
   ```

## <a name="query-the-data"></a>Consulta de los datos

1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **Ejecutar**:
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. Se muestran los resultados de la consulta:

   ![Vista de resultados](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>Next Steps

Obtenga información sobre los [escenarios disponibles para Postgres en Azure Data Studio](postgres-extension.md). 