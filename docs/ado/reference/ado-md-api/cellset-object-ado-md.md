---
description: Cellset 개체(ADO MD)
title: Cellset 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
author: rothja
ms.author: jroth
ms.openlocfilehash: 65e5e28443fd4656aa2b953f18b07c952bcbb66a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778312"
---
# <a name="cellset-object-ado-md"></a>Cellset 개체(ADO MD)
다차원 쿼리 결과를 나타냅니다. 큐브 또는 다른 셀 집합에서 선택 된 셀의 컬렉션입니다.  
  
## <a name="remarks"></a>설명  
 **셀 집합** 내의 데이터는 직접 배열 유사 액세스를 사용 하 여 검색 됩니다. 특정 멤버로 드릴 다운 하 여 해당 멤버에 대 한 데이터를 가져올 수 있습니다. 예를 들어 다음 코드는 라는 셀 집합의 첫 번째 축에서 첫 번째 위치의 캡션을 반환 합니다 `cst` .  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>설명  
 셀 집합에는 현재 셀에 대 한 개념이 없습니다. 대신 [Item](./item-property-ado-md-cellset.md) 속성은 셀 집합에서 특정 [셀](./cell-object-ado-md.md) 개체를 검색 합니다. **항목** 속성의 인수는 검색 되는 셀을 결정 합니다. 셀의 고유 서 수 값을 지정할 수 있습니다. 셀 집합의 각 축에서 해당 위치 번호를 사용 하 여 셀을 검색할 수도 있습니다. 셀을 검색 하는 방법에 대 한 자세한 내용은 [Item](./item-property-ado-md-cellset.md) 속성을 참조 하세요.  
  
 **셀 집합** 개체의 컬렉션, 메서드 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [ActiveConnection](./activeconnection-property-ado-md.md) 속성을 설정 하 여 열린 연결을 **Cellset** 개체와 연결 합니다.  
  
-   [Open](./open-method-ado-md.md) 메서드를 사용 하 여 다차원 쿼리 결과를 실행 하 고 검색 합니다.  
  
-   [항목](./item-property-ado-md-cellset.md) 속성을 사용 하 여 셀 **집합** 에서 **셀** 을 검색 합니다.  
  
-   [축](./axes-collection-ado-md.md) 컬렉션을 사용 하 여 **셀 집합** 을 정의 하는 [축](./axis-object-ado-md.md) 개체를 반환 합니다.  
  
-   [Filteraxis](./filteraxis-property-ado-md.md) 속성을 사용 하 여 **셀 집합** 의 데이터를 필터링 하는 데 사용 되는 차원에 대 한 정보를 검색 합니다.  
  
-   [Source](./source-property-ado-md.md) 속성을 사용 하 여 **셀 집합** 을 정의 하는 데 사용 되는 쿼리를 반환 하거나 지정 합니다.  
  
-   [상태](./state-property-ado-md.md) 속성을 사용 하 여 **셀 집합** (열기, 닫기, 실행 또는 연결)의 현재 상태를 반환 합니다.  
  
-   [Close](./close-method-ado-md.md) 메서드를 사용 하 여 열린 **셀 집합** 을 닫습니다.  
  
-   표준 ADO [속성](../ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 **셀 집합** 에 대 한 공급자 관련 정보를 검색 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](./cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [셀 집합 예제 (VB)](./cellset-example-vb.md)   
 [축 컬렉션 (ADO MD)](./axes-collection-ado-md.md)   
 [Cell 개체 (ADO MD)](./cell-object-ado-md.md)   
 [Connection 개체 (ADO)](../ado-api/connection-object-ado.md)   
 [Properties 컬렉션(ADO)](../ado-api/properties-collection-ado.md)