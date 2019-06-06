---
title: Read 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f4594e4b85ad66b1ab11a2966bc7a0d79815db09
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702977"
---
# <a name="read-method"></a>Read 메서드
이진 파일에서 지정 된 바이트 수를 읽고 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *NumBytes*  
 (선택 사항) A **긴** 파일에서 읽을 바이트 수를 지정 하는 값 또는 [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) 값 **adReadAll**, 기본값입니다.  
  
## <a name="return-value"></a>반환 값  
 합니다 **읽기** 메서드는 지정된 된 수의 바이트 또는에서 전체 스트림을 읽습니다를 **Stream** 개체 및 결과 데이터를 반환 합니다를 **Variant**합니다.  
  
## <a name="remarks"></a>Remarks  
 하는 경우 *NumBytes* 바이트의 수보다 큰에 그대로 합니다 **Stream**, 남은 바이트만 반환 됩니다. 지정 된 길이 맞게 데이터 읽기는 채워지지 않습니다 *NumBytes*합니다. 읽을 바이트가 없는 경우 null 값을 사용 하 여 변형을 반환 됩니다. **읽기** 이전 버전과 읽는 데 사용할 수 없습니다.  
  
> [!NOTE]
>  *NumBytes* 항상 바이트를 측정 합니다. 텍스트에 대 한 **Stream** 개체 ([유형](../../../ado/reference/ado-api/type-property-ado-stream.md) 됩니다 **adTypeText**)를 사용 하 여 [ReadText](../../../ado/reference/ado-api/readtext-method.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [ReadText 메서드](../../../ado/reference/ado-api/readtext-method.md)
