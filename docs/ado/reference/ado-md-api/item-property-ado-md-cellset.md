---
title: Item 속성 (ADO MD Cellset) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c7fbce544cac188db7ed3b3d40478aa63809405
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949621"
---
# <a name="item-property-ado-md-cellset"></a>Item 속성(ADO MD Cellset)
셀을 검색 한 [cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 좌표를 사용 하 여 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>매개 변수  
 *위치*  
 A **VariantArray** 셀을 고유 하 게 지정 하는 값입니다. *위치* 다음 중 하나일 수 있습니다.  
  
-   위치 숫자의 배열  
  
-   멤버 이름의 배열  
  
-   서 수 위치  
  
## <a name="remarks"></a>설명  
 사용 하 여 합니다 **항목** 반환할 속성을 [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md) 내에서 개체를 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체입니다. 경우는 **항목** 속성에 해당 하는 셀을 찾을 수 없습니다는 *위치* 인수 오류가 발생 합니다.  
  
 **항목** 속성은 기본 속성을 **셀 집합** 개체입니다. 다음 구문 형식 서로:  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>설명  
 합니다 *위치* 인수를 반환 하는 셀을 지정 합니다. 셀 서 수 위치 또는 각 축 따라 위치를 지정할 수 있습니다. 각 축 따라 위치에 따라 셀을 지정할 때 위치 숫자 값 이나 각 위치에 대 한 멤버의 이름을 지정할 수 있습니다.  
  
 서 수 위치는 하나의 셀 내에서 고유 하 게 식별 하는 번호를 **Cellset**합니다. 이론적으로 셀 번호가 매겨집니다를 **셀 집합** 처럼 합니다 **셀 집합** 된를 *p*-차원 배열에 있는 *p* 는 축의 개수입니다. 셀은 행 중심의 순서로 번호가 매겨집니다. 다음은 셀의 서 수를 계산 하는 것에 대 한 수식:  
  
 마찬가지로 문자열을 멤버 이름을 전달 하는 경우 **항목**, 멤버는 숫자 축 식별자의 오름차순으로 나열 되어야 합니다. 축에서 멤버는 차원 중첩의 오름차순으로 나열 되어야 합니다-즉, 가장 바깥쪽 차원 멤버는 먼저 내부 차원의 멤버 뒤에 있습니다. 별도 문자열로로 표시 되도록 각 차원 및 멤버 문자열 목록을 쉼표로 구분 해야 합니다.  
  
> [!NOTE]
>  셀 멤버 이름으로 검색 데이터 공급자에서 지원 될 수 있습니다. 자세한 내용은 공급자 설명서를 참조 하십시오.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목  
 [Cell 개체 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
