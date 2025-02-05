---
title: Editar las propiedades de tabla | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- editTabProps
ms.assetid: 95ea72ba-8e40-4177-a963-0fb4d10c56e3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 618a155390d8719e639d0e12d241b2f824e5375d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62835995"
---
# <a name="edit-the-table-properties"></a>Editar las propiedades de tabla
  Use este cuadro de diálogo para editar las columnas específicas de la tabla seleccionada donde se están capturando cambios. También puede editar la información de **Rol de seguridad** y de **Instancia de captura** .  
  
### <a name="to-edit-the-columns-to-include-in-the-cdc-instance"></a>Para editar las columnas que se van a incluir en la instancia CDC  
  
1.  Realice una o ambas de las acciones siguientes:  
  
    -   Active la casilla situada junto a cualquier columna adicional que desee incluir.  
  
    -   Desactive la casilla situada junto a cualquier columna que ya no desee incluir.  
  
### <a name="to-edit-the-security-role"></a>Para editar el rol de seguridad  
  
1.  Escriba un nuevo nombre o edite el nombre del rol de seguridad en el campo **Rol de seguridad** .  
  
### <a name="to-create-a-new-capture-instance"></a>Para crear una instancia de captura nueva  
  
1.  En la sección **Rol de seguridad** , en el campo **Nombre** , escriba un nombre para la instancia de captura. De forma predeterminada, el nombre especificado en el campo es el nombre de la instancia de captura actual al final del cual se ha agregado **_NEW** (por ejemplo, **instancia_anterior_NEW**).  
  
2.  Guarde la instancia de captura de una de las maneras siguientes:  
  
    -   **New Capture Instance** (Nueva instancia de captura): en este caso se guarda una nueva instancia de captura y la antigua no se elimina.  
  
         **Nota**: No puede tener más de dos instancias de captura por tabla. Si ya hay dos instancias de captura, esta opción no estará disponible.  
  
    -   **Replace Existing** (Reemplazar existente): en este caso, la instancia de captura actual se elimina y se reemplaza por la instancia de captura que ha creado. Si hay dos instancias de captura definidas para esta tabla, debe seleccionar una para reemplazar.  
  
 **Nota**: Puede quitar una instancia de captura de la lista de tablas en la pestaña **Tabla**.  
  
 Cuando termine de especificar la información en este cuadro de diálogo, haga clic en **Aceptar** para aceptar los cambios.  
  
## <a name="see-also"></a>Vea también  
 [Cómo editar las propiedades de la instancia CDC](how-to-edit-the-cdc-instance-properties.md)   
 [Realizar cambios en las tablas seleccionadas para capturar cambios](make-changes-to-the-tables-selected-for-capturing-changes.md)  
  
  
