---
title: Item 속성 (ADO MD 셀 집합) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949621"
---
# <a name="item-property-ado-md-cellset"></a>Item 속성(ADO MD Cellset)
좌표를 사용 하 여 셀 [집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 에서 셀을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>매개 변수  
 *위치*  
 셀을 고유 하 게 지정 하는 값의 **VariantArray** 입니다. *위치* 는 다음 중 하나일 수 있습니다.  
  
-   위치 번호의 배열입니다.  
  
-   멤버 이름 배열  
  
-   서 수 위치입니다.  
  
## <a name="remarks"></a>설명  
 **Item** 속성을 사용 하 여 셀 [집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체 내에 [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md) 개체를 반환 합니다. **항목** 속성이 *위치* 인수에 해당 하는 셀을 찾을 수 없는 경우 오류가 발생 합니다.  
  
 **Item** 속성은 **셀 집합** 개체의 기본 속성입니다. 다음 구문 형식은 서로 바꿔 사용할 수 있습니다.  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>설명  
 *위치* 인수는 반환할 셀을 지정 합니다. 서 수 위치로 또는 각 축의 위치를 기준으로 셀을 지정할 수 있습니다. 각 축을 따라 위치 별로 셀을 지정 하는 경우 각 위치에 대 한 멤버 이름 또는 위치의 숫자 값을 지정할 수 있습니다.  
  
 서 수 위치는 셀 **집합**내의 셀 하나를 고유 하 게 식별 하는 숫자입니다. 개념적으로 **셀은** 셀 집합에서 셀 개수가 *p*차원 배열인 **것 처럼 번호가** 매겨집니다. 여기서 *p* 는 축 수입니다. 셀은 행 중심의 순서로 번호가 매겨집니다. 다음은 셀의 서 수 번호를 계산 하는 수식입니다.  
  
 멤버 이름이 **항목**에 문자열로 전달 되는 경우에는 멤버를 숫자 축 식별자의 오름차순으로 나열 해야 합니다. 축 내에서 멤버는 차원 중첩 순서를 오름차순으로 나열 되어야 합니다. 즉, 가장 바깥쪽 차원의 멤버가 먼저 오고 그 다음에 내부 차원의 멤버가 표시 되어야 합니다. 각 차원은 별도의 문자열로 표시 되어야 하며 멤버 문자열 목록은 쉼표로 구분 해야 합니다.  
  
> [!NOTE]
>  멤버 이름으로 셀을 검색 하는 것은 데이터 공급자가 지원 하지 않을 수 있습니다. 자세한 내용은 공급자에 대 한 설명서를 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [Cell 개체 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
