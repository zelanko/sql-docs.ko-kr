---
title: "명령 사용 하 여 저장된 프로시저를 호출 | Microsoft Docs"
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
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 613c9d2e018360798eb71748473750712dec461e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="calling-a-stored-procedure-with-a-command"></a>명령 사용 하 여 저장된 프로시저 호출
저장된 프로시저를 호출 하는 명령을 사용할 수 있습니다. 이 항목의 끝에 있는 코드 샘플 CustOrdersOrders 다음과 같이 정의 된 호출 Northwind 샘플 데이터베이스의 저장된 프로시저를 참조 합니다.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 저장 프로시저를 정의 하 고 호출 하는 방법에 대 한 자세한 내용은 SQL Server 설명서를 참조 하십시오.  
  
 이 저장된 프로시저에 사용 되는 명령에 비슷합니다. [Command 개체 매개 변수](../../../ado/guide/data/command-object-parameters.md)합니다. 고객 ID 매개 변수를 사용 하 고 해당 고객의 주문에 대 한 정보를 반환 합니다. 다음 코드 예제는 ADO에 대 한이 저장된 프로시저를 원본으로 사용 **레코드 집합**합니다.  
  
 ADO의 다른 기능에 액세스할 수 있습니다는 저장된 프로시저를 사용 하 여:는 **매개 변수** 컬렉션 **새로 고침** 메서드. 이 메서드를 사용 하 여 런타임 시 명령에 필요한 매개 변수에 대 한 모든 정보 ADO 자동으로 채울 수 있습니다. ADO는 매개 변수에 대 한 정보에 대 한 데이터 원본을 쿼리하도록 되므로이 방법을 사용 하 여 성능 저하는.  
  
 다른 중요 한 차이점이 다음 코드 샘플의 코드 사이의 [Command 개체 매개 변수](../../../ado/guide/data/command-object-parameters.md)매개 변수 수동으로 입력 된, 합니다. 먼저,이 코드는 설정 하지 않습니다는 **Prepared** 속성을 **True** SQL Server 저장 프로시저가 고 정의 의해 미리 컴파일된 있기 때문에 있습니다. 두 번째는 **CommandType** 속성의는 **명령** 개체로 변경 **adCmdStoredProc** 은 명령이 저장된 프로시저 했음을 ADO를 알리기 위해 두 번째 예제에서 합니다.  
  
 마지막으로, 두 번째 예제에서 매개 변수 참조 해야 인덱스로 값을 설정할 때 디자인 타임에 매개 변수 이름을 모를 수도 있으므로 합니다. 매개 변수의 이름을 알면 새 설정할 수 [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) 의 속성은 **명령** True로 개체 및 속성의 이름을 참조 합니다. 저장된 프로시저에서 첫 번째 매개 변수가 있는 위치 언급 하는 이유가 궁금할 수 있습니다 (@CustomerID)는 0이 아닌 1 (`objCmd(1) = "ALFKI"`). SQL Server 저장 프로시저의 반환 값을 포함 하는 매개 변수 0 때문입니다.  
  
```  
'BeginAutoParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set CommandText equal to the stored procedure name.  
    objCmd.CommandText = "CustOrdersOrders"  
    objCmd.CommandType = adCmdStoredProc  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Automatically fill in parameter info from stored procedure.  
    objCmd.Parameters.Refresh  
  
    ' Set the param value.  
    objCmd(1) = "ALFKI"  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' ...then set new param value, re-execute command, and display.  
    objCmd(1) = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndAutoParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
## <a name="see-also"></a>관련 항목:  
 [기술 자료 문서 117500](http://go.microsoft.com/fwlink/?LinkId=117500)
