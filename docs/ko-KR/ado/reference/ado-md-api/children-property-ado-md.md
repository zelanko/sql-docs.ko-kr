---
title: Children 속성 (ADO MD) | Microsoft Docs
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
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 630ddeaf83b09dfe502cf07efd7a4185011cff41
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="children-property-ado-md"></a>ADO MD children 속성
반환 된 [멤버](../../../ado/reference/ado-md-api/members-collection-ado-md.md) 컬렉션입니다 현재 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 계층 구조에서 부모입니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **멤버** 컬렉션 읽기 전용입니다.  
  
## <a name="remarks"></a>주의  
 **자식** 속성을 포함 한 **멤버** 컬렉션입니다 현재 **멤버** 계층적 부모인 합니다. 리프 수준 **멤버** 개체 자식 멤버가 없는 **멤버** 컬렉션입니다. 이 속성은 에서만 지원 **멤버** 에 속하는 개체는 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체입니다. 이 속성에서 참조 되는 동안 오류가 발생 **멤버** 에 속하는 개체는 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ChildCount 속성(ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
