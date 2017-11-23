---
title: "UpdateBatch 메서드 | Microsoft Docs"
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
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords: UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1522f6165e08a2a45cbd35e0b66d996ad93c1c4c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="updatebatch-method"></a>UpdateBatch 메서드
모든 보류 중인 일괄 처리 업데이트를 디스크에 기록 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>매개 변수  
 *AffectRecords*  
 (선택 사항) [AffectEnum](../../../ado/reference/ado-api/affectenum.md) 레코드를 나타내는 값의 **UpdateBatch** 메서드에 영향을 줍니다.  
  
 *PreserveStatus*  
 (선택 사항) A **부울** 나타내듯이 현지 변경 여부를 지정 하는 값은 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 적용 해야 합니다. 이 값 설정 하는 경우 **True**, **상태** 업데이트가 완료 된 후 각 레코드의 속성 변경 되지 않습니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **UpdateBatch** 수정 하는 경우 메서드는 **레코드 집합** 일괄 업데이트 모드에서 변경한 모든 내용을 전송 하는 개체는 **레코드 집합** 를 기본 데이터베이스 개체입니다.  
  
 경우는 **레코드 집합** 를 호출 하기 전에 로컬로 하나 이상의 레코드의 여러 변경 내용을 캐시할 수 있습니다, 개체 지원 일괄 처리 업데이트는 **UpdateBatch** 메서드. 현재 레코드를 편집 하거나 호출 하는 경우 새 레코드를 추가 하는 경우는 **UpdateBatch** 메서드, ADO를 자동으로 호출 된 [업데이트](../../../ado/reference/ado-api/update-method.md) 하기 전에 현재 레코드에 보류 중인 변경 내용을 저장 하는 메서드 공급자에 게 일괄 처리 된 변경 내용을 전송 합니다. 키 집합 또는 정적 커서에만 사용 하 여 업데이트 하는 일괄 처리를 사용 해야 합니다.  
  
> [!NOTE]
>  지정 **adAffectGroup** 으로이 매개 변수의 값에 현재 표시 된 레코드 있을 때 오류가 발생 합니다 **레코드 집합** (예: 없는 레코드를 일치 하는 필터).  
  
 원본 데이터와 충돌이 발생 하 여 일부 또는 모든 레코드에 대 한 변경 내용을 전송할 시도가 실패 하면 (예를 들어 레코드 이미 삭제 되었습니다 다른 사용자에 의해), 공급자가 반환 하지 않을 경고는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션 및 런타임 오류가 발생합니다. 사용 하 여는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성 (**adFilterAffectedRecords**) 및 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성 충돌 레코드를 찾을 수 있습니다.  
  
 모든 보류 중인 일괄 처리 업데이트를 취소 하려면 사용 하 여는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드.  
  
 경우는 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 및 [업데이트 Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) 동적 속성을 설정 및 **레코드 집합** 여러 테이블에서 조인 작업을 실행 한 결과 경우 실행은 **UpdateBatch** 메서드 이어서 암시적으로 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 의 설정에 따라 메서드는 [업데이트 다시 동기화](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) 속성.  
  
 데이터 원본에 대해 일괄 처리의 개별 업데이트 실행 되는 순서 아닐 로컬에서 수행 되는 순서와 동일 하 게 **레코드 집합**합니다. 업데이트 순서 공급자에 따라 달라 집니다. 삽입 또는 업데이트 시 foreign key 제약 조건 등 서로 관련 된 업데이트 코드를 작성할 때이를 고려 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [UpdateBatch 및 CancelBatch 메서드 예제 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 및 CancelBatch 방법 예 (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 속성 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)
