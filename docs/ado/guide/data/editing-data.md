---
title: 데이터 편집 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
author: rothja
ms.author: jroth
ms.openlocfilehash: cc80c8ad9985efc21e2f583d8ca72751e21c1a2b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761039"
---
# <a name="editing-data"></a>데이터 편집
ADO를 사용 하 여 데이터 원본에 연결 하 고, 명령을 실행 하 고, **레코드 집합** 개체에서 결과를 가져오고, **레코드 집합**내에서 탐색 하는 방법에 대해 설명 했습니다. 이 섹션에서는 다음 기본 ADO 작업 인 데이터 편집에 대해 중점적으로 설명 합니다.  
  
 이 섹션에서는 중요 한 변경 내용으로 [데이터 검사](../../../ado/guide/data/examining-data.md)에 도입 된 샘플 **레코드 집합** 을 계속 사용 합니다. 다음 코드는 **레코드 집합**을 여는 데 사용 됩니다.  
  
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
  
 코드의 중요 한 변경 내용에는 클라이언트 커서 사용을 나타내는 *Getnewconnection* 함수 (다음 예제에서 표시)에서 **Connection** 개체의 **CursorLocation** 속성을 **adUseClient** 로 설정 하는 작업이 포함 됩니다. 클라이언트 쪽 커서와 서버측 커서 간의 차이점에 대 한 자세한 내용은 [커서 및 잠금 이해](../../../ado/guide/data/understanding-cursors-and-locks.md)를 참조 하세요.  
  
 **CursorLocation** 속성의 **adUseClient** 설정은 커서 위치를 데이터 원본 (이 경우 SQL Server)에서 클라이언트 코드의 위치 (데스크톱 워크스테이션)로 이동 합니다. 이 설정을 통해 ADO는 커서를 만들고 관리 하기 위해 클라이언트에서 OLE DB에 대 한 클라이언트 커서 엔진을 호출 합니다.  
  
 **Open** 메서드의 **LockType** 매개 변수가 **adlockbatchoptimistic**으로 변경 된 것을 알 수도 있습니다. 그러면 커서가 일괄 처리 모드로 열립니다. 이 공급자는 여러 변경 내용을 캐시 하 고 **UpdateBatch** 메서드를 호출 하는 경우에만 기본 데이터 소스에 씁니다. **레코드 집합** 에 대 한 변경 내용은 **UpdateBatch** 메서드가 호출 될 때까지 데이터베이스에서 업데이트 되지 않습니다.  
  
 마지막으로이 섹션의 코드는 수정 된 버전의 GetNewConnection 함수를 사용 합니다. 이 버전의 함수는 이제 클라이언트 쪽 커서를 반환 합니다. 함수는 다음과 같습니다.  
  
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
  
-   [Delete 메서드를 사용하여 레코드 삭제](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [대안: SQL 문 사용](../../../ado/guide/data/alternatives-using-sql-statements.md)
