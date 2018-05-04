---
title: UnderlyingValue 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72962e5ba9b99f93c21547370e110706bdf0ee0e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="underlyingvalue-property"></a>UnderlyingValue 속성
현재 값을 표시 한 [필드](../../../ado/reference/ado-api/field-object.md) 데이터베이스의 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **Variant** 의 값을 나타내는 값은 **필드**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **UnderlyingValue** 속성 데이터베이스에서 현재 필드 값을 반환 합니다. 필드 값에는 **UnderlyingValue** 속성은 트랜잭션이 게 표시 되 고 다른 트랜잭션에 의해 최근 업데이트의 결과 얻을 수 있는 값입니다. 다를 수 있습니다이 [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 원래 반환 된 값을 반영 하는 속성은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
 이것은 사용 하 여 비슷합니다는 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드를 되지만 **UnderlyingValue** 속성은 현재 레코드에서 특정 필드에 대 한 값만을 반환 합니다. 이 동일 값는 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드 사용 하 여 대체는 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성.  
  
 이 속성을 사용 하는 경우는 **OriginalValue** 속성을 일괄 처리 업데이트에서 발생 하는 충돌을 해결할 수 있습니다.  
  
## <a name="record"></a>레코드  
 에 대 한 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체의 경우이 속성은 앞에 추가 하는 필드에 대 한 채워지지 [업데이트](../../../ado/reference/ado-api/update-method.md) 호출 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [OriginalValue 및 UnderlyingValue 속성 예제 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 및 UnderlyingValue 속성 예제 (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue 속성 (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Resync 메서드](../../../ado/reference/ado-api/resync-method.md)
