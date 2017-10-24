---
title: "ADO 오류 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 54a44c69afd01647c5dca1cab97993f890d81c21
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ado-run-time-errors"></a>ADO 런타임 오류
ADO 오류를 프로그램 실행 시간 오류로 보고 됩니다. 트래핑 하 고 처리 하는 프로그래밍 언어의 오류 트래핑 메커니즘을 사용할 수 있습니다. 예를 들어 Visual Basic에서 사용 하 여는 **On Error** 문. Visual c + +에서 ADO 라이브러리에 액세스 하는 데 사용 하는 방법에 따라 다릅니다. #Import를 사용 하 여 한 **try / catch** 블록입니다. C + + 프로그래머를 명시적으로 호출 하 여 오류 개체를 검색 해야 하는 그렇지 않은 경우 **GetErrorInfo**합니다. 다음 Visual Basic sub 프로시저는 ADO 오류를 트래핑 하는 방법을 보여 줍니다.

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

 이 **Form_Load** 이벤트 프로시저 동일한 열려고 시도 하 여 오류를 의도적으로 만듭니다 **연결** 두 번 개체입니다. 두 번째는 **열려** 메서드가 호출 되 면 오류 처리기가 활성화 됩니다. 형식의 오류는이 경우 **adErrObjectOpen**프로그램 실행을 다시 시작 하기 전에 다음과 같은 메시지를 표시 하는 오류 처리기,:

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 오류 메시지에는 각 Visual Basic에서 제공 하는 정보의 포함 **Err** 을 제외 하 고 개체는 **LastDLLError** 값으로, 여기에 적용 되지 않습니다. 오류 번호 어떤 오류가 발생 했는지를 알려 줍니다. 설명은를 원하지 않는 오류를 처리 하는 경우에 유용 합니다. 사용자를 따라를 전달 하면 있습니다. 하지만 응용 프로그램에 대 한 사용자 지정 된 메시지를 사용 하려는 일반적으로 모든 오류; 예측할 수는 없습니다. 설명을 무엇이 잘못 되었는지에 대 한 단서를 제공 합니다. 샘플 코드에서 오류에 의해 보고 되었으므로 **연결** 개체입니다. 개체의 형식 또는 프로그래밍 ID 여기 나타납니다-변수 이름이 아닙니다.

> [!NOTE]
>  Visual Basic **Err** 개체는 가장 최근의 오류에 대 한 정보만 포함 합니다. ADO **오류** 의 컬렉션은 **연결** 개체 하나에 포함 되어 **오류** 가장 최근의 ADO 작업에 의해 발생 하는 각 오류에 대 한 개체입니다. 사용 하 여는 **오류** 컬렉션 보다는 **Err** 여러 오류를 처리 하는 개체입니다. 에 대 한 자세한 내용은 **오류** 컬렉션 참조 [공급자 오류 정보](../../../ado/guide/data/provider-errors.md)합니다. 그러나 더 유효한 경우 **연결** 개체는 **Err** 개체는 ADO 오류에 대 한 정보에 대 한 유일한 원본입니다.

 작업의 종류는 ADO 오류가 발생할 가능성이 높은? 일반적인 ADO 오류 개체를 같은 열을 포함할 수는 **연결** 또는 **레코드 집합**, 데이터를 업데이트 하는 동안 또는 공급자가 지원 되지 않는 속성 또는 메서드 호출 합니다.

 OLE DB 오류에서 런타임 오류로 응용 프로그램에 전달할 수도 있습니다는 **오류** 컬렉션입니다.

 다음 항목 ADO 오류에 대 한 자세한 정보를 제공합니다.

-   [ADO 오류 참조](../../../ado/guide/data/ado-error-reference.md)

