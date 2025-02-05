---
title: Llamar a procedimientos almacenados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58e5160065847d5729548702b5f1d65eb31bf694
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200264"
---
# <a name="call-stored-procedures-odbc"></a>Llamar a procedimientos almacenados (ODBC)
  Cuando una instrucción SQL llama a un procedimiento almacenado mediante la cláusula de escape ODBC CALL, Microsoft?? SQL Server??? controlador envía el procedimiento a SQL Server mediante el mecanismo de procedimiento almacenado remoto (RPC) de la llamada. Las solicitudes de RPC omiten gran parte del análisis de la instrucción y del procesamiento del parámetro en SQL Server, y es más rápido que usar la instrucción Transact-SQL EXECUTE.  
  
 Para una aplicación de ejemplo que muestra esta característica, consulte [proceso códigos de retorno y parámetros de salida &#40;ODBC&#41;](running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>Para ejecutar un procedimiento como una RPC  
  
1.  Cree una instrucción SQL que use la secuencia de escape ODBC CALL. La instrucción usa marcadores de parámetros para cada parámetro de entrada, de entrada/salida y de salida, así como para el valor devuelto por el procedimiento (si existe):  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  Llame a [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) para cada parámetro de entrada, de entrada/salida y de salida, así como para el valor devuelto por el procedimiento (si existe).  
  
3.  Ejecute la instrucción con [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399).  
  
> [!NOTE]  
>  Si una aplicación envía un procedimiento con la sintaxis de Transact-SQL EXECUTE (en contraposición al flujo de escape ODBC CALL), el controlador ODBC de SQL Server pasa la llamada al procedimiento a SQL Server como una instrucción SQL en lugar de como una RPC. Además, los parámetros de salida no se devuelven si se usa la instrucción Transact-SQL EXECUTE.  
  
## <a name="see-also"></a>Vea también  
 [Temas de procedimientos almacenados de ejecución &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [Procesamiento por lotes las llamadas de procedimiento almacenado](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [Ejecutar procedimientos almacenados](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Llamar a un procedimiento almacenado](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [Procedimientos](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  
