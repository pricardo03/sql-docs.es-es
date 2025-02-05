---
title: SQLSetStmtAttr (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc222c1c8669769060de4fc0a1390a9bf02e3f31
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091696"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLSetStmtAttr** función en la biblioteca de cursores. Para obtener información general sobre **SQLSetStmtAttr**, consulte [función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 La biblioteca de cursores es compatible con los siguientes atributos de instrucción con **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 La biblioteca de cursores solo admite los SQL_CURSOR_FORWARD_ONLY y SQL_CURSOR_STATIC valores del atributo de instrucción SQL_ATTR_CURSOR_TYPE.  
  
 Para los cursores de solo avance, la biblioteca de cursores es compatible con el valor SQL_CONCUR_READ_ONLY del atributo de instrucción SQL_ATTR_CONCURRENCY. Para los cursores estáticos, la biblioteca de cursores es compatible con los valores de atributo de instrucción SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY y SQL_CONCUR_VALUES.  
  
 La biblioteca de cursores admite solo el valor SQL_SC_NON_UNIQUE del atributo de instrucción SQL_ATTR_SIMULATE_CURSOR.  
  
 Aunque la especificación de ODBC admite llamadas a **SQLSetStmtAttr** con los atributos SQL_ATTR_PARAM_BIND_TYPE o SQL_ATTR_ROW_BIND_TYPE después **SQLFetch** o **SQLFetchScroll**  se ha llamado, el cursor no lo hace biblioteca. Antes de que puede cambiar el tipo de enlace en la biblioteca de cursores, la aplicación debe cerrar el cursor. La biblioteca de cursores admite el cambio de la SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR y atributos de instrucción SQL_ATTR_PARAMS_PROCESSED_PTR cuando un cursor está abierto.  
  
 Una aplicación puede llamar a **SQLSetStmtAttr** con un **atributo** de SQL_ATTR_ROW_ARRAY_SIZE para cambiar el tamaño del conjunto de filas mientras está abierto un cursor. El nuevo tamaño del conjunto de filas surtirá efecto la próxima vez **SQLFetchScroll** o **SQLFetch** se llama.  
  
 La biblioteca de cursores es compatible con el atributo de instrucción SQL_ATTR_PARAM_BIND_OFFSET_PTR o SQL_ATTR_ROW_BIND_OFFSET_PTR para habilitar los desplazamientos de enlace. El desplazamiento de enlace no se usará para las llamadas a **SQLFetch** cuando se usa la biblioteca de cursores con un ODBC 2. *x* controlador.  
  
 La biblioteca de cursores admite establecer el atributo de instrucción SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE.
