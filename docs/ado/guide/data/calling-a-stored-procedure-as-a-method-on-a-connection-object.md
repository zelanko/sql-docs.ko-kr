---
title: 연결 개체의 메서드로 저장 프로시저 호출 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 35ffdb79-a931-4271-a3bb-0cd804cf173e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3202b607f3971dd1fcad2c3ae5e0ed83a667e923
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472804"
---
# <a name="calling-a-stored-procedure-as-a-method-on-a-connection-object"></a>연결 개체의 메서드로 저장 프로시저 호출
연결 열기 네이티브 메서드인 것 처럼 저장된 프로시저를 호출할 수 있습니다 **연결** 개체입니다. 명명 된 명령을 호출 비슷합니다는 **연결** 개체입니다.  
  
 다음 Visual Basic 코드 예제에서는 CustOrdersOrders 나열 된 다음 다시 사용자 편의 위해 호출 하는 Northwind 샘플 데이터베이스에서 저장된 프로시저를 호출 합니다.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 다음 코드 예제에서는 연결된을 열 때 네이티브 메서드인 것 처럼 저장된 프로시저를 호출 하는 방법을 보여 줍니다 **연결** 개체입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
