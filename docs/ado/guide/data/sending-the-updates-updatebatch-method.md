---
title: '업데이트 전송: UpdateBatch 메서드 | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924253"
---
# <a name="sending-the-updates-updatebatch-method"></a>업데이트 전송: UpdateBatch 메서드
다음 코드는 LockType 속성을 adLockBatchOptimistic으로 설정 하 고 CursorLocation를 adUseClient로 설정 하 여 일괄 처리 모드로 레코드 집합을 엽니다. 새 레코드 두 개를 추가 하 고 기존 레코드의 필드 값을 변경 하 여 원래 값을 저장 한 다음 UpdateBatch를 호출 하 여 변경 내용을 데이터 원본으로 다시 보냅니다.  
  
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
  
 현재 레코드를 편집 하거나 UpdateBatch 메서드를 호출할 때 새 레코드를 추가 하는 경우, ADO는 일괄 처리 된 변경 내용을 공급자에 전송 하기 전에 업데이트 메서드를 자동으로 호출 하 여 현재 레코드에 대 한 보류 중인 변경 내용을 저장 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
