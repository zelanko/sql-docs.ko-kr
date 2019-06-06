---
title: MaxRecords 속성 예제 (VC + +) | Microsoft Docs
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
- MaxRecords property [ADO], VC++ example
ms.assetid: af6b399b-e546-4de5-9cd1-5a6e0ec7ddc7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 503651db5d71403802c82a4931e4bdf9b1a69fd4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707618"
---
# <a name="maxrecords-property-example-vc"></a>MaxRecords 속성 예제(VC++)
이 예제에서는 합니다 [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md) 를 엽니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 에서 10 개의 가장 비싼 책 제목을 포함 하는 ***제목*** 테이블.  
  
## <a name="example"></a>예제  
  
```  
// MaxRecords_Property_Example.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF","EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// This class extracts titles and type from the titles table  
class CTitleRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CTitleRs)  
  
      // Column title is the 1st field in the Recordset  
      ADO_VARIABLE_LENGTH_ENTRY2(1, adVarChar,m_szau_Title,  
      sizeof(m_szau_Title), lau_TitleStatus, FALSE)  
  
      // Column price is the 2nd field in the Recordset  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adDouble, m_szau_Price,  
      sizeof(m_szau_Price), lau_PriceStatus, FALSE)  
  
   END_ADO_BINDING()  
  
public:  
   CHAR m_szau_Title[81];  
   ULONG lau_TitleStatus;  
   DOUBLE m_szau_Price;  
   ULONG lau_PriceStatus;  
};  
  
// Function Declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void MaxRecordsX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   MaxRecordsX();  
   ::CoUninitialize();  
}  
  
void  MaxRecordsX() {  
   // Define ADO ObjectPointers.  Initialize Pointers on define  
   // These are in the ADODB :: namespace  
   _RecordsetPtr pRstTemp = NULL;  
  
   // Define Other Variables  
   IADORecordBinding *picRs = NULL;   // Interface Pointer Declared    
   CTitleRs titlers;   // C++ Class Object  
  
   try {  
      // Assign Connection String to Variable  
      _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
      // Open Recordset containing the 10 most expensive titles in the Titles table.  
      TESTHR(pRstTemp.CreateInstance(__uuidof(Recordset)));  
  
      pRstTemp->MaxRecords = 10;  
  
      pRstTemp->Open("SELECT title,price FROM Titles ORDER BY Price DESC",  
         strCnn, adOpenForwardOnly, adLockReadOnly, adCmdText);  
  
      // Open IADORecordBinding interface pointer for binding Recordset to a class  
      TESTHR(pRstTemp->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ class here  
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Display the contents of the Recordset  
      printf("Top Ten Titles by Price:\n\n");  
  
      while ( !(pRstTemp->EndOfFile) ) {  
         printf("%s ---  %6.2lf\n", titlers.lau_TitleStatus == adFldOK ?   
            titlers.m_szau_Title : "<NULL>", titlers.lau_PriceStatus == adFldOK ?   
            titlers.m_szau_Price : 0.00);  
         pRstTemp->MoveNext();  
      }  
   }  
   catch(_com_error &e) {  
      // Display errors, if any.  Pass connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstTemp->GetActiveConnection();  
  
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
  
   // Clean up objects before exit. Release the IADORecordset Interface here     
   if (picRs)  
      picRs->Release();  
  
   if (pRstTemp)  
      if (pRstTemp->State == adStateOpen)  
         pRstTemp->Close();  
};  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object  
   // pErr is a record object in the Connection's Error collection  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count)>0 ) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount-1  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error Number :%x \t %s", pErr->Number, pErr->Description);  
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
  
 **가격으로 상위 10 개의 제목:**  
**하지만 사용자 친숙 한이? ---22.95**  
**Phobic 및 비 Phobic 개인용 컴퓨터: 동작의 변형을---21.59**  
**Onions, Leeks, 및 마늘: ---20.95 지중해의 요리 비밀**  
**실리콘밸리---20.00의 비밀**  
**사용 중인 경영진의 데이터베이스 가이드---19.99**  
**컴퓨터---19.99에 대 한 직접 강연**  
**실리콘밸리 Gastronomic 처리---19.99**  
**장기적인된 데이터 Deprivation: 네 가지 사례 연구---19.99**  
**Sushi, Anyone? ---   14.99**  
**50 년 Buckingham Palace 사용---11.95에**   
## <a name="see-also"></a>관련 항목  
 [MaxRecords 속성 (ADO)](../../../ado/reference/ado-api/maxrecords-property-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
