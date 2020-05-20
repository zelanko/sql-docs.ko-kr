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
author: rothja
ms.author: jroth
ms.openlocfilehash: c5747704601e5e325624c79ce853526e36f6cbe1
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765604"
---
# <a name="delete-method-ado-recordset"></a>Delete 메서드(ADO 레코드 집합)
현재 레코드 또는 레코드 그룹을 삭제 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>매개 변수  
 *AffectRecords*  
 **삭제** 메서드에서 영향을 주는 레코드 수를 결정 하는 [AffectEnum](../../../ado/reference/ado-api/affectenum.md) 값입니다. 기본값은 **adAffectCurrent**입니다.  
  
> [!NOTE]
>  **adAffectAll** 및 **adAffectAllChapters** 은 **삭제할**수 있는 인수가 아닙니다.  
  
## <a name="remarks"></a>설명  
 **Delete** 메서드를 사용 하면 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 레코드 그룹 또는 현재 레코드를 삭제 하도록 표시 합니다. 레코드 **집합** 개체가 레코드 삭제를 허용 하지 않으면 오류가 발생 합니다. 즉시 업데이트 모드에 있는 경우 데이터베이스에서 즉시 삭제가 발생 합니다. 예를 들어 데이터베이스 무결성 위반으로 인해 레코드를 삭제할 수 없는 경우 [업데이트](../../../ado/reference/ado-api/update-method.md)를 호출한 후에도 레코드는 편집 모드로 유지 됩니다. 즉, 현재 레코드 (예: [Close](../../../ado/reference/ado-api/close-method-ado.md), [Move](../../../ado/reference/ado-api/move-method-ado.md)또는 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md))를 이동 하기 전에 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 로 업데이트를 취소 해야 합니다.  
  
 일괄 업데이트 모드에 있는 경우 레코드가 캐시에서 삭제 되도록 표시 되 고 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드를 호출 하면 실제 삭제가 발생 합니다. [필터](../../../ado/reference/ado-api/filter-property.md) 속성을 사용 하 여 삭제 된 레코드를 볼 수 있습니다.  
  
 삭제 된 레코드에서 필드 값을 검색 하면 오류가 발생 합니다. 현재 레코드를 삭제 한 후에는 다른 레코드로 이동할 때까지 삭제 된 레코드는 최신 상태로 유지 됩니다. 삭제 된 레코드에서 멀리 이동 하면 더 이상 액세스할 수 없습니다.  
  
 트랜잭션에 삭제를 중첩 하는 경우 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 메서드를 사용 하 여 삭제 된 레코드를 복구할 수 있습니다. 일괄 업데이트 모드에 있는 경우 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 사용 하 여 보류 중인 삭제 또는 보류 중인 삭제 그룹을 취소할 수 있습니다.  
  
 원본 데이터와의 충돌 때문에 레코드를 삭제 하려는 시도가 실패 한 경우 (예: 다른 사용자가 레코드를 이미 삭제 한 경우) 공급자는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션에 대 한 경고를 반환 하지만 프로그램 실행을 중단 하지는 않습니다. 요청 된 모든 레코드에 충돌이 있는 경우에만 런타임 오류가 발생 합니다.  
  
 [Unique table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) dynamic 속성을 설정 하 고 **레코드 집합** 을 여러 테이블에서 조인 작업을 실행 한 결과 이면 **delete** 메서드는 [Unique table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 속성의 테이블 에서만 행을 삭제 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Delete 메서드 예제 (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete 메서드 예제 (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Delete 메서드 예제 (VC + +)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete 메서드 (ADO Fields Collection)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO Parameters Collection)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 메서드(ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
