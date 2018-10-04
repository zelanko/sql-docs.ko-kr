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
manager: craigg
ms.openlocfilehash: 18370885fedb106f02c9b404ea946680aa048b8b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811131"
---
# <a name="provider-errors"></a>공급자 오류
공급자 오류가 발생 하면-2147467259의 런타임 오류를 반환 됩니다. 이 오류를 받게 되 면 확인 합니다 **오류** 활성 컬렉션 **연결** 발생 한 문제를 설명 하는 하나 이상의 오류를 포함 하는 개체입니다.  
  
## <a name="the-ado-errors-collection"></a>ADO 오류 컬렉션  
 ADO를 통해 오류 개체의 컬렉션을 노출 특정 ADO 작업을 여러 공급자 오류가 발생할 수 있으므로 합니다 **연결** 개체입니다. 작업이 성공적으로 완료 하 고 하나 이상 포함 하는 경우이 컬렉션에 개체가 없습니다 **오류** 개체 뭔가 잘못 되 고 공급자가 하나 이상의 오류가 발생 합니다. 오류의 정확한 원인을 파악 하려면 각 오류 개체를 검사 합니다.  
  
 발생 한 모든 오류 처리를 완료 하는 즉시 호출 하 여 컬렉션을 지울 수 있습니다 합니다 **의 선택을 취소** 메서드. 특히 명시적으로 선택 취소 해야 합니다 **오류** 를 호출 하기 전에 컬렉션의 **다시 동기화**, **UpdateBatch**, 또는 **CancelBatch**메서드를는 **레코드 집합** 개체를 **열기** 메서드를를 **연결** 개체를 가져오거나 설정 합니다 **필터** 속성을를 **레코드 집합** 개체입니다. 컬렉션을 명시적으로 지우면 수 있는 모든 **오류** 이전 작업에서 컬렉션의 개체를 통해 남아 있지 않습니다.  
  
 일부 작업 오류 외에도 경고를 생성할 수 있습니다. 경고도도 표현 됩니다 **오류** 개체를 **오류** 컬렉션입니다. 공급자를 컬렉션에는 경고를 추가 하면 런타임 오류는 생성 하지 않습니다. 확인는 **수** 의 속성을 **오류** 경고가 특정 작업에 의해 생성 된 여부를 결정 하기 위해 컬렉션. Count가 하나 이상를 **오류** 개체 컬렉션에 추가 되었습니다. 확인 했으므로 즉시 합니다 **오류** 오류나 경고를 포함 하는 컬렉션, 컬렉션을 반복 하 고 각각에 대 한 정보를 검색할 수 있습니다 **오류** 포함 하는 개체입니다. 다음 간단한 Visual Basic에서는이 보여 줍니다.  
  
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
  
 오류 처리 루틴을 포함 한 **각각에 대 한** 루프의 각 개체를 검사 하는 **오류** 컬렉션. 이 예제에서는 표시에 대 한 메시지를 누적 합니다. 각 오류에 대 한 적절 한 작업을 수행 하는 코드 작성 작업 프로그램에서 모든 닫기와 같은 파일을 열고를 순차적 방식으로 프로그램을 종료 합니다.  
  
## <a name="the-error-object"></a>Error 개체  
 검사 하 여는 **오류** 발생 한 오류 수를 결정 하 고 더 중요 한 응용 프로그램 또는 개체에 따라 오류가 발생 한 개체입니다. 합니다 **오류** 개체에는 다음 속성이 있습니다.  
  
|속성 이름|Description|  
|-------------------|-----------------|  
|**설명**|발생 한 오류의 텍스트 설명입니다.|  
|**HelpContext, HelpFile**|발생 한 오류에 대 한 설명을 포함 하는 도움말 및 도움말 파일을 가리킵니다.|  
|**NativeError**|공급자 특정 오류 번호입니다.|  
|**Number**|수를 나타내는 정수 (Long) (나오는 합니다 **ErrorValueEnum**) 발생 한 오류입니다.|  
|**원본**|개체 또는 오류를 생성 한 응용 프로그램의 이름을 나타냅니다.|  
|**SQLState**|SQL 문의 프로세스 중 공급자를 반환 하는 5 문자 오류 코드입니다.|  
  
 ADO **오류** 개체는 표준 Visual Basic 매우 비슷합니다 **Err** 개체입니다. 해당 속성에는 발생 한 오류를 설명 합니다. 오류 번호를 하는 것 외에도 두 가지 관련된 정보를 받을 있습니다. **NativeError** 은 오류 번호를 포함 하는 속성 사용은 공급자별으로 다릅니다. 이전 예제에서는 공급자가는 Microsoft OLE DB Provider for SQL Server, 따라서 **NativeError** SQL Server 관련 오류가 포함 됩니다. 합니다 **SQLState** 속성이 SQL 문에서 오류를 설명 하는 5 문자 코드입니다.  
  
## <a name="event-related-errors"></a>이벤트 관련 오류  
 합니다 **오류** 개체는 이벤트와 관련 된 오류가 발생 하는 경우에 사용 됩니다. ADO 이벤트를 확인 하 여 발생 하는 프로세스에서 오류가 발생 했는지 여부를 확인할 수 있습니다 합니다 **오류** 개체 이벤트 매개 변수로 전달 합니다.  
  
 이벤트를 발생 시키는 작업은 성공적으로 완료 하는 경우는 *adStatus* 이벤트 처리기의 매개 변수 설정할 *adStatusOK*합니다. 반면, 이벤트를 발생 시킨 작업에 성공 하면 합니다 *adStatus* 매개 변수는 설정 *adStatusErrorsOccurred*합니다. 이런 경우는 *pError* 매개 변수가 포함 됩니다는 **오류** 오류를 설명 하는 개체입니다.
