---
title: Ejemplo de la propiedad de estado (campo) (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c28a0b615a9f250c8539e87abf9fefbc11f513ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916827"
---
# <a name="status-property-example-field-vb"></a>Ejemplo de la propiedad de estado (campo) (VB)
El siguiente ejemplo abre un documento desde una carpeta de lectura/escritura mediante el [Internet Publishing Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). El [estado](../../../ado/reference/ado-api/status-property-ado-field.md) propiedad de un [campo](../../../ado/reference/ado-api/field-object.md) objeto de la [registro](../../../ado/reference/ado-api/record-object-ado.md) primero se establecerá en **adFieldPendingInsert**, a continuación, se puede actualizar a **adFieldOk**.  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=https://MyServer/"  
   Cnxn.Open strCnxn  
  
   Set File = New ADODB.Record  
   strFile = "Folder/FileName"  
   ' Open a read/write document  
   File.Source = strFile  
   File.ActiveConnection = Cnxn  
   File.Mode = adModeReadWrite  
   File.Open  
  
   Debug.Print "Append a couple of fields"  
  
   File.Fields.Append "chektest:fld1", adWChar, 42, adFldUpdatable, "fld1"  
   File.Fields.Append "chektest:fld2", adWChar, 42, adFldUpdatable, "fld2"  
  
   Debug.Print "status for the fields"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert  
  
    'turn off error-handling to verify field status  
   On Error Resume Next  
  
   File.Fields.Update  
  
   Debug.Print "Update succeeds"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert + adFieldUnavailable  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert + adFieldUnavailable  
  
    ' resume default error-handling  
   On Error GoTo 0  
  
     ' clean up  
    File.Close  
    Cnxn.Close  
    Set File = Nothing  
    Set Cnxn = Nothing  
  
End Sub  
'EndStatusFieldVB  
```  
  
 En el ejemplo siguiente se elimina un conocido **campo** desde un **registro** abierto desde un documento. El **estado** propiedad se establecerá en primer lugar en **adFieldOK**, a continuación, **adFieldPendingUnknown**.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 El código siguiente elimina una **campo** desde un **registro** abierto en un documento de solo lectura. **Estado** se establecerá en **adFieldPendingDelete**. En [actualización](../../../ado/reference/ado-api/update-method.md), se producirá un error en la eliminación y **estado** será **adFieldPendingDelete** plus **adFieldPermissionDenied**. [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) borra la pendiente **estado** configuración.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Propiedad Status (Field ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)
