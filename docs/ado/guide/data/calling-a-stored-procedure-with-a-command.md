---
title: 명령 사용 하 여 저장된 프로시저 호출 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4763939e3eccd0bf4783df87141619cbc0fb011c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702331"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>명령을 사용하여 저장 프로시저 호출
저장된 프로시저를 호출 하는 명령을 사용할 수 있습니다. 이 항목의 끝에 있는 코드 샘플에서는 CustOrdersOrders 다음과 같이 정의 되어 있는 호출 Northwind 샘플 데이터베이스에 저장된 프로시저를 가리킵니다.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 저장 프로시저를 정의 하 고 호출 하는 방법에 대 한 자세한 내용은 SQL Server 설명서를 참조 하세요.  
  
 이 저장된 프로시저에 사용 된 명령 비슷합니다 [명령 개체 매개 변수](../../../ado/guide/data/command-object-parameters.md)합니다. 고객 ID 매개 변수를 사용 하 고 해당 고객의 주문 정보를 반환 합니다. 다음 코드 샘플 ADO에 대 한이 저장된 프로시저를 원본으로 사용 **레코드 집합**합니다.  
  
 저장된 프로시저를 사용 하면 ADO의 다른 기능에 액세스할 수 있습니다: 합니다 **매개 변수** 컬렉션 **새로 고침** 메서드. 이 메서드를 사용 하 여 ADO 런타임에 명령에 필요한 매개 변수에 대 한 모든 정보에서 자동으로 채울 수 있습니다. ADO 매개 변수 정보에 대 한 데이터 원본을 쿼리하도록 않으므로이 기법을 사용 하 여 성능이 저하가 됩니다.  
  
 다른 중요 한 차이점이 다음 코드 샘플의 코드 사이의 [명령 개체 매개 변수](../../../ado/guide/data/command-object-parameters.md)매개 변수를 수동으로 입력 되었습니다. 먼저이 코드는 설정 하지 않습니다 합니다 **Prepared** 속성을 **True** 하기 때문에 SQL Server 저장 프로시저를 정의 하 여 미리 컴파일된 됩니다. 두 번째는 **CommandType** 의 속성을 **명령** 개체를 변경 **adCmdStoredProc** 명령 된 저장된 프로시저는 ADO를 알리기 위해 두 번째 예제에서.  
  
 마지막으로, 두 번째 예제에서 매개 변수 참조 해야 인덱스로 값을 설정 하는 경우 디자인 타임에 매개 변수의 이름을 모르는 때문입니다. 매개 변수의 이름을 알고 있으면 새 설정할 수 [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) 의 속성을 **명령** 로 개체 및 속성의 이름을 참조 합니다. 저장된 프로시저의 첫 번째 매개 변수의 위치 언급 하는 이유는 궁금할 수 있습니다 (@CustomerID)는 0 대신 1 (`objCmd(1) = "ALFKI"`). SQL Server 저장 프로시저의 반환 값을 포함 하는 매개 변수 0 때문입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [기술 자료 문서 117500](https://go.microsoft.com/fwlink/?LinkId=117500)
