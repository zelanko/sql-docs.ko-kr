---
title: "Position 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76a3d94b97fa32e372cd6cc67367450d2f62530b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="position-property-ado"></a>Position 속성 (ADO)
내에서 현재 위치를 나타내기는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **긴** 스트림의 현재 위치부터에서의 바이트 수에 오프셋을 지정 하는 값입니다. 기본값은 스트림의 첫 번째 바이트를 나타내는 0입니다.  
  
## <a name="remarks"></a>주의  
 스트림의 끝 지점으로 현재 위치를 이동할 수 있습니다. 스트림의 끝을 넘어 현재 위치를 지정 하는 경우는 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 의 **스트림** 개체를 적절 하 게 증가 합니다. 이러한 방식으로 추가 된 새 바이트 null이 됩니다.  
  
> [!NOTE]
>  **위치** 항상 바이트를 측정 합니다. 멀티 바이트 문자 집합을 사용 하는 텍스트 스트림의 문자 크기가 아니라 문자 수를 확인 하 여 위치를 곱하십시오. 예를 들어 2 바이트 문자 집합에 대 한 첫 번째 문자에서 위치 4, 0, 2, 세 번째 문자 위치에 있는 두 번째 문자 위치에는.  
  
> [!NOTE]
>  현재 위치를 변경 하려면 음수 값을 사용할 수 없으므로 한 **스트림**합니다. 양의 정수만 사용할 수 있습니다 **위치**합니다.  
  
> [!NOTE]
>  에 대 한 읽기 전용 **스트림** 개체, ADO 경우 오류를 반환 하지 것입니다 **위치** 보다 큰 값으로 설정 되는 **크기** 의 **스트림**합니다. 이 크기를 변경 되지 않습니다는 **스트림**, alter 또는 **스트림** 어떤 방식으로든에서 콘텐츠입니다. 그러나이 작업을 수행 하면 안 있기 때문에 의미 없는 **위치**값입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Charset 속성(ADO)](../../../ado/reference/ado-api/charset-property-ado.md)

