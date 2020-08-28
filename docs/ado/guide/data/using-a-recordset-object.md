---
description: 레코드 집합 개체 사용
title: 레코드 집합 개체 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
author: rothja
ms.author: jroth
ms.openlocfilehash: a9f75190ae5375b357d6baba93aac7aa2959e188
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979104"
---
# <a name="using-a-recordset-object"></a>레코드 집합 개체 사용
또는 **레코드 집합** 을 사용 하 여 암시적으로 연결을 설정 하 고 단일 작업으로 해당 연결을 통해 명령을 실행할 수 있습니다. 예를 들어 Visual Basic에서 다음을 수행 합니다.  
  
```  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.CursorLocation = adUseClient  
oRs.Open sSQL, sConn, adOpenStatic, _  
               adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
oRs.Close          
Set oRs = Nothing  
```  
  
 **ORs** 는 **Connection** 개체 (*oconn*) 대신 연결 문자열 (*sconn*)을 **ActiveConnection** 매개 변수의 값으로 사용 합니다. 또한 클라이언트 쪽 커서 형식은 **레코드 집합** 개체에 대해 **CursorLocation** 속성을 설정 하 여 적용 됩니다. 다시, **HelloData** 예제와 대조 합니다.
