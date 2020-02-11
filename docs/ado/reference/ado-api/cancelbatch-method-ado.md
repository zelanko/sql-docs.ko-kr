---
title: CancelBatch 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f1c6a9f57d30b47641b9280e25a97336c28b0496
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920164"
---
# <a name="cancelbatch-method-ado"></a>CancelBatch 메서드(ADO)
보류 중인 일괄 처리 업데이트를 취소 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>매개 변수  
 *AffectRecords*  
 (선택 사항) **CancelBatch** 메서드가 영향을 줄 수 있는 레코드 수를 나타내는 [AffectEnum](../../../ado/reference/ado-api/affectenum.md) 값입니다.  
  
## <a name="remarks"></a>설명  
 **CancelBatch** 메서드를 사용 하 여 일괄 업데이트 모드에서 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 보류 중인 업데이트를 모두 취소할 수 있습니다. **레코드 집합이** 즉시 업데이트 모드에 있는 경우 **adAffectCurrent** 없이 **CancelBatch** 를 호출 하면 오류가 생성 됩니다.  
  
 현재 레코드를 편집 하거나 **CancelBatch**를 호출할 때 새 레코드를 추가 하는 경우 ADO는 먼저 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드를 호출 하 여 캐시 된 변경 내용을 취소 합니다. 그 후에는 **레코드 집합** 의 보류 중인 모든 변경 내용이 취소 됩니다.  
  
 **CancelBatch** 호출 후 현재 레코드를 확인할 수 없습니다. 특히 새 레코드를 추가 하는 프로세스에서 발생 한 것입니다. 이러한 이유로 **CancelBatch** 호출 후에 **레코드 집합** 의 알려진 위치로 현재 레코드 위치를 설정 하는 것이 좋습니다. 예를 들어 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 메서드를 호출 합니다.  
  
 기본 데이터와의 충돌 때문에 보류 중인 업데이트를 취소 하려는 시도가 실패 하는 경우 (예: 다른 사용자가 레코드를 삭제 한 경우) 공급자는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션에 대 한 경고를 반환 하지만 프로그램 실행을 중단 하지는 않습니다. 요청 된 모든 레코드에 충돌이 있는 경우에만 런타임 오류가 발생 합니다. [Filter](../../../ado/reference/ado-api/filter-property.md) 속성 (**AdFilterAffectedRecords**) 및 [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 사용 하 여 충돌이 발생 한 레코드를 찾을 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [UpdateBatch 및 CancelBatch 메서드 예제 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 및 CancelBatch 메서드 예제 (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel 메서드 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 메서드 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelUpdate 메서드 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 메서드 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 속성 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
