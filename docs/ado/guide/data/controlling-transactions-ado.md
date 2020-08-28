---
description: 트랜잭션 제어(ADO)
title: 트랜잭션 제어 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
ms.assetid: 189240e8-3ffa-4024-81a9-c6cb5d17eee0
author: rothja
ms.author: jroth
ms.openlocfilehash: 003bbddc0942e7fe40ca24f80fb94d1252d40bc0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991514"
---
# <a name="controlling-transactions-ado"></a>트랜잭션 제어(ADO)
ADO **는 연결 개체에** 대 한 **BeginTrans**, **CommitTrans**및 **RollbackTrans** 메서드를 통해 연결 내에서 트랜잭션 처리를 지원 합니다. ADO에서 트랜잭션 처리를 구현 하는 일반적인 개념은 다음 간단한 코드 조각에 설명 되어 있습니다.  
  
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
  
 여기에서 트랜잭션 처리를 사용 하 여 두 레코드가 하나의 작업 단위로 업데이트 되 고 두 제품 이름이 함께 사용 되거나 변경 되지 않도록 합니다.  
  
 트랜잭션 처리에 대 한 자세한 논의는 [데이터 업데이트 및 유지](./updating-and-persisting-data.md)를 참조 하세요.