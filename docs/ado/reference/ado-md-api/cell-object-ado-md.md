---
description: Cell 개체(ADO MD)
title: Cell 개체 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b6fceeea4ebe6728ae4adf9bce52cb6b642a926d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987213"
---
# <a name="cell-object-ado-md"></a>Cell 개체(ADO MD)
셀 집합에 포함 된 축 좌표가 교차 하는 지점의 데이터를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 셀 개체는 **셀** [집합](./cellset-object-ado-md.md) 개체의 [Item](./item-property-ado-md-cellset.md) 속성에서 반환 됩니다.  
  
 **Cell** 개체의 컬렉션 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Value](./value-property-ado-md.md) 속성을 사용 하 여 **셀** 의 데이터를 반환 합니다.  
  
-   [FormattedValue](./formattedvalue-property-ado-md.md) 속성을 사용 하 여 **값** 속성의 형식이 지정 된 표시를 나타내는 문자열을 반환 합니다.  
  
-   [서 수](./ordinal-property-ado-md-cell.md) 속성을 사용 하 여 셀 **집합** 내에 있는 **셀** 의 서 수 값을 반환 합니다.  
  
-   [위치](./positions-collection-ado-md.md) 컬렉션을 사용 하 여 [CubeDef](./cubedef-object-ado-md.md) 내에서 **셀** 의 위치를 확인 합니다.  
  
-   표준 ADO [속성](../ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 **셀** 에 대 한 기타 정보를 검색 합니다.  
  
 **속성** 컬렉션에는 공급자가 제공한 속성이 포함 되어 있습니다. 다음 표에서는 사용할 수 있는 속성을 보여 줍니다. 실제 속성 목록은 공급자의 구현에 따라 다를 수 있습니다. 사용 가능한 속성의 전체 목록은 공급자 설명서를 참조 하세요.  
  
|Name|설명|  
|----------|-----------------|  
|BackColor|셀을 표시할 때 사용 되는 배경색입니다.|  
|FontFlags|글꼴 효과를 자세히 설명 하는 비트 마스크입니다.|  
|FontName|셀 값을 표시 하는 데 사용 되는 글꼴입니다.|  
|FontSize|셀 값을 표시 하는 데 사용 되는 글꼴 크기입니다.|  
|ForeColor|셀을 표시할 때 사용 되는 전경색입니다.|  
|FormatString|형식이 지정 된 문자열의 값입니다.|  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](./cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [축 예 (VBScript)](./axis-example-vbscript.md)   
 [Cellset 개체 (ADO MD)](./cellset-object-ado-md.md)   
 [위치 컬렉션 (ADO MD)](./positions-collection-ado-md.md)   
 [Properties 컬렉션(ADO)](../ado-api/properties-collection-ado.md)