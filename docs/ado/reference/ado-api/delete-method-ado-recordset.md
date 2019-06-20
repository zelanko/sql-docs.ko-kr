---
title: Delete 메서드 (ADO 레코드 집합) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fab7baf1771ad0600f4c1a0a8cac931f0adcc0a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695423"
---
# <a name="delete-method-ado-recordset"></a>Delete 메서드(ADO 레코드 집합)
현재 레코드 또는 레코드 그룹을 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>매개 변수  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md) 레코드 수를 결정 하는 값을 **삭제** 메서드 적용 됩니다. 기본값은 **adAffectCurrent**합니다.  
  
> [!NOTE]
>  **adAffectAll** 하 고 **adAffectAllChapters** 에 유효한 인수 없는 **삭제**합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하는 **삭제** 메서드는 현재 레코드 또는 레코드의 그룹을 표시를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 삭제 합니다. 경우는 **레코드 집합** 개체 허용 하지 않습니다 레코드 삭제 오류가 발생 합니다. 즉시 업데이트 모드에 있는 경우 삭제는 데이터베이스에 즉시 발생 합니다. 호출한 후 레코드를 편집 모드로 유지 됩니다 (으로 인해 데이터베이스 무결성 위반, 예를 들어) 레코드를 성공적으로 삭제할 수 없습니다, 하는 경우 [업데이트](../../../ado/reference/ado-api/update-method.md)합니다. 즉, 사용 하 여 업데이트를 취소 해야 하면 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 현재 레코드를 이동 하기 전에 (예를 들어 [닫기](../../../ado/reference/ado-api/close-method-ado.md)합니다 [이동](../../../ado/reference/ado-api/move-method-ado.md), 또는 [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 일괄 업데이트 모드에 있는 경우 레코드를 캐시에서 삭제 표시 되 고 호출 하는 경우 발생 하는 실제 삭제 합니다 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드. 사용 하 여 합니다 [필터](../../../ado/reference/ado-api/filter-property.md) 속성이 삭제 된 레코드를 볼 수 있습니다.  
  
 삭제 된 레코드에서 필드 값을 검색 하는 오류가 발생 합니다. 현재 레코드를 삭제 한 후 삭제 된 레코드는 다른 레코드로 이동할 때까지 현재 남아 있습니다. 한 번 멀리 이동 하면 삭제 된 레코드는 것이 더 이상 액세스할 수 없습니다.  
  
 트랜잭션에서 삭제 작업을 중첩 하는 경우 사용 하 여 삭제 된 레코드를 복구할 수 있습니다 합니다 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드. 일괄 업데이트 모드에 있는 보류 중인 삭제 또는 삭제 된 보류 중인 그룹을 취소할 수 있습니다 합니다 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드.  
  
 기본 데이터 충돌로 인해 실패 하면 레코드를 삭제 하려고 (예를 들어, 레코드에 이미 삭제 된 다른 사용자에 의해), 공급자에 대 한 경고를 반환 합니다 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션 프로그램을 중단 하지는 않습니다 하지만 실행 합니다. 런타임 오류는 요청 된 모든 레코드에 충돌이 있는 경우에 발생 합니다.  
  
 경우는 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 동적 속성을 설정 하며 **레코드 집합** 여러 테이블에서 조인 작업을 실행 한 결과 해당 **삭제** 메서드는 삭제만 에 지정 된 테이블에서 행을 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Delete 메서드 예제 (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete 메서드 예제 (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Delete 메서드 예제 (VC + +)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO 매개 변수 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 메서드(ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
