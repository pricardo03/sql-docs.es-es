---
title: Compatibilidad con elementos de espacio de nombres en el modo PATH | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, namespace support
- namespaces [XML in SQL Server]
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72449f54a5256987b7336c82fb5119235ab302b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137465"
---
# <a name="namespace-support-in-path-mode"></a>Compatibilidad con elementos de espacio de nombres en el modo PATH
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Se incluye la compatibilidad con elementos de espacio de nombres en el modo PATH mediante WITH NAMESPACES. Por ejemplo, la consulta siguiente muestra la sintaxis WITH NAMESPACES para declarar un espacio de nombres ("a:") que se puede usar a continuación en la instrucción SELECT posterior:  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## <a name="examples"></a>Ejemplos  
 Estas muestras ilustran la utilización del modo PATH en la creación de XML a partir de una consulta SELECT. Muchas de estas consultas se especifican usando los documentos XML de instrucciones de fabricación de bicicletas almacenados en la columna Instructions de la tabla ProductModel.  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
