---
title: Estado de fila | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a62bad0e69a8bf8b5365575f97e4791cbbf270d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057111"
---
# <a name="row-status"></a>Estado de fila
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 La biblioteca de cursores, crea un búfer en la memoria caché para el estado de fila. La biblioteca de cursores recupera los valores de la matriz de Estados de fila (especificado con el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR) de este búfer. Para cada fila, la biblioteca de cursores establece en este búfer:  
  
-   SQL_ROW_DELETED cuando se ejecuta en una posición elimine la instrucción en la fila.  
  
-   SQL_ROW_ERROR cuando encuentra un error al recuperar la fila del origen de datos con **SQLFetch**.  
  
-   SQL_ROW_SUCCESS cuando captura correctamente la fila del origen de datos con **SQLFetch**.  
  
-   SQL_ROW_UPDATED cuando ejecuta una instrucción de actualización por posición en la fila.
