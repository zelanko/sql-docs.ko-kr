---
description: Catalog ActiveConnection 속성 예제(VC++)
title: Catalog ActiveConnection 속성 예제 (VC + +) | Microsoft Docs
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
- ActiveConnection property [ADOX], VC++ example
ms.assetid: 518905a9-6044-4194-af6c-84952d95939d
author: rothja
ms.author: jroth
ms.openlocfilehash: 37b50500b66c4f9e4bdca19facf27e290ac242c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440395"
---
# <a name="catalog-activeconnection-property-example-vc"></a>Catalog ActiveConnection 속성 예제(VC++)
[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 속성을 유효한 열린 연결로 설정 하면 카탈로그가 열립니다. 열려 있는 카탈로그에서 해당 카탈로그 내에 포함 된 스키마 개체에 액세스할 수 있습니다.  
  
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
      cout << "Error occurred in OpenConnectionX...." << endl;  
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
      cout << "Error occurred in OpenConnectionWithStringX...." << endl;  
   }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection 속성(ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
