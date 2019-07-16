---
title: 셀 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell
helpviewer_keywords:
- Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbf97a4095f2295b8851f87ba20ab083938e70ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947745"
---
# <a name="cell-object-ado-md"></a>Cell 개체(ADO MD)
셀 집합에 포함 된 축 좌표의 교집합에서 데이터를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 A **셀** 개체를 반환 합니다 [항목](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) 속성을 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체.  
  
 컬렉션 및 속성을 사용 하 여는 **셀** 개체를 다음을 수행할 수 있습니다.  
  
-   데이터를 반환 합니다 **셀** 사용 하 여 합니다 [값](../../../ado/reference/ado-md-api/value-property-ado-md.md) 속성입니다.  
  
-   서식이 지정 된 표시를 나타내는 문자열을 반환 합니다 **값** 속성을 합니다 [FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md) 속성.  
  
-   서 수 값을 반환 합니다 **셀** 내에서 **셀 집합** 사용 하 여는 [서 수](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md) 속성.  
  
-   위치를 결정 합니다 **셀** 내는 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 사용 하 여를 [위치](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) 컬렉션입니다.  
  
-   에 대 한 기타 정보를 검색 합니다 **셀** 표준 ado [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
 합니다 **속성** 공급자가 제공한 속성을 포함 하는 컬렉션입니다. 다음 표에서 사용할 수 있는 속성을 보여 줍니다. 실제 속성은 공급자의 구현에 따라 달라질 수 있습니다. 사용 가능한 속성의 전체 목록에 대 한 공급자에 대 한 설명서를 참조 하세요.  
  
|이름|설명|  
|----------|-----------------|  
|BackColor|셀을 표시할 때 사용 되는 배경색입니다.|  
|FontFlags|글꼴 효과 자세하게 비트 마스크입니다.|  
|FontName|셀 값을 표시 하는 데 사용 하는 글꼴입니다.|  
|FontSize|셀 값을 표시 하는 데 사용 되는 글꼴 크기입니다.|  
|ForeColor|셀을 표시할 때 사용 되는 전경색입니다.|  
|FormatString|서식이 지정 된 문자열에서 값입니다.|  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [속성, 메서드 및 이벤트](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Axis 예제 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Cellset 개체 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Positions 컬렉션 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
