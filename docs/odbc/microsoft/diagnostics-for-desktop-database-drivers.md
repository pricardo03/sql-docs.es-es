---
title: Controladores de base de datos de diagnóstico de escritorio | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4e7c8ea96708886f9edf54047bd2a2104ba0ec8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031222"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnóstico de controladores de escritorio de la base de datos
Todos los errores y advertencias no comprueba ni activada parcialmente por el Administrador de controladores se controlan mediante el controlador. El controlador también asigna nativo errores o los errores devueltos por el origen de datos para SQLSTATEs. Cada función que figure en la *referencia del programador de ODBC* contiene una sección de "Diagnostics" que especifica las condiciones y los mensajes.  
  
 Las aplicaciones llaman a **SQLGetDiagRec** para recuperar SQLSTATE, el código de error nativo y los mensajes de diagnóstico. Una llamada a **SQLGetDiagField** y especificar el campo recupera los campos individuales de diagnóstico. El nivel de compatibilidad de los identificadores de diagnóstico se muestra en la tabla siguiente.  
  
|DiagIdentifiers|Nivel de compatibilidad|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|No compatible|  
|SQL_DIAG_CLASS_ORIGIN|Se admite. Siempre "ODBC 3.0" para las versiones 3.0 y posteriores de este controlador.|  
|SQL_DIAG_COLUMN_NUMBER|Compatible|  
|SQL_DIAG_CURSOR_ROW_COUNT|No compatible|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|No compatible|  
|SQL_DIAG_MESSAGE_TEXT|Compatible|  
|SQL_DIAG_NATIVE|Compatible|  
|SQL_DIAG_NUMBER|Compatible|  
|SQL_DIAG_RETURNCODE|Compatible pero implementado por el Administrador de controladores|  
|SQL_DIAG_ROW_COUNT|Compatible|  
|SQL_DIAG_ROW_NUMBER|Compatible|  
|SQL_DIAG_SERVER_NAME|No compatible|  
|SQL_DIAG_SQLSTATE|Compatible|  
|SQL_DIAG_SUBCLASS_ORIGIN|Compatible|
