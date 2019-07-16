---
title: UnderlyingValue 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 582d0b87edd4729ce54cc2a7323b0a63443cab82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938852"
---
# <a name="underlyingvalue-property"></a>UnderlyingValue 속성
현재 값을 나타내는 [필드](../../../ado/reference/ado-api/field-object.md) 데이터베이스의 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환을 **Variant** 의 값을 나타내는 값을 **필드**합니다.  
  
## <a name="remarks"></a>설명  
 사용 된 **UnderlyingValue** 속성을 데이터베이스에서 현재 필드 값을 반환 합니다. 필드 값을 **UnderlyingValue** 속성은 트랜잭션이에 표시 되 고 다른 트랜잭션에 의해 최근 업데이트의 결과 얻을 수 있는 값입니다. 다를 수 있습니다이 [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 원래 반환 된 값을 반영 하는 속성을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
 사용 하 여 비슷합니다는 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드를 하지만 **UnderlyingValue** 속성은 현재 레코드에서 특정 필드의 값만 반환 합니다. 동일 하는 값을 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드 사용 하 여 합니다 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성.  
  
 이 속성을 사용 하는 경우는 **OriginalValue** 속성인 일괄 업데이트에서 발생 하는 충돌을 해결할 수 있습니다.  
  
## <a name="record"></a>녹음  
 에 대 한 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체를이 속성 앞에 추가 하는 필드에 대 한 빈 됩니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 라고 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [OriginalValue 및 UnderlyingValue 속성 예제 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 및 UnderlyingValue 속성 예제 (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue 속성 (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Resync 메서드](../../../ado/reference/ado-api/resync-method.md)
