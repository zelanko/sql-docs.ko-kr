---
title: 업데이트 된 레코드에 대 한 필터링 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 70f74c9c3782cb8da5a12f5b785e410356a2c088
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700712"
---
# <a name="filtering-for-updated-records"></a>업데이트된 레코드 필터링
UpdateBatch을 호출 하기 전에 레코드 집합을 연 후 변경 된 레코드만 표시할 레코드 집합 필터 속성 또는 UpdateBatch 마지막 호출을 사용할 수 있습니다. 이렇게 하려면 필터를 그 다음 섹션의 코드 예제에 표시 된 대로 업데이트할 레코드 수를 확인 하려면 같음 설정 합니다.  
  
## <a name="remarks"></a>Remarks  
 이 예제는 UpdateBatch 호출 직전 레코드 집합을 필터링 하 고 레코드를 변경 하는 사용자를 보여 주는 (CancelBatch 메서드 사용) 업데이트를 취소할 수 있도록 하 여 이전 UpdateBatch 예제를 확장 합니다.  
  
```  
'BeginFilterPend  
    '...  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    objRs1.Filter = adFilterPendingRecords  
  
    MsgBox "There are " & objRs1.RecordCount & " records pending.", _  
            , "Filter Pending"  
  
    ' Cancel the updates  
    objRs1.CancelBatch  
'EndFilterPend  
```  
  
## <a name="see-also"></a>관련 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
