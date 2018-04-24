---
title: Size 속성 (ADO 스트림) | Microsoft Docs
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
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b1ecbc53ec085ec67b827338dbf7899245278e9
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="size-property-ado-stream"></a>Size 속성 (ADO 스트림)
바이트 수가 스트림 크기를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **긴** 스트림의 크기 바이트 수를 지정 하는 값입니다. 기본 값은 스트림의 크기를 알 수 없는 경우, 스트림 또는-1의 크기입니다.  
  
## <a name="remarks"></a>주의  
 **크기** 열기에만 사용할 수 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
> [!NOTE]
>  비트에 저장할 수는 **스트림** 개체를 시스템 리소스로 제한 합니다. 경우는 **스트림** 로 나타내야 보다 더 많은 비트가 포함 되어는 **긴** 값 **크기** 잘리고 따라서 정확 하 게 나타내지 않습니다는 길이**스트림**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Size 속성(ADO 매개 변수)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
