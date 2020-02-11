---
title: Field 개체 | Microsoft Docs
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
ms.openlocfilehash: 04dbf3069896b9a7668d64a2f1d322f0b17ca5f3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918680"
---
# <a name="field-object"></a>Field 개체
공통 데이터 형식으로 데이터의 열을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 각 **Field** 개체는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)의 열에 해당 합니다. **Field** 개체의 [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성을 사용 하 여 현재 레코드에 대 한 데이터를 설정 하거나 반환 합니다. 공급자가 제공 하는 기능에 따라 **필드** 개체의 일부 컬렉션, 메서드 또는 속성을 사용 하지 못할 수 있습니다.  
  
 **Field** 개체의 컬렉션, 메서드 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](../../../ado/reference/ado-api/name-property-ado.md) 속성을 사용 하 여 필드 이름을 반환 합니다.  
  
-   **Value** 속성을 사용 하 여 필드의 데이터를 보거나 변경 합니다. **Value** 는 **Field** 개체의 기본 속성입니다.  
  
-   [형식](../../../ado/reference/ado-api/type-property-ado.md), [전체 자릿수](../../../ado/reference/ado-api/precision-property-ado.md)및 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 속성을 사용 하 여 필드의 기본 특성을 반환 합니다.  
  
-   [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) 속성을 사용 하 여 필드의 선언 된 크기를 반환 합니다.  
  
-   [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) 속성을 사용 하 여 지정 된 필드에 있는 데이터의 실제 크기를 반환 합니다.  
  
-   [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성 및 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 지정 된 필드에 대해 지원 되는 기능 유형을 결정 합니다.  
  
-   [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 및 [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) 메서드를 사용 하 여 긴 이진 또는 긴 문자 데이터를 포함 하는 필드의 값을 조작 합니다.  
  
-   공급자에서 일괄 업데이트를 지 원하는 경우 일괄 업데이트 중 [Originalvalue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 및 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) 속성을 사용 하 여 필드 값의 불일치를 해결 합니다.  
  
 모든 메타 데이터 속성 (**Name**, **Type**, **DefinedSize**, **Precision**및 **NumericScale**)은 **필드** 개체의 **레코드 집합**을 열기 전에 사용할 수 있습니다. 이를 설정 하는 경우 폼을 동적으로 생성 하는 데 유용 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Field 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
