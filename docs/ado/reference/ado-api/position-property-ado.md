---
title: Position 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7b777179ad83250d9707f7717b5833bbbff4fec7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703406"
---
# <a name="position-property-ado"></a>Position 속성(ADO)
내 현재 위치를 나타내는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **긴** 스트림의 현재 위치부터에서의 바이트 수에서 오프셋을 지정 하는 값입니다. 기본값은 스트림의 첫 번째 바이트를 나타내는 0입니다.  
  
## <a name="remarks"></a>Remarks  
 현재 위치가 스트림의 맨 끝 뒤 지점으로 이동할 수 있습니다. 스트림의 끝을 넘어서 현재 위치를 지정 하는 경우는 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 의 합니다 **Stream** 개체를 적절 하 게 증가 합니다. 이러한 방식으로 추가 된 새 바이트 null이 됩니다.  
  
> [!NOTE]
>  **위치** 항상 바이트를 측정 합니다. 텍스트 스트림에서 멀티 바이트 문자 집합을 사용 하는 문자 수를 확인 하려면 문자 크기에 따라 위치를 곱하십시오. 예를 들어, 2 바이트 문자 집합에 대 한 첫 번째 문자는 위치 0, 2, 세 번째 문자 위치에 있는 두 번째 문자 위치 4에 있습니다.  
  
> [!NOTE]
>  현재 위치를 변경 하려면 음수 값을 사용할 수 없습니다는 **Stream**합니다. 양의 정수만 사용할 수 있습니다 **위치**합니다.  
  
> [!NOTE]
>  에 대 한 읽기 전용 **Stream** 개체, 경우 ADO 오류를 반환 하지 것입니다 **위치** 보다 큰 값으로 설정 되는 **크기** 의 합니다 **Stream**합니다. 크기 변경 되지 않습니다 합니다 **Stream**, alter 또는 합니다 **Stream** 어떤 방식으로든에서 콘텐츠. 그러나이 작업을 수행 하므로 피해 야 그 결과 의미가 **위치**값입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Charset 속성(ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
