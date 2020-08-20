---
description: Delete 메서드를 사용하여 레코드 삭제
title: Delete 메서드를 사용 하 여 레코드 삭제 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d8a29f2e1f35ddddc28e4aa3fb3c52c649e3056
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453535"
---
# <a name="deleting-records-using-the-delete-method"></a>Delete 메서드를 사용하여 레코드 삭제
**Delete** 메서드를 사용 하면 **레코드 집합** 개체의 레코드 그룹 또는 현재 레코드를 삭제 하도록 표시 합니다. 레코드 **집합** 개체가 레코드 삭제를 허용 하지 않는 경우 오류가 발생 합니다. 즉시 업데이트 모드에 있는 경우 데이터베이스에서 즉시 삭제가 발생 합니다. 예를 들어 데이터베이스 무결성 위반으로 인해 레코드를 삭제할 수 없는 경우 업데이트를 호출한 후에도 레코드는 편집 모드로 유지 됩니다 **.** 즉, 현재 레코드를 이동 하기 전에 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 를 사용 하 여 업데이트를 취소 해야 합니다 (예: [Close](../../../ado/reference/ado-api/close-method-ado.md), [Move](../../../ado/reference/ado-api/move-method-ado.md)또는 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)사용).  
  
 일괄 업데이트 모드에 있는 경우 레코드가 캐시에서 삭제 되도록 표시 되 고 **UpdateBatch** 메서드를 호출 하면 실제 삭제가 발생 합니다. 삭제 된 레코드를 보려면 **Delete** 를 호출한 후 **Filter** 속성을 **adFilterAffectedRecords** 로 설정 합니다.  
  
 삭제 된 레코드에서 필드 값을 검색 하려고 하면 오류가 생성 됩니다. 현재 레코드를 삭제 한 후에는 다른 레코드로 이동할 때까지 삭제 된 레코드는 최신 상태로 유지 됩니다. 삭제 된 레코드에서 멀리 이동 하면 더 이상 액세스할 수 없습니다.  
  
 트랜잭션에 삭제를 중첩 하는 경우 **RollbackTrans** 메서드를 사용 하 여 삭제 된 레코드를 복구할 수 있습니다. 일괄 업데이트 모드에 있는 경우 **CancelBatch** 메서드를 사용 하 여 보류 중인 삭제 또는 삭제 보류 중인 그룹을 취소할 수 있습니다.  
  
 원본 데이터와의 충돌 때문에 레코드를 삭제 하려는 시도가 실패 한 경우 (예: 다른 사용자가 레코드를 이미 삭제 한 경우) 공급자는 **오류** 컬렉션에 대 한 경고를 반환 하지만 프로그램 실행을 중단 하지는 않습니다. 요청 된 모든 레코드에 충돌이 있는 경우에만 런타임 오류가 발생 합니다.  
  
 **Unique table** dynamic 속성을 설정 하 고 **레코드 집합** 을 여러 테이블에서 조인 작업을 실행 한 결과 이면 **delete** 메서드는 **Unique table** 속성의 테이블 에서만 행을 삭제 합니다.  
  
 **Delete** 메서드는 선택적 인수를 사용 하 여 **삭제** 작업의 영향을 받는 레코드를 지정할 수 있습니다. 이 인수에 대 한 올바른 값은 다음 ADO **AffectEnum** 열거 상수 중 하나입니다.  
  
-   **adAffectCurrent** 현재 레코드에만 영향을 줍니다.  
  
-   **adAffectGroup** 현재 **필터** 속성 설정을 만족 하는 레코드에만 영향을 줍니다. 이 옵션을 사용 하려면 **필터** 속성을 **filtergroupenum** 값 또는 **책갈피** 배열로 설정 해야 합니다.  
  
 다음 코드에서는 **Delete** 메서드를 호출할 때 **adAffectGroup** 를 지정 하는 예를 보여 줍니다. 이 예에서는 예제 레코드 **집합** 에 일부 레코드를 추가 하 고 데이터베이스를 업데이트 합니다. 그런 다음 **adFilterAffectedRecords** filter 열거형 상수를 사용 하 여 **레코드 집합** 을 필터링 합니다. 그러면 새로 추가 된 레코드만 **레코드 집합에 표시 됩니다.** 마지막으로 **Delete** 메서드를 호출 하 고 현재 **필터** 속성 설정 (새 레코드)을 만족 하는 모든 레코드를 삭제 하도록 지정 합니다.  
  
```  
'BeginDeleteGroup  
    'add some bogus records  
    With objRs  
        For i = 0 To 8  
            .AddNew  
            .Fields("CompanyName") = "Shipper Number " & i + 1  
            .Fields("Phone") = "(425) 555-000" & (i + 1)  
            .Update  
        Next i  
  
        ' update  
        .UpdateBatch  
  
        'filter on newly added records  
        .Filter = adFilterAffectedRecords  
        Debug.Print "Deleting the " & .RecordCount & _  
                    " records you just added."  
  
        'delete the newly added bogus records  
        .Delete adAffectGroup  
        .Filter = adFilterNone  
        Debug.Print .RecordCount & " records remain."  
    End With  
'EndDeleteGroup  
```
