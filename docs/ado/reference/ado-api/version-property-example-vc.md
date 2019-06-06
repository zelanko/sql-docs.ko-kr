---
title: Version 속성 예제 (VC + +) | Microsoft Docs
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
- Version property [ADO], VC++ example
ms.assetid: 2440b6ff-2536-497c-a5f4-41db0cf1945e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e74633d19bf165b362995f587f9cf641baadb1d3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710089"
---
# <a name="version-property-example-vc"></a>Version 속성 예제(VC++)
이 예제에서는 합니다 [버전](../../../ado/reference/ado-api/version-property-ado.md) 의 속성을 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 현재 ADO 버전을 표시 하는 개체입니다. 또한 여러 동적 속성을 사용 하 여 보여 줍니다.  
  
-   현재 DBMS 이름과 버전입니다.  
  
-   OLE DB 버전입니다.  
  
-   공급자 이름 및 버전입니다.  
  
-   ODBC 버전입니다.  
  
-   ODBC 드라이버 이름과 버전입니다.  
  
> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 하거나 **Integrated Security = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.  
  
```  
// BeginVersionCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void VersionX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
    if (FAILED(::CoInitialize(NULL)))  
        return -1;  
  
    VersionX();  
  
    ::CoUninitialize();  
}  
  
void VersionX() {  
    HRESULT hr = S_OK;  
  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
    // Define ADO object pointers.  Initialize pointers on define.  
    // These are in the ADODB::  namespace.  
    _ConnectionPtr pConnection = NULL;  
  
    try {  
        // Open connection.  
        TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
        pConnection->Open (strCnn, "", "", adConnectUnspecified);  
  
        printf("ADO Version   : %s\n\n",(LPCSTR) pConnection->Version);  
        printf("DBMS Name   : %s\n\n",(LPCSTR) (_bstr_t)   
            pConnection->Properties->GetItem("DBMS Name")->Value);  
        printf("DBMS Version   : %s\n\n",(LPCSTR) (_bstr_t)  
            pConnection->Properties->GetItem("DBMS Version")->Value);  
        printf("OLE DB Version   : %s\n\n",(LPCSTR) (_bstr_t)   
            pConnection->Properties->GetItem("OLE DB Version")->Value);  
        printf("Provider Name   : %s\n\n",(LPCSTR) (_bstr_t)   
            pConnection->Properties->GetItem("Provider Name")->Value);  
        printf("Provider Version   : %s\n\n",(LPCSTR) (_bstr_t)   
            pConnection->Properties->GetItem("Provider Version")->Value);  
        printf("Driver Name   : %s\n\n",(LPCSTR) (_bstr_t)   
            pConnection->Properties->GetItem("Driver Name")->Value);  
        printf("Driver Version   : %s\n\n",(LPCSTR) (_bstr_t)   
            pConnection->Properties->GetItem("Driver Version")->Value);  
        printf("Driver ODBC Version   : %s\n\n",(LPCSTR) (_bstr_t)   
            pConnection->Properties->GetItem("Driver ODBC Version")->Value);  
  
    }  
  
    catch (_com_error &e) {  
        // Notify the user of errors if any.  
        PrintProviderError(pConnection);  
        PrintComError(e);  
    }  
  
    if (pConnection)  
        if (pConnection->State == adStateOpen)  
            pConnection->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
    // Print Provider Errors from Connection object.  
    // pErr is a record object in the Connection's Error collection.  
    ErrorPtr pErr = NULL;  
  
    if ( (pConnection->Errors->Count) > 0) {  
        long nCount = pConnection->Errors->Count;  
        // Collection ranges from 0 to nCount -1.  
        for ( long i = 0 ; i < nCount ; i++) {  
            pErr = pConnection->Errors->GetItem(i);  
            printf("Error number: %x\t%s\n", pErr->Number, (LPCSTR) pErr->Description);  
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
  
## <a name="see-also"></a>관련 항목  
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Version 속성(ADO)](../../../ado/reference/ado-api/version-property-ado.md)
