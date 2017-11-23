---
title: "공급자 오류 정보 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 327869785bddfbd0d43bfff051a9b7ef6b97c8fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="provider-errors"></a>공급자 오류 정보
공급자 오류가 발생 하는 경우에-2147467259 런타임에 오류가 반환 됩니다. 이 오류를 받으면 확인는 **오류** 활성의 컬렉션 **연결** 하나 이상의 오류가 발생 한 문제를 설명 하는 포함 하는 개체입니다.  
  
## <a name="the-ado-errors-collection"></a>ADO 오류 컬렉션  
 ADO를 통해 오류 개체의 컬렉션을 노출 특정 ADO 작업에서 여러 공급자 오류가 발생할 수 있으므로 **연결** 개체입니다. 작업이 성공적으로 완료 되었으며 그리고 하나 이상 포함 하는 경우이 컬렉션에 개체가 없습니다 **오류** 문제가 발생 하는 공급자가 하나 이상의 오류가 발생 하는 경우 개체입니다. 오류의 정확한 원인을 파악 하려면 각 오류 개체를 검사 합니다.  
  
 발생 한 모든 오류 처리를 완료 하는 즉시 호출 하 여 컬렉션을 지울 수 있습니다는 **지우기** 메서드. 특히 명시적으로 선택 취소 해야는 **오류** 호출 하기 전에 컬렉션의 **Resync**, **UpdateBatch**, 또는 **CancelBatch**메서드를는 **레코드 집합** 개체는 **열려** 메서드를 한 **연결** , 개체 또는 설정는 **필터** 속성에는 **레코드 집합** 개체입니다. 컬렉션을 명시적으로 해제 하 여 특정를 할 수 있습니다 모든 **오류** 이전 작업에서 컬렉션의 개체를 통해 남아 있지 않습니다.  
  
 일부 작업 오류 뿐 아니라 경고를 생성할 수 있습니다. 경고도도 표현 됩니다 **오류** 개체에 **오류** 컬렉션입니다. 공급자를 추가 하면 경고 컬렉션에 런타임 오류를 생성 하지 않습니다. 확인는 **개수** 의 속성에서 **오류** 경고는 특정 작업에 의해 생성 된 여부를 결정 하기 위해 컬렉션입니다. Count가 하나 이상는 **오류** 개체 컬렉션에 추가 했습니다. 확인 했으므로으로 **오류** 오류 또는 경고 컬렉션에 포함 되어, 컬렉션에서 반복 하 고 각각에 대 한 정보를 검색할 **오류** 포함 된 개체입니다. 다음 짧은 Visual Basic에서는이 보여 줍니다.  
  
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
  
 오류 처리 루틴에 포함 되어는 **각** 루프에 있는 각 개체를 검사 하는 **오류** 컬렉션입니다. 이 예제에서는 표시를 위해 메시지 누적 시킵니다. 작업 중인 프로그램에서 각 오류에 대 한 적절 한 작업을 수행 하려면 코드 작성 모두 닫고 같은 파일을 열 및 순서에서 프로그램을 종료 합니다.  
  
## <a name="the-error-object"></a>Error 개체  
 검사 하 여 프로그램 **오류** 어떤 오류가 발생 했는지를 결정 하 고 더 중요 한 응용 프로그램이 나 개체 오류가 발생 한 개체입니다. **오류** 개체 속성은 다음과 같습니다.  
  
|속성 이름|Description|  
|-------------------|-----------------|  
|**Description**|발생 한 오류의 텍스트 설명입니다.|  
|**HelpContext, 도움말 파일**|발생 한 오류에 대 한 설명을 포함 하는 도움말 항목 및 도움말 파일을 가리킵니다.|  
|**NativeError**|공급자 특정 오류 번호입니다.|  
|**번호**|한 수를 나타내는 정수 (Long) (에 나열 된는 **ErrorValueEnum**)에 발생 한 오류입니다.|  
|**원본**|개체 또는 오류를 생성 한 응용 프로그램의 이름을 나타냅니다.|  
|**SQLState**|공급자는 SQL 문의 과정을 반환 하는 5 자의 오류 코드입니다.|  
  
 ADO **오류** 개체는 표준 Visual Basic와 매우 유사 **Err** 개체입니다. 해당 속성에 발생 한 오류에 설명 합니다. 발생 한 오류 수 뿐만 아니라 관련 된 두 가지 정보를 받을 있습니다. **NativeError** 속성에 오류 번호가 사용 중인 공급자와 관련 됩니다. 이전 예제에서는 공급자가 Microsoft OLE DB Provider for SQL Server, 따라서 **NativeError** 오류 SQL Server에 포함 됩니다. **SQLState** 속성에는 SQL 문에서 오류를 설명 하는 5 개 문자로 된 코드입니다.  
  
## <a name="event-related-errors"></a>이벤트 관련 오류  
 **오류** 개체는 이벤트 관련 오류가 발생 하는 경우에 사용 됩니다. ADO 이벤트를 확인 하 여 발생 하는 프로세스에서 오류가 발생 했는지 확인할 수 있습니다는 **오류** 이벤트 매개 변수로 전달 된 개체입니다.  
  
 이벤트를 발생 시키는 작업을 성공적으로 완료 하는 경우는 *adStatus* 이벤트 처리기의 매개 변수를로 설정 됩니다 *adStatusOK*합니다. 반면에, 이벤트를 발생 시킨 작업에 성공 하면는 *adStatus* 로 설정 된 *adStatusErrorsOccurred*합니다. 이 경우에 *pError* 매개 변수가 포함 됩니다는 **오류** 오류를 설명 하는 개체입니다.
