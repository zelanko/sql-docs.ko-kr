---
title: "명명 된 명령에 매개 변수를 전달 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f98080e73f2a0eb32450c0bc8e5779471adc74c6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="passing-parameters-to-a-named-command"></a>명명 된 명령에 매개 변수 전달
로 전달 됩니다 명령의 결과 마찬가지로 *아웃* 명명 된 명령의 매개 변수 매개 변수화 된 명령 수에로 전달 된 *에* 명명 된 명령에는 변수입니다.  
  
 다음 코드 예제를 갖는 고객에 의해 모든 주문을 검색 하려고 배치 **CustomerID** Northwind 데이터베이스에서 "ALKFI" 됩니다. 값 **CustomerID** 명령어를 호출할 때 시간에 제공 됩니다.  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = ? " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a named command.  
objComm.CommandText = CommandText  
objComm.CommandType = adCmdText  
objComm.Name = "GetOrdersOf"  
Set objComm.ActiveConnection = objConn  
  
' Call the named command, passing a CustomerID value  
' as the input parameter.   
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objConn.GetOrdersOf "ALKFI", objRs  
  
' Display the result.  
Debug.Print "All orders by ALFKI:"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
' Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
 모든 출력 변수 앞에 야 모든 입력된 매개 변수 및 매개 변수의 데이터 형식과 일치 해야 합니다 또는 해당 필드의로 변환할 수를 확인 합니다. 다음 문은-  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 — 필요한 입력된 매개 변수 이므로 일치 하지 않는 데이터 형식 중 오류가 발생 합니다는 **문자열** 형식 아닌는 **정수** 유형입니다.  
  
 다음 호출-  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 -유효 하지만 이러한 레코드가 데이터베이스에 존재 하기 때문에 설정 하는 빈 결과 생성 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
