---
title: Buscar en un documento activo de forma incremental | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ac382ee5c57cbecdcbc183e2c246fd8ac5ed28b5
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264220"
---
# <a name="search-an-active-document-incrementally"></a>Buscar en un documento activo de forma incremental
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Es posible buscar en un único documento o ventana de forma incremental mediante la especificación de texto. La operación de búsqueda destaca el primer juego de caracteres que coincide con los especificados durante la búsqueda incremental en el documento o ventana. La búsqueda incremental busca automáticamente en todo el texto de un documento o ventana, excepto el texto oculto.  
  
 Con la opción **Coincidir mayúsculas y minúsculas** , la búsqueda incremental utiliza los criterios de la búsqueda anterior. Por ejemplo, si se ha buscado en varios archivos mediante el cuadro de diálogo **Buscar en archivos** y se ha activado **Coincidir mayúsculas y minúsculas**, si la siguiente vez se busca de forma incremental, la búsqueda distinguirá entre mayúsculas y minúsculas.  
  
### <a name="to-search-incrementally"></a>Para buscar de forma incremental  
  
1.  Abra el archivo o ventana en que desea realizar la búsqueda.  
  
2.  En el menú **Editar** , elija **Avanzado**y, a continuación, haga clic en **Búsqueda incremental**.  
  
     El cursor cambia a unos prismáticos con una flecha, que indica la dirección de la búsqueda, y la barra de estado muestra "Búsqueda incremental".  
  
3.  Comience a escribir la cadena de texto.  
  
     La barra de estado muestra el texto que se está escribiendo, mientras el editor resalta la primera repetición del texto. A medida que se continúa escribiendo, el editor pasa a la siguiente coincidencia y la resalta. Si no hay coincidencias, la barra de estado muestra lo siguiente.  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 Las búsquedas incrementales se llevan a cabo desde la ubicación actual en el documento hacia abajo y de izquierda a derecha. Se pueden realizar mediante métodos abreviados de teclado.  
  
> [!NOTE]  
>  Para obtener una lista completa de las teclas de método abreviado, vea [Métodos abreviados de teclado de SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
## <a name="see-also"></a>Consulte también  
 [Buscar y reemplazar](../../relational-databases/scripting/search-and-replace.md)   
 [Buscar documentos de forma interactiva](../../relational-databases/scripting/search-documents-interactively.md)   
 [Buscar en documentos mediante las listas de resultados](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [Buscar texto con caracteres comodín](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Buscar texto mediante expresiones regulares](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
