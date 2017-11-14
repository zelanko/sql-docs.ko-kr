---
title: "데이터 편집 | Microsoft Docs"
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
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76a5921185f6643f328559e3bc73dfac46bfee0c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="editing-data"></a>데이터 편집
설명한가 어떻게 하 고 데이터 원본에 연결, 명령 실행 결과 얻을 ADO를 사용 하는 **레코드 집합** 개체를 탐색할는 **레코드 집합**합니다. 이 여기서는 다음 기본 ADO 작업 설명: 데이터를 편집 합니다.  
  
 이 섹션의 샘플을 사용 하려면 계속 **레코드 집합** 에 도입 된 [데이터 검사](../../../ado/guide/data/examining-data.md), 한 가지 중요 한 변경 합니다. 다음 코드는 여는 데 사용 되는 **레코드 집합**:  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 코드에는 중요 한 변경 사항에 설정 해야는 **앞** 의 속성은 **연결** 개체와 같은 **adUseClient** 에  *GetNewConnection* 함수 (다음 예제에 표시), 클라이언트 커서의 사용을 나타냅니다. 클라이언트 쪽 및 서버측 커서 차이점에 대 한 자세한 내용은 참조 [커서 및 잠금 이해](../../../ado/guide/data/understanding-cursors-and-locks.md)합니다.  
  
 **앞** 속성의 **adUseClient** 설정 (SQL Server,이 경우) 데이터 원본에서 클라이언트 코드 (데스크톱 워크스테이션)의 위치를 커서의 위치를 이동 합니다. 이 설정을 하면 ADO 만들어 커서를 관리 하려면 클라이언트에서 OLE DB에 대 한 클라이언트 커서 엔진을 호출 합니다.  
  
 또한 보았을 것입니다는 **LockType** 의 매개 변수는 **열려** 메서드 변경 **adLockBatchOptimistic**합니다. 이 일괄 처리 모드에서 커서를 엽니다. (공급자는 여러 변경 내용을 캐시 하 고 호출 된 경우에 기본 데이터 원본에 기록 된 **UpdateBatch** 메서드.) 에 대 한 변경 내용을 **레코드 집합** 될 때까지 데이터베이스에서 업데이트 되지 것입니다는 **UpdateBatch** 메서드를 호출 합니다.  
  
 마지막으로,이 섹션의 코드는 수정 된 버전의 GetNewConnection 함수를 사용합니다. 이제이 버전의 함수는 클라이언트 쪽 커서를 반환합니다. 함수는 다음과 같습니다.  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [기존 레코드 편집](../../../ado/guide/data/editing-existing-records.md)  
  
-   [레코드 추가](../../../ado/guide/data/adding-records.md)  
  
-   [지원되는 기능 확인](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [삭제 메서드를 사용하여 레코드 삭제](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [대안: SQL 문 사용](../../../ado/guide/data/alternatives-using-sql-statements.md)

