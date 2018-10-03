---
title: 레코드 집합 개체를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 985cb58b860c594e8cfc3e405934fafd9cfb245a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789451"
---
# <a name="using-a-recordset-object"></a>레코드 집합 개체 사용
사용할 수 있습니다 **Recordset.Open** 를 암시적으로 연결을 설정 하 고 단일 작업에서 해당 연결을 통해 명령을 실행 합니다. Visual Basic의 예를 들어:  
  
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
  
 있음을 **oRs.Open** 연결 문자열을 사용 (*sConn*)를 대신 한 **연결** 개체 (*oConn*), 해당값으로 **ActiveConnection** 매개 변수입니다. 설정 하 여 클라이언트 쪽 커서 형식이 적용 되는 또한 합니다 **CursorLocation** 속성에는 **레코드 집합** 개체입니다. 다시 사용 하 여이 대조 합니다 **HelloData** 예제입니다.
