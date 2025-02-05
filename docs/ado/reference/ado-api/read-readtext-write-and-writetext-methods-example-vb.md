---
title: Lectura, ReadText, escritura y ejemplo de los métodos WriteText (VB) | Microsoft Docs
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
- ReadText method [ADO], Visual Basic example
- Write method [ADO], Visual Basic example
- Read method [ADO], Visual Basic example
- WriteText method [ADO], Visual Basic example
ms.assetid: 699b73f7-04f9-4d46-94b2-6cb12be6de56
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f77b2d395b76b537107ad87cf1487bb4d25a430c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931440"
---
# <a name="read-readtext-write-and-writetext-methods-example-vb"></a>Lectura, ReadText, escritura y ejemplo de los métodos WriteText (VB)
En este ejemplo se muestra cómo leer el contenido de un cuadro de texto en un texto [Stream](../../../ado/reference/ado-api/stream-object-ado.md) y un archivo binario **Stream**. Otras propiedades y métodos que se muestran incluyen [posición](../../../ado/reference/ado-api/position-property-ado.md), [tamaño](../../../ado/reference/ado-api/size-property-ado-parameter.md), [Charset](../../../ado/reference/ado-api/charset-property-ado.md), y [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
```  
'BeginReadVB  
Private Sub cmdRead_Click()  
    On Error GoTo ErrorHandler  
  
    'Declare variables  
    Dim objStream As Stream  
    Dim varA As Variant  
    Dim bytA() As Byte  
    Dim i As Integer  
    Dim strBytes As String  
  
    'Instantiate and Open Stream  
    Set objStream = New Stream  
    objStream.Open  
  
    'Write the text content of a textbox to the stream  
    If Text1.Text = "" Then  
        Err.Raise 1, , "The text field is blank."  
    End If  
    objStream.WriteText Text1.Text  
  
    'Display the text contents and size of the stream  
    objStream.Position = 0  
    Debug.Print "Default text:"  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    'Switch character set and display  
    objStream.Position = 0  
    objStream.Charset = "Windows-1252"  
    Debug.Print "New Charset text:"  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    'Switch to a binary stream and display  
    objStream.Position = 0  
    objStream.Type = adTypeBinary  
    Debug.Print "Binary:"  
    Debug.Print objStream.Read  
    Debug.Print objStream.Size  
  
    'Load an array of bytes with the text box text  
    ReDim bytA(Len(Text1.Text))  
    For i = 1 To Len(Text1.Text)  
        bytA(i - 1) = CByte(Asc(Mid(Text1.Text, i, 1)))  
    Next  
  
    'Write the buffer to the binary stream and display  
    objStream.Position = 0  
    objStream.Write bytA()  
    objStream.SetEOS  
    objStream.Position = 0  
    Debug.Print "Binary after Write:"  
    Debug.Print objStream.Read  
    Debug.Print objStream.Size  
  
    'Switch back to a text stream and display  
    Debug.Print "Translated back:"  
    objStream.Position = 0  
    objStream.Type = adTypeText  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    ' clean up  
    objStream.Close  
    Set objStream = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not objStream Is Nothing Then  
        If objStream.State = adStateOpen Then objStream.Close  
    End If  
    Set objStream = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndReadVB  
```  
  
## <a name="see-also"></a>Vea también  
 [Juego de caracteres (propiedad, ADO)](../../../ado/reference/ado-api/charset-property-ado.md)   
 [Propiedad Position (ADO)](../../../ado/reference/ado-api/position-property-ado.md)   
 [Método Read](../../../ado/reference/ado-api/read-method.md)   
 [Método ReadText](../../../ado/reference/ado-api/readtext-method.md)   
 [SetEOS (método)](../../../ado/reference/ado-api/seteos-method.md)   
 [Propiedad Size (Stream de ADO)](../../../ado/reference/ado-api/size-property-ado-stream.md)   
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Escribir (método)](../../../ado/reference/ado-api/write-method.md)   
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
