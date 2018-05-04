---
title: Delete 메서드를 사용 하 여 레코드를 삭제 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36a6a7e7f2ecd6deb3b25a2d2ed6dc65c8b6f98d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="deleting-records-using-the-delete-method"></a>Delete 메서드를 사용 하 여 레코드 삭제
사용 하는 **삭제** 현재 레코드 또는 그룹에 있는 레코드의 메서드를 표시 한 **레코드 집합** 개체를 삭제 합니다. 경우는 **레코드 집합** 개체 하지 못하도록 레코드 삭제 오류가 발생 합니다. 즉시 업데이트 모드에 있는 경우 삭제는 데이터베이스에 즉시 수행 합니다. 레코드를 호출한 후 편집 모드에 유지 됩니다 (위반으로 인해 데이터베이스 무결성 예를 들어) 레코드를 성공적으로 삭제할 수 없으면, **업데이트 합니다.** 사용 하 여 업데이트를 취소 해야 하는 것이 즉 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 현재 레코드를 이동 하기 전에 (예를 들어를 사용 하 여 [닫기](../../../ado/reference/ado-api/close-method-ado.md), [이동](../../../ado/reference/ado-api/move-method-ado.md), 또는 [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 레코드 캐시에서 삭제에 대 한 표시 되 고 호출 하는 경우 발생 하는 실제 삭제 일괄 업데이트 모드에 있는 경우는 **UpdateBatch** 메서드. (삭제 된 레코드를 보려면 설정에서 **필터** 속성을 **adFilterAffectedRecords** 후 **삭제** 호출 됩니다.)  
  
 삭제 된 레코드에서 필드 값을 검색 하려고 해도 오류가 발생 합니다. 현재 레코드를 삭제 한 후 삭제 된 레코드가 다른 레코드로 이동할 때까지 현재 남아 있습니다. 한 번 멀리 이동 하면 삭제 된 레코드는 액세스할 수 없게 합니다.  
  
 트랜잭션에서 삭제 작업을 중첩 하는 경우 사용 하 여 삭제 된 레코드를 복구할 수 있습니다는 **RollbackTrans** 메서드. 사용 하 여 삭제 보류 중 또는 그룹을 삭제 보류 중인 일괄 업데이트 모드에 있는 경우 취소할 수 있습니다는 **CancelBatch** 메서드.  
  
 원본 데이터와 충돌이 발생 하 여 레코드를 삭제 시도가 실패 하면 (예를 들어 레코드 이미 삭제 되었습니다 다른 사용자에 의해), 공급자에 대 한 경고를 반환 된 **오류** 컬렉션 하지만 프로그램을 중단 하지 않습니다 실행 합니다. 런타임 오류는 요청 된 모든 레코드에 충돌이 있는 경우에 발생 합니다.  
  
 경우는 **고유 테이블** 동적 속성을 설정 및 **레코드 집합** 은 실행 중인 여러 테이블에서 조인 작업의 결과 **삭제** 메서드는 행만 삭제 됩니다 에 지정 된 테이블에서의 **고유 테이블** 속성입니다.  
  
 **삭제** 레코드의 영향을 받는 지정할 수 있는 선택적 인수를 사용 하는 메서드는 **삭제** 작업 합니다. 이 인수에 유효한 값은 다음 ADO의 **AffectEnum** 상수를 열거 합니다.  
  
-   **adAffectCurrent** 현재 레코드에만 영향을 줍니다.  
  
-   **adAffectGroup** 현재 만족 하는 레코드에만 영향을 줍니다 **필터** 속성을 설정 합니다. **필터** 속성으로 설정 되어 있어야는 **FilterGroupEnum** 값 또는 배열 **책갈피** 이 옵션을 사용 하도록 합니다.  
  
 다음 코드를 지정 하는 예를 보여 줍니다. **adAffectGroup** 호출 하는 경우는 **삭제** 메서드. 이 샘플에 일부 레코드를 추가 하는이 예제 **레코드 집합** 는 데이터베이스를 업데이트 합니다. 필터링 하 여 다음의 **레코드 집합** 를 사용 하 여는 **adFilterAffectedRecords** 필터 열거형된 상수는 새로 추가 된 레코드만에 표시 된 상태로 **레코드 집합입니다.** 마지막으로 호출 하 여 **삭제** 메서드 되도록 지정 현재를 만족 하는 레코드의 모든 **필터** 속성 설정 (새 레코드)을 삭제 해야 합니다.  
  
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
