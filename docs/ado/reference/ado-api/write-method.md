---
title: Write 메서드 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 911a9dfb21c054dc95c54d9fb429d628d8e01fa4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764434"
---
# <a name="write-method"></a>Write 메서드
[스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체에 이진 데이터를 씁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>매개 변수  
 *버퍼*  
 쓸 바이트 배열을 포함 하는 **Variant** 입니다.  
  
## <a name="remarks"></a>설명  
 지정 된 바이트는 각 바이트 사이에 공백을 넣지 않고 **Stream** 개체에 기록 됩니다.  
  
 현재 [위치](../../../ado/reference/ado-api/position-property-ado.md) 는 쓴 데이터 다음의 바이트로 설정 됩니다. **Write** 메서드는 스트림의 나머지 데이터를 자르지 않습니다. 이러한 바이트를 잘라내는 경우 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)를 호출 합니다.  
  
 현재 [EOS](../../../ado/reference/ado-api/eos-property.md) 위치를 지나서 쓰는 경우 **스트림의** [크기가](../../../ado/reference/ado-api/size-property-ado-stream.md) 새 바이트를 포함 하도록 증가 하 고 **EOS** 가 **스트림의**새 마지막 바이트로 이동 합니다.  
  
> [!NOTE]
>  **Write** 메서드는 이진 스트림과 함께 사용 됩니다 ( **Adtypebinary**[형식](../../../ado/reference/ado-api/type-property-ado-stream.md) ). 텍스트 스트림의 경우 (**형식** 은 **adTypeText**) [WriteText](../../../ado/reference/ado-api/writetext-method.md)를 사용 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [WriteText 메서드](../../../ado/reference/ado-api/writetext-method.md)
