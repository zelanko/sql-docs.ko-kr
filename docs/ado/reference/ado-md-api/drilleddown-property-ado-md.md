---
title: DrilledDown 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 83db7cfc6cac6dde34ca8d2a974c9d926ba9f086
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709450"
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown 속성(ADO MD)
자식 즉시 따르는지 여부를 나타냅니다 합니다 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 축의 합니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **부울** 값 및 읽기 전용입니다. **DrilledDown** 반환 **True** 축에 현재 멤버의 자식 멤버가 없으면입니다. **DrilledDown** 반환 **False** 현재 멤버에 축에 하나 이상의 자식 멤버가 있는 경우.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **DrilledDown** 축이이 멤버 바로 다음에이 멤버의 자식이 하나 이상 있는지 여부를 결정 하는 속성입니다. 이 정보는 멤버를 표시할 때 유용 합니다.  
  
 이 속성 에서만 지원 됩니다 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 에 속하는 개체를 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체입니다. 이 속성에서 참조 되는 동안 오류가 발생 **멤버** 에 속하는 개체를 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목  
 [ParentSameAsPrev 속성(ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
