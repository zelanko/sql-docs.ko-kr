---
title: Description 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 070ad4fc974a0471703060a511b51253acbf346d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="description-property"></a>Description 속성
에 대해 설명 된 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **문자열** 오류에 대 한 설명을 포함 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **설명** 속성을 오류에 대 한 간단한 설명을 가져옵니다. 한 오류를 처리할 수 없거나 처리 되지 않을 사용자에 게 알리도록 하려면이 속성을 표시 합니다. 문자열은 ADO 또는 공급자에서 가져옵니다.  
  
 공급자는 ado 관련 오류 텍스트를 전달 합니다. 추가 하는 ADO는 [오류](../../../ado/reference/ado-api/error-object.md) 개체는 **오류** 컬렉션 각 공급자에 대 한 오류 또는 경고 수신 합니다. 열거는 **오류** 공급자 전달 하는 오류를 추적 하는 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext, 도움말 파일 속성](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 속성 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 속성(ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)
