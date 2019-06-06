---
title: ReadText 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e7f9a484ecb873a141f9b91a88c64f65ff25336
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712208"
---
# <a name="readtext-method"></a>ReadText 메서드
지정한 텍스트에서 문자 수를 읽습니다 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *NumChars*  
 (선택 사항) A **긴** 파일에서 읽을 문자 수를 지정 하는 값 또는 [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) 값입니다. 기본값은 **adReadAll**합니다.  
  
## <a name="return-value"></a>반환 값  
 합니다 **ReadText** 메서드는 지정 된 개수의 문자나 전체 줄을에서 전체 스트림을 읽습니다를 **Stream** 개체를 결과 문자열을 반환 합니다.  
  
## <a name="remarks"></a>Remarks  
 하는 경우 *NumChar* 보다 많은 수의 문자 스트림을에 그대로, 남아 있는 문자만 반환 됩니다. 지정 된 길이 맞게 문자열 읽기은 채워지지 *NumChar*합니다. 읽을 문자가 없는 경우 값이 null 인 변형 반환 됩니다. **ReadText** 이전 버전과 읽는 데 사용할 수 없습니다.  
  
> [!NOTE]
>  **ReadText** 메서드는 텍스트 스트림 사용 됩니다 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 는 **adTypeText**). 이진 스트림에 대 한 (**형식** 됩니다 **adTypeBinary**)를 사용 하 여 [읽기](../../../ado/reference/ado-api/read-method.md)합니다.  
  
 통해 반환 되는 XML 데이터의 양이 발생 하는 쿼리를 **ReadText** 에서 호출 되는 COM + 구성 요소에서 이렇게 하는 경우 데이터 개체 (ADO (ActiveX) Stream 개체의 메서드; 실행 시간이 많이 걸릴 수 있습니다는 ASP 페이지에서 사용자의 세션 시간 초과 될 수 있습니다. ADO에서 u t F-8 인코딩을 유니코드로; Stream 개체 데이터를 변환 합니다. 빈도가 높은 메모리 재할당 한 번에 이러한 많은 양의 데이터 변환에 관련 된 상당한 시간이 소요 됩니다. 를 해결 하려면에 대 한 반복된 호출을 확인 합니다 **ReadText** ADO 메서드의 개체, 명령 및 문자 수를 적게 지정 합니다. 테스트는 최적의 128k (131,072)에 해당 값을 설명 했습니다. 응답 시간이이 값은 감소 하는 대로 감소 합니다. 자세한 내용은 기술 자료 문서 280067를을 참조 하세요. "PRB: ADO 스트림 개체의 ReadText 메서드를 사용 하 여 SQL Server 2000에서 매우 큰 XML 문서를 검색 속도가 느릴 수"에서 Microsoft 기술 자료에서 https://support.microsoft.com합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Read 메서드](../../../ado/reference/ado-api/read-method.md)
