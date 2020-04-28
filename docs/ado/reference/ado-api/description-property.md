---
title: Description 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48b3a6987e6c7b6c3754f5041d90d248520345ab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933083"
---
# <a name="description-property"></a>Description 속성
[오류](../../../ado/reference/ado-api/error-object.md) 개체에 대해 설명 합니다.  
  
## <a name="return-value"></a>Return Value  
 오류에 대 한 설명을 포함 하는 **문자열** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **설명** 속성을 사용 하 여 오류에 대 한 간단한 설명을 가져옵니다. 이 속성을 표시 하 여 사용자에 게 처리 하지 않거나 처리 하지 않을 오류를 사용자에 게 알립니다. 이 문자열은 ADO 또는 공급자에서 제공 됩니다.  
  
 공급자는 특정 오류 텍스트를 ADO에 전달 하는 일을 담당 합니다. ADO는 받은 각 공급자 오류 또는 경고에 대 한 [오류 개체를](../../../ado/reference/ado-api/error-object.md) **오류 컬렉션에 추가 합니다.** **오류** 컬렉션을 열거 하 여 공급자가 전달 하는 오류를 추적 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext, HelpFile 속성](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 속성 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 속성(ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)
