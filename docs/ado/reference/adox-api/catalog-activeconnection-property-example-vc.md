---
title: "카탈로그 ActiveConnection 속성 예제 (VC + +) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- ActiveConnection property [ADOX], VC++ example
ms.assetid: 518905a9-6044-4194-af6c-84952d95939d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1f4307883e400990f36caa55384c00a991b36feb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="catalog-activeconnection-property-example-vc"></a>카탈로그 ActiveConnection 속성 예제 (VC + +)
설정의 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 속성 유효한 열린 연결을 "열립니다" 카탈로그입니다. 열려 있는 카탈로그에서 해당 카탈로그에 포함 된 스키마 개체를 액세스할 수 있습니다.  
  
```  
// CatalogActiveConnectionCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void OpenConnectionX();  
void OpenConnectionWithStringX();  
  
int main() {  
   if ( FAILED( ::CoInitialize(NULL) ) )  
      return -1;  
  
   OpenConnectionX();  
   OpenConnectionWithStringX();  
   ::CoUninitialize();  
}  
  
void OpenConnectionX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
  
   // Define string variables.  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = 'c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      m_pCnn->Open(strcnn, "", "", NULL);  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *) m_pCnn));  
      _variant_t vIndex = (short) 0;  
      cout<<m_pCatalog->Tables->GetItem(vIndex)->Type<<endl;  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in OpenConnectionX...." << endl;  
   }  
  
   if (m_pCnn)  
      if (m_pCnn->State == 1)  
         m_pCnn->Close();  
}  
  
void OpenConnectionWithStringX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
  
   // Define string variables.  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = 'c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      m_pCatalog->PutActiveConnection(strcnn);  
      _variant_t vIndex = (short) 0;  
      cout<<m_pCatalog->Tables->GetItem(vIndex)->Type<<endl;  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in OpenConnectionWithStringX...." << endl;  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ActiveConnection 속성(ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
