---
title: UpdateBatch 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e9d74fe938ce486a4cd15573af8166dbed12ba6f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67937849"
---
# <a name="updatebatch-method"></a>UpdateBatch 메서드
모든 보류 중인 일괄 처리 업데이트를 디스크에 기록 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>매개 변수  
 *AffectRecords*  
 (선택 사항) **UpdateBatch** 메서드에서 영향을 줄 레코드 수를 나타내는 [AffectEnum](../../../ado/reference/ado-api/affectenum.md) 값입니다.  
  
 *PreserveStatus*  
 (선택 사항) [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성에 표시 된 대로 로컬 변경 내용을 커밋해야 하는지 여부를 지정 하는 **부울** 값입니다. 이 값을 **True**로 설정 하면 업데이트가 완료 된 후 각 레코드의 **Status** 속성이 변경 되지 않은 상태로 유지 됩니다.  
  
## <a name="remarks"></a>설명  
 일괄 업데이트 모드에서 **레코드 집합** 개체를 수정 하 여 **레코드 집합** 개체의 모든 변경 내용을 기본 데이터베이스로 전송 하려면 **UpdateBatch** 메서드를 사용 합니다.  
  
 **레코드 집합** 개체가 일괄 처리 업데이트를 지 원하는 경우 **UpdateBatch** 메서드를 호출할 때까지 하나 이상의 레코드에 대 한 여러 변경 내용을 로컬로 캐시할 수 있습니다. 현재 레코드를 편집 하거나 **UpdateBatch** 메서드를 호출할 때 새 레코드를 추가 하는 경우, ADO는 일괄 처리 된 변경 내용을 공급자에 전송 하기 전에 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 자동으로 호출 하 여 현재 레코드에 대 한 보류 중인 변경 내용을 저장 합니다. 일괄 처리 업데이트는 키 집합 또는 정적 커서로만 사용 해야 합니다.  
  
> [!NOTE]
>  **AdAffectGroup** 을이 매개 변수의 값으로 지정 하면 레코드가 일치 하지 않는 필터와 같은 현재 **레코드 집합** 에 표시 되는 레코드가 없는 경우 오류가 발생 합니다.  
  
 기본 데이터와의 충돌 때문에 (예: 다른 사용자가 레코드를 이미 삭제 한 경우) 변경 내용에 대 한 전송 시도에 실패 하는 경우 공급자는 [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션에 경고를 반환 하 고 런타임 오류가 발생 합니다. [Filter](../../../ado/reference/ado-api/filter-property.md) 속성 (**AdFilterAffectedRecords**) 및 [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 사용 하 여 충돌이 발생 한 레코드를 찾을 수 있습니다.  
  
 보류 중인 모든 일괄 처리 업데이트를 취소 하려면 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 사용 합니다.  
  
 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 및 업데이트 다시 [동기화](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) 동적 속성을 설정 하 고 레코드 집합을 여러 테이블에 대해 조인 작업을 실행 한 결과 **레코드 집합** 은 [업데이트 다시 동기화](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) 속성의 설정에 따라 암시적으로 다시 [동기화](../../../ado/reference/ado-api/resync-method.md) 메서드를 실행 합니다. **UpdateBatch**  
  
 일괄 처리의 개별 업데이트가 데이터 원본에서 수행 되는 순서는 로컬 **레코드 집합**에 대해 수행 된 순서와 동일할 필요는 없습니다. 업데이트 순서는 공급자에 따라 달라 집니다. 삽입 또는 업데이트에 대 한 foreign key 제약 조건과 같이 서로 관련 된 업데이트를 코딩 하는 경우이를 고려 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [UpdateBatch 및 CancelBatch 메서드 예제 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 및 CancelBatch 메서드 예제 (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 속성 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)
