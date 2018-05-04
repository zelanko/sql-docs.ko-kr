---
title: ADO MD ChildCount 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da861dbc7648edbe93926e8f4df7b560fc4a415f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="childcount-property-ado-md"></a>ADO MD ChildCount 속성
에 대 한 멤버 수를 나타내는 현재 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체는 계층의 부모입니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **긴** 정수 읽기 전용입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **ChildCount** 자녀 수의 예측을 반환 하는 **멤버** 했습니다. 실제 자식은 **멤버** 에서 반환할 수는 [자식](../../../ado/reference/ado-md-api/children-property-ado-md.md) 속성입니다.  
  
 에 대 한 **멤버** 에서 개체는 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체를 반환 하는 최대 수는 65536입니다. 자식 수가 실제 65536을 초과할 경우 반환 되는 값은 계속 65536 됩니다. 따라서 응용 프로그램 해석 해야는 **ChildCount** 자식 65536 보다 크거나 같은으로 합니다.  
  
 에 대 한 **멤버** 에서 개체는 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체, ADO 컬렉션을 사용 하 여 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성에는 **자식** 결정 하기 위해 컬렉션은 자식의 정확한 수입니다. 자식의 정확한 수를 결정 하는 컬렉션의 자식 수가 많은 경우 느릴 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ADO MD children 속성](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count 속성 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Members 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
