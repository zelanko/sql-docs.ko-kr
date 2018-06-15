---
title: 레코드 업데이트에 대 한 필터링 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 529845297ff3c4264cc152c652b31c0bd12f5441
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270882"
---
# <a name="filtering-for-updated-records"></a>업데이트 된 레코드 필터링
UpdateBatch을 호출 하기 전에 레코드 집합을 연 이후 변경 된 레코드에만 보려는 Recordset Filter 속성 또는 UpdateBatch에 대 한 마지막 호출을 사용할 수 있습니다. 이 작업을 수행 하려면 필터를 그 다음 섹션의 코드 예제에 나와 있는 것 처럼 레코드 수가 업데이트 됩니다 확인 하려면 같음 설정 합니다.  
  
## <a name="remarks"></a>Remarks  
 이 예제는 고 하 여 바로 전에 호출 된 UpdateBatch 레코드 집합 필터링, 사용자 레코드를 변경 합니다 (CancelBatch 메서드를 사용 하 여) 업데이트를 취소할 수 있도록 이전 UpdateBatch 예제를 확장 합니다.  
  
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
