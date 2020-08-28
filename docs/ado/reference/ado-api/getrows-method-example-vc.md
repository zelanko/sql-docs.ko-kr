---
description: GetRows 메서드 예제(VC++)
title: GetRows 메서드 예제 (VC + +) | Microsoft Docs
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
- Getrows method [ADO], VC++ example
ms.assetid: 08e5c5bf-f7de-4bf9-97a9-f214c128ad8c
author: rothja
ms.author: jroth
ms.openlocfilehash: 012d0bc96f50919b02e11329f4aebc5bb3ecb269
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990884"
---
# <a name="getrows-method-example-vc"></a>GetRows 메서드 예제(VC++)
이 예에서는 [GetRows](./getrows-method-ado.md) 메서드를 사용 하 여 [레코드 집합](./recordset-object-ado.md) 에서 지정 된 수의 행을 검색 하 고 결과 데이터로 배열을 채웁니다. **Getrows** 메서드는 [EOF](./bof-eof-properties-ado.md) 에 도달 했거나 **getrows** 에서 다른 사용자가 삭제 한 레코드를 검색 하려고 시도 하는 경우 두 경우에 원하는 수의 행 보다 작은 값을 반환 합니다. 함수는 두 번째 사례가 발생 하는 경우에만 **False** 를 반환 합니다. GetRowsOK 함수는이 프로시저를 실행 하는 데 필요 합니다.  
  
## <a name="example"></a>예제  
  
```  
// BeginGetRowsCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <stdio.h>  
#include <ole2.h>  
#include <conio.h>  
  
// Function Declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void GetRowsX();  
bool GetRowsOK(_RecordsetPtr pRstTemp, int intNumber, _variant_t& avarData);  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   GetRowsX();  
   ::CoUninitialize();  
}  
  
void GetRowsX() {  
   HRESULT hr = S_OK;  
  
   // Define string variables.  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers, initialize pointers on define.   
   // These are in the ADODB::  namespace.  
   _RecordsetPtr pRstEmployees = NULL;  
  
   try  {  
      // Open recordset with names and hire dates from employee table.  
      TESTHR(pRstEmployees.CreateInstance(__uuidof(Recordset)));  
  
      pRstEmployees->Open("SELECT fName, lName, hire_date "  
         "FROM Employee ORDER BY lName",strCnn, adOpenStatic, adLockReadOnly, adCmdText);  
  
      while (true) {   // continuous loop  
         int intLines = 0;  
  
         // Get user input for number of rows.  
         printf("Enter number of rows to retrieve (0 to exit): ");  
         int intRows;  
         scanf_s("%d", &intRows);  
  
         if (intRows <= 0)  
            break;  
  
         // If GetRowsOK is successful, print the results,  
         // noting if the end of the file was reached.  
         _variant_t avarRecords;  
  
         if (GetRowsOK(pRstEmployees, intRows, avarRecords)) {  
            long lUbound;  
            HRESULT hr = SafeArrayGetUBound(avarRecords.parray, 2, &lUbound);  
  
            if (hr == 0) {  
               if (intRows > lUbound + 1) {  
                  printf("\n(Not enough records in Recordset to retrieve %d rows)\n", intRows);  
               }  
            }  
            printf("%d record(s) found.\n", lUbound + 1);  
  
            // Print the retrieved data.  
            for (int intRecords = 0 ; intRecords < lUbound+1 ; intRecords++) {  
               long rgIndices[2];  
               rgIndices[0] = 0;   
               rgIndices[1] = intRecords;  
               _variant_t result;  
               result.vt = VT_BSTR;  
  
               hr = SafeArrayGetElement(avarRecords.parray, rgIndices, &result);  
  
               if (hr == 0)  
                  printf("%s ",(LPCSTR)(_bstr_t)result);  
  
               rgIndices[0] = 1;  
  
               hr = SafeArrayGetElement(avarRecords.parray, rgIndices, &result);  
  
               if (hr == 0)  
                  printf("%s, ",(LPCSTR)(_bstr_t)result);  
  
               rgIndices[0] = 2;  
  
               hr = SafeArrayGetElement(avarRecords.parray, rgIndices, &result);  
  
               if (hr == 0)  
                  printf("%s\n", (LPCSTR)(_bstr_t)result);  
  
               intLines ++;  
  
               if (intLines % 10 == 0) {  
                  printf("\nPress any key to continue...");  
                  _getch();  
                  intLines = 0;  
                  system("cls");  
               }  
            }  
            printf("\n");  
         }  
         else {  
            // Assume GetRows error caused by another user's data changes,   
            // use Requery to refresh the Recordset and start over.  
            printf("GetRows failed--retry?\n");  
            char chKey;  
            do {  
               chKey = _getch();  
            } while (toupper(chKey) != 'Y'  && toupper(chKey) != 'N');  
  
            if (toupper(chKey) == 'Y')  
               pRstEmployees->Requery(adOptionUnspecified);  
            else {  
               printf("GetRows failed!\n");  
               break;  
            }  
         }  
  
         // Because using GetRows leaves the current record pointer at the last record   
         // accessed, move the pointer back to the beginning of the Recordset before   
         // looping back for another search.  
         pRstEmployees->MoveFirst();  
      }  
   }    
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      // Pass a connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstEmployees->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
         case VT_BSTR:  
            PrintComError(e);  
            break;  
         case VT_DISPATCH:  
            PrintProviderError(vtConnect);  
            break;  
         default:  
            printf("Errors occured.");  
            break;  
      }  
   }  
  
   // Clean up objects before exit.  
   if (pRstEmployees)  
      if (pRstEmployees->State == adStateOpen)  
         pRstEmployees->Close();  
}  
  
bool GetRowsOK(_RecordsetPtr pRstTemp,int intNumber, _variant_t& avarData) {  
   // Store results of GetRows method in array.  
   avarData = pRstTemp->GetRows(intNumber);  
  
   // Return False only if fewer than the desired number of rows were returned,   
   // but not because the end of the Recordset was reached.  
   long lUbound;  
   HRESULT hr = SafeArrayGetUBound(avarData.parray, 2, &lUbound);     
   if (hr == 0) {  
      if ((intNumber > lUbound + 1) && (!(pRstTemp->EndOfFile)))  
         return false;  
      else  
         return true;     
   }  
   else  {  
      printf ("\nUnable to Get the Array's Upper Bound\n");  
      return false;  
   }  
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
         printf("\t Error number: %x\t%s", pErr->Number, (LPCSTR) pErr->Description);  
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
  
 입력  
  
```  
2  
0  
```  
  
## <a name="sample-output"></a>샘플 출력  
  
```  
2 record(s) found.  
Paolo Accorti, 8/27/1992  
Pedro Afonso, 12/24/1990  
```  
  
## <a name="see-also"></a>참고 항목  
 [BOF, EOF 속성 (ADO)](./bof-eof-properties-ado.md)   
 [GetRows 메서드 (ADO)](./getrows-method-ado.md)   
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)