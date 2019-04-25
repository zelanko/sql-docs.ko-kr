---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57b570b93d4e8a6cf10d879659f0886e1c6f0c8e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469298"
---
# <a name="cellset-object-ado-md"></a>Cellset 개체(ADO MD)
다차원 쿼리 결과를 나타냅니다. 큐브 또는 기타 셀 집합에서 선택 된 셀의 컬렉션입니다.  
  
## <a name="remarks"></a>Remarks  
 내에서 데이터를 **Cellset** 직접 배열 유사 액세스를 사용 하 여 검색 됩니다. 해당 멤버에 대 한 데이터를 가져올 특정 멤버를 다운 드릴 수 있습니다. 예를 들어, 다음 코드 캡션을 반환 하는 첫 번째 멤버의 첫 번째 위치에서 명명 된 셀 집합의 첫 번째 축에 `cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>Remarks  
 집합에서 현재 셀의 개념이 없었습니다 있습니다. 대신 합니다 [항목](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) 속성을 특정 검색 [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md) 셀 집합에서 개체입니다. 인수는 **항목** 속성이 검색 되는 셀을 결정 합니다. 셀의 고유한 서 수 값을 지정할 수 있습니다. 셀은 셀 집합의 각 축 따라 위치 번호를 사용 하 여 검색할 수도 있습니다. 셀을 검색 하는 방법에 대 한 자세한 내용은 참조는 [항목](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) 속성입니다.  
  
 컬렉션, 메서드 및 속성을 사용 하 여는 **Cellset** 개체를 다음을 수행할 수 있습니다.  
  
-   연결 된 열려 있는 연결을 **셀 집합** 개체를 설정 하 여 해당 [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) 속성입니다.  
  
-   실행 하 고 사용 하 여 다차원 쿼리의 결과 검색 합니다 [열고](../../../ado/reference/ado-md-api/open-method-ado-md.md) 메서드.  
  
-   검색을 **셀** 에서 합니다 **셀 집합** 사용 하 여는 [항목](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) 속성입니다.  
  
-   반환 된 [축](../../../ado/reference/ado-md-api/axis-object-ado-md.md) 정의 하는 개체를 **셀 집합** 사용 하 여는 [축](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) 컬렉션.  
  
-   데이터를 필터링 하는 데 사용 하는 차원에 대 한 정보를 검색 합니다 **셀 집합** 사용 하 여 합니다 [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) 속성.  
  
-   반환 하거나 정의 하는 쿼리를 지정 합니다 **셀 집합** 사용 하 여 합니다 [원본](../../../ado/reference/ado-md-api/source-property-ado-md.md) 속성.  
  
-   현재 상태를 반환 합니다 **셀 집합** (열기, 닫혀 있고 실행 중 또는 연결)와 [상태](../../../ado/reference/ado-md-api/state-property-ado-md.md) 속성입니다.  
  
-   개방적이 고 닫으려면 **Cellset** 사용 하 여는 [닫기](../../../ado/reference/ado-md-api/close-method-ado-md.md) 메서드.  
  
-   에 대 한 공급자 관련 정보를 검색 합니다 **Cellset** 표준 ADO를 사용 하 여 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Cellset 예제 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Axes 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Cell 개체 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
