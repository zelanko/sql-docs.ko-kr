---
title: NumericScale 및 Precision 속성 예제 (VC + +) 열을 | Microsoft Docs
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
- Precision property [ADOX], VC++ example
- NumericScale property [ADOX], VC++ example
ms.assetid: 69653366-ebd7-4ff6-a654-761772223b0c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71ecb8c981bafad0bcbc2c53b27140adad9281ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710378"
---
# <a name="numericscale-and-precision-properties-of-the-column-object-example-vc"></a>Column 개체의 NumericScale 및 Precision 속성 예제(VC++)
이 예제에서는 합니다 [NumericScale](../../../ado/reference/adox-api/numericscale-property-adox.md) 및 [정밀도](../../../ado/reference/adox-api/precision-property-adox.md) 의 속성을 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체. 이 코드에 대 한 해당 값을 표시 합니다 **Order Details** 목차를 *Northwind* 데이터베이스.  
  
```  
// BeginNumericScalePrecCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   HRESULT hr = S_OK;  
  
   // Define and initialize ADOX object pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
   _ColumnPtr m_pColumn = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
  
   // Declare string variables  
   _bstr_t strCnn("Provider='Microsoft.JET.OLEDB.4.0';Data Source='c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
  
      // Connect the catalog.  
      m_pCnn->Open (strCnn, "", "", NULL);  
  
      m_pCatalog->PutActiveConnection(variant_t((IDispatch *)m_pCnn));  
  
      // Retrieve the Order Details table  
      m_pTable = m_pCatalog->Tables->GetItem("Order Details");  
  
      // Display numeric scale and precision of small integer fields.  
      _variant_t vIndex;  
      for ( long lIndex = 0 ; lIndex < m_pTable->Columns->Count ; lIndex++ ) {  
         vIndex = lIndex ;  
         m_pColumn = m_pTable->Columns->GetItem(vIndex);  
         if (m_pColumn->Type == adSmallInt) {  
            cout << "Column: " << m_pColumn->GetName() << endl;  
            cout << "Numeric scale: " << (_bstr_t) m_pColumn->GetNumericScale() << endl;  
            cout << "Precision: " << m_pColumn->GetPrecision() << endl;  
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
      cout << "Error occured in NumericScalePrecX...." << endl;  
   }  
   ::CoUninitialize();  
}  
```
