---
title: Members 컬렉션 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e7f2221f511d48acc68c379dce72e7708819b1aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709040"
---
# <a name="members-collection-ado-md"></a>Members 컬렉션(ADO MD)
포함 된 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 수준 또는 축 따라 위치에서 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 A **멤버** 컬렉션은 다음 형식의 멤버도 포함 됩니다.  
  
-   큐브의 수준을 구성 하는 멤버입니다. 에 포함 된 이러한 합니다 **멤버** 의 컬렉션을 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md) 개체입니다. 예를 들어, 샘플을 사용 하 여 [다차원 스키마의 개요 및 데이터](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), 캐나다, 미국, 영국 및 독일 국가 수준의 네 가지 멤버 됩니다.  
  
-   계층 내에서 특정 멤버의 자식 멤버입니다. 이러한 멤버에서 반환 되는 [자식을](../../../ado/reference/ado-md-api/children-property-ado-md.md) 부모 **멤버** 개체입니다. 예를 들어, 동일한 예제를 다시 사용할 두 Canada 멤버의 자식은 캐나다 동부 및 캐나다 서 부입니다.  
  
-   축 따라 특정 위치를 정의 하는 멤버를 [cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)합니다. 셀 집합을 사용 하 여 [다차원 데이터를 사용 하 여 작업](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) 예를 들어 x 축에 첫 번째 위치 두 멤버는 발렌타인 데이 및 시애틀 합니다. 이러한 멤버에 포함 되는 **멤버** 의 컬렉션을 [위치](../../../ado/reference/ado-md-api/position-object-ado-md.md) 개체입니다.  
  
 **멤버** 은 표준 ADO 컬렉션입니다. 속성 및 컬렉션의 메서드를 사용 하 여 다음을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션에서 개체의 번호를 가져올는 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   기본값을 사용 하 여 컬렉션에서 개체를 반환 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   공급자에서 컬렉션의 개체를 업데이트 합니다 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Members 예제 (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Member 개체(ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
