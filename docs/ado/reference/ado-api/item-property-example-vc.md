---
title: 항목 속성 예제 (VC + +) | Microsoft Docs
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
- Item property [ADO], VC++ example
ms.assetid: 05ae3f5a-a0c1-459d-aa7d-ed7f3b2ecd60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b228ad46c89766475e8a74e26a0aaf389130acd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864435"
---
# <a name="item-property-example-vc"></a>Item 속성 예제(VC++)
이 예제에서는 하는 방법을 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성 컬렉션의 멤버에 액세스 합니다. 예제 열립니다는 ***작성자*** 목차 합니다 ***Pubs*** 매개 변수가 있는 명령 사용 하 여 데이터베이스입니다.  
  
 액세스 하는 데이터베이스에 대해 실행 한 명령 매개 변수를 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체의 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 인덱스 및 이름을 사용 하 여 컬렉션입니다. 그런 다음 반환 된 필드 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) 해당 개체에서 액세스 하는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 인덱스 및 이름을 사용 하 여 컬렉션입니다.  
  
```  
// BeginItemCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ItemX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   ItemX();  
   ::CoUninitialize();  
}  
  
void ItemX() {  
   HRESULT hr = S_OK;  
  
   // Define ADO object pointers.  Initialize pointers on define.  These are in the ADODB::  namespace.  
   _ConnectionPtr pConnection = NULL;  
   _RecordsetPtr pRst = NULL;  
   _CommandPtr pCmd = NULL;  
   _ParameterPtr pPrm = NULL;  
   FieldPtr pFld = NULL;  
  
   // Other Variables.  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
   _variant_t Column[9];  
   _variant_t vIndex;  
  
   try {  
      // Open connection.  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      TESTHR(pRst.CreateInstance(__uuidof(Recordset)));  
      TESTHR(pCmd.CreateInstance(__uuidof(Command)));  
  
      // Set the array with the authors table field (column) names  
      Column[0] = "au_id";  
      Column[1] = "au_lname";  
      Column[2] = "au_fname";  
      Column[3] = "phone";  
      Column[4] = "address";  
      Column[5] = "city";  
      Column[6] = "state";  
      Column[7] = "zip";  
      Column[8] = "contract";  
  
      _bstr_t strText("SELECT * FROM authors WHERE state = ?");  
      pCmd->CommandText = strText;  
  
      pPrm = pCmd->CreateParameter("ItemXparm", adChar, adParamInput, 2, "CA");  
      pCmd->Parameters->Append(pPrm);  
  
      pConnection->Open(strCnn, "", "", adConnectUnspecified);  
      pCmd->ActiveConnection = pConnection;  
  
      // Connection and CommandType are omitted because a Command object is provided.  
      _variant_t Conn;  
      Conn.vt = VT_ERROR;  
      Conn.scode = DISP_E_PARAMNOTFOUND;  
  
      pRst->Open((_variant_t((IDispatch *) pCmd)), Conn, adOpenStatic, adLockReadOnly, -1);  
  
      printf("The Parameters collection accessed by index...\n");  
  
      vIndex = (short) 0;  
      pPrm = pCmd->Parameters->GetItem(&vIndex);  
      printf("Parameter name = '%s', value = '%s'\n",  
         (LPCSTR)pPrm->Name, (LPSTR)(_bstr_t)pPrm->Value);  
  
      printf("\nThe Parameters collection accessed by name...\n");  
      pPrm = pCmd->Parameters->Item["ItemXparm"];  
      printf("Parameter name = '%s', value = '%s'\n",  
         (LPCSTR)pPrm->Name, (LPSTR)(_bstr_t)pPrm->Value);  
  
      printf("\nThe Fields collection accessed by index...\n");  
      pRst->MoveFirst();  
      long limit = 0;  
      limit = ((pRst->Fields->Count) - 1);  
      int intLineCnt = 8;   
      for (short iIndex = 0 ; iIndex <= limit ; iIndex++) {  
         vIndex = iIndex;  
  
         pFld = pRst->Fields->GetItem(&vIndex);  
         printf("Field %d : Name =  '%s', ", iIndex, (LPCSTR)pFld->GetName());  
         _variant_t FldVal = pFld->GetValue();    
  
         // Because Value is the default property of a Property object, the use   
         // of the actual keyword here is optional.  
         switch(FldVal.vt) {  
         case (VT_BOOL):  
            if (FldVal.boolVal)  
               printf("Value = 'True'");  
            else  
               printf("Value = 'False'");  
            printf("\n");  
            break;  
         case (VT_BSTR):  
            printf("Value = '%s'",  
               (LPCSTR)(_bstr_t)FldVal.bstrVal);  
            printf("\n");  
            break;  
         case (VT_I4):  
            printf("Value = '%s'",(LPCSTR)FldVal.iVal);  
            printf("\n");  
            break;  
         case (VT_EMPTY):  
            printf("Value = '%s'",(LPCSTR)FldVal.lVal);  
            printf("\n");  
            break;  
         default:  
            break;  
         }  
      }  
  
      printf("\nThe Fields collection accessed by name...\n");  
      pRst->MoveFirst();  
  
      for (int iIndex = 0; iIndex <= 8 ; iIndex++) {  
         intLineCnt++;  
  
         pFld = pRst->Fields->GetItem(Column[iIndex]);  
         printf("Field name = '%s', ", (LPCSTR)pFld->GetName());  
         _variant_t FldVal = pFld->GetValue();  
  
         // Because Value is the default property of a Property object,  
         // the use of the actual keyword here is optional.  
         switch(FldVal.vt) {  
         case (VT_BOOL):  
            if (FldVal.boolVal)  
               printf("Value = 'True'");  
            else  
               printf("Value = 'False'");  
            printf("\n");  
            break;  
         case (VT_BSTR):  
            printf("Value = '%s'",  
               (LPCSTR)(_bstr_t)FldVal.bstrVal);  
            printf("\n");  
            break;  
         case (VT_I4):  
            printf("Value = '%s'", (LPCSTR)FldVal.iVal);  
            printf("\n");  
            break;  
         case (VT_EMPTY):  
            printf("Value = '%s'", (LPCSTR)FldVal.lVal);  
            printf("\n");  
            break;  
         default:  
            break;  
         }  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      // Pass a connection pointer accessed from the Recordset.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   // Clean up objects before exit.  
   if (pRst)  
      if (pRst->State == adStateOpen)  
         pRst->Close();  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for (long i = 0 ; i < nCount ; i++) {  
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
 [명령 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [필드 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Item 속성 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
