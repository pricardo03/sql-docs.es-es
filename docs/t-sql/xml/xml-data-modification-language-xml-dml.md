---
title: Lenguaje de manipulación de datos XML (XML DML) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modifying data [SQL Server], XML DML
- XML [SQL Server], DML
- XML DML [SQL Server]
- data modification language [XML DML]
- data modifications [XML DML]
- DML [XML in SQL Server]
- XQuery, XML DML
- xml data type [SQL Server], XML DML
ms.assetid: 20ce50d2-c07b-4e41-93a7-1380d2cd49cb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 28de1be430d02a9288b0a1fe27567965fb0a32e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140890"
---
# <a name="xml-data-modification-language-xml-dml"></a>Lenguaje de manipulación de datos XML (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El Lenguaje de manipulación de datos XML (XML DML) es una extensión del lenguaje XQuery. Según W3C, el lenguaje XQuery carece de la parte de manipulación de datos (DML). El lenguaje XML DML que se presenta en este tema, así como el lenguaje XQuery, proporciona un lenguaje de consultas y modificación de datos completamente funcional que se puede usar con el tipo de datos **xml**.  
  
 XML DML agrega a XQuery las siguientes palabras clave, donde se distingue entre mayúsculas y minúsculas:  
  
-   **insert**  
  
-   **delete**  
  
-   **replace value of**  
  
 Como se describe en [Tipo de datos XML y columnas &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md), se pueden crear variables y columnas de tipo **xml** y asignarles documentos o fragmentos XML. Para modificar o actualizar estas instancias XML, realice el siguiente procedimiento:  
  
-   Use [Modify() (método del tipo de datos xml)](../../t-sql/xml/modify-method-xml-data-type.md) del tipo de datos **xml**.  
  
-   Especifique las instrucciones XML DML correspondientes en el método **modify()** .  
  
 Tenga en cuenta que no se pueden insertar ni eliminar algunos atributos, y a veces tampoco es posible modificar sus valores. Por ejemplo:  
  
-   En **xml** con o sin tipo, los atributos son **xmlns**, **xmlns:\*** y **xml:base**.  
  
-   En **xml** solo con tipo, los atributos son **xsi:nil** y **xsi:type**.  
  
 Entre otras restricciones se pueden citar las siguientes:  
  
-   En **xml** con o sin tipo, se producirá un error al insertar el atributo **xml:base**.  
  
-   En **xml** con tipo, se producirá un error al eliminar y modificar el atributo **xsi:nil**. En **xml** sin tipo, se puede eliminar el atributo o modificar su valor.  
  
-   En **xml** con tipo, se producirá un error si se modifica el valor del atributo **xs:type**. En **xml** sin tipo, se puede modificar el valor del atributo.  
  
 Cuando se modifica una instancia XML con tipo, el formato final debe ser una instancia válida de ese tipo. En caso contrario, se devuelve un error de validación.  
  
## <a name="see-also"></a>Consulte también  
 [insert &#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md)   
 [delete &#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md)   
 [replace value of &#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)  
  
  
