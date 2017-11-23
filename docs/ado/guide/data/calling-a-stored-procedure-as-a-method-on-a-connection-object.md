---
title: "저장 프로시저는 연결 개체의 메서드로 호출 | Microsoft Docs"
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
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 35ffdb79-a931-4271-a3bb-0cd804cf173e
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 09d72e54d02fc6d13b34532ef5b847fcdca44d79
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="calling-a-stored-procedure-as-a-method-on-a-connection-object"></a>저장 프로시저는 연결 개체의 메서드로 호출
연결된 열기에 대 한 네이티브 메서드 처럼 저장된 프로시저를 호출할 수 있습니다 **연결** 개체입니다. 명명된 된 명령을 호출 비슷합니다는 **연결** 개체입니다.  
  
 다음 Visual Basic 코드 예제에서는 CustOrdersOrders로, 여기에 나열 되어 다시 사용자 편의 위해 호출 하는 Northwind 샘플 데이터베이스의 저장된 프로시저를 호출 합니다.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 다음 코드 예제에서는 열려 있는 연결된에서 네이티브 메서드인 것 처럼 저장된 프로시저를 호출 하는 방법을 보여 줍니다 **연결** 개체입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
