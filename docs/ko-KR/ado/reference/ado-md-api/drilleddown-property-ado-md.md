---
title: ADO MD DrilledDown 속성 | Microsoft Docs
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
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8be1a63b9d4f1c979d7670c2ed3a79766070ca4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="drilleddown-property-ado-md"></a>ADO MD DrilledDown 속성
자식 즉시 따르는지 여부를 나타냅니다는 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 축에 있습니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **부울** 값 및 읽기 전용입니다. **DrilledDown** 반환 **True** 축에 현재 멤버의 자식 멤버가 없는 경우. **DrilledDown** 반환 **False** 현재 멤버 축에 하나 이상의 자식 멤버의 경우.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **DrilledDown** 속성을이 멤버 바로 뒤에 축이 멤버에 자식이 하나 이상 있는지 여부를 확인 합니다. 이 정보는 구성원을 표시할 때 유용 합니다.  
  
 이 속성은 에서만 지원 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 에 속하는 개체는 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체입니다. 이 속성에서 참조 되는 동안 오류가 발생 **멤버** 에 속하는 개체는 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ParentSameAsPrev 속성(ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
