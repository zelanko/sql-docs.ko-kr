---
title: 충돌 감지 및 해결 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05e79fec4c5ddf9d33c9cfaa17581b6d50e0e42b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="detecting-and-resolving-conflicts"></a>충돌 감지 및 해결
직접 실행 모드에서 레코드 집합으로 처리 하는 경우 훨씬 더 적은 동시성 문제가 발생할 가능성이 있습니다. 반면에 응용 프로그램에서 일괄 업데이트 모드를 사용 하는 경우 있을 수 있습니다 좋은 변경 동일한 레코드를 편집 하는 다른 사용자가 수행한 변경 내용을 저장 하기 전에 사용자 레코드를 변경 합니다. 이 경우 응용 프로그램을 정상적으로 충돌을 처리 합니다. 마지막 사용자에 대 한 업데이트는 서버에 보내도록 "알고리즘이 적용 됩니다." 내리 세요 수 있습니다. 또는 가장 최근 사용자가 업데이트 우선 그 제공 두 개의 충돌 하는 값 중 하나를 선택 하 여 결정을 할 수 있습니다.  
  
 어느 경우에 든 ADO 이러한 충돌 유형을 처리 하도록 필드 개체의 UnderlyingValue 및 OriginalValue 속성을 제공 합니다. 조합 하 여 이러한 속성을 사용 하 여 Resync 메서드 및 레코드 집합의 필터 속성을 사용 합니다.  
  
## <a name="remarks"></a>주의  
 ADO가 일괄 처리 업데이트를 사용 하는 동안 충돌을 발견 경고 Errors 컬렉션에 추가 됩니다. 따라서 항상 확인 해야 오류에 대 한 직후 BatchUpdate를를 호출 하 고, 찾을 경우 충돌이 발생 가정 테스트를 시작 합니다. 레코드 집합에 대 한 같음 adFilterConflictingRecords에 Filter 속성을 설정 하는 첫 번째 단계가입니다. 충돌 하는 레코드를 레코드 집합에서 보기를 제한 합니다. RecordCount 속성이이 단계는 0 일 이면 충돌이 이외의 방법으로 오류 발생 알 수 있습니다.  
  
 BatchUpdate를 호출 하는 경우 ADO 및 공급자를 생성 하는 SQL 문을 데이터 원본에서 업데이트를 수행 합니다. 특정 데이터 원본 제한에 열 유형의 WHERE 절에 사용할 있습니다 한지 기억 합니다.  
  
 다음으로 AffectRecords 인수 adAffectGroup와 adResyncUnderlyingValues 동일 하 게 설정 ResyncValues 인수 설정 레코드 집합에서 Resync 메서드를 호출 합니다. Resync 메서드는 기본 데이터베이스에서 현재 레코드 집합 개체의에서 데이터를 업데이트합니다. AdAffectGroup를 사용 하 여 데이터베이스와 현재 필터 충돌 하는 레코드만 즉, 설정으로 표시 되는 레코드는 재 동기화를 보장 됩니다. 큰 레코드 집합으로 처리 하는 경우 상당한 성능 차이가 없습니다. UnderlyingValue 속성 데이터베이스에서 (충돌) 값을 포함 하는, Value 속성에서 사용자가 입력 한 값을 유지 관리할 확인을 설정 하 여 ResyncValues 인수 adResyncUnderlyingValues를 재 동기화를 호출 하는 경우 및 OriginalValue 속성 (만들어진 마지막 성공한 UpdateBatch 호출 되기 전의 값) 필드에 대 한 원래 값을 포함 됩니다. 다음 충돌을 프로그래밍 방식으로 해결 또는 사용자가 사용 되는 값을 선택 하려면 이러한 값을 사용할 수 있습니다.  
  
 이 방법은 다음 코드 예제에 표시 됩니다. 이 예제는 인위적 UpdateBatch가 호출 되기 전에 원본 테이블에 값을 변경 하려면 별도 레코드 집합을 사용 하 여 충돌을 만듭니다.  
  
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
  
 어떤 유형의 충돌이 발생 확인 하려면 현재 레코드 또는 특정 필드의 Status 속성을 사용할 수 있습니다.  
  
 오류 처리에 대 한 자세한 내용은 참조 하십시오. [의 오류 처리](../../../ado/guide/data/error-handling.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
