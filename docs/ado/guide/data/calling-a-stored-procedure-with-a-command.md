---
description: 명령을 사용하여 저장 프로시저 호출
title: 명령을 사용 하 여 저장 프로시저 호출 | Microsoft Docs
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
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c510bd71d8b81eae9f86e48c398cc6ff7e81cea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453695"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>명령을 사용하여 저장 프로시저 호출
명령을 사용 하 여 저장 프로시저를 호출할 수 있습니다. 이 항목의 끝에 있는 코드 샘플은 다음과 같이 정의 된 CustOrdersOrders 이라는 Northwind 샘플 데이터베이스의 저장 프로시저를 참조 합니다.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 저장 프로시저를 정의 하 고 호출 하는 방법에 대 한 자세한 내용은 SQL Server 설명서를 참조 하세요.  
  
 이 저장 프로시저는 [명령 개체 매개 변수에](../../../ado/guide/data/command-object-parameters.md)사용 되는 명령과 비슷합니다. 고객 ID 매개 변수를 사용 하 여 해당 고객의 주문에 대 한 정보를 반환 합니다. 다음 코드 예제에서는이 저장 프로시저를 ADO **레코드 집합**의 원본으로 사용 합니다.  
  
 저장 프로시저를 사용 하 여 ADO의 다른 기능에 액세스할 수 있습니다. **매개 변수** 컬렉션 **Refresh** 메서드. 이 메서드를 사용 하 여 ADO는 런타임에 명령에 필요한 매개 변수에 대 한 모든 정보를 자동으로 채울 수 있습니다. ADO는 매개 변수에 대 한 정보를 데이터 소스에 쿼리해야 하므로이 기법을 사용 하면 성능 저하가 발생 합니다.  
  
 매개 변수가 수동으로 입력 된 다음 코드 샘플과 [Command 개체 매개 변수의](../../../ado/guide/data/command-object-parameters.md)코드 사이에는 다른 중요 한 차이점이 있습니다. 첫째,이 코드는 SQL Server 저장 프로시저이 고 정의에 의해 미리 컴파일되어 **준비** 된 속성을 **True** 로 설정 하지 않습니다. 두 번째 예에서는 명령이 저장 프로시저 임을 ADO에 알리기 위해 **명령** 개체의 **CommandType** 속성이 **adCmdStoredProc** 로 변경 되었습니다.  
  
 마지막으로, 두 번째 예제에서는 디자인 타임에 매개 변수 이름을 알 수 없기 때문에 값을 설정할 때 인덱스에서 매개 변수를 참조 해야 합니다. 매개 변수의 이름을 알고 있는 경우 **명령** 개체의 새 [Namedparameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) 속성을 True로 설정 하 고 속성의 이름을 참조할 수 있습니다. 저장 프로시저 ()에서 언급 된 첫 번째 매개 변수의 위치가 @CustomerID 0 ()이 아닌 1 인 이유가 궁금할 수 있습니다 `objCmd(1) = "ALFKI"` . 이는 매개 변수 0에 SQL Server 저장 프로시저의 반환 값이 포함 되어 있기 때문입니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [기술 자료 문서 117500](https://go.microsoft.com/fwlink/?LinkId=117500)
