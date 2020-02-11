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
ms.openlocfilehash: d6c174d2e6a659a3b9da8f89816b5bdf90342416
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917368"
---
# <a name="readtext-method"></a>ReadText 메서드
텍스트 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체에서 지정 된 수의 문자를 읽습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *NumChars*  
 (선택 사항) 파일에서 읽을 문자 수 또는 [Streamreadenum](../../../ado/reference/ado-api/streamreadenum.md) 값을 지정 하는 **Long** 값입니다. 기본값은 **Adreadall**입니다.  
  
## <a name="return-value"></a>Return Value  
 **ReadText** 메서드는 **스트림** 개체에서 지정 된 수의 문자, 전체 줄 또는 전체 스트림을 읽고 결과 문자열을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 *NumChar* 가 스트림에 남아 있는 문자 수보다 많은 경우 남은 문자만 반환 됩니다. 읽은 문자열은 *NumChar*에 지정 된 길이와 일치 하도록 채워지지 않습니다. 읽을 문자가 없는 경우 값이 null 인 변형이 반환 됩니다. **ReadText** 를 사용 하 여 역방향으로 읽을 수 없습니다.  
  
> [!NOTE]
>  **ReadText** 메서드는 텍스트 스트림과 함께 사용 됩니다 ( **adTypeText**[형식](../../../ado/reference/ado-api/type-property-ado-stream.md) ). 이진 스트림의 경우 (**형식이** **adtypebinary**인 경우) [읽기](../../../ado/reference/ado-api/read-method.md)를 사용 합니다.  
  
 ADO (ActiveX Data Object) 스트림 개체의 **ReadText** 메서드를 통해 많은 양의 XML 데이터를 반환 하는 쿼리는 실행 하는 데 시간이 오래 걸릴 수 있습니다. ASP 페이지에서 호출 되는 COM + 구성 요소에서이 작업을 수행 하면 사용자의 세션이 시간 초과 될 수 있습니다. ADO는 스트림 개체 데이터를 UTF-8 인코딩에서 유니코드로 변환 합니다. 한 번에 많은 양의 데이터를 변환 하는 데 자주 사용 되는 메모리 재할당은 시간이 많이 소요 됩니다. 이 문제를 해결 하려면 ADO 명령 개체의 **ReadText** 메서드를 반복 해 서 호출 하 고 더 적은 수의 문자를 지정 합니다. 테스트에서 128K (131072)에 해당 하는 값이 최적 임을 보여 줍니다. 이 값이 줄어들면 응답 시간이 줄어듭니다. 자세한 내용은 Microsoft 기술 자료에서 기술 자료 문서 280067, "PRB: ADO 스트림 개체의 ReadText 메서드를 사용 하 여 SQL Server 2000에서 매우 큰 XML 문서 검색 속도가 느릴 수 있습니다 https://support.microsoft.com."를 참조 하십시오.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Read 메서드](../../../ado/reference/ado-api/read-method.md)
