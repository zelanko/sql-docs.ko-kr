---
title: 명명 된 명령에 매개 변수 전달 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9799fb3f05871c16cfcd8edb5f2a50c6f7792978
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924698"
---
# <a name="passing-parameters-to-a-named-command"></a>명명된 명령에 매개 변수 전달
명령의 결과가 명명 된 명령의 *out* 변수로 전달 되는 것과 마찬가지로 매개 변수가 있는 명령에 대 한 매개 변수는 명명 된 명령에 대 한 *변수로 전달* 될 수 있습니다.  
  
 다음 코드 예제에서는 고객이 Northwind 데이터베이스에서 **CustomerID** 인 "ALKFI"로 배치 된 모든 주문을 검색 하려고 시도 합니다. **CustomerID** 의 값은 명명 된 명령이 호출 될 때 제공 됩니다.  
  
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
  
 모든 입력 매개 변수는 모든 출력 변수 앞에와 야 하며 매개 변수의 데이터 형식이 일치 하거나 해당 필드의 데이터 형식으로 변환 될 수 있는지 확인 합니다. 다음 문  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -필수 입력 매개 변수가 **정수** 유형이 아닌 **문자열** 유형 이므로 일치 하지 않는 데이터 형식에 오류가 발생 합니다.  
  
 다음 호출  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 -는 유효 하지만 해당 레코드가 데이터베이스에 없기 때문에 빈 결과 집합을 생성 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
