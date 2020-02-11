---
title: Ordinal 속성 (ADO MD 셀) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 194b72ce66eb2efdc3a246f24948b01c790f7b8e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949373"
---
# <a name="ordinal-property-ado-md-cell"></a>Ordinal 속성(ADO MD Cell)
셀 집합의 위치를 기준으로 [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md) 을 고유 하 게 식별 합니다.  
  
## <a name="return-values"></a>반환 값  
 는 **Long** 정수를 반환 하며 읽기 전용입니다.  
  
## <a name="remarks"></a>설명  
 셀의 서 수 값은 셀 집합 내의 셀을 고유 하 게 식별 합니다. 개념적으로 셀은 셀 집합에서 셀 개수가 *p*차원 배열인 것 처럼 번호가 매겨집니다. 여기서 *p* 는 [축](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)수입니다. 셀의 번호는 0부터 시작 하 여 행의 오름차순으로 정렬 됩니다. 다음은 셀의 서 수 번호를 계산 하는 수식입니다.  
  
 셀의 서 수 값은 [셀](../../../ado/reference/ado-md-api/cell-object-ado-md.md)을 신속 하 게 검색 하기 위해 셀 [집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체의 [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) 속성에 사용할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Cell 개체(ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [축 예 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Cellset 개체 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Item 속성 (ADO MD 셀 집합)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Ordinal 속성(ADO MD Position)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
