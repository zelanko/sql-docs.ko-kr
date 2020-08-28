---
description: NumericScale 및 Precision 속성 예제(VC++)
title: NumericScale 및 Precision 속성 예제 (VC + +) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- NumericScale property [ADO], VC++ example
- Precision property [ADO], VC++ example
ms.assetid: 55d91ba8-4d80-4df6-af8e-060a19ddc138
author: rothja
ms.author: jroth
ms.openlocfilehash: fbca744c17ffd3dfa9b84b679e9efeaf0d27ad9a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990394"
---
# <a name="numericscale-and-precision-properties-example-vc"></a>NumericScale 및 Precision 속성 예제(VC++)
이 예에서는 [NumericScale](./numericscale-property-ado.md) 및 [precision](./precision-property-ado.md) 속성을 사용 하 여 ***Pubs*** 데이터베이스의 ***할인율*** 테이블에 있는 필드의 숫자 소수 자릿수와 전체 자릿수를 표시 합니다.  
  
```cpp
// BeginNumericScaleCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void NumericScaleX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   NumericScaleX();  
   ::CoUninitialize();  
}  
  
void NumericScaleX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace  
   _RecordsetPtr pRstDiscounts = NULL;  
   FieldsPtr fldTemp = NULL;  
  
   // Define Other Variables  
   _variant_t Index;  
   Index.vt = VT_I2;  
  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open recordset.  
      TESTHR(pRstDiscounts.CreateInstance(__uuidof(Recordset)));  
      pRstDiscounts->Open("discounts", strCnn, adOpenForwardOnly, adLockReadOnly, adCmdTable);  
  
      // Display numeric scale and precision of numeric and small integer fields.  
      fldTemp = pRstDiscounts->GetFields();  
  
      for (short int intLoop = 0 ; intLoop < (int)fldTemp->GetCount() ; intLoop++ ) {  
         Index.iVal = intLoop;  
  
         if ( (fldTemp->GetItem(Index)->Type == adNumeric) ||   
            (fldTemp->GetItem(Index)->Type == adSmallInt) ) {   
            printf("Field: %s\n" , (LPCSTR)fldTemp->GetItem(Index)->GetName());  
            printf("Numeric scale: %d\n", fldTemp->GetItem(Index)->GetNumericScale());  
            printf("Precision: %d\n", fldTemp->GetItem(Index)->GetPrecision());  
         }  
      }  
   }  
   catch(_com_error &e) {      
      // Display errors, if any. Pass a connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstDiscounts->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
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
   if (pRstDiscounts)  
      if (pRstDiscounts->State == adStateOpen)  
         pRstDiscounts->Close();  
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
  
## <a name="see-also"></a>참고 항목  
 [NumericScale 속성 (ADO)](./numericscale-property-ado.md)   
 [Precision 속성(ADO)](./precision-property-ado.md)