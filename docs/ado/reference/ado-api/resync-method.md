---
title: Resync 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6907bfa9b83370074db9d9e2e522ed49d2c96e7e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243214"
---
# <a name="resync-method"></a>Resync 메서드
현재 레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 [Record](../../../ado/reference/ado-api/record-object-ado.md) 개체의 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 있는 데이터를 기본 데이터베이스에서 새로 고칩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>매개 변수  
 *AffectRecords*  
 (선택 사항) 다시 **동기화** 방법이 영향을 줄 수 있는 레코드 수를 결정 하는 [AffectEnum](../../../ado/reference/ado-api/affectenum.md) 값입니다. 기본값은 **adAffectAll**입니다. **Record** 개체의 **Fields** 컬렉션에 대 한 **Resync** 메서드에서는이 값을 사용할 수 없습니다.  
  
 *ResyncValues*  
 (선택 사항) 내부 값을 덮어쓸지 여부를 지정 하는 [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) 값입니다. 기본값은 **adResyncAllValues**입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="recordset"></a>레코드 집합  
 **Resync** 메서드를 사용 하 여 현재 **레코드 집합** 의 레코드를 기본 데이터베이스와 다시 동기화 합니다. 이는 정적 또는 전진 전용 커서를 사용 하지만 기본 데이터베이스에서 변경 내용을 확인 하려는 경우에 유용 합니다.  
  
 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정 하는 경우 읽기 전용이 아닌 **레코드 집합** 개체에 대해서만 다시 **동기화** 를 사용할 수 있습니다.  
  
 [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드와 달리 **Resync** 메서드는 **레코드 집합** 개체의 기본 명령을 다시 실행 하지 않습니다. 기본 데이터베이스의 새 레코드는 표시 되지 않습니다.  
  
 원본 데이터와의 충돌 때문에 다시 동기화 하려는 시도가 실패 하는 경우 (예: 다른 사용자가 레코드를 삭제 한 경우) 공급자는 [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션에 경고를 반환 하 고 런타임 오류가 발생 합니다. [Filter](../../../ado/reference/ado-api/filter-property.md) 속성 (**AdFilterConflictingRecords**) 및 [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 사용 하 여 충돌이 발생 한 레코드를 찾을 수 있습니다.  
  
 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 및 다시 [동기화 명령](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) 동적 속성을 설정 하 고 **레코드 집합** 을 여러 테이블에 대해 조인 작업을 실행 한 결과, 다시 **동기화** 메서드는 **unique Table** 속성에 명명 된 테이블에 대해서만 **resync 명령** 속성에 지정 된 명령을 실행 합니다.  
  
## <a name="fields"></a>필드  
 **Resync** 메서드를 사용 하 여 **Record** 개체의 **Fields** 컬렉션 값을 기본 데이터 원본과 다시 동기화 합니다. [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성은이 메서드의 영향을 받지 않습니다.  
  
 *ResyncValues* 가 **adResyncAllValues** (기본값)로 설정 된 경우 컬렉션에 있는 [Field](../../../ado/reference/ado-api/field-object.md) 개체의 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md), [value](../../../ado/reference/ado-api/value-property-ado.md)및 [originalvalue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 속성이 동기화 됩니다. *ResyncValues* 을 **adResyncUnderlyingValues**로 설정 하면 **UnderlyingValue** 속성만 동기화 됩니다.  
  
 호출 시 각 **Field** 개체의 **Status** 속성 값도 다시 **동기화**동작에 영향을 줍니다. **Adfieldpendingunknown** 또는 **Adfieldpendingunknown**의 **상태** 값이 있는 **Field** 개체의 경우 **Resync** 는 영향을 주지 않습니다. **Adfieldpendingchange** 또는 **Adfieldpendingdelete**의 **상태** 값에 대해 다시 **동기화** 는 데이터 원본에 여전히 존재 하는 필드에 대 한 데이터 값을 동기화 합니다.  
  
 다시 **동기화는** 다시 **동기화** 가 호출 될 때 오류가 발생 하지 않는 한 **필드** 개체의 **상태** 값을 수정 하지 않습니다. 예를 들어 필드가 더 이상 존재 하지 않는 경우 공급자는 **adFieldDoesNotExist**와 같은 **field** 개체에 대 한 적절 한 **상태** 값을 반환 합니다. 반환 된 **상태** 값은 **상태** 속성의 값 내에서 논리적으로 조합할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [Resync 메서드 예제 (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Resync 메서드 예제 (VC + +)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [UnderlyingValue 속성](../../../ado/reference/ado-api/underlyingvalue-property.md)
