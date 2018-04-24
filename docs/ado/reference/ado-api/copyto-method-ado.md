---
title: CopyTo 메서드 (ADO) | Microsoft Docs
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
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3164fbdffe9bad363a09f6ff7accf8cf6d55d751
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="copyto-method-ado"></a>CopyTo 메서드 (ADO)
지정한 개수의 문자 또는 바이트 복사 (에 따라 [형식](../../../ado/reference/ado-api/type-property-ado-stream.md))에 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 다른 **스트림** 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DestStream*  
 열린에 대 한 참조를 포함 하는 개체 변수 값 **스트림** 개체입니다. 현재 **스트림** 대상에 복사 **스트림** 에 지정 된 *DestStream*합니다. 대상 **스트림** 이미 열려 있어야 합니다. 그렇지 않은 경우 런타임 오류가 발생 합니다.  
  
> [!NOTE]
>  *DestStream* 매개 변수에서의 프록시 되지 않을 수 있습니다 **스트림** 개인 인터페이스에 대 한 액세스에 필요 하기 때문에 개체는 **스트림** 를 원격으로 연결할 수 없는 개체는 클라이언트입니다.  
  
 *NumChars*  
 (선택 사항) **정수** 소스에서 현재 위치에서 복사 될 문자 또는 바이트 수를 지정 하는 값 **스트림** 대상 **스트림**합니다. 기본값은-1로, 모든 문자 또는 바이트를 현재 위치에서 복사 되도록 지정 [EOS](../../../ado/reference/ado-api/eos-property.md)합니다.  
  
## <a name="remarks"></a>주의  
 이 메서드는 지정한 수의 문자 또는 지정 된 현재 위치에서 시작 하 여 바이트 복사는 [위치](../../../ado/reference/ado-api/position-property-ado.md) 속성입니다. 지정된 된 숫자 바이트까지 사용할 수 있는 수보다 큰 경우 **EOS**, 다음만 문자 또는 바이트를 현재 위치에서 **EOS** 복사 됩니다. 하는 경우의 값 *NumChars* 1 이거나 생략 하면 모든 문자 또는 현재 위치에서 시작 하는 바이트 복사 됩니다.  
  
 기존 문자 또는 대상 스트림은 바이트, 복사가 종료 되는 지점 이후의 모든 내용이 그대로 유지 하 고 잘리지 않습니다. **위치** 은 바이트 바로 다음의 마지막 바이트가 복사 합니다. 이러한 접두사 바이트 truncate 하려면 호출 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)합니다.  
  
 **CopyTo** 데이터를 복사 하는 대상으로 쓰일 수 **스트림** 소스로 같은 유형의 **스트림** (자신의 **형식** 속성 설정은 모두 **adTypeText** 또는 둘 다 **adTypeBinary**). 텍스트에 대 한 **스트림** 개체를 변경할 수는 [Charset](../../../ado/reference/ado-api/charset-property-ado.md) 대상의 속성 설정을 **스트림** 한 문자 집합을 다른 변환 하 합니다. 또한 텍스트 **스트림** 이진 파일에 개체를 성공적으로 복사 하려면 **스트림** 개체가 아니라 이진 **스트림** 텍스트에 개체를 복사할 수 없습니다 **스트림**  개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
