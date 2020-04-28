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
ms.openlocfilehash: 0b5afe84664719da5a1dbc7777aef524be28c459
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925330"
---
# <a name="filtering-for-updated-records"></a>업데이트된 레코드 필터링
UpdateBatch를 호출 하기 전에 레코드 집합 필터 속성을 사용 하 여 레코드 집합을 연 이후 변경 된 레코드 또는 UpdateBatch에 대 한 마지막 호출을 볼 수 있습니다. 이렇게 하려면 다음 섹션의 코드 예제에 표시 된 것 처럼 필터를 adFilterPendingRecords로 설정 하 여 업데이트할 레코드 수를 결정 합니다.  
  
## <a name="remarks"></a>설명  
 이 예에서는 사용자가 UpdateBatch를 호출 하기 직전에 레코드 집합을 필터링 하 여 이전 UpdateBatch 예를 확장 하 고 레코드가 변경 되는 사용자를 표시 하 고 CancelBatch 메서드를 사용 하 여 업데이트를 취소할 수 있도록 허용 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
