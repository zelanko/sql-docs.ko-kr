---
title: 메서드를 작성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 59a89db47036129e3c345d26ded57ecf4e26fc84
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710029"
---
# <a name="write-method"></a>Write 메서드
이진 데이터를 쓰는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Buffer*  
 A **Variant** 쓸 바이트의 배열을 포함 하는 합니다.  
  
## <a name="remarks"></a>Remarks  
 지정 된 바이트는 **Stream** 각 바이트 사이 공백 넣지 않고 개체입니다.  
  
 현재 [위치](../../../ado/reference/ado-api/position-property-ado.md) 바이트 기록된 된 데이터를 다음으로 설정 됩니다. 합니다 **쓰기** 메서드 스트림에서 데이터의 나머지 부분을 잘라내지 않습니다. 이러한 바이트를 잘라내려면 원한다 면 호출 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)합니다.  
  
 현재 이전 작성 하는 경우 [EOS](../../../ado/reference/ado-api/eos-property.md) 위치를 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 의 **Stream** 포함 된 새 바이트 증가 및 **EOS** 이동 새 마지막 바이트에는 **Stream**합니다.  
  
> [!NOTE]
>  합니다 **작성** 이진 스트림을 사용 하 여 메서드를 사용 하는 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 됩니다 **adTypeBinary**). 텍스트 스트림에 대 한 (**형식** 됩니다 **adTypeText**)를 사용 하 여 [WriteText](../../../ado/reference/ado-api/writetext-method.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [WriteText 메서드](../../../ado/reference/ado-api/writetext-method.md)
