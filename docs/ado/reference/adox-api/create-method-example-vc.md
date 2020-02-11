---
title: Create 메서드 예제 (VC + +) | Microsoft Docs
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
- Create method [ADOX], VC++ example
ms.assetid: 57fcb0eb-5d40-4ad4-996d-380732de8a3d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8b694c8d8e7381a8237511f8bba3ffd444cd5d37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "76910538"
---
# <a name="create-method-example-vc"></a>Create 메서드 예제(VC++)
다음 코드에서는 [create](../../../ado/reference/adox-api/create-method-adox.md) 메서드를 사용 하 여 새 Microsoft Jet 데이터베이스를 만드는 방법을 보여 줍니다.  
  
```  
// BeginCreateDatabaseCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#define TESTHR(x) if FAILED(x) _com_issue_error(x);  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
void CreateDatabaseX(void);  
  
int main() {  
   HRESULT hr = S_OK;  
  
   hr = ::CoInitialize(NULL);  
   if (SUCCEEDED(hr)) {  
      CreateDatabaseX();  
      ::CoUninitialize();  
   }  
}  
  
// Create a new Jet database with the Create method  
void CreateDatabaseX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
  
   // Set ActiveConnection of Catalog to this string  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = c:\\new.mdb");  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      m_pCatalog->Create(strcnn);  
      printf("Database 'c:\\new.mdb' is created.\n");  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occurred in CreateDatabaseX...." << endl;  
   }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [Create 메서드(ADOX)](../../../ado/reference/adox-api/create-method-adox.md)
