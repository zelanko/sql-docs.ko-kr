---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4dcaa288df7b6e232c187ae50dac3e4ac51d8be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747211"
---
# <a name="count-property-example-vc"></a>Count 속성 예제(VC++)
이 예제에서는 합니다 [수](../../../ado/reference/ado-api/count-property-ado.md) 에서 두 개의 컬렉션을 사용 하 여 속성을 ***직원*** 데이터베이스. 각 컬렉션의 개체 수를 가져옵니다 속성과 해당이 컬렉션을 열거 하는 루프에 대 한 상한값을 설정 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [Count 속성(ADO)](../../../ado/reference/ado-api/count-property-ado.md)
