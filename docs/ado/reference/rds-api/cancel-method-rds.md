---
title: Cancel (método) (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90d3e60a77df15d1b2db302df8a3c1d4a39de245
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964614"
---
# <a name="cancel-method-rds"></a>Cancel (método) (RDS)
Cancela la ejecución de una pendiente, llamada de método asincrónico.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>Comentarios  
 Cuando se llama a **cancelar**, [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) se establece automáticamente en **adcReadyStateLoaded**y el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) estará vacía.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método Cancel (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel (método) (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Propiedad ExecuteOptions (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


