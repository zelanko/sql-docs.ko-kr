---
description: Visual C++ 확장 예제
title: Visual C++ 확장 예제 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions example
ms.assetid: 9739c278-582c-402b-a158-7f68a1b2c293
author: rothja
ms.author: jroth
ms.openlocfilehash: 06e7ca7204d673ac5888962f3d4f5095e9fe5a9d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453945"
---
# <a name="visual-c-extensions-example"></a>Visual C++ 확장 예제
이 프로그램은 필드에서 값을 검색 하 고 C/c + + 변수로 변환 하는 방법을 보여 줍니다.  
  
 또한이 예제에서는 `QueryInterface` **IADORecordBinding** 인터페이스에 대 한 호출 및 참조 계산에 대 한 COM 관련 세부 정보를 자동으로 처리 하는 "스마트 포인터"를 활용 합니다.  
  
 스마트 포인터가 없으면 다음 코드를 사용할 수 있습니다.  
  
```cpp
IADORecordBinding   *picRs = NULL;  
...  
TESTHR(pRs->QueryInterface(  
          __uuidof(IADORecordBinding), (LPVOID*)&picRs));  
...  
if (picRs) picRs->Release();  
```  
  
 스마트 포인터를 사용 하면 `IADORecordBindingPtr` 다음 문을 사용 하 여 인터페이스에서 형식을 파생 시킬 수 있습니다 `IADORecordBinding` .  
  
```cpp
_COM_SMARTPTR_TYPEDEF(IADORecordBinding, __uuidof(IADORecordBinding));  
```  
  
 다음과 같이 포인터를 인스턴스화합니다.  
  
```cpp
IADORecordBindingPtr picRs(pRs);  
```  
  
 Visual C++ 확장은 **레코드 집합** 개체에 의해 구현 되기 때문에 스마트 포인터에 대 한 생성자는 `picRs` _ `RecordsetPtr` 포인터를 사용 `pRs` 합니다. 생성자는를 호출 하 여 `QueryInterface` `pRs` 인터페이스를 찾습니다 `IADORecordBinding` .  
  
```cpp
// Visual_Cpp_Extensions_Example.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <icrsint.h>  
_COM_SMARTPTR_TYPEDEF(IADORecordBinding, __uuidof(IADORecordBinding));  
  
inline void TESTHR(HRESULT _hr) { if FAILED(_hr) _com_issue_error(_hr); }  
  
class CCustomRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CCustomRs)  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_ch_fname, sizeof(m_ch_fname), m_ul_fnameStatus, false)  
      ADO_VARIABLE_LENGTH_ENTRY2(4, adVarChar, m_ch_lname, sizeof(m_ch_lname), m_ul_lnameStatus, false)  
   END_ADO_BINDING()  
  
public:  
   CHAR m_ch_fname[22];  
   CHAR m_ch_lname[32];  
   ULONG m_ul_fnameStatus;  
   ULONG m_ul_lnameStatus;  
};  
  
int main() {  
   ::CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      CCustomRs rs;  
      IADORecordBindingPtr picRs(pRs);  
  
      pRs->Open(L"SELECT * FROM Employee ORDER BY lname", L"dsn=DataPubs;Trusted_Connection=yes;", adOpenStatic, adLockOptimistic, adCmdText);  
  
      TESTHR(picRs->BindToRecordset(&rs));  
  
      while (!pRs->EndOfFile) {  
         // Process data in the CCustomRs C++ instance variables.  
         printf("Name = %s %s\n",  
            (rs.m_ul_fnameStatus == adFldOK ? rs.m_ch_fname: "<Error>"),   
            (rs.m_ul_lnameStatus == adFldOK ? rs.m_ch_lname: "<Error>") );  
  
         // Move to the next row of the Recordset.   Fields in the new row will   
         // automatically be placed in the CCustomRs C++ instance variables.  
  
         pRs->MoveNext();  
      }  
   }  
   catch (_com_error &e ) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Meaning = %s\n", e.ErrorMessage());  
      printf("Source = %s\n", (LPCSTR) e.Source());  
      printf("Description = %s\n", (LPCSTR) e.Description());  
   }  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual C++ 확장 사용](../../../ado/guide/appendixes/using-visual-c-extensions.md)   
 [Visual C++ 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)
