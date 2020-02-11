---
title: Clustered 속성 예제 (VC + +) | Microsoft Docs
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
- Clustered property [ADOX], VC++ example
ms.assetid: b993e357-3e2e-48a7-a627-76909160c97f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac845019bf2f8a8582f20adb5d4f8861f622fe44
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "76925490"
---
# <a name="clustered-property-example-vc"></a>Clustered 속성 예제(VC++)
이 예에서는 [인덱스](../../../ado/reference/adox-api/index-object-adox.md)의 [클러스터형](../../../ado/reference/adox-api/clustered-property-adox.md) 속성을 보여 줍니다. Microsoft Jet 데이터베이스는 클러스터형 인덱스를 지원 하지 않으므로이 예에서는 *Northwind* 데이터베이스에 있는 모든 인덱스의 **클러스터형** 속성에 대해 **False** 를 반환 합니다.  
  
```  
// BeginClusteredCpp.cpp  
// compile with: /EHsc  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ClusteredX();  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL) ) )  
      return -1;  
  
   ClusteredX();  
   ::CoUninitialize();  
}  
  
void ClusteredX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
   _IndexPtr m_pIndex = NULL;  
  
   // Define other variables here  
   _variant_t vIndex;  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
  
      // Connect to the catalog.  
      m_pCatalog->PutActiveConnection("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';");  
  
      // Enumerate Tables.  
      for (short iTable = 0 ; iTable < m_pCatalog->Tables->Count ; iTable++ ) {  
         vIndex = iTable;  
         m_pTable = m_pCatalog->Tables->GetItem(vIndex);  
  
         // Enumerate Indexes.  
         for (short iIndex = 0 ; iIndex < m_pTable->Indexes->Count ; iIndex++) {  
            vIndex = iIndex;  
            m_pIndex = m_pTable->Indexes->GetItem(vIndex);  
            cout << m_pTable->Name << "   " ;  
            cout << m_pIndex->Name << "   " << (m_pIndex->GetClustered() ? "True" : "False") << endl;  
         }  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occurred in ClusteredX...."<< endl;  
   }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [Clustered 속성 (ADOX)](../../../ado/reference/adox-api/clustered-property-adox.md)   
 [인덱스 개체(ADOX)](../../../ado/reference/adox-api/index-object-adox.md)
