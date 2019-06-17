---
title: Handler 속성 예제 (VC + +) | Microsoft Docs
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
- Handler property [ADO], VC++ example
ms.assetid: d046d89c-622b-48bc-9d30-f454c3e13595
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 75511a0a3dac6815bd2ceb9c35a0da18cd0d1782
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712499"
---
# <a name="handler-property-example-vc"></a>Handler 속성 예제(VC++)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 이 예제에서는 합니다 [RDS DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체 [처리기](../../../ado/reference/rds-api/handler-property-rds.md) 속성입니다. (참조 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md) 대 한 자세한 내용은 합니다.)  
  
 서버에 있는 매개 변수 파일 Msdfmap.ini에서 다음 섹션에서는 가정 합니다.  
  
```  
[connect AuthorDataBase]  
Access=ReadWrite  
Connect="DSN=Pubs"  
[sql AuthorById]  
SQL="SELECT * FROM Authors WHERE au_id = ?"  
```  
  
 코드는 다음과 같습니다. 에 할당 한 명령을 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성 일치는 ***AuthorById*** 식별자 및 Michael O'Leary 작성자에 대 한 행을 검색 합니다. 있지만 합니다 [Connect](../../../ado/reference/rds-api/connect-property-rds.md) Northwind 데이터 소스를 지정 하는 코드에서 속성을 Msdfmap.ini로 해당 데이터 원본을 덮어쓰게 됩니다 *연결* 섹션. 합니다 **DataControl** 개체 [레코드 집합](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) 속성은 할당 하 여 연결이 끊어진 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 코딩 편의 위해 전적으로 개체입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Handler 속성(RDS)](../../../ado/reference/rds-api/handler-property-rds.md)






















