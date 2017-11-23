---
title: "메서드를 다시 동기화 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords: Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8fe3a2a123061cd0fc4de31d2b08ab82d41f7542
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="resync-method"></a>Resync 메서드
현재에서 데이터를 새로 고칩니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션은 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 기본 데이터베이스에서 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>매개 변수  
 *AffectRecords*  
 (선택 사항) [AffectEnum](../../../ado/reference/ado-api/affectenum.md) 레코드를 결정 하는 값은 **Resync** 메서드에 영향을 줍니다. 기본값은 **adAffectAll**합니다. 이 값은 사용할 수 없습니다는 **Resync** 의 메서드는 **필드** 의 컬렉션은 **레코드** 개체입니다.  
  
 *ResyncValues*  
 (선택 사항) A [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) 원본 값을 덮어쓸지 여부를 지정 하는 값입니다. 기본값은 **adResyncAllValues**합니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="recordset"></a>레코드 집합  
 사용 하 여는 **Resync** 메서드 현재에서 레코드를 다시 동기화를 **레코드 집합** 내부 데이터베이스와 합니다. 정적 또는 정방향 전용 커서를 사용 하는 기본 데이터베이스의 변경 내용을 보려는 경우 유용 합니다.  
  
 설정 하는 경우는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**, **Resync** 은 에서만 사용할 수 읽기 전용이 아닌 **레코드 집합** 개체입니다.  
  
 와 달리는 [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드를는 **Resync** 메서드를 다시 실행 하지 않습니다는 **레코드 집합** 개체 명령 원본으로 사용 합니다. 기본 데이터베이스에 새 레코드를 볼 수 없게 됩니다.  
  
 원본 데이터와 충돌이 발생 하 여 다시 동기화 할 경우 실패 (예를 들어 레코드가 삭제 되었습니다 다른 사용자에 의해), 공급자에 대 한 경고를 반환는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션 및 런타임 오류가 발생 합니다. 사용 하 여는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성 (**adFilterConflictingRecords**) 및 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성 충돌 레코드를 찾을 수 있습니다.  
  
 경우는 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 및 [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) 동적 속성을 설정 및 **레코드 집합** 는 다음여러테이블에서조인작업을실행한결과 **다시 동기화** 메서드는에 지정 된 명령을 실행 합니다.는 **Resync Command** 속성에 명명 된 테이블에 대해서만 **고유 테이블** 속성입니다.  
  
## <a name="fields"></a>필드  
 사용 하 여는 **Resync** 메서드는 값의 다시 동기화를 **필드** 의 컬렉션은 **레코드** 데이터 원본 개체입니다. [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성이이 메서드에 의해 영향을 받지 않습니다.  
  
 경우 *ResyncValues* 로 설정 된 **adResyncAllValues** (기본값)는 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md), [값](../../../ado/reference/ado-api/value-property-ado.md), 및 [ OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 의 속성 [필드](../../../ado/reference/ado-api/field-object.md) 개체 컬렉션에 동기화 됩니다. 경우 *ResyncValues* 로 설정 된 **adResyncUnderlyingValues**만 **UnderlyingValue** 속성 동기화 됩니다.  
  
 값은 **상태** 각 속성이 **필드** 메서드를 호출할 때에는 개체의 동작에도 영향을 줍니다 **다시 동기화**합니다. 에 대 한 **필드** 개체 **상태** 값 **adFieldPendingUnknown** 또는 **adFieldPendingInsert**, **다시 동기화**  영향을 주지 않습니다. 에 대 한 **상태** 값 **adFieldPendingChange** 또는 **adFieldPendingDelete**, **Resync** 필드에 대 한 데이터 값을 동기화 하는 데이터 원본에 여전히 존재 합니다.  
  
 **다시 동기화** 수정 하지는 것입니다 **상태** 값 **필드** 오류가 발생 하지 않는 한 개체 때 **다시 동기화** 호출 됩니다. 예를 들어 필드가 더 이상 존재 하는 경우 하면 공급자는 반환 적절 한 **상태** 에 대 한 값은 **필드** 와 같은 개체를 **adFieldDoesNotExist**합니다. 반환 된 **상태** 값으로 값을 논리적으로 결합할 수는 **상태** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [메서드 예제 (VB)를 다시 동기화](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Resync 메서드 예제 (VC + +)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [UnderlyingValue 속성](../../../ado/reference/ado-api/underlyingvalue-property.md)
