---
title: CopyTo 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25d57116e1fa24658d62a0c9083e00a3e320d2a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933379"
---
# <a name="copyto-method-ado"></a>CopyTo 메서드(ADO)
지정한 개수의 문자 또는 바이트 복사 (에 따라 [형식](../../../ado/reference/ado-api/type-property-ado-stream.md))에 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 간 **Stream** 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DestStream*  
 개방적이 고에 대 한 참조를 포함 하는 개체 변수 값 **Stream** 개체입니다. 현재 **Stream** 대상에 복사 됩니다 **Stream** 에 지정 된 *DestStream*합니다. 대상 **Stream** 이미 열려 있어야 합니다. 그렇지 않은 경우 런타임 오류가 발생 합니다.  
  
> [!NOTE]
>  합니다 *DestStream* 매개 변수에서의 프록시 되지 않을 수 있습니다 **Stream** 개인 인터페이스에 대 한 액세스에 필요 하기 때문에 개체를 **Stream** 원격으로 실행할 수 없는 개체는 클라이언트입니다.  
  
 *NumChars*  
 (선택 사항) **정수** 바이트 또는 원본의 현재 위치에서 복사할 문자 수를 지정 하는 값 **Stream** 대상으로 **Stream**합니다. 기본값은-1로, 모든 문자 또는 바이트를 현재 위치에서 복사 되도록 지정 [EOS](../../../ado/reference/ado-api/eos-property.md)합니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 지정한 수의 문자 또는 지정 된 현재 위치에서 시작 하는 바이트를 복사 합니다 [위치](../../../ado/reference/ado-api/position-property-ado.md) 속성입니다. 지정된 된 수까지 바이트 수를 사용할 수 있는 보다 크면 **EOS**, 다음만 문자 또는 바이트를 현재 위치의 **EOS** 복사 됩니다. 경우 값 *NumChars* -1 이거나 생략 하면 모든 문자 또는 현재 위치에서 시작 하는 바이트 복사 됩니다.  
  
 기존 경우 문자 또는 대상 스트림에 바이트를 복사 끝나는 지점 이후의 모든 내용이 그대로 남아 있고 잘리지 않습니다. **위치** 은 바로 다음의 마지막 바이트가 복사 바이트입니다. 이러한 바이트를 잘라내려면 원한다 면 호출 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)합니다.  
  
 **CopyTo** 대상으로 복사 하려면 데이터를 사용 해야 **Stream** 원본으로 동일한 형식의 **Stream** (해당 **형식** 속성 설정이 모두 **adTypeText** 또는 둘 다 **adTypeBinary**). 텍스트에 대 한 **Stream** 개체를 변경할 수 있습니다 합니다 [Charset](../../../ado/reference/ado-api/charset-property-ado.md) 대상의 속성 설정을 **Stream** 한 문자 집합을 다른 변환 하 합니다. 또한 텍스트 **Stream** 이진 개체를 성공적으로 복사할 수 있습니다 **Stream** 개체가 아니라 이진 **Stream** 개체를 텍스트로 복사할 수 없습니다 **Stream**  개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
