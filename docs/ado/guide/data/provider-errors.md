---
title: 공급자 오류 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85d4a7607fae1df7dfb6ec62b8a3bfae8f58001b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924541"
---
# <a name="provider-errors"></a>공급자 오류
공급자 오류가 발생 하면-2147467259의 런타임 오류가 반환 됩니다. 이 오류가 표시 되 면 활성 **연결** 개체의 **오류** 컬렉션을 확인 합니다 .이 컬렉션에는 발생 한 작업을 설명 하는 하나 이상의 오류가 포함 됩니다.  
  
## <a name="the-ado-errors-collection"></a>ADO Errors 컬렉션  
 특정 ADO 작업은 여러 공급자 오류를 생성할 수 있기 때문에 ADO는 **연결** 개체를 통해 오류 개체의 컬렉션을 제공 합니다. 작업이 성공적으로 완료 되 고 **오류가** 발생 하 고 공급자에서 하나 이상의 오류가 발생 한 경우이 컬렉션은 개체를 포함 하지 않습니다. 각 오류 개체를 검사 하 여 오류의 정확한 원인을 확인 합니다.  
  
 발생 한 오류에 대 한 처리를 완료 하는 즉시 **clear** 메서드를 호출 하 여 컬렉션을 지울 수 있습니다. **레코드 집합** 개체에 대해 **Resync**, **UpdateBatch**또는 **CancelBatch** 메서드를 호출 하기 전에 명시적으로 **오류** 컬렉션을 지우거 나 **Connection** 개체의 **Open** 메서드를 명시적으로 지우거 나 **레코드 집합** 개체에 대해 **Filter** 속성을 설정 하는 것이 특히 중요 합니다. 컬렉션을 명시적으로 지우면 컬렉션의 모든 **오류** 개체가 이전 작업에서 남겨진 것이 확실 하지 않을 수 있습니다.  
  
 일부 작업은 오류 외에도 경고를 생성할 수 있습니다. 경고는 **Errors** 컬렉션의 **오류** 개체로도 표시 됩니다. 공급자가 컬렉션에 경고를 추가 하면 런타임 오류가 생성 되지 않습니다. **오류** 컬렉션의 **Count** 속성을 확인 하 여 특정 작업에서 경고가 생성 되었는지 여부를 확인 합니다. 개수가 하나 이상이 면 컬렉션에 **오류** 개체가 추가 된 것입니다. **오류** 컬렉션에 오류 또는 경고가 포함 되어 있음을 확인 한 후에는 컬렉션을 반복 하 고 포함 된 각 **오류** 개체에 대 한 정보를 검색할 수 있습니다. 다음의 간단한 Visual Basic 예제에서는이를 보여 줍니다.  
  
```  
' BeginErrorHandlingVB02  
Private Function DeleteCustomer(ByVal CompanyName As String) As Long  
    On Error GoTo DeleteCustomerError  
  
    rst.Find "CompanyName='" & CompanyName & "'"  
DeleteCustomerError:  
Dim objError As ADODB.Error  
Dim strError As String  
  
    If cnn.Errors.Count > 0 Then  
        For Each objError In cnn.Errors  
            strError = strError & "Error #" & objError.Number & _  
                " " & objError.Description & vbCrLf & _  
                "NativeError: " & objError.NativeError & vbCrLf & _  
                "SQLState: " & objError.SQLState & vbCrLf & _  
                "Reported by: " & objError.Source & vbCrLf & _  
                "Help file: " & objError.HelpFile & vbCrLf & _  
                "Help Context ID: " & objError.HelpContext  
        Next  
        MsgBox strError  
    End If  
End Function  
' EndErrorHandlingVB02  
```  
  
 오류 처리 루틴은 **Errors** 컬렉션에서 각 개체를 검사 하는 **for each** 루프를 포함 합니다. 이 예제에서는 표시를 위해 메시지를 누적 합니다. 작업 중인 프로그램에서 열려 있는 모든 파일을 닫고 순차적으로 프로그램을 종료 하는 것과 같이 각 오류에 대해 적절 한 작업을 수행 하는 코드를 작성 합니다.  
  
## <a name="the-error-object"></a>Error 개체  
 **오류 개체를** 검사 하 여 발생 한 오류 및 더 중요 한 응용 프로그램 또는 오류를 발생 시킨 개체를 확인할 수 있습니다. **Error** 개체에는 다음과 같은 속성이 있습니다.  
  
|속성 이름|Description|  
|-------------------|-----------------|  
|**설명**|발생 한 오류에 대 한 텍스트 설명입니다.|  
|**HelpContext, HelpFile**|발생 한 오류에 대 한 설명이 포함 된 도움말 항목 및 도움말 파일을 참조 하세요.|  
|**NativeError**|공급자별 오류 번호입니다.|  
|**번호**|발생 한 오류의 숫자 ( **Errorvalueenum**에 나열 됨)를 나타내는 정수 (Long)입니다.|  
|**소스**|오류를 생성 한 개체 또는 응용 프로그램의 이름을 나타냅니다.|  
|**SQLState**|SQL 문 프로세스 중에 공급자가 반환 하는 다섯 문자 오류 코드입니다.|  
  
 ADO **Error** 개체는 표준 Visual Basic **Err** 개체와 매우 비슷합니다. 해당 속성은 발생 한 오류를 설명 합니다. 오류 수 외에도 관련 된 두 가지 정보를 받을 수 있습니다. **NativeError** 속성에는 사용 중인 공급자와 관련 된 오류 번호가 포함 되어 있습니다. 이전 예제에서 공급자는 SQL Server에 대 한 Microsoft OLE DB 공급자 이므로 **NativeError** 는 SQL Server 관련 된 오류를 포함 합니다. **SQLState** 속성에는 SQL 문의 오류를 설명 하는 5 자리 코드가 있습니다.  
  
## <a name="event-related-errors"></a>이벤트 관련 오류  
 **Error** 개체는 이벤트 관련 오류가 발생 하는 경우에도 사용 됩니다. 이벤트 매개 변수로 전달 된 **오류** 개체를 확인 하 여 ADO 이벤트를 발생 시킨 프로세스에서 오류가 발생 했는지 여부를 확인할 수 있습니다.  
  
 이벤트를 발생 시킨 작업이 성공적으로 완료 되 면 이벤트 처리기의 *Adstatus* 매개 변수가 *adstatusok*로 설정 됩니다. 반면 이벤트를 발생 시킨 작업이 실패 한 경우 *Adstatus* 매개 변수는 *adStatusErrorsOccurred*로 설정 됩니다. 이 경우 *pError* 매개 변수는 오류를 설명 하는 **오류** 개체를 포함 합니다.
