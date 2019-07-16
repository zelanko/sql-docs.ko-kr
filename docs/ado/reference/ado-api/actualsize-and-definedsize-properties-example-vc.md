---
title: ActualSize 및 DefinedSize 속성 예제 (VC + +) | Microsoft Docs
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
- ActualSize property [ADO], VC++ example
- DefinedSize property [ADO], VC++ example
ms.assetid: 05f7cc97-b806-41d2-939d-a955d10844c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 340f471215e9f8ec8bf4f0feaabec5cce559a9a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921478"
---
# <a name="actualsize-and-definedsize-properties-example-vc"></a>ActualSize 및 DefinedSize 속성 예제 (VC + +)
이 예제에서는 합니다 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) 및 [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) 속성을 정의 크기와 필드의 실제 크기를 표시 합니다.  
  
## <a name="example"></a>예제  
  
```  
// BeginActualSizeCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include "conio.h"   
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void ActualSizeX();  
void PrintProviderError(_ConnectionPtr pConnection);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
   ActualSizeX();  
   ::CoUninitialize();  
}  
  
void ActualSizeX() {  
   HRESULT hr = S_OK;  
  
   // Define ADO object pointers. Initialize pointers on define.  
   // These are in the ADODB::  namespace.  
   _RecordsetPtr pRstStores = NULL;  
  
   // Define Other variables  
   _bstr_t strMessage;  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open a recordset for the stores table.  
      TESTHR(pRstStores.CreateInstance(__uuidof(Recordset)));  
  
      // You have to explicitly pass the Cursor type and LockType to the Recordset here.  
      hr = pRstStores->Open("stores", strCnn, adOpenForwardOnly, adLockReadOnly, adCmdTable);  
  
      // Loop through the recordset displaying the contents of the stor_name field,   
      // the field's defined size, and its actual size.  
      pRstStores->MoveFirst();  
  
      while (!(pRstStores->EndOfFile)) {  
         strMessage = "Store Name: ";  
         strMessage += (_bstr_t)pRstStores->Fields->Item["stor_name"]->Value + "\n";  
         strMessage += "Defined Size: ";   
         strMessage += (_bstr_t)pRstStores->Fields->Item["stor_name"]->DefinedSize + "\n";  
         strMessage += "Actual Size: ";  
         strMessage += (_bstr_t) pRstStores->Fields->Item["stor_name"]->ActualSize + "\n";   
  
         printf("%s\n",(LPCSTR)strMessage);  
         pRstStores->MoveNext();  
      }  
   }  
   catch(_com_error &e) {  
      _variant_t vtConnect = pRstStores->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
         case VT_BSTR:  
            printf("Error:\n");  
            printf("Code = %08lx\n", e.Error());  
            printf("Message = %s\n", e.ErrorMessage());  
            printf("Source = %s\n", (LPCSTR) e.Source());  
            printf("Description = %s\n", (LPCSTR) e.Description());  
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
   if (pRstStores)  
      if (pRstStores->State == adStateOpen)  
         pRstStores->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
   long nCount = 0;      
   long i = 0;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for (i = 0 ; i < nCount ; i++) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number,(LPCSTR ) pErr->Description);  
      }  
   }  
}  
```  
  
 **저장소 이름: Eric 읽기 책**  
**정의 된 크기: 40**  
**실제 크기: 19**  
**저장소 이름: Barnum의**  
**정의 된 크기: 40**  
**실제 크기: 8**  
**저장소 이름: 뉴스 및 맥주**  
**정의 된 크기: 40**  
**실제 크기: 12**  
**저장소 이름: 문서-U-하 게 접지 되도록 합니다. 품질 세탁 및 온라인 설명서**  
**정의 된 크기: 40**  
**실제 크기: 36**  
**저장소 이름: Fricative Bookshop**  
**정의 된 크기: 40**  
**실제 크기: 18**  
**저장소 이름: Bookbeat**  
**정의 된 크기: 40**  
**실제 크기: 8**   
## <a name="see-also"></a>관련 항목  
 [ActualSize 속성 (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)   
 [DefinedSize 속성](../../../ado/reference/ado-api/definedsize-property.md)
