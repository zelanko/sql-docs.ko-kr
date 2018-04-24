---
title: Item 속성 (ADO MD Cellset) | Microsoft Docs
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
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82ac69cd33e87d480ccd1908f4e7c7d778f7726d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="item-property-ado-md-cellset"></a>Item 속성 (ADO MD Cellset)
셀을 검색 한 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 좌표를 사용 하 여 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>매개 변수  
 *위치*  
 A **VariantArray** 셀을 고유 하 게 지정 하는 값입니다. *위치* 다음 중 하나일 수 있습니다.  
  
-   위치 번호의 배열  
  
-   멤버 이름 배열  
  
-   서 수 위치  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **항목** 반환 하는 [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md) 내에서 개체는 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체입니다. 경우는 **항목** 속성에 해당 하는 셀을 찾을 수 없습니다는 *위치* 인수, 오류가 발생 합니다.  
  
 **항목** 속성은 기본 속성에 대 한는 **셀 집합** 개체입니다. 다음 구문 형식은 서로 전환이 가능 합니다.  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>주의  
 *위치* 인수는 반환할 셀을 지정 합니다. 셀 서 수 위치 별로 또는 각 축 위치를 지정할 수 있습니다. 각 축 따라 위치에 따라 셀을 지정할 때 위치 숫자 값 또는 각 위치에 대 한 멤버의 이름을 지정할 수 있습니다.  
  
 서 수 위치는에서 하나의 셀을 고유 하 게 식별 하는 숫자는 **셀 집합**합니다. 이론적으로 셀은 번호가 매겨집니다는 **셀 집합** 처럼는 **셀 집합** 된는 *p*-차원 배열 여기서 *p* 축의 수입니다. 셀은 행 중심의 순서로 번호가 매겨집니다. 다음은 셀의 서 수를 계산 하는 것에 대 한 수식:  
  
 마찬가지로 문자열을 멤버 이름을 전달 하는 경우 **항목**, 멤버 숫자 축 식별자의 오름차순으로 나열 되어야 합니다. 축에서 멤버의 차원 중첩 오름차순으로 나열 합니다-즉, 가장 바깥쪽 차원 되어 내부 차원의 멤버가 옵니다. 각 차원에서 별도 문자열로 나타낼지 및 멤버 문자열 목록을 쉼표로 구분 해야 합니다.  
  
> [!NOTE]
>  셀 멤버 이름으로 검색 데이터 공급자가 지원 되지 않을 수 있습니다. 자세한 내용은 공급자 설명서를 참조 하십시오.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ADO MD cell 개체](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
