---
description: 연결 개체의 메서드로 저장 프로시저 호출
title: 연결 개체에서 저장 프로시저를 메서드로 호출 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 35ffdb79-a931-4271-a3bb-0cd804cf173e
author: rothja
ms.author: jroth
ms.openlocfilehash: 887730cdedd1dca884bca18bb6df449fdec2e1dc
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90989956"
---
# <a name="calling-a-stored-procedure-as-a-method-on-a-connection-object"></a>연결 개체의 메서드로 저장 프로시저 호출
저장 프로시저는 연결 된 열린 **연결** 개체의 네이티브 메서드인 것 처럼 호출할 수 있습니다. 이는 **Connection** 개체에서 명명 된 명령을 호출 하는 것과 유사 합니다.  
  
 다음 Visual Basic 코드 예에서는 편의를 위해 여기에 다시 나열 된 CustOrdersOrders 이라는 Northwind 샘플 데이터베이스의 저장 프로시저를 호출 합니다.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 다음 코드 예제에서는 저장 프로시저를 연결 된 열린 **연결** 개체의 네이티브 메서드인 것 처럼 호출 하는 방법을 보여 줍니다.  
  
```  
Const DS = "MySQLServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a stored procedure  
  
Set objComm.ActiveConnection = objConn  
  
' Execute the stored procedure on  
' the active connection object...  
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objComm(1) = "ALFKI"
Set objRs = objComm.Execute

' Display the result.  
Debug.Print "Results returned from sp_CustOrdersOrders for ALFKI: "  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
 Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
## <a name="see-also"></a>참고 항목  
 [연결 개체(ADO)](../../reference/ado-api/connection-object-ado.md)
