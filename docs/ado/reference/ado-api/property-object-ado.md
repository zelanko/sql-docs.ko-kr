---
title: 속성 개체 (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43bfa816a9ca8a93cdc1188a98e54d3e0d9111b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917551"
---
# <a name="property-object-ado"></a>속성 개체(ADO)
공급자가 정의한 ADO 개체의 동적 특성을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 ADO 개체에는 두 가지 유형의 속성: 기본 제공 및 동적입니다.  
  
 기본 제공 속성은 이러한 ado에서 구현 하 고 즉시 사용할 수 있는 새 개체 속성을 사용 하 여는 `MyObject.Property` 구문입니다. 로 표시 되지 않습니다 **속성** 개체의 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 특징을 수정할 수 없습니다. 해당 값을 변경할 수 있지만 있도록 합니다.  
  
 동적 속성은 기본 데이터 공급자가 정의 되 고에 표시 합니다 **속성** 적절 한 ADO 개체의 컬렉션입니다. 경우 공급자에 게 특정 속성을 나타낼 수 있습니다 예를 들어를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 트랜잭션이나 업데이트 개체를 지원 합니다. 이러한 추가 속성으로 나타납니다 **속성** 하는 개체 **Recordset** 개체의 **속성** 컬렉션입니다. 동적 속성 컬렉션을 통해서만 참조할 수 있습니다 사용 하는 `MyObject.Properties(0)` 또는 `MyObject.Properties("Name")` 구문입니다.  
  
 두 가지 속성을 삭제할 수 없습니다.  
  
 동적 **속성** 개체에는 자체의 네 가지 기본 제공 속성:  
  
-   합니다 [이름을](../../../ado/reference/ado-api/name-property-ado.md) 속성은 속성을 식별 하는 문자열입니다.  
  
-   합니다 [형식](../../../ado/reference/ado-api/type-property-ado.md) 속성은 속성 데이터 형식을 지정 하는 정수입니다.  
  
-   합니다 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성이 속성 설정이 포함 된 변형입니다. **값** 에 대 한 기본 속성을 **속성** 개체입니다.  
  
-   합니다 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성은 공급자와 관련 된 속성의 특성을 나타내는 long 값입니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Property 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [명령 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
