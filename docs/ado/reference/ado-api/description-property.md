---
title: "Description 속성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords: Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc23f481c709c0901eb6a2020b51629a16f659eb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
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
