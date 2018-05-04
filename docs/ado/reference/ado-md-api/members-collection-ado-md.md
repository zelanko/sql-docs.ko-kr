---
title: Members 컬렉션 ADO MD | Microsoft Docs
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
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18a3fac9cff0a41c9d1e7dc820d68ae77c294d4a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="members-collection-ado-md"></a>(ADO MD) members 컬렉션
포함 된 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 한 수준이 나 축의 위치 개체입니다.  
  
## <a name="remarks"></a>주의  
 A **멤버** 컬렉션 다음과 같은 유형의 멤버를 포함 하는 데 사용 됩니다.  
  
-   큐브의 수준을 구성 하는 멤버입니다. 에 들어 있습니다는 **멤버** 의 컬렉션을 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체입니다. 예를 들어에서 샘플을 사용 하 여 [개 및 데이터](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), 캐나다, 일본, 영국 및 독일 국가 수준의 4 개 멤버 됩니다.  
  
-   이 멤버는 계층 내에서 특정 멤버의 자식 항목입니다. 메서드에서 반환 되는 이러한 멤버는 [자식](../../../ado/reference/ado-md-api/children-property-ado-md.md) 부모 **멤버** 개체입니다. 예를 들어 동일한 샘플을 사용 하 여 다시, Canada 멤버의 두 명의 자식은 캐나다 동부 및 캐나다-서입니다.  
  
-   축 따라 특정 위치를 정의 하는 멤버는 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)합니다. 셀 집합을 사용 하 여 [다차원 데이터 작업](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) 예를 들어 x 축에 첫 번째 위치 두 멤버는 발렌타인 데이 및 Seattle 합니다. 이러한 멤버에 포함 되는 **멤버** 의 컬렉션을 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체입니다.  
  
 **멤버** 은 표준 ADO 컬렉션입니다. 속성과 컬렉션의 메서드를 사용 하 여 다음을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션의 개체 수를 가져옵니다는 [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   기본값을 사용 하 여 컬렉션에서 개체를 반환 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하는 공급자에서 컬렉션의 개체를 업데이트 하는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [멤버 예 (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
