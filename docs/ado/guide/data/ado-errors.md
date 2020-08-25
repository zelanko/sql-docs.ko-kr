---
description: ADO 런타임 오류
title: ADO 오류 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
author: rothja
ms.author: jroth
ms.openlocfilehash: f753e66e6711c3abcf59e2541b9bad6cd390e71a
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806687"
---
# <a name="ado-run-time-errors"></a>ADO 런타임 오류
ADO 오류는 런타임 오류로 프로그램에 보고 됩니다. 프로그래밍 언어의 오류 트래핑 메커니즘을 사용 하 여이를 트래핑 하 고 처리할 수 있습니다. 예를 들어 Visual Basic에서 **On Error** 문을 사용 합니다. Visual C++에서 ADO 라이브러리에 액세스 하는 데 사용 하는 방법에 따라 달라 집니다. #Import를 사용 **하 여 try-catch 블록을** 사용 합니다. 그렇지 않으면 c + + 프로그래머는 **Geterrorinfo**를 호출 하 여 오류 개체를 명시적으로 검색 해야 합니다. 다음 Visual Basic 하위 절차에서는 ADO 오류를 트래핑 하는 방법을 보여 줍니다.

```
' BeginErrorHandlingVB01
Private Sub Form_Load()
' Turn on error handling
On Error GoTo FormLoadError

'Open the database and the recordset for processing.
'
Dim strCnn As String
strCnn = "Provider=sqloledb;" & _
    "Data Source=a-iresmi2000;" & _
    "Initial Catalog=Northwind;Integrated Security=SSPI"

' cnn is a Public Connection Object because
' it was defined WithEvents
Set cnn = New ADODB.Connection
cnn.Open strCnn

' The next line of code intentionally causes
' an error by trying to open a connection
' that has already been opened.
cnn.Open strCnn

' rst is a Public Recordset because it
' was defined WithEvents
Set rst = New ADODB.Recordset
rst.Open "Customers", cnn

Exit Sub

' Error handler
FormLoadError:
    Dim strErr As String
    Select Case Err
        Case adErrObjectOpen
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            strErr = strErr & "Error reported by: " & Err.Source & vbCrLf
            strErr = strErr & "Help File: " & Err.HelpFile & vbCrLf
            strErr = strErr & "Topic ID: " & Err.HelpContext
            MsgBox strErr
            Debug.Print strErr
            Err.Clear
            Resume Next
        ' If some other error occurs that
        ' has nothing to do with ADO, show
        ' the number and description and exit.
        Case Else
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            MsgBox strErr
            Debug.Print strErr
            Unload Me
    End Select
End Sub
' EndErrorHandlingVB01
```

 이 **Form_Load** 이벤트 프로시저는 동일한 **연결** 개체를 두 번 열려고 시도 하 여 의도적으로 오류를 생성 합니다. **Open** 메서드를 두 번째로 호출할 때 오류 처리기가 활성화 됩니다. 이 경우 오류는 **adErrObjectOpen**형식 이므로 오류 처리기는 프로그램 실행을 다시 시작 하기 전에 다음 메시지를 표시 합니다.

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 오류 메시지에는 여기에 적용 되지 않는 **LastDLLError** 값을 제외 하 고 Visual Basic **Err** 개체에서 제공 하는 각 정보 조각이 포함 됩니다. 오류 번호는 발생 한 오류를 알려 줍니다. 설명은 오류를 직접 처리 하지 않으려는 경우에 유용 합니다. 단순히 사용자에 게 전달할 수 있습니다. 일반적으로 응용 프로그램에 대해 사용자 지정 된 메시지를 사용 하려는 경우에도 모든 오류를 예측할 수는 없습니다. 설명은 무엇이 잘못 되었는지에 대 한 단서를 제공 합니다. 예제 코드에서는 **연결** 개체에서 오류를 보고 했습니다. 여기서는 변수 이름이 아니라 개체의 형식 또는 프로그래밍 ID를 볼 수 있습니다.

> [!NOTE]
>  Visual Basic **Err** 개체는 가장 최근의 오류에 대 한 정보만 포함 합니다. **연결** 개체의 ado **Errors** 컬렉션에는 가장 최근 ADO 작업에서 발생 한 각 오류에 대 한 **오류** 개체 하나가 포함 되어 있습니다. **Err** 개체가 아닌 **errors** 컬렉션을 사용 하 여 여러 오류를 처리 합니다. **오류** 컬렉션에 대 한 자세한 내용은 [공급자 오류](./provider-errors.md)를 참조 하세요. 그러나 유효한 **연결** 개체가 없으면 **ERR** 개체는 ADO 오류에 대 한 정보를 위한 유일한 원본입니다.

 ADO 오류가 발생할 수 있는 작업의 종류는 무엇 인가요? 일반적인 ADO 오류에는 **연결** 또는 **레코드 집합과**같은 개체를 열거나, 데이터를 업데이트 하거나, 공급자가 지원 하지 않는 메서드나 속성을 호출 하는 작업이 포함 될 수 있습니다.

 OLE DB 오류는 **오류** 컬렉션의 런타임 오류로 응용 프로그램에 전달 될 수도 있습니다.

 다음 항목에서는 ADO 오류에 대 한 자세한 정보를 제공 합니다.

-   [ADO 오류 참조](./ado-error-reference.md)