---
title: 개체 필드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9b57ce165337dc2cef87daf8c2a835bde0c5f85b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697857"
---
# <a name="field-object"></a>Field 개체
일반적인 데이터 형식 사용 하 여 데이터의 열을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 각 **필드** 개체의 열에 해당 합니다 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. 사용할 합니다 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성을 **필드** 현재 레코드에 대 한 데이터를 반환 하는 개체입니다. 기능에 따라 공급자가 제공 몇 가지 컬렉션, 메서드 또는 속성을 **필드** 개체를 사용할 수 없습니다.  
  
 컬렉션, 메서드 및 속성을 사용 하 여는 **필드** 개체를 다음을 수행할 수 있습니다.  
  
-   사용 하 여 필드의 이름을 반환 합니다 [이름을](../../../ado/reference/ado-api/name-property-ado.md) 속성입니다.  
  
-   보거나 사용 하 여 필드의 데이터를 변경 합니다 **값** 속성입니다. **값** 의 기본 속성을 **필드** 개체입니다.  
  
-   사용 하 여 필드의 기본 특성을 반환 합니다 [형식](../../../ado/reference/ado-api/type-property-ado.md), [정밀도](../../../ado/reference/ado-api/precision-property-ado.md), 및 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 속성입니다.  
  
-   사용 하 여 필드의 선언 된 크기를 반환 합니다 [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) 속성입니다.  
  
-   사용 하 여 지정된 된 필드의 데이터의 실제 크기를 반환 합니다 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) 속성입니다.  
  
-   기능의 유형을 사용 하 여 지정된 된 필드에 대 한 지원 되는지 확인 합니다 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성 및 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
-   사용 하 여 긴 이진 또는 긴 문자 데이터를 포함 하는 필드의 값을 조작 합니다 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 하 고 [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) 메서드.  
  
-   공급자 일괄 처리 업데이트를 지 원하는 경우 일괄 처리로 업데이트 하는 동안 필드 값 불일치 해결 합니다 [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 하 고 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) 속성.  
  
 모든 메타 데이터 속성 (**이름을**, **형식**를 **DefinedSize**를 **정밀도**, 및 **NumericScale**) 열기 전에 사용할 합니다 **필드** 개체의 **Recordset**합니다. 해당 시점에 설정 하는 폼을 동적으로 생성 유용 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Field 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [필드 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
