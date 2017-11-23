---
title: "연결 닫기 메서드를 테이블 형식 속성 예제 (VC + +) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords:
- Type property [ADOX], VC++ example
- Close method [ADOX], VC++ example
ms.assetid: d0e250aa-fc57-4fd3-9610-d64f50c5507f
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 22ca4649d8cab1b34bdfdcf064091c8faea9033a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="connection-close-method-table-type-property-example-vc"></a>Close 메서드 연결, 테이블 형식 속성 예제 (VC + +)
설정의 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 속성을 **Nothing** 해야 "닫기" 카탈로그입니다. 연결된 컬렉션은 비어 있게 됩니다. 카탈로그의 스키마 개체에서 생성 된 모든 개체가 분리 됩니다. 캐시 된 경우 해당 개체에 속성을 사용할 수 있지만 공급자에 대 한 호출을 요구 하는 속성을 읽는 중에 실패 합니다.  
  
```  
// BeginCloseConnectionCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void CloseConnectionByNothingX();  
void CloseConnectionX();  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL) ) )  
      return -1;  
  
   CloseConnectionByNothingX();  
   CloseConnectionX();  
  
   ::CoUninitialize();  
}  
  
void CloseConnectionByNothingX() {  
   HRESULT hr = S_OK;  
  
   // Define and initialize ADOX object pointers, in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
  
   // Define other variables  
   _variant_t vIndex = (short) 0;  
  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
  
      m_pCnn->Open("Provider='Microsoft.JET.OLEDB.4.0';Data Source= 'c:\\Northwind.mdb';", "", "", NULL);  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
      m_pTable = m_pCatalog->Tables->GetItem(vIndex);  
  
      // Cache m_pTable.Type info  
      cout << m_pTable->Type << endl;  
  
      _variant_t vCnn;  
      vCnn.vt = VT_DISPATCH;  
      vCnn.pdispVal = NULL;  
      m_pCatalog->PutActiveConnection(vCnn);  
  
      // m_pTable is orphaned, will succeed if this was cached  
      cout << m_pTable->Type << endl;  
  
      cout << m_pTable->Columns->GetItem(vIndex)->DefinedSize << endl;  
      // Previous line will fail if this info has not been cached  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\nError\n\tSource :  %s \n\tdescription : %s \n", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in CloseConnectionByNothingX...." << endl;  
   }  
}  
  
void CloseConnectionX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB  namespace.  
  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
  
   // Define other variables  
   _variant_t vIndex = (short) 0;  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      m_pCnn->Open("Provider='Microsoft.JET.OLEDB.4.0';Data Source= 'c:\\Northwind.mdb';", "", "", NULL);  
  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
  
      m_pTable = m_pCatalog->Tables->GetItem(vIndex);  
  
      // Cache m_pTable.Type info  
      cout << m_pTable->Type << endl;  
  
      m_pCnn->Close();  
  
      // m_pTable is orphaned, will succeed if this was cached  
      cout << m_pTable->Type << endl;  
  
      cout << m_pTable->Columns->GetItem(vIndex)->DefinedSize << endl;  
      // Previous line will fail if this info has not been cached  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\nError\n\tSource :  %s \n\tdescription : %s \n", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in CloseConnectionX...." << endl;  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ActiveConnection 속성(ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
