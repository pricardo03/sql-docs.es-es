---
title: Usar diagramas de actualización para modificar datos en SQLXML 4.0 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- data insertions [SQLXML]
- data deletions [SQLXML]
- updating data [SQLXML]
- modifying data [SQLXML]
- OPENXML function
- updategrams [SQLXML]
- database modifications [SQLXML]
- data updates [SQLXML]
- modifying databases
- data modifications [SQLXML]
- deleting data
- inserting data
ms.assetid: b8b3b892-cb73-41d0-b945-bce148d81d9b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 97baf1266240ad26255df50096b859ae581953cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085830"
---
# <a name="using-updategrams-to-modify-data-in-sqlxml-40"></a>Utilizar los diagramas de actualización para modificar datos en SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Puede modificar (Insertar, actualizar o eliminar) una base de datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde un documento XML de documentos mediante el uso de un diagrama de actualización o la OPENXML [!INCLUDE[tsql](../../../includes/tsql-md.md)] función.  
  
 En esta sección se proporciona información sobre los diagramas de actualización y ejemplos de uso.  
  
## <a name="in-this-section"></a>En esta sección  
 [Introducción a los diagramas de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/introduction-to-updategrams-sqlxml-4-0.md)  
 Proporciona información básica y ejemplos de diagramas de actualización.  
  
 [Especificar un esquema de asignación anotados en un diagrama de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)  
 Explica y proporciona ejemplos de esquemas de asignación anotados en los diagramas de actualización.  
  
 [Control de valores NULL &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/null-handling-sqlxml-4-0.md)  
 Describe cómo especificar NULL para los valores de elemento y atributo.  
  
 [Insertar datos con diagramas de actualización XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
 Describe y proporciona ejemplos de uso de los diagramas de actualización para insertar los datos.  
  
 [Eliminar datos con diagramas de actualización XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/deleting-data-using-xml-updategrams-sqlxml-4-0.md)  
 Describe y proporciona ejemplos de uso de los diagramas de actualización para eliminar los datos.  
  
 [Actualizar datos con diagramas de actualización XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md)  
 Describe y proporciona ejemplos de uso de los diagramas de actualización para modificar los datos existentes.  
  
 [Pasar parámetros a diagramas de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)  
 Describe y proporciona ejemplos de paso de parámetros a los diagramas de actualización.  
  
 [Controlar problemas de simultaneidad de base de datos en los diagramas de actualización &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/handling-database-concurrency-issues-in-updategrams-sqlxml-4-0.md)  
 Describe los distintos niveles de protección posibles para administrar los problemas de simultaneidad en los diagramas de actualización y proporciona los ejemplos.  
  
 [Aplicaciones de ejemplo de updategram &#40;SQLXML 4.0&#41;](https://msdn.microsoft.com/library/d2287e10-4007-4ba4-ad84-4e2b6adfede5)  
 Proporciona aplicaciones de ejemplo que usan los diagramas de actualización.  
  
 [Instrucciones y limitaciones de los diagramas de actualización XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/guidelines-and-limitations-of-xml-updategrams-sqlxml-4-0.md)  
 Enumera algunas cosas que hay que recordar a la hora de trabajar con los diagramas de actualización.  
  
  
