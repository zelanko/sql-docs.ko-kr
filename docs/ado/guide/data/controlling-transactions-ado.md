---
title: "트랜잭션 (ADO) 제어 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transactions [ADO]
ms.assetid: 189240e8-3ffa-4024-81a9-c6cb5d17eee0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1535ff20e7dbc40b8f478902512d068fd5501b27
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="controlling-transactions-ado"></a>트랜잭션 (ADO) 제어
ADO 지원 되며, 트랜잭션 처리를 사용 하 여 연결 내에서 **BeginTrans**, **CommitTrans**, 및 **RollbackTrans** 에 대 한 메서드는  **연결** 개체입니다. 다음과 같은 간단한 코드 조각을 ADO에서 트랜잭션 처리를 구현 하는의 일반적인 개념을 보여 줍니다.  
  
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
  
 여기서 트랜잭션 처리는 두 레코드의 작업을 하나의 단위로 업데이트 되 고 교환 또는 전혀 변경 되지 두 개의 제품 이름이 하나 지 확인 하는 데 사용 됩니다.  
  
 자세한 내용은 트랜잭션 처리의 참조에 대 한 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.
