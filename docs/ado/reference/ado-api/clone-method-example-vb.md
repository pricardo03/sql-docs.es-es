---
title: Ejemplo (VB) del método Clone | Microsoft Docs
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
- Clone method [ADO], Visual Basic example
ms.assetid: 64cb1753-e074-4a2d-8b74-7c35f3f6f64d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05bd5c203b252909ad4707681aff49181bfde162
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919998"
---
# <a name="clone-method-example-vb"></a>Ejemplo del método Clone (VB)
Este ejemplo se usa el [clon](../../../ado/reference/ado-api/clone-method-ado.md) método para crear copias de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) y permite al usuario, a continuación, colocar el puntero de registro de cada copia de forma independiente.  
  
```  
'BeginCloneVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset array and connection variables  
    Dim arstStores(1 To 3) As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strSQLStore As String  
    Dim strCnxn As String  
     'record variables  
    Dim intLoop As Integer  
    Dim strMessage As String  
    Dim strFind As String  
  
    ' Open a connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset as a static cursor type recordset  
    Set arstStores(1) = New ADODB.Recordset  
    strSQLStore = "SELECT stor_name FROM Stores ORDER BY stor_name"  
    arstStores(1).Open strSQLStore, strCnxn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Create two clones of the original Recordset  
    Set arstStores(2) = arstStores(1).Clone  
    Set arstStores(3) = arstStores(1).Clone  
  
    ' Loop through the array so that on each pass the user  
    ' is searching a different copy of the same Recordset  
    Do  
        For intLoop = 1 To 3  
             ' Ask for search string while showing where  
             ' the current record pointer is for each Recordset  
            strMessage = _  
                "Recordsets from stores table:" & vbCr & _  
                "  1 - Original - Record pointer at " & arstStores(1)!stor_name & vbCr & _  
                "  2 - Clone - Record pointer at " & arstStores(2)!stor_name & vbCr & _  
                "  3 - Clone - Record pointer at " & arstStores(3)!stor_name & vbCr & _  
                "Enter search string for #" & intLoop & ":"  
  
            strFind = Trim(InputBox(strMessage))  
             ' make sure something was entered, if not then EXIT loop  
            If strFind = "" Then Exit Do  
  
             ' otherwise locate the record from the entered string  
            arstStores(intLoop).Filter = "stor_name = '" & strFind & "'"  
  
             'if there's no match, jump to the last record  
            If arstStores(intLoop).EOF Then  
                arstStores(intLoop).Filter = adFilterNone  
                arstStores(intLoop).MoveLast  
            Else  
                MsgBox "Found " & strFind  
            End If  
        Next intLoop  
    Loop  
  
    ' clean up  
    arstStores(1).Close  
    arstStores(2).Close  
    arstStores(3).Close  
    Cnxn.Close  
    Set arstStores(1) = Nothing  
    Set arstStores(2) = Nothing  
    Set arstStores(3) = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not arstStores(1) Is Nothing Then  
        If arstStores(1).State = adStateOpen Then arstStores(1).Close  
    End If  
    Set arstStores(1) = Nothing  
    If Not arstStores(2) Is Nothing Then  
        If arstStores(2).State = adStateOpen Then arstStores(2).Close  
    End If  
    Set arstStores(2) = Nothing  
    If Not arstStores(3) Is Nothing Then  
        If arstStores(3).State = adStateOpen Then arstStores(3).Close  
    End If  
    Set arstStores(3) = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndCloneVB  
```  
  
## <a name="see-also"></a>Vea también  
 [Clone (método) (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
