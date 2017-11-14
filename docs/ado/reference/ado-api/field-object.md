---
title: "개체 필드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f876e76b29dbc2436d6d1dba317c5035ebbc9ca1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="field-object"></a>Field 개체
일반 데이터 형식과 데이터의 열을 나타냅니다.  
  
## <a name="remarks"></a>주의  
 각 **필드** 의 열에 해당 하는 개체는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. 사용 하면는 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성 **필드** 개체를 설정 하거나 현재 레코드에 대 한 데이터를 반환 합니다. 기능에 따라 공급자가 제공 컬렉션, 메서드 또는 속성의 일부는 **필드** 개체를 사용할 수 없습니다.  
  
 컬렉션, 메서드 및 속성의는 **필드** 개체를 다음을 수행할 수 있습니다.  
  
-   필드의 이름을 반환는 [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성입니다.  
  
-   보기 또는 변경 된 필드의 데이터는 **값** 속성입니다. **값** 은의 기본 속성은 **필드** 개체입니다.  
  
-   반환 된 필드의 기본 특성의 [형식](../../../ado/reference/ado-api/type-property-ado.md), [정밀도](../../../ado/reference/ado-api/precision-property-ado.md), 및 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 속성입니다.  
  
-   반환 된 필드의 선언 된 크기는 [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) 속성입니다.  
  
-   으로 지정된 된 필드에 데이터의 실제 크기를 반환 합니다.는 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) 속성입니다.  
  
-   어떤 종류의 기능으로 지정된 된 필드에 대 한 지원 되는지 확인은 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성 및 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
-   사용 하 여 긴 이진 또는 긴 문자 데이터를 포함 하는 필드의 값을 조작는 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 및 [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) 메서드.  
  
-   공급자가 일괄 처리 업데이트를 지 원하는 경우 일괄 처리로 업데이트 하는 동안 필드 값에서 불일치를 해결할는 [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 및 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) 속성입니다.  
  
 모든 메타 데이터 속성 (**이름**, **형식**, **DefinedSize**, **정밀도**, 및 **NumericScale**) 열기 전에 사용할 수는 **필드** 개체의 **레코드 집합**합니다. 해당 시간에이 설정 하는 것은 동적으로 폼을 만드는 데 유용 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [필드 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

