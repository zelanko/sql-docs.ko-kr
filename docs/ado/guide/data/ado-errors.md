---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1fe29d28d3d860b7108972abc1e1f20a10de1edc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701035"
---
# <a name="ado-run-time-errors"></a>ADO에서 런타임 오류
ADO 오류는 런타임 오류로 프로그램에 보고 됩니다. 트래핑 하 고 처리할 프로그래밍 언어의 오류 트래핑 메커니즘을 사용할 수 있습니다. 예를 들어, Visual Basic의 경우를 사용 합니다 **오류 발생 시** 문입니다. 시각적 개체의 C++, ADO 라이브러리에 액세스 하는 방법에 따라 다릅니다. #Import, 사용 된 **try / catch** 블록. 그렇지 않으면 C++ 명시적으로 호출 하 여 오류 개체를 검색 해야 하는 프로그래머 **GetErrorInfo**합니다. 다음 Visual Basic sub 프로시저는 ADO 오류를 트래핑 하는 방법을 보여 줍니다.

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

 이렇게 **Form_Load** 이벤트 프로시저를 열어 동일한 오류를 의도적으로 만듭니다 **연결** 개체를 두 번입니다. 두 번째는 **열려** 메서드가 호출 되 면 오류 처리기가 활성화 됩니다. 형식의 오류는이 예제의 **adErrObjectOpen**이므로 프로그램 실행을 다시 시작 하기 전에 오류 처리기에 다음 메시지가 표시 됩니다.

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 Visual Basic에서 제공 하는 정보를 포함 하는 오류 메시지 **Err** 제외 하 고 개체를 **LastDLLError** 값으로, 여기에 적용 되지 않습니다. 오류 번호는 오류 발생을 알려 줍니다. 에 대 한 설명에는 원하지 않는 오류를 직접 처리 하는 경우에 유용 합니다. 전달할 수 있습니다 단순히를 따라 사용자에 게 합니다. 모든 오류를 예상할 수 있지만 응용 프로그램에 대 한 사용자 지정 된 메시지를 사용 하려는 일반적으로 설명을은 무엇이 잘못 되었는지에 대 한 단서를 제공 합니다. 샘플 코드에서는 오류를 보고 합니다 **연결** 개체입니다. 개체의 형식 또는 프로그래밍 방식으로 ID 여기를 보면 변수 이름이 아닙니다.

> [!NOTE]
>  Visual Basic **Err** 개체는 가장 최근의 오류에 대 한 정보만 포함 합니다. ADO **오류** 의 컬렉션을 **연결** 개체 하나가 포함 되어 있습니다 **오류** 최근 ADO 작업에서 발생 하는 각 오류에 대 한 개체입니다. 사용 된 **오류** 컬렉션 대신 **Err** 여러 오류를 처리 하는 개체입니다. 에 대 한 자세한 내용은 합니다 **오류** 컬렉션에 참조 [공급자 오류](../../../ado/guide/data/provider-errors.md)합니다. 그러나 없으면 잘못 **연결** 개체를 **Err** 개체는 ADO 오류에 대 한 정보에 대 한 유일한 원본입니다.

 작업의 종류를 ADO 오류를 일으킬 가능성이? 일반적인 ADO 오류와 같은 개체를 열고 포함할 수는 **연결** 하거나 **레코드 집합**, 데이터를 업데이트 하는 동안 또는 공급자가 지원 되지 않는 속성 또는 메서드 호출 합니다.

 OLE DB 오류 응용 프로그램에서 런타임 오류도 전달할 수도 있습니다는 **오류** 컬렉션입니다.

 다음 항목에서는 ADO 오류에 대 한 자세한 정보를 제공합니다.

-   [ADO 오류 참조](../../../ado/guide/data/ado-error-reference.md)
