---
title: 충돌 감지 및 해결 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce9917f144e8c63160f571a986263d8d7e97b21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925560"
---
# <a name="detecting-and-resolving-conflicts"></a>충돌 감지 및 해결
직접 실행 모드에서는 레코드 집합을 사용 하 여 처리 하는 경우 동시성 문제가 발생할 가능성이 낮아집니다 있습니다. 반면에 응용 프로그램 일괄 업데이트 모드를 사용 하는 경우 있을 잘 변경 동일한 레코드를 편집 하는 다른 사용자가 수행한 변경 내용을 저장 하기 전에 하나의 사용자 레코드를 변경 됩니다. 이러한 경우 응용 프로그램을 정상적으로 충돌을 처리 해야 합니다. 마지막으로 서버에 업데이트를 보내는 사용자 "알고리즘이 적용 됩니다." 내리 세요 수도 있습니다. 또는 가장 최근 사용자가 결정 업데이트 충돌 하는 두 값 중에서 선택 사항이 제공 하 여 보다 우선적으로 적용 해야 하는 것이 좋습니다.  
  
 경우에 든 ADO는 이러한 유형의 충돌을 처리 하는 필드 개체의 OriginalValue 및 UnderlyingValue 속성을 제공 합니다. Resync 메서드 및 레코드 집합의 속성 필터 조합 하 여 이러한 속성을 사용 합니다.  
  
## <a name="remarks"></a>설명  
 ADO에서 일괄 처리 업데이트를 사용 하는 동안 충돌이 발생을 하는 경우 경고를 오류 컬렉션에 추가 됩니다. 따라서 항상 확인 해야 오류에 대 한 직후 BatchUpdate, 호출 하 고, 경우 충돌이 발생 한 가정을 테스트를 시작 합니다. 첫 번째 단계에서 레코드 집합에 대 한 같음 adFilterConflictingRecords 필터 속성을 설정 하는 것입니다. 이 충돌 하는 레코드를 레코드 집합에서 보기를 제한 합니다. RecordCount 속성이이 단계를 수행한 후 0 인 경우 충돌이 아닌 오류 발생 알 수 있습니다.  
  
 BatchUpdate를 호출 하는 경우 ADO 및 공급자는 데이터 원본에서 업데이트를 수행 하는 SQL 문을 생성 합니다. 특정 데이터 원본 제한 사항은 열의 형식을 사용할 수는 WHERE 절에 있는 것을 기억 합니다.  
  
 다음으로, AffectRecords 인수 설정 adAffectGroup adResyncUnderlyingValues 같음 설정 ResyncValues 인수를 사용 하 여 레코드 집합에는 다시 동기화 메서드를 호출 합니다. Resync 메서드는 기본 데이터베이스에서 현재 레코드 집합 개체의 데이터를 업데이트합니다. AdAffectGroup를 사용 하 여 데이터베이스를 사용 하 여 충돌 하는 레코드만, 설정을 현재 필터를 사용 하 여 표시 되는 레코드는 재 동기화를 보장 됩니다. 큰 레코드 집합을 사용 하 여 처리 하는 경우 상당한 성능 차이가 수 없습니다. ResyncValues 인수 adResyncUnderlyingValues 다시 동기화를 호출할 때로 설정 하면 Value 속성은 사용자가 입력 한 값을 유지 관리 하는, UnderlyingValue 속성 데이터베이스에서 (충돌) 값을 포함 하 고 OriginalValue 속성 (마지막으로 성공한 UpdateBatch 호출이 이루어진 전의 값) 필드에 대 한 원래 값을 포함 됩니다. 그런 다음 프로그래밍 방식으로 충돌을 해결 하거나 사용자가 사용 되는 값을 선택 해야 이러한 값을 사용할 수 있습니다.  
  
 이 기술은 다음 코드 예제에 표시 됩니다. 인위적 UpdateBatch 호출 되기 전에 기본 테이블의 값을 변경 하려면 별도 레코드 집합을 사용 하 여 충돌을 만듭니다.  
  
```  
'BeginConflicts  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT * FROM Shippers WHERE ShipperID = 2"  
  
    'Open Rs and change a value  
    Set objRs1 = New ADODB.Recordset  
    Set objRs2 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Introduce a conflict at the db...  
    objRs2.Open strSQL, strConn, adOpenKeyset, adLockOptimistic, adCmdText  
    objRs2("Phone") = "(999) 555-9999"  
    objRs2.Update  
    objRs2.Close  
    Set objRs2 = Nothing  
  
    On Error Resume Next  
    objRs1.UpdateBatch  
  
    If objRs1.ActiveConnection.Errors.Count <> 0 Then  
        Dim intConflicts As Integer  
  
        intConflicts = 0  
  
        objRs1.Filter = adFilterConflictingRecords  
  
        intConflicts = objRs1.RecordCount  
  
        'Resync so we can see the UnderlyingValue and offer user a choice.  
        'This sample only displays all three values and resets to original.  
        objRs1.Resync adAffectGroup, adResyncUnderlyingValues  
  
        If intConflicts > 0 Then  
            strMsg = "A conflict occurred with updates for " & intConflicts & _  
                     " record(s)." & vbCrLf & "The values will be restored" & _  
                     " to their original values." & vbCrLf & vbCrLf  
  
            objRs1.MoveFirst  
            While Not objRs1.EOF  
              strMsg = strMsg & "SHIPPER = " & objRs1("CompanyName") & vbCrLf  
              strMsg = strMsg & "Value = " & objRs1("Phone").Value & vbCrLf  
              strMsg = strMsg & "UnderlyingValue = " & _  
                                 objRs1("Phone").UnderlyingValue & vbCrLf  
              strMsg = strMsg & "OriginalValue = " & _  
                                 objRs1("Phone").OriginalValue & vbCrLf  
              strMsg = strMsg & vbCrLf & "Original value has been restored."  
  
              MsgBox strMsg, vbOKOnly, _  
                    "Conflict " & objRs1.AbsolutePosition & _  
                    " of " & intConflicts  
  
              objRs1("Phone").Value = objRs1("Phone").OriginalValue  
              objRs1.MoveNext  
            Wend  
  
            objRs1.UpdateBatch adAffectGroup  
        Else  
            'Other error occurred. Minimal handling in this example.  
             strMsg = "Errors occurred during the update. " & _  
                        objRs1.ActiveConnection.Errors(0).Number & " " & _  
                        objRs1.ActiveConnection.Errors(0).Description  
        End If  
  
        On Error GoTo 0  
    End If  
  
    objRs1.MoveFirst  
    objRs1.Close  
    Set objRs1 = Nothing  
'EndConflicts  
```  
  
 어떤 종류의 충돌 발생을 확인 하려면 특정 필드 또는 현재 레코드의 상태 속성을 사용할 수 있습니다.  
  
 오류 처리에 대 한 자세한 내용은 [오류 처리](../../../ado/guide/data/error-handling.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
