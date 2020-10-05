---
description: Handler 속성 예제(VC++)
title: Handler 속성 예제 (VC + +) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Handler property [ADO], VC++ example
ms.assetid: d046d89c-622b-48bc-9d30-f454c3e13595
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f8815ce6d607de39861f56bdcecca6c37e9dcc6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722163"
---
# <a name="handler-property-example-vc"></a>Handler 속성 예제(VC++)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
 이 예제에서는 [RDS DataControl](./datacontrol-object-rds.md) 개체 [처리기](./handler-property-rds.md) 속성을 보여 줍니다. 자세한 내용은 [DataFactory 사용자 지정](../../guide/remote-data-service/datafactory-customization.md) 을 참조 하세요.  
  
 서버에 있는 Msdfmap.ini 매개 변수 파일에서 다음 섹션을 가정 합니다.  
  
```  
[connect AuthorDataBase]  
Access=ReadWrite  
Connect="DSN=Pubs"  
[sql AuthorById]  
SQL="SELECT * FROM Authors WHERE au_id = ?"  
```  
  
 코드는 다음과 같습니다. [SQL](./sql-property.md) 속성에 할당 되는 명령은 ***AuthorById*** 식별자와 일치 하 고 author Michael O'Leary에 대 한 행을 검색 합니다. 코드의 [connect](./connect-property-rds.md) 속성이 Northwind 데이터 원본을 지정 하는 경우에도 해당 데이터 원본은 Msdfmap.ini *연결* 섹션에 의해 덮어쓰여집니다. **DataControl** 개체 [레코드 집합](./recordset-sourcerecordset-properties-rds.md) 속성은 코딩 편의를 위해 연결 되지 않은 [레코드 집합](../ado-api/recordset-object-ado.md) 개체에만 할당 됩니다.  
  
```  
// BeginHandlerCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
#import "msadco.dll"  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void HandlerX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   HRESULT hr = S_OK;  
   hr = ::CoInitialize(NULL);  
   if (SUCCEEDED(hr)) {  
      HandlerX();  
      ::CoUninitialize();  
   }  
}  
  
void HandlerX() {  
   HRESULT  hr = S_OK;  
   // Define and initialize ADO object pointers, in the ADODB namespace.     
   _RecordsetPtr pRst = NULL;  
  
   // Define RDS object pointers.  
   RDS::IBindMgrPtr dc;  
  
   try {  
      TESTHR(hr = dc.CreateInstance(__uuidof(RDS::DataControl)));  
      dc->Handler = "MSDFMAP.Handler";  
      dc->ExecuteOptions = 1;  
      dc->FetchOptions = 1;  
      dc->Server = "https://MyServer";  
      dc->Connect = "Data Source=AuthorDatabase";  
      dc->SQL = "AuthorById('267-41-2394')";  
  
      // Retrieve the record.  
      dc->Refresh();  
  
      // Use another Recordset as a convenience.  
      pRst = dc->GetRecordset();  
      printf("Author is %s %s",   
         (LPSTR)(_bstr_t) pRst->Fields->GetItem("au_fname")->Value,   
         (LPSTR)(_bstr_t) pRst->Fields->GetItem("au_lname")->Value);  
      pRst->Close();  
  
   }  // End Try statement.  
   catch (_com_error &e) {  
      PrintProviderError(pRst->GetActiveConnection());  
      PrintComError(e);  
   }  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
   long nCount = 0;  
   long i = 0;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for ( i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
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
  
## <a name="see-also"></a>참고 항목  
 [DataControl 개체 (RDS)](./datacontrol-object-rds.md)   
 [Handler 속성(RDS)](./handler-property-rds.md)