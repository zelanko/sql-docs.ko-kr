---
title: Groups 및 Users Append, ChangePassword 메서드 예제 (VC + +) | Microsoft Docs
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
- ChangePassword method [ADOX], VC++ example
- Groups Append method [ADOX], VC++ example
- Append method [ADOX], VC++ example
- Users Append method [ADOX], VC++ example
ms.assetid: 7e7067d0-6405-4c09-bff3-b1c2f2d783e0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5c3a1e66be521a08ef94719cffff813206ce965e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706733"
---
# <a name="groups-and-users-append-changepassword-methods-example-vc"></a>Groups 및 Users Append, ChangePassword 메서드 예제(VC++)
이 예제에서는 [Append](../../../ado/reference/adox-api/append-method-adox-groups.md) 메서드의 [그룹](../../../ado/reference/adox-api/groups-collection-adox.md), 뿐만 [추가](../../../ado/reference/adox-api/append-method-adox-users.md) 메서드의 [사용자](../../../ado/reference/adox-api/users-collection-adox.md) 새 추가하여[그룹](../../../ado/reference/adox-api/group-object-adox.md) 및 새 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 시스템입니다. 새 **그룹** 에 추가 되는 **그룹** 새 컬렉션 **사용자**합니다. 따라서 새 **사용자** 에 추가 되는 **그룹**합니다. 또한 합니다 [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) 메서드를 지정 하는 합니다 **사용자** 암호.  
  
> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 하거나 **Integrated Security = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.  
  
```  
// BeginGroupCpp.cpp  
// compile with: /EHsc  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   HRESULT hr = S_OK;  
  
   // Define and initialize ADOX object pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _UserPtr m_pUserNew = NULL;  
   _UserPtr m_pUser = NULL;  
   _GroupPtr m_pGroup = NULL;  
  
   // Define String Variables.  
   _bstr_t strCnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = 'c:\\Northwind.mdb';jet oledb:system database='c:\\system.mdw'");  
  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      m_pCatalog->PutActiveConnection(strCnn);  
  
      // Create and append new group with a string.  
      m_pCatalog->Groups->Append("Accounting");  
  
      // Create and append new user with an object.  
      TESTHR(hr = m_pUserNew.CreateInstance(__uuidof(User)));  
      m_pUserNew->PutName("Pat Smith");  
      m_pUserNew->ChangePassword("", "Password1");  
      m_pCatalog->Users->Append(_variant_t((IDispatch *)m_pUserNew), "");  
  
      // Make the user Pat Smith a member of the Accounting group by creating and adding the  
      // appropriate Group object to the user's Groups collection. The same is accomplished if a User  
      // object representing Pat Smith is created and appended to the Accounting group Users collection  
      m_pUserNew->Groups->Append("Accounting");  
  
      // Enumerate all User objects in the catalog's Users collection.  
      long lUsrIndex;  
      long lGrpIndex;  
      _variant_t vIndex;  
      for ( lUsrIndex = 0 ; lUsrIndex < m_pCatalog->Users->Count ; lUsrIndex++ ) {  
         vIndex = lUsrIndex;  
         m_pUser = m_pCatalog->Users->GetItem(vIndex);  
         cout << "  " << m_pUser->Name << endl;  
         cout << "   Belongs to these groups:" << endl;  
  
         // Enumerate all Group objects in each User object's Groups collection.  
         if (m_pUser->Groups->Count != 0)  
            for ( lGrpIndex = 0 ; lGrpIndex < m_pUser->Groups->Count ; lGrpIndex++ ) {  
               vIndex = lGrpIndex;  
               m_pGroup = m_pUser->Groups->GetItem(vIndex);  
               cout << "     " << m_pGroup->Name << endl;  
            }  
         else  
            cout << "       [None]" << endl;  
      }  
  
      // Enumerate all Group objects in the default workspace's Groups collection.  
      for ( lGrpIndex = 0 ; lGrpIndex < m_pCatalog->Groups->Count ; lGrpIndex++ ) {  
         vIndex = lGrpIndex;  
         m_pGroup = m_pCatalog->Groups->GetItem(vIndex);  
         cout << "   " << m_pGroup->Name << endl;  
         cout << "    Has as its members:" << endl;  
  
         // Enumerate all User objects in each Group object's Users Collection.  
         if ( m_pGroup->Users->Count != 0)  
            for ( lUsrIndex = 0 ; lUsrIndex < m_pGroup->Users->Count ; lUsrIndex++ ) {  
               vIndex = lUsrIndex;  
               m_pUser = m_pGroup->Users->GetItem(vIndex);  
               cout << "    " << m_pUser->Name << endl;  
            }  
         else  
            cout << "      [None]" << endl;  
      }  
  
      // Delete new User and Group object because this is only a demonstration.  
      m_pCatalog->Users->Delete("Pat Smith");  
      m_pCatalog->Groups->Delete("Accounting");  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in include files...." << endl;  
   }  
  
   ::CoUninitialize();  
}  
```
