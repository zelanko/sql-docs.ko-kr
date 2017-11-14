---
title: "레코드 집합 개체를 사용 하 여 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5c9c3d117c6c5ed3bf6c9e5e3f5c6822915681fc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-recordset-object"></a>레코드 집합 개체를 사용 하 여
사용할 수 있습니다 **Recordset.Open** 하 암시적으로 연결을 설정 하 고 한 번에 해당 연결에 대해 명령을 실행 합니다. Visual Basic의 예를 들어:  
  
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
  
 다음에 유의 **oRs.Open** 연결 문자열 (*sConn*), 대신는 **연결** 개체 (*oConn*), 해당 의값으로 **ActiveConnection** 매개 변수입니다. 설정 하 여 클라이언트 쪽 커서 형식이 적용 되는 또한는 **앞** 속성에는 **레코드 집합** 개체입니다. 마찬가지로 이와 반대로와 **HelloData** 예제입니다.

