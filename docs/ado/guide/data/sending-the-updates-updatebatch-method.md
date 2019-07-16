---
title: '업데이트 보내기: UpdateBatch 메서드 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 182e444587ce9bb3ca73166fb05dfac2506a39aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924253"
---
# <a name="sending-the-updates-updatebatch-method"></a>업데이트 보내기: UpdateBatch 메서드
다음 코드는 adLockBatchOptimistic 및 adUseClient에 CursorLocation LockType 속성을 설정 하 여 일괄 처리 모드에서 레코드 집합을 엽니다. 두 개의 새 레코드를 추가 및 원래 값이 저장 된 기존 레코드의 필드 값을 변경 하 고 변경 내용을 다시 데이터 원본에 보낼 UpdateBatch 호출.  
  
## <a name="remarks"></a>설명  
  
```  
'BeginBatchUpdate  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT ShipperId, CompanyName, Phone FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
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
  
    ' Send the updates  
    objRs1.UpdateBatch  
'EndBatchUpdate  
```  
  
 현재 레코드를 편집 또는 UpdateBatch 메서드를 호출 하는 경우 새 레코드를 추가 하는 경우 ADO 공급자에 게 일괄 처리 된 변경 내용을 전송 하기 전에 현재 레코드에 보류 중인 변경 내용을 저장 하려면 Update 메서드를 자동으로 호출 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
