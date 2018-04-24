---
title: Write 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f05ef9a599711493c4efaa50d7f9ecbc3a078ac4
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="write-method"></a>Write 메서드
이진 데이터를 쓰는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Buffer*  
 A **Variant** 쓸 바이트의 배열을 포함 하는 합니다.  
  
## <a name="remarks"></a>주의  
 지정 된 바이트는 **스트림** 각 바이트 사이 공백 넣지 않고 개체입니다.  
  
 현재 [위치](../../../ado/reference/ado-api/position-property-ado.md) 바이트 기록된 된 데이터를 다음으로 설정 됩니다. **쓰기** 메서드 나머지 스트림에서 데이터를 잘라내지 않습니다. 이러한 접두사 바이트 truncate 하려면 호출 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)합니다.  
  
 현재 이전 작성 하는 경우 [EOS](../../../ado/reference/ado-api/eos-property.md) 위치는 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 의 **스트림** 포함 된 새 바이트 증가 시켜 및 **EOS** 이동 합니다 새 마지막 바이트 까지의 **스트림**합니다.  
  
> [!NOTE]
>  **쓰기** 메서드 이진 스트림 함께 사용 됩니다 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 은 **adTypeBinary**). 텍스트 스트림에 대 한 (**형식** 은 **adTypeText**)를 사용 하 여 [WriteText](../../../ado/reference/ado-api/writetext-method.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [WriteText 메서드](../../../ado/reference/ado-api/writetext-method.md)
