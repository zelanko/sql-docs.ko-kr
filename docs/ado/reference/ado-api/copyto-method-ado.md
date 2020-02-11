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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933379"
---
# <a name="copyto-method-ado"></a>CopyTo 메서드(ADO)
[스트림에](../../../ado/reference/ado-api/stream-object-ado.md) 따라 지정 된 문자 또는 바이트 수를 다른 **스트림** 개체에 복사 합니다. [](../../../ado/reference/ado-api/type-property-ado-stream.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DestStream*  
 열려 있는 **스트림** 개체에 대 한 참조를 포함 하는 개체 변수 값입니다. 현재 **스트림이** *deststream*에 의해 지정 된 대상 **스트림에** 복사 됩니다. 대상 **스트림이** 이미 열려 있어야 합니다. 그렇지 않으면 런타임 오류가 발생 합니다.  
  
> [!NOTE]
>  *Deststream* 매개 변수는 클라이언트에 원격으로 연결할 수 없는 **스트림** 개체의 전용 인터페이스에 대 한 액세스를 필요로 하기 때문에 **스트림** 개체의 프록시가 될 수 없습니다.  
  
 *NumChars*  
 (선택 사항) 소스 **스트림의** 현재 위치에서 대상 **스트림으로**복사할 바이트 또는 문자 수를 지정 하는 **정수** 값입니다. 기본값은-1입니다 .이 값은 모든 문자 또는 바이트가 현재 위치에서 [EOS](../../../ado/reference/ado-api/eos-property.md)로 복사 되도록 지정 합니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 [position](../../../ado/reference/ado-api/position-property-ado.md) 속성에 지정 된 현재 위치에서 시작 하 여 지정 된 수의 문자 또는 바이트를 복사 합니다. 지정 된 숫자가 **eos**까지 사용 가능한 바이트 수를 초과할 경우 현재 위치에서 **EOS** 까지의 문자나 바이트만 복사 됩니다. *NumChars* 의 값이-1 이거나 생략 된 경우 현재 위치에서 시작 하는 모든 문자 또는 바이트가 복사 됩니다.  
  
 대상 스트림에 기존 문자 또는 바이트가 있는 경우 복사가 끝난 지점을 벗어난 모든 콘텐츠가 잘리지 않습니다. **Position** 은 마지막으로 복사한 바이트 바로 다음 바이트가 됩니다. 이러한 바이트를 잘라내는 경우 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)를 호출 합니다.  
  
 **CopyTo** 는 원본 **스트림과** 동일한 형식의 대상 **스트림에** 데이터를 복사 하는 데 사용 해야 합니다. 해당 **Type** 속성 설정은 **adTypeText** 또는 둘 다 **adtypebinary**입니다. 텍스트 **스트림** 개체의 경우 한 문자 집합에서 다른 문자 집합으로 변환 하기 위해 대상 **스트림의** [Charset](../../../ado/reference/ado-api/charset-property-ado.md) 속성 설정을 변경할 수 있습니다. 또한 텍스트 **스트림** 개체는 이진 **스트림** 개체로 복사 될 수 있지만 이진 **스트림** 개체는 텍스트 **스트림** 개체에 복사할 수 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
