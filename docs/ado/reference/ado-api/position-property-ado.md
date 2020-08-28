---
description: Position 속성(ADO)
title: Position 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 55ae275db06b8b0c73598977e78954bac0fd22be
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990064"
---
# <a name="position-property-ado"></a>Position 속성(ADO)
[스트림](./stream-object-ado.md) 개체 내의 현재 위치를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 스트림의 시작 부분에서 현재 위치의 오프셋 (바이트 수)을 지정 하는 **Long** 값을 설정 하거나 반환 합니다. 기본값은 0 이며 스트림의 첫 번째 바이트를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 현재 위치를 스트림 끝의 지점으로 이동할 수 있습니다. 스트림의 끝을 넘어 현재 위치를 지정 하면 **스트림** 개체의 [크기가](./size-property-ado-stream.md) 그에 따라 증가 됩니다. 이러한 방식으로 추가 된 새 바이트는 모두 null이 됩니다.  
  
> [!NOTE]
>  **Position** 은 항상 바이트를 측정 합니다. 멀티 바이트 문자 집합을 사용 하는 텍스트 스트림의 경우 위치를 문자 크기와 곱하여 문자 번호를 결정 합니다. 예를 들어 2 바이트 문자 집합의 경우 첫 번째 문자는 위치 0, 위치 2의 두 번째 문자, 위치 4의 세 번째 문자 등에 있습니다.  
  
> [!NOTE]
>  음수 값은 **스트림에서**현재 위치를 변경 하는 데 사용할 수 없습니다. **위치**에는 양수만 사용할 수 있습니다.  
  
> [!NOTE]
>  읽기 전용 **스트림** 개체의 경우 **Position** 이 **스트림의** **크기** 보다 큰 값으로 설정 된 경우 ADO에서 오류를 반환 하지 않습니다. 이는 **스트림**크기를 변경 하거나 **스트림** 내용을 변경 하지 않습니다. 그러나이 작업을 수행 하면 의미 없는 **위치**값이 발생 하므로이 작업을 수행 하지 말아야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Charset 속성(ADO)](./charset-property-ado.md)