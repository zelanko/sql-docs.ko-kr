---
title: Property 개체 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
author: rothja
ms.author: jroth
ms.openlocfilehash: d2f4a8b6cdeabcbab0802a0052ed697af70ef45a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759969"
---
# <a name="property-object-ado"></a>속성 개체(ADO)
공급자에 의해 정의 된 ADO 개체의 동적 특성을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 ADO 개체에는 기본 제공 및 동적 속성의 두 가지 유형이 있습니다.  
  
 기본 제공 속성은 ADO에서 구현 되 고 구문을 사용 하 여 새 개체에서 즉시 사용할 수 있는 속성입니다 `MyObject.Property` . 이러한 속성은 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 **속성** 개체로 표시 되지 않으므로 해당 값을 변경할 수 있지만 특성을 수정할 수는 없습니다.  
  
 동적 속성은 기본 데이터 공급자에 의해 정의 되 고 해당 ADO 개체의 **properties** 컬렉션에 표시 됩니다. 예를 들어 공급자와 관련 된 속성은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체가 트랜잭션을 지원 하는지 또는 업데이트를 지원 하는지 여부를 나타낼 수 있습니다. 이러한 추가 속성은 해당 **레코드 집합** 개체의 **속성** 컬렉션에 **속성** 개체로 표시 됩니다. 동적 속성은 또는 구문을 사용 하 여 컬렉션을 통해서만 참조할 수 있습니다 `MyObject.Properties(0)` `MyObject.Properties("Name")` .  
  
 두 종류의 속성을 모두 삭제할 수는 없습니다.  
  
 동적 **속성** 개체에는 자체의 기본 제공 속성 4 개가 있습니다.  
  
-   [Name](../../../ado/reference/ado-api/name-property-ado.md) 속성은 속성을 식별 하는 문자열입니다.  
  
-   [Type](../../../ado/reference/ado-api/type-property-ado.md) 속성은 속성 데이터 형식을 지정 하는 정수입니다.  
  
-   [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성은 속성 설정을 포함 하는 변형입니다. **Value** 는 **속성** 개체의 기본 속성입니다.  
  
-   [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md) 속성은 공급자와 관련 된 속성의 특징을 나타내는 long 값입니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [속성 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Command 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
