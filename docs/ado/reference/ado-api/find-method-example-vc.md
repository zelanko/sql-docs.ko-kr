---
title: "메서드 예제 (VC + +) 찾기 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- Find method [ADO], VC++ example
ms.assetid: 594c51cb-1157-4417-802b-d91b875ba020
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aa68bfc51fa7305ec97d8aacbb5a0c95ed409fa3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="find-method-example-vc"></a>찾을 메서드 예제 (VC + +)
사용 하 여이 예제는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 [찾을](../../../ado/reference/ado-api/find-method-ado.md) 찾고의 비즈니스 이름 수를 계산 하는 메서드는 **Pubs** 데이터베이스입니다. 이 예제에서는 기본 공급자와 비슷한 기능을 지원 하지 않습니다 가정 합니다.  
  
```  
// BeginFindCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// This Class extracts only titleId from Titles table.  
class CTitlesRs : public CADORecordBinding {  
BEGIN_ADO_BINDING(CTitlesRs)  
  
   // Column title_id is the first field in the recordset from Titles table.  
   ADO_VARIABLE_LENGTH_ENTRY2(1, adVarChar, m_szt_titleid, sizeof(m_szt_titleid), lt_titleidStatus, FALSE)  
  
END_ADO_BINDING()  
  
public:  
   CHAR m_szt_titleid[150];  
   ULONG lt_titleidStatus;  
};  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void FindX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
   FindX();  
   ::CoUninitialize();  
}  
  
void FindX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   _RecordsetPtr pRstTitles = NULL;  
   IADORecordBinding *picRs = NULL;   // Interface Pointer declared.  
   CTitlesRs titlers;   // C++ class object  
  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
      // Open title Table  
      TESTHR(pRstTitles.CreateInstance(__uuidof(Recordset)));  
  
      pRstTitles->Open("SELECT title_id FROM titles",   
         _variant_t((IDispatch *)pConnection),   
         adOpenStatic, adLockReadOnly, adCmdText);  
  
      // The default parameters are sufficient to search forward through a Recordset.  
  
      pRstTitles->Find ("title_id LIKE 'BU%'", 0, adSearchForward, "");  
  
      // Open an IADORecordBinding interface pointer for Binding Recordset to a class      
      TESTHR(pRstTitles->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ Class here      
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Skip the current record to avoid finding the same row repeatedly.   
      // The bookmark is redundant because Find searches from the current position.  
      int count = 0;  
  
      // Continue if last find succeeded.  
      while (!(pRstTitles->EndOfFile)) {  
         printf("Title ID: %s\n", titlers.lt_titleidStatus == adFldOK ?  
            titlers.m_szt_titleid : "<NULL>");  
         count++;   // Count the last title found.  
  
         _variant_t mark = pRstTitles->Bookmark;   // Note current pos.  
         pRstTitles->Find("title_id LIKE 'BU%'", 1, adSearchForward, mark);  
      }  
      printf("The number of business titles is %d\n", count);  
   }  
   catch(_com_error &e) {  
      // Display errors, if any. Pass connection pointer accessed from the Recordset.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }      
  
   // Clean up objects before exit. Release the IADORecordset Interface here     
   if (picRs)  
      picRs->Release();  
  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen)  
         pRstTitles->Close();  
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
         printf("\t Error number: %x\t%s", pErr->Number, (LPCSTR)pErr->Description);  
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
  
## <a name="see-also"></a>관련 항목:  
 [Find 메서드 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

