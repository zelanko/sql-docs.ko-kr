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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68ca8ac6d223100f437a7ba0ca8bf7776953d40a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789721"
---
# <a name="resync-method"></a>Resync 메서드
현재 데이터를 새로 고칩니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 기본 데이터베이스 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>매개 변수  
 *AffectRecords*  
 (선택 사항) [AffectEnum](../../../ado/reference/ado-api/affectenum.md) 레코드 수를 결정 하는 값을 **다시 동기화** 메서드 적용 됩니다. 기본값은 **adAffectAll**합니다. 이 값을 사용 하 여 사용할 수 없습니다는 **다시 동기화** 메서드는 **필드** 의 컬렉션을 **레코드** 개체입니다.  
  
 *ResyncValues*  
 (선택 사항) A [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) 원본 값을 덮어쓸지 여부를 지정 하는 값입니다. 기본값은 **adResyncAllValues**합니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="recordset"></a>레코드 집합  
 사용 합니다 **Resync** 현재에서 레코드를 다시 동기화 하는 방법 **레코드 집합** 기본 데이터베이스를 사용 하 여 합니다. 정적 또는 정방향 전용 커서를 사용 하지만 기본 데이터베이스의 변경 내용을 확인 하려는 경우에 유용 합니다.  
  
 설정 하는 경우는 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**를 **Resync** 에 제공 됩니다 읽기 전용이 아닌 **레코드 집합** 개체입니다.  
  
 달리 합니다 [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드를를 **다시 동기화** 메서드 다시 실행 되지 않습니다는 **레코드 집합** 개체의 기본 명령입니다. 기본 데이터베이스에서 새 레코드를 볼 수 있습니다.  
  
 다시 동기화 할 원본 데이터와 충돌로 인해 실패 하는 경우 (예를 들어, 레코드에 된 다른 사용자가 삭제), 공급자에 대 한 경고를 반환 합니다 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션 및 런타임 오류를 발생 합니다. 사용 합니다 [필터](../../../ado/reference/ado-api/filter-property.md) 속성 (**adFilterConflictingRecords**) 및 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 사용 하 여 충돌 레코드를 찾습니다.  
  
 경우는 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 및 [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) 동적 속성을 설정 하며 **레코드 집합** 여러 테이블을 다음 합니다 에서조인작업을실행한결과 **다시 동기화** 메서드는에 지정 된 명령을 실행 합니다는 **Resync Command** 테이블에서 명명 된 속성을 **고유 테이블** 속성.  
  
## <a name="fields"></a>필드  
 사용 하 여는 **다시 동기화** 의 값을 다시 동기화 하는 방법 합니다 **필드** 의 컬렉션을 **레코드** 내부 데이터 소스를 사용 하 여 개체. 합니다 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성이이 메서드에 의해 영향을 받지 않습니다.  
  
 하는 경우 *ResyncValues* 로 설정 된 **adResyncAllValues** (기본값)를 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)를 [값](../../../ado/reference/ado-api/value-property-ado.md), 및 [ OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 속성을 [필드](../../../ado/reference/ado-api/field-object.md) 컬렉션의 개체 동기화 됩니다. 하는 경우 *ResyncValues* 로 설정 되어 **adResyncUnderlyingValues**만 합니다 **UnderlyingValue** 속성 동기화 됩니다.  
  
 값을 **상태** 각각에 대 한 속성 **필드** 호출 시 개체의 동작에도 영향을 줍니다 **다시 동기화**합니다. 에 대 한 **필드** 이 있는 개체 **상태** 의 값 **adFieldPendingUnknown** 하거나 **adFieldPendingInsert**, **다시 동기화**  영향을 주지 않습니다. 에 대 한 **상태** 의 값 **adFieldPendingChange** 또는 **adFieldPendingDelete**, **Resync** 필드에 대 한 데이터 값을 동기화 하는 데이터 원본에 여전히 존재 합니다.  
  
 **다시 동기화** 수정 하지 것입니다 **상태** 의 값 **필드** 오류가 발생 하지 않는 한 개체 때 **재 동기화** 라고 합니다. 예를 들어, 필드를 더 이상 존재 하는 경우는 공급자가 반환 하는 적절 한 **상태** 에 대 한 값을 **필드** 개체로 **adFieldDoesNotExist**합니다. 반환 **상태** 의 값 내의 값을 논리적으로 결합할 수 있습니다 합니다 **상태** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Resync 메서드 예제 (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Resync 메서드 예제 (VC + +)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [UnderlyingValue 속성](../../../ado/reference/ado-api/underlyingvalue-property.md)
