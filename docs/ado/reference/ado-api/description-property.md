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
manager: craigg
ms.openlocfilehash: b9a97e1e63e3896cd451c68d6198baa991945e7a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704532"
---
# <a name="description-property"></a>Description 속성
에 대해 설명 합니다는 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **문자열** 오류에 대 한 설명을 포함 하는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **설명** 속성을 오류에 대 한 간단한 설명을 가져옵니다. 이 속성을 오류를 처리할 수 없거나 처리 하지 않으려는 사용자 경고를 표시 합니다. 문자열은 ADO 또는 공급자를 가져옵니다.  
  
 공급자는 ADO를 관련 오류 텍스트를 전달 하는 일을 담당 합니다. ADO 추가 [오류](../../../ado/reference/ado-api/error-object.md) 개체를 **오류** 컬렉션 각 공급자에 대 한 오류 또는 경고를 수신 합니다. 열거 된 **오류** 공급자를 전달 하는 오류를 추적 하는 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext, HelpFile 속성](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 속성 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 속성(ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)
