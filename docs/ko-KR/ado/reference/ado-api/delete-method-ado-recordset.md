---
title: Delete 메서드 (ADO 레코드 집합) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b78659a62de2a968f107ff81518c72e12010c57
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="delete-method-ado-recordset"></a>Delete 메서드 (ADO 레코드 집합)
현재 레코드 또는 레코드의 그룹을 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>매개 변수  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md) 레코드를 결정 하는 값은 **삭제** 메서드에 영향을 줍니다. 기본값은 **adAffectCurrent**합니다.  
  
> [!NOTE]
>  **adAffectAll** 및 **adAffectAllChapters** 에 유효한 인수가 **삭제**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하는 **삭제** 현재 레코드 또는 그룹에 있는 레코드의 메서드를 표시 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 삭제 합니다. 경우는 **레코드 집합** 개체 허용 하지 않습니다 레코드 삭제 오류가 발생 합니다. 즉시 업데이트 모드에 있는 경우 삭제는 데이터베이스에 즉시 수행 합니다. 레코드를 호출한 후 편집 모드에 유지 됩니다 (위반으로 인해 데이터베이스 무결성 예를 들어) 레코드를 성공적으로 삭제할 수 없으면, [업데이트](../../../ado/reference/ado-api/update-method.md)합니다. 즉,와 업데이트를 취소 해야 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 현재 레코드를 이동 하기 전에 (예: [닫기](../../../ado/reference/ado-api/close-method-ado.md), [이동](../../../ado/reference/ado-api/move-method-ado.md), 또는 [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 레코드 캐시에서 삭제에 대 한 표시 되 고 호출 하는 경우 발생 하는 실제 삭제 일괄 업데이트 모드에 있는 경우는 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드. 사용 하 여는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성이 삭제 된 레코드를 볼 수 있습니다.  
  
 삭제 된 레코드에서 필드 값을 검색 해도 오류가 발생 합니다. 현재 레코드를 삭제 한 후 삭제 된 레코드가 다른 레코드로 이동할 때까지 현재 남아 있습니다. 한 번 멀리 이동 하면 삭제 된 레코드는 액세스할 수 없게 합니다.  
  
 트랜잭션에서 삭제 작업을 중첩 하는 경우와 삭제 된 레코드를 복구할 수 있습니다는 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드. 삭제 보류 중 또는 그룹을 삭제 된 보류 중인 일괄 업데이트 모드에 있는 경우 취소할 수 있습니다는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드.  
  
 원본 데이터와 충돌이 발생 하 여 레코드를 삭제 시도가 실패 하면 (예를 들어 레코드 이미 삭제 되었습니다 다른 사용자에 의해), 공급자에 대 한 경고를 반환 된 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션 하지만 프로그램을 중단 하지 않습니다 실행 합니다. 런타임 오류는 요청 된 모든 레코드에 충돌이 있는 경우에 발생 합니다.  
  
 경우는 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 동적 속성을 설정 및 **레코드 집합** 여러 테이블에서 조인 작업을 실행 한 결과 하면 **삭제** 메서드는 삭제 에 지정 된 테이블의 행은 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [삭제 (VB) 메서드 예제](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [삭제 메서드 (VBScript) 예제](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [삭제 메서드 예제 (VC + +)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO Parameters 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 메서드(ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
