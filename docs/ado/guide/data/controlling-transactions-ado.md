---
title: 트랜잭션 제어 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
ms.assetid: 189240e8-3ffa-4024-81a9-c6cb5d17eee0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8059df4275a336d084144a73910cdef99abf9467
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472659"
---
# <a name="controlling-transactions-ado"></a>트랜잭션 제어(ADO)
ADO에서는 트랜잭션 처리를 활용 하 여 연결을 지원 합니다 **BeginTrans**, **CommitTrans**, 및 **RollbackTrans** 메서드를  **연결** 개체입니다. ADO에서 트랜잭션 처리를 구현 하는 일반적인 개념은 다음 간단한 코드 조각에 나와 있습니다.  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim oConn As ADODB.Connection  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
  
sConn = "Provider=" & DP & _  
          ";Data Source=" & DS & _  
          ";Initial Catalog=" & DB & _  
          ";Integrated Security=SSPI;"  
  
sSQL = "SELECT ProductID, ProductName FROM Products"  
  
Set oConn = New ADODB.Connection  
oConn.Open sConn  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.Open sSQL, oConn, adOpenStatic, adLockOptimistic, adCmdText  
  
If oRs.RecordCount > 1 Then  
  
    oRs.MoveFirst  
    Id1 = oRs("ProductID")  
    Name1 = oRs("ProductName")  
    oRs.MoveNext  
    Id2 = oRs("ProductID")  
    Name2 = oRs("ProductName")  
  
    q = "Switch ID's of " & Name1 & " and " & Name2 & "?"  
    If MsgBox(q, vbYesNo) = vbYes Then  
        oRs.MoveFirst  
        oRs("ProductName") = Name2  
        oRs.Update  
  
        oRs.MoveNext  
        oRs("ProductName") = Name1  
        oRs.Update  
  
        If MsgBox("Save changes?", vbYesNo) = vbYes Then  
  
        Else  
  
        End If  
    End If  
  
End If  
  
oRs.Close  
oConn.Close  
```  
  
 여기서 트랜잭션 처리 한 단위의 작업으로 두 레코드를 업데이트 하는 두 개의 제품 이름 중 하나는 교환 또는 전혀 변경 되지 않도록 하는 데 사용 됩니다.  
  
 트랜잭션 처리의 자세한 토론을 참조 하세요 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.
