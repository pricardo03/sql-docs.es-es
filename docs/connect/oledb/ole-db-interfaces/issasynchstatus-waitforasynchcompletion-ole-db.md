---
title: 'ISSAsynchStatus:: WaitForAsynchCompletion (OLE DB) | Microsoft Docs'
description: ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
apitype: COM
helpviewer_keywords:
- WaitForAsynchCompletion method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 6779c0892137ee60f011f365e0f3ee4d46b046f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994364"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Espera hasta que la operación que se ejecuta de forma asincrónica haya finalizado o hasta que se produzca un tiempo de espera.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT WaitForAsynchCompletion(   
        DWORD dwMillisecTimeOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *dwMillisecTimeOut*[entrada]  
 Tiempo de espera en milisegundos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_UNEXPECTED  
 Un conjunto de filas está en un estado no usado porque se ha llamado a **ITransaction::Commit** o a **ITransaction::Abort**, o bien el conjunto de filas se ha cancelado durante su fase de inicialización.  
  
 DB_E_CANCELED  
 El procesamiento asincrónico se ha cancelado durante el rellenado del conjunto de filas o la inicialización del objeto de origen de datos.  
  
 DB_S_ASYNCHRONOUS  
 La operación todavía no se ha completado aunque se ha alcanzado el tiempo de espera especificado.  
  
> [!NOTE]  
>  Además de los valores de código de retorno enumerados anteriormente, el método **ISSAsynchStatus::WaitForAsynchCompletion** también admite los valores de código de retorno que devuelven los métodos **ICommand::Execute** e **IDBInitialize::Initialize** de OLEDB básicos.  
  
## <a name="remarks"></a>Notas  
 No se devolverá el método **ISSAsynchStatus::WaitForAsynchCompletion** hasta que haya transcurrido el valor de tiempo de espera (en milisegundos) o se haya completado la operación pendiente. El objeto **Command** incluye una propiedad **CommandTimeout** que controla el número de segundos durante los que se ejecutará una consulta antes de que se exceda el tiempo de espera. La propiedad **CommandTimeout** se omitirá si se usa junto con el método **ISSAsynchStatus::WaitForAsynchCompletion**.  
  
 La propiedad de tiempo de espera se omite en las operaciones asincrónicas. El parámetro de tiempo de espera de **ISSAsynchStatus::WaitForAsynchCompletion** especifica el tiempo máximo que debe transcurrir antes de que se devuelva el control al autor de la llamada. Si este tiempo de espera expira, se devolverá DB_S_ASYNCHRONOUS. Los tiempos de espera nunca cancelan las operaciones asincrónicas. Si la aplicación necesita cancelar una operación asincrónica que no se ha completado en un período de tiempo de espera, debe esperar a que finalice el tiempo de espera y, a continuación, cancelar explícitamente la operación si se devuelve DB_S_ASYNCHRONOUS.  
  
> [!NOTE]  
>  Si se utilizan OLE DB Service Components, se puede devolver S_OK cuando se espera DB_S_ASYNCHRONOUS, por lo que las aplicaciones deben llamar a [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) para comprobar la finalización cuando se devuelven S_OK o DB_S_ASYNCHRONOUS.  
  
 Si el valor *dwMillisecTimeOut* se establece en INFINITE, el método **ISSAsynchStatus::WaitForAsynchCompletion** se bloquea hasta que se completa la operación. Si el valor *dwMillisecTimeOut* se establece en 0, el método se devolverá inmediatamente con el estado de la operación pendiente. Si el tiempo de espera expira antes de que se complete la operación, se devolverá DB_S_ASYNCHRONOUS.  
  
 Si la operación se completa antes de que el tiempo de espera expire, el HRESULT devuelto será el HRESULT devuelto por la operación (el HRESULT que se habría devuelto si la operación se hubiese realizado de forma sincrónica).  
  
 Además, se ha agregado la propiedad SSPROP_ISSAsynchStatus al conjunto de propiedades DBPROPSET_SQLSERVERROWSET. Los proveedores que admiten la interfaz [ISSAsynchStatus](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md) deben implementar esta propiedad con un valor de VARIANT_TRUE.  
  
## <a name="see-also"></a>Consulte también  
 [Realizar operaciones asincrónicas](../../oledb/features/performing-asynchronous-operations.md)   
 [OLE DB &#40;ISSAsynchStatus&#41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
