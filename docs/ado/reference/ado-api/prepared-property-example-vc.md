---
title: Prepara el ejemplo de la propiedad (VC ++) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Prepared property [ADO], VC++ example
ms.assetid: f697ac1a-f125-42b5-bbf6-762a7fa30ae3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58da870e9c65be459e6bd4a8c35bb84aef325c61
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917583"
---
# <a name="prepared-property-example-vc"></a>Ejemplo de la propiedad Prepared (VC ++)
Este ejemplo se muestra el [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) propiedad abriendo dos [comando](../../../ado/reference/ado-api/command-object-ado.md) objetos - uno preparado y otro no preparado.  
  
## <a name="example"></a>Ejemplo  
  
```  
// Prepared_Property_Sample.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include <winbase.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void PreparedX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   PreparedX();  
   ::CoUninitialize();  
}  
  
void PreparedX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB:: namespace.  
   _ConnectionPtr pConnection = NULL;  
   _CommandPtr pCmd1 = NULL;  
   _CommandPtr pCmd2 = NULL;  
  
   // Define string variables.    
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open a connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
      _bstr_t strCmd ("SELECT title,type FROM titles ORDER BY type");  
  
      // Create two command objects for the same command; one prepared and one not.  
      TESTHR(pCmd1.CreateInstance(__uuidof(Command)));  
      pCmd1->ActiveConnection = pConnection;  
      pCmd1->CommandText = strCmd;  
  
      TESTHR(pCmd2.CreateInstance(__uuidof(Command)));  
      pCmd2->ActiveConnection = pConnection;  
      pCmd2->CommandText = strCmd;  
      pCmd2->PutPrepared(true);  
  
      // Set a timer,then execute the unprepared command 20 times.  
      DWORD sngStart = GetTickCount();   
  
      for ( int intLoop = 1 ; intLoop <= 20 ; intLoop++ )  
         pCmd1->Execute(NULL, NULL, adCmdText);  
  
      DWORD sngEnd=GetTickCount();   
      float sngNotPrepared = (float)(sngEnd - sngStart) / (float)1000;  
  
      // Reset the timer,then execute the prepared command 20 times  
      sngStart = GetTickCount();   
      for ( int intLoop = 1 ; intLoop <= 20 ; intLoop++ )  
         pCmd2->Execute(NULL, NULL, adCmdText);  
  
      sngEnd=GetTickCount();   
  
      float sngPrepared = (float)(sngEnd - sngStart) / (float)1000;  
  
      // Display performance results  
      printf("Performance Results:");  
      printf("\n\nNot Prepared: %6.3f seconds", sngNotPrepared);  
      printf("\nPrepared:     %6.3f seconds", sngPrepared);  
   }  
   catch (_com_error &e) {  
      // Display errors, if any. Pass a connection pointer accessed from the Connection.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print COM errors.   
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
 **Resultados de rendimiento:**  
**No se ha preparado:  0.016 segundos**  
**Preparado:      0.016 segundos**   
## <a name="see-also"></a>Vea también  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Propiedad Prepared (ADO)](../../../ado/reference/ado-api/prepared-property-ado.md)
