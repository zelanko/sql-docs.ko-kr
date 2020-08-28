---
description: ConnectionString, ConnectionTimeout 및 State 속성 예제 (VC + +)
title: 연결 속성 예제 (VC + +) | Microsoft Docs
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
- ConnectionString property [ADO], VC++ example
- ConnectionTimeout property [ADO], VC++ example
- State property [ADO], VC++ example
ms.assetid: c6bd2609-4c49-462f-a1aa-7bee0f615adb
author: rothja
ms.author: jroth
ms.openlocfilehash: 99d285a4fdd8d3eabc1df1b353b650e17a4571c5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974784"
---
# <a name="connectionstring-connectiontimeout-and-state-properties-example-vc"></a>ConnectionString, ConnectionTimeout 및 State 속성 예제 (VC + +)
이 예에서는 [ConnectionString](./connectionstring-property-ado.md) 속성을 사용 하 여 [연결](./connection-object-ado.md) 개체를 여는 다양 한 방법을 보여 줍니다. 또한 [ConnectionTimeout](./connectiontimeout-property-ado.md) 속성을 사용 하 여 연결 제한 시간을 설정 하 고 [상태](./state-property-ado.md) 속성을 사용 하 여 연결 상태를 확인 합니다. GetState 함수는이 프로시저를 실행 하는 데 필요 합니다.  
  
> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.  
  
```  
// ConnectionStringSampleCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ConnectionStringX();  
_bstr_t GetState(int intState);   
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return 0;  
  
   ConnectionStringX();  
   ::CoUninitialize();  
}  
  
void ConnectionStringX() {  
   // Define Connection object pointers.  Initialize pointers on define.  These are in the ADODB::  namespace  
   _ConnectionPtr pConnection1 = NULL;  
   _ConnectionPtr pConnection2 = NULL;  
   _ConnectionPtr pConnection3 = NULL;  
   _ConnectionPtr pConnection4 = NULL;  
  
   // Define Other Variables  
   HRESULT hr = S_OK;  
  
   try {  
      // Open a connection using OLE DB syntax.  
      TESTHR(pConnection1.CreateInstance(__uuidof(Connection)));  
      pConnection1->ConnectionString = "Provider='sqloledb';Data Source='(local)';"  
         "Initial Catalog='Pubs';Integrated Security='SSPI';";  
      pConnection1->ConnectionTimeout = 30;  
      pConnection1->Open("", "", "",adConnectUnspecified);  
      printf("cnn1 state: %s\n", (LPCTSTR)GetState(pConnection1->State));  
  
      // Open a connection using a DSN and ODBC tags.  
      // It is assumed that you have create DSN 'DataPubs' with a user name as   
      // 'MyUserId' and password as 'MyPassword'.  
      TESTHR(pConnection2.CreateInstance(__uuidof(Connection)));  
      pConnection2->ConnectionString = "DSN=DataPubs;UID=MyUserId;PWD=MyPassword;";  
      pConnection2->Open("", "", "", adConnectUnspecified);  
      printf("cnn2 state: %s\n", (LPCTSTR)GetState(pConnection2->State));  
  
      // Open a connection using a DSN and OLE DB tags.  
      TESTHR(pConnection3.CreateInstance(__uuidof(Connection)));  
      pConnection3->ConnectionString = "Data Source=DataPubs;";  
      pConnection3->Open("", "", "", adConnectUnspecified);  
      printf("cnn3 state: %s\n", (LPCTSTR)GetState(pConnection3->State));  
  
      // Open a connection using a DSN and individual arguments instead of a connection string.  
      // It is assumed that you have create DSN 'DataPubs' with a user name as   
      // 'MyUserId' and password as 'MyPassword'.  
      TESTHR(pConnection4.CreateInstance(__uuidof(Connection)));  
      pConnection4->Open("DataPubs", "MyUserId", "MyPassword", adConnectUnspecified);  
      printf("cnn4 state: %s\n", (LPCTSTR)GetState(pConnection4->State));  
   }  
   catch(_com_error &e) {  
      // Notify user of any errors.  Pass a connection pointer accessed from the Connection.  
      PrintProviderError(pConnection1);  
      if (pConnection2)  
         PrintProviderError(pConnection2);  
  
      if (pConnection3)  
         PrintProviderError(pConnection3);  
  
      if (pConnection4)  
         PrintProviderError(pConnection4);  
  
      PrintComError(e);  
   }  
  
   // Cleanup objects before exit.  
   if (pConnection1)  
      if (pConnection1->State == adStateOpen)  
         pConnection1->Close();  
  
   if (pConnection2)  
      if (pConnection2->State == adStateOpen)  
         pConnection2->Close();  
  
   if (pConnection3)  
      if (pConnection3->State == adStateOpen)  
         pConnection3->Close();  
  
   if (pConnection4)  
      if (pConnection4->State == adStateOpen)  
         pConnection4->Close();  
}  
  
_bstr_t GetState(int intState) {  
   _bstr_t strState;   
   switch(intState) {  
   case adStateClosed:  
      strState = "adStateClosed";  
      break;  
   case adStateOpen:  
      strState = "adStateOpen";  
      break;  
   default:  
      ;  
   }  
   return strState;  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr  pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("Error number: %x\t%s\n", pErr->Number, (LPCSTR)pErr->Description);  
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
 [Connection 개체 (ADO)](./connection-object-ado.md)   
 [ConnectionString 속성 (ADO)](./connectionstring-property-ado.md)   
 [ConnectionTimeout 속성 (ADO)](./connectiontimeout-property-ado.md)   
 [State 속성(ADO)](./state-property-ado.md)