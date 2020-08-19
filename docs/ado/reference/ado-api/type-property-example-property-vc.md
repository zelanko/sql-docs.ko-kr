---
description: Type 속성 예제(속성)(VC++)
title: Type 속성 예제 (속성) (VC + +) | Microsoft Docs
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
- Type property [property] [ADO], VC++ example
ms.assetid: a4e23508-fbf3-4468-be55-212e7238802b
author: rothja
ms.author: jroth
ms.openlocfilehash: 00c0121f7418fa63280950191c445ff499dcb133
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441685"
---
# <a name="type-property-example-property-vc"></a>Type 속성 예제(속성)(VC++)
이 예제에서는 [Type](../../../ado/reference/ado-api/type-property-ado.md) 속성을 보여 줍니다. [속성](../../../ado/reference/ado-api/properties-collection-ado.md), [필드](../../../ado/reference/ado-api/fields-collection-ado.md)등과 같은 컬렉션의 이름 및 형식을 나열 하는 유틸리티의 모델입니다.  
  
 **속성** 컬렉션에 액세스 하기 위해 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 열 필요는 없습니다. 이는 **레코드 집합** 개체가 인스턴스화될 때 존재 합니다. 그러나 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient** 로 설정 하면 **레코드 집합** 개체의 **properties** 컬렉션에 몇 가지 동적 속성을 추가 하 여 예제를 좀 더 흥미로운 방법으로 만들 수 있습니다. 설명을 위해 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성을 명시적으로 사용 하 여 각 [속성](../../../ado/reference/ado-api/property-object-ado.md) 개체에 액세스 합니다.  
  
```  
// BeginTypePropertyCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void TypeX();  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   TypeX();  
   ::CoUninitialize();  
}  
  
void TypeX() {  
   // Define ADO object pointers, initialize pointers. These are in the ADODB:: namespace  
   _RecordsetPtr pRst = NULL;  
   PropertyPtr pProperty = NULL;  
  
   // Define Other Variables  
   _bstr_t strMsg;  
   _variant_t vIndex;  
   int intLineCnt = 0;     
  
   try {  
      TESTHR(pRst.CreateInstance (__uuidof(Recordset)));  
  
      // Set the Recordset Cursor Location  
      pRst->CursorLocation = adUseClient;  
  
      for (short iIndex = 0; iIndex <= (pRst->Properties->GetCount() - 1);iIndex++) {  
         vIndex = iIndex;  
         pProperty = pRst->Properties->GetItem(vIndex);  
  
         int propType = (int)pProperty->GetType();  
  
         switch(propType) {  
         case adBigInt:  
            strMsg = "adBigInt";  
            break;  
         case adBinary:  
            strMsg = "adBinary";  
            break;  
         case adBoolean:  
            strMsg = "adBoolean";  
            break;  
         case adBSTR:  
            strMsg = "adBSTR";  
            break;  
         case adChapter:  
            strMsg = "adChapter";  
            break;  
         case adChar:  
            strMsg = "adChar";  
            break;  
         case adCurrency:  
            strMsg = "adCurrency";  
            break;  
         case adDate:  
            strMsg = "adDate";  
            break;  
         case adDBDate:  
            strMsg = "adDBDate";  
            break;  
         case adDBTime:  
            strMsg = "adDBTime";  
            break;  
         case adDBTimeStamp:  
            strMsg = "adDBTimeStamp";  
            break;  
         case adDecimal:  
            strMsg = "adDecimal";  
            break;  
         case adDouble:  
            strMsg = "adDouble";  
            break;  
         case adEmpty:  
            strMsg = "adEmpty";  
            break;  
         case adError:  
            strMsg = "adError";  
            break;  
         case adFileTime:  
            strMsg = "adFileTime";  
            break;  
         case adGUID:  
            strMsg = "adGUID";  
            break;  
         case adIDispatch:  
            strMsg = "adIDispatch";  
            break;  
         case adInteger:  
            strMsg = "adInteger";  
            break;  
         case adIUnknown:  
            strMsg = "adIUnknown";  
            break;  
         case adLongVarBinary:  
            strMsg = "adLongVarBinary";  
            break;  
         case adLongVarChar:  
            strMsg = "adLongVarChar";  
            break;  
         case adLongVarWChar:  
            strMsg = "adLongVarWChar";  
            break;  
         case adNumeric:  
            strMsg = "adNumeric";  
            break;  
         case adPropVariant:  
            strMsg = "adPropVariant";  
            break;  
         case adSingle:  
            strMsg = "adSingle";  
            break;  
         case adSmallInt:  
            strMsg = "adSmallInt";  
            break;  
         case adTinyInt:  
            strMsg = "adTinyInt";  
            break;  
         case adUnsignedBigInt:  
            strMsg = "adUnsignedBigInt";  
            break;  
         case adUnsignedInt:  
            strMsg = "adUnsignedInt";  
            break;  
         case adUnsignedSmallInt:  
            strMsg = "adUnsignedSmallInt";  
            break;  
         case adUnsignedTinyInt:  
            strMsg = "adUnsignedTinyInt";  
            break;  
         case adUserDefined:  
            strMsg = "adUserDefined";  
            break;  
         case adVarBinary:  
            strMsg = "adVarBinary";  
            break;  
         case adVarChar:  
            strMsg = "adVarChar";  
            break;  
         case adVariant:  
            strMsg = "adVariant";  
            break;  
         case adVarNumeric:  
            strMsg = "adVarNumeric";  
            break;  
         case adVarWChar:  
            strMsg = "adVarWChar";  
            break;  
         case adWChar:  
            strMsg = "adWChar";  
            break;  
         default:  
            strMsg = "*UNKNOWN*";  
            break;  
         }  
  
         intLineCnt++;  
  
         printf ("Property %d : %s,Type = %s\n",iIndex, (LPCSTR)pProperty->GetName(),  
            (LPCSTR)strMsg);  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      PrintComError(e);  
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
 [Property 개체 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)   
 [Type 속성(ADO)](../../../ado/reference/ado-api/type-property-ado.md)
