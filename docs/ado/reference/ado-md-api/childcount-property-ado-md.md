---
title: ChildCount 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01be10781c0925683ed2da9fdff24190d175fca6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611411"
---
# <a name="childcount-property-ado-md"></a>ChildCount 속성(ADO MD)
멤버 수를 나타내는 현재 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체가 계층의 부모입니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **긴** 정수 읽기 전용 이며 합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **ChildCount** 자녀 수의 추정치를 반환 하도록 속성을 **멤버** 에. 실제 자식의 **멤버** 에서 반환 될 수는 [자식을](../../../ado/reference/ado-md-api/children-property-ado-md.md) 속성입니다.  
  
 에 대 한 **멤버** 에서 개체를 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체를 반환 하는 최대는 65536입니다. 자식의 실제 수가 65536를 초과 하면, 반환 되는 값은 여전히 65536 됩니다. 따라서 응용 프로그램 해석 해야는 **ChildCount** 자식 65536 보다 크거나 같음으로.  
  
 에 대 한 **멤버** 에서 개체를 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체, ADO 컬렉션을 사용 하 여 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성에는 **자식** 결정 하기 위해 컬렉션은 자식의 정확한 수입니다. 자식의 정확한 수를 결정 하는 컬렉션의 자식 수가 큰 경우에 느려질 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목  
 [Children 속성 (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count 속성 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Members 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
