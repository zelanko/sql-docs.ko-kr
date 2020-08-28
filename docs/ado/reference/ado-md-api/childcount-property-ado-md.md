---
description: ChildCount 속성(ADO MD)
title: ChildCount 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
author: rothja
ms.author: jroth
ms.openlocfilehash: a5c3668a115de8137cd96f489f3e11483cb50045
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987134"
---
# <a name="childcount-property-ado-md"></a>ChildCount 속성(ADO MD)
현재 [멤버](./member-object-ado-md.md) 개체가 계층의 부모인 멤버 수를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 는 **Long** 정수를 반환 하며 읽기 전용입니다.  
  
## <a name="remarks"></a>설명  
 **ChildCount** 속성을 사용 하 여 **멤버** 에 포함 된 자식의 수를 예상 값으로 반환 합니다. **멤버** 의 실제 자식은 [children](./children-property-ado-md.md) 속성에 의해 반환 될 수 있습니다.  
  
 [Position](./position-object-ado-md.md) 개체의 **멤버** 개체의 경우 반환 되는 최대 수는 65536입니다. 실제 자식 수가 65536를 초과 하는 경우 반환 되는 값은 여전히 65536입니다. 따라서 응용 프로그램은 65536의 **ChildCount** 를 65536 자식과 같거나 큰 값으로 해석 해야 합니다.  
  
 [수준](./level-object-ado-md.md) 개체의 **멤버** 개체의 경우 **자식** 컬렉션의 ADO collection [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 정확한 자식 수를 확인 합니다. 컬렉션의 자식 수가 클 경우 정확히 자식의 수를 확인 하는 것은 느릴 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [Children 속성 (ADO MD)](./children-property-ado-md.md)   
 [Count 속성 (ADO)](../ado-api/count-property-ado.md)   
 [Members 컬렉션(ADO MD)](./members-collection-ado-md.md)