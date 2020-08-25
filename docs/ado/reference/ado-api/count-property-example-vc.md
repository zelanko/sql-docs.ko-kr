---
description: Count 속성 예제(VC++)
title: Count 속성 예제 (VC + +) | Microsoft Docs
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
- Count property [ADO], VC++ example
ms.assetid: 54dfb1dd-636c-4560-8a3f-32b1f6aa07d7
author: rothja
ms.author: jroth
ms.openlocfilehash: 2bd196830ad1212d495778d037c915b2f4d86874
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775652"
---
# <a name="count-property-example-vc"></a>Count 속성 예제(VC++)
이 예에서는 ***Employee*** 데이터베이스에 두 개의 컬렉션이 있는 [Count](./count-property-ado.md) 속성을 보여 줍니다. 속성은 각 컬렉션의 개체 수를 가져오고 이러한 컬렉션을 열거 하는 루프의 상한 값을 설정 합니다.  
  
```  
// BeginCountCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include<conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void CountX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
   CountX();  
   ::CoUninitialize();  
}  
  
void CountX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace  
   _RecordsetPtr pRstEmployee = NULL;  
  
   // Define Other Variables  
   _variant_t Index;  
   Index.vt = VT_I2;  
   int j = 0;  
  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open recordset with data from Employee table.  
      TESTHR(pRstEmployee.CreateInstance(__uuidof(Recordset)));  
      pRstEmployee->Open("Employee", strCnn, adOpenForwardOnly, adLockReadOnly, adCmdTable);  
  
      // Print information about Fields collection.  
      printf("%d Fields in Employee\n", pRstEmployee->Fields->Count);  
      for (short int intLoop = 0 ; intLoop <= (pRstEmployee->Fields->Count-1) ; intLoop++) {  
         Index.iVal = intLoop;  
         printf(" %s\n", (LPSTR) pRstEmployee->Fields->GetItem(Index)->Name);  
      }  
  
      // Print information about Properties collection.  
      printf("\n%d Properties in Employee\n", pRstEmployee->Properties->Count);  
      for (short int intLoop = 0 ; intLoop <= (pRstEmployee->Properties->Count - 1) ; intLoop++) {  
         j++;  
         Index.iVal = intLoop;  
         printf(" %s\n" , (LPSTR)pRstEmployee->Properties->GetItem(Index)->Name);  
      }  
   }  
   catch(_com_error &e) {  
      // Display any errors that result from executing the query.  
      // Pass a connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstEmployee->GetActiveConnection();  
  
      switch(vtConnect.vt) {  
      case VT_BSTR:  
         PrintComError(e);  
         break;  
      case VT_DISPATCH:  
         PrintProviderError(vtConnect);  
         break;  
      default:  
         printf("Errors occured.");  
         break;  
      }  
   }  
   // Clean up objects before exit.  
   if (pRstEmployee)  
      if (pRstEmployee->State == adStateOpen)  
         pRstEmployee->Close();  
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
         printf("Error number: %x\t%s\n", pErr->Number, pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print Com errors.  
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [Count 속성(ADO)](./count-property-ado.md)