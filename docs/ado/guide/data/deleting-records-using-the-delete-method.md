---
title: Delete 메서드를 사용 하 여 레코드를 삭제 합니다. | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b4798e2658bf23edaf7cd04fb819e26de2a55cc9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700822"
---
# <a name="deleting-records-using-the-delete-method"></a>Delete 메서드를 사용하여 레코드 삭제
사용 하는 **삭제** 메서드는 현재 레코드 또는 레코드의 그룹을 표시를 **레코드 집합** 개체를 삭제 합니다. 경우는 **레코드 집합** 개체 수 없도록 레코드 삭제 오류가 발생 합니다. 즉시 업데이트 모드에 있는 경우 삭제는 데이터베이스에 즉시 발생 합니다. 호출한 후 레코드를 편집 모드로 유지 됩니다 (으로 인해 데이터베이스 무결성 위반, 예를 들어) 레코드를 성공적으로 삭제할 수 없으면, **업데이트 합니다.** 이 사용 하 여 업데이트를 취소 해야 하는 것을 의미 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 현재 레코드를 이동 하기 전에 (예를 들어,를 사용 하 여 [닫기](../../../ado/reference/ado-api/close-method-ado.md)합니다 [이동](../../../ado/reference/ado-api/move-method-ado.md), 또는 [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 일괄 업데이트 모드에 있는 경우 레코드를 캐시에서 삭제 표시 되 고 호출 하는 경우 발생 하는 실제 삭제 합니다 **UpdateBatch** 메서드. (삭제 된 레코드를 보려면 다음을 설정 합니다 **필터** 속성을 **adFilterAffectedRecords** 후 **삭제** 라고 합니다.)  
  
 삭제 된 레코드에서 필드 값을 검색 하는 동안 오류가 발생 합니다. 현재 레코드를 삭제 한 후 삭제 된 레코드는 다른 레코드로 이동할 때까지 현재 남아 있습니다. 한 번 멀리 이동 하면 삭제 된 레코드는 것이 더 이상 액세스할 수 없습니다.  
  
 트랜잭션에서 삭제 작업을 중첩 하는 경우 사용 하 여 삭제 된 레코드를 복구할 수 있습니다 합니다 **RollbackTrans** 메서드. 일괄 업데이트 모드에 있는 보류 중인 삭제 또는 삭제 보류 중인 그룹을 사용 하 여 취소할 수는 **CancelBatch** 메서드.  
  
 기본 데이터 충돌로 인해 실패 하면 레코드를 삭제 하려고 (예를 들어, 레코드에 이미 삭제 된 다른 사용자에 의해), 공급자에 대 한 경고를 반환 합니다 **오류** 컬렉션 프로그램을 중단 하지는 않습니다 하지만 실행 합니다. 런타임 오류는 요청 된 모든 레코드에 충돌이 있는 경우에 발생 합니다.  
  
 경우는 **고유 테이블** 동적 속성을 설정 및 **레코드 집합** 은 여러 테이블에서 조인 작업을 실행 하는 결과 **삭제** 메서드는 행만 삭제 에 지정 된 테이블에서의 **고유 테이블** 속성입니다.  
  
 **삭제할** 영향을 받는 레코드를 지정할 수 있도록 선택적 인수를 사용 하는 메서드를 **삭제** 작업 합니다. 이 인수에만 유효한 값은 다음 ADO 중 하나 **AffectEnum** 상수를 열거 합니다.  
  
-   **adAffectCurrent** 현재 레코드에만 영향을 줍니다.  
  
-   **adAffectGroup** 현재 충족 하는 레코드에만 영향을 주는 **필터** 속성을 설정 합니다. **필터** 속성 설정 해야 합니다는 **FilterGroupEnum** 값 또는 배열을 **책갈피** 이 옵션을 사용 하도록 합니다.  
  
 다음 코드를 지정 하는 예를 보여 줍니다 **adAffectGroup** 를 호출할 때 합니다 **삭제** 메서드. 샘플에 몇 가지 레코드를 추가 하는이 예제 **레코드 집합** 하 고 데이터베이스를 업데이트 합니다. 필터링 한 다음 합니다 **레코드 집합** 사용 하 여는 **adFilterAffectedRecords** 필터 열거 상수에 새로 추가 된 레코드만에 표시 된 상태로 둡니다는 **레코드 집합입니다.** 마지막으로 호출 하는 **삭제** 메서드 지정 하 고 현재 충족 하는 레코드를 모두 **필터** 속성 설정 (새 레코드)를 삭제 해야 합니다.  
  
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
