---
title: 만들기 및 간단한 명령을 실행 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], creating and executing
- commands [ADO], creating and executing
ms.assetid: 0b81af6f-b9ae-4f7c-b59b-b5bdd775036f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 644ee0c1ca4baee72a5fd33aeb16843dc7c59795
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472639"
---
# <a name="creating-and-executing-a-simple-command"></a>간단한 명령 만들기 및 실행
간단한 명령은 없는 지 속성을 하며 매개 변수가 없는 것입니다. 만들고 간단한 명령을 실행 하는 방법은 세 가지가 있습니다.  
  
-   사용 하는 **명령** 개체  
  
-   사용 하는 **연결** 개체  
  
-   사용 하는 **레코드 집합** 개체  
  
## <a name="using-a-command-object"></a>명령 개체를 사용 하 여  
 사용 하 여 간단한 명령을 만드는 **명령** 개체를 명령에 할당 해야 합니다는 **CommandText** 속성을 **명령** 개체 및 적절 한 값을 설정 합니다 **CommandType** 속성입니다. 명령 실행에 대해 열린 연결에 할당 되어 있는지 필요를 **ActiveConnection** 의 속성을 **명령** 개체를 호출 하 여를 **Execute** 메서드 에 **명령** 개체입니다.  
  
 다음 코드 조각을 사용 하 여 기본 메서드를 보여 줍니다.는 **명령** 데이터 원본에 대해 명령을 실행 하는 개체입니다. 행을 반환 하는 명령을 사용 하 고으로 명령 실행의 결과 반환 하는이 예제는 **레코드 집합** 개체입니다.  
  
```  
    'BeginBasicCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objRs As New ADODB.Recordset  
  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = 'ALFKI' " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print "ALFKI"  
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
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndBasicCmd  
  
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
  
## <a name="using-a-recordset-object"></a>레코드 집합 개체를 사용 하 여  
 명령을 pa 및 텍스트 문자열을 만들 수도 있습니다 하는 **열기** 메서드를 **레코드 집합** 개체 명령 유형 (adCmdText)와 함께 실행에 대 한. 다음 코드 조각은이 보여 줍니다.  
  
```  
  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objRs As New ADODB.Recordset  
Dim CommandText As String  
Dim ConnctionString As String  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = 'ALFKI' " & _  
                     "ORDER BY OrderID"  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to data source and execute the SQL command.  
objRs.Open CommandText, ConnectionString, _  
            adOpenStatic, adLockReadOnly, adCmdText  
  
Debug.Print "ALFKI"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
Set objRs = Nothing  
```  
  
## <a name="using-a-connection-object"></a>연결 개체를 사용 하 여  
 또한 열려 있는 연결 개체에서 명령을 실행할 수 있습니다. 이전 코드 예제는이:  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = 'ALFKI' " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Execute command through the connection and display...  
Set objRs = objConn.Execute(CommandText)  
  
Debug.Print "ALFKI"  
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
```
