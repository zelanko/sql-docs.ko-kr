---
title: Create 메서드 예 (VC + +) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Create method [ADOX], VC++ example
ms.assetid: 57fcb0eb-5d40-4ad4-996d-380732de8a3d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 410e35fd85e427f1552860e81f6e79412d395c85
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35285602"
---
# <a name="create-method-example-vc"></a>Create 메서드 예 (VC + +)
다음 코드에 있는 새 Microsoft Jet 데이터베이스를 만드는 방법을 보여 줍니다는 [만들기](../../../ado/reference/adox-api/create-method-adox.md) 메서드.  
  
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
      cout << "Error occured in CreateDatabaseX...." << endl;  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [Create 메서드(ADOX)](../../../ado/reference/adox-api/create-method-adox.md)
