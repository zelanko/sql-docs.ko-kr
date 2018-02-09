---
title: "ReadText 메서드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e26f365d2b25bab878f0a8b9a321240d7c8ee347
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="readtext-method"></a>ReadText 메서드
지정한 텍스트의 문자 수를 읽습니다 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *NumChars*  
 (선택 사항) A **긴** 파일에서 읽을 문자 수를 지정 하는 값 또는 [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) 값입니다. 기본값은 **adReadAll**합니다.  
  
## <a name="return-value"></a>반환 값  
 **ReadText** 메서드는 지정된 된 수의 문자, 전체 행 또는에서 전체 스트림을 읽습니다는 **스트림** 개체를 결과 문자열을 반환 합니다.  
  
## <a name="remarks"></a>주의  
 경우 *NumChar* 스트림에 남아 보다 많은 수의 문자, 나머지 문자만 반환 됩니다. 로 지정 된 길이 일치 하도록 읽기 문자열은 채워지지 *NumChar*합니다. 왼쪽에서 읽을 문자가 더 인 경우 값이 null 인 variant 반환 됩니다. **ReadText** 뒤로 읽는 데 사용할 수 없습니다.  
  
> [!NOTE]
>  **ReadText** 메서드 텍스트 스트림 함께 사용 됩니다 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 은 **adTypeText**). 이진 스트림에 대 한 (**형식** 은 **adTypeBinary**)를 사용 하 여 [읽기](../../../ado/reference/ado-api/read-method.md)합니다.  
  
 대량의 XML 데이터를 통해 반환 되 고 발생 하는 쿼리는 **ReadText** 에서 호출 되는 COM + 구성 요소에서 수행 하는 경우 데이터 개체 ADO (ActiveX) 스트림 개체의 메서드를 상당; 실행 하는 시간이 걸릴 수 있습니다는 ASP 페이지에서 사용자의 세션 시간 초과 될 수 있습니다. ADO; 유니코드 인코딩을 u t F-8에서 스트림 개체 데이터를 변환 합니다. 이러한 많은 양의 데이터를 한 번에 변환에 관련 된 빈번한 메모리 재할당은 매우 빠릅니다. 를 해결 하려면 확인 반복된 하 여 호출 된 **ReadText** 의 ADO 명령 개체에 메서드와 문자 수를 적게 지정 합니다. 테스트 값 128k (131,072)에 해당 하는 최적의 방법 표시 했습니다. 응답 시간에는이 값은 감소 하는 대로 감소 합니다. 자세한 내용은 280067, 기술 자료 문서를 참조 하십시오. "PRB: ADO 스트림 개체의 ReadText 방법을 사용 하 여 SQL Server 2000에서에서 매우 큰 XML 문서 검색 속도가 느려질 수 있습니다", http://support.microsoft.com에서 Microsoft 기술 자료에서 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Read 메서드](../../../ado/reference/ado-api/read-method.md)
