---
title: Editar tablas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1bdff1386edf4563eadfb04694cbe573f6b1d5c4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060756"
---
# <a name="edit-tables"></a>Editar tablas

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use la pestaña **Tablas** para realizar cambios en las tablas y columnas que seleccionó en la base de datos de origen de Oracle. Esta pestaña contiene los elementos siguientes:  
  
 **Lista de la tabla**  
 La lista de tablas tiene tres columnas:  
  
-   **Nombre de la tabla de Oracle**: nombre de la tabla, incluido el esquema de tabla.  
  
-   **Instancia de captura**: el nombre de la instancia de captura que se usa para denominar los objetos de captura de datos modificados específicos de una instancia. La instancia de captura no puede ser NULL. Si no se especifica, el nombre deriva del nombre del esquema de origen más el nombre de la tabla de origen, con el formato `<schema-name>_<table-name>.` . El nombre de la instancia de captura no puede tener más de 100 caracteres y debe ser único dentro de la base de datos. Puede hacer clic en cualquier celda de esta columna para editar manualmente **capture_instance**.  
  
-   **Rol de seguridad**: nombre del rol de base de datos usado para obtener acceso a los datos modificados. Puede hacer clic en cualquier celda de esta columna para editar manualmente **security_role**.  
  
 **Agregar tablas**  
 Haga clic en **Agregar tablas** para abrir el cuadro de diálogo Selección de tabla, donde puede [Agregar tablas a una instancia CDC](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md). La primera vez que tenga acceso a la base de datos de Oracle en esta sesión, debe [Connect to Oracle](../../integration-services/change-data-capture/connect-to-oracle.md).  
  
 **Editar**  
 Seleccione una tabla de la lista y haga clic en **Editar** para abrir el cuadro de diálogo **Propiedades** de la tabla, donde puede [Editar las propiedades de tabla](../../integration-services/change-data-capture/edit-the-table-properties.md).  
  
> [!NOTE]  
>  No puede editar la asignación de tipos para las tablas que ya tienen tablas reflejadas. Solo puede hacerlo para las tablas nuevas.  
  
 **Quitar**  
 Seleccione una tabla de la lista y haga clic en **Quitar** para quitar la tabla de la instancia CDC.  
  
## <a name="see-also"></a>Consulte también  
 [Cómo editar las propiedades de la instancia CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Seleccione las columnas y tablas de Oracle ](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
