---
title: 충돌 검색 및 해결 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925560"
---
# <a name="detecting-and-resolving-conflicts"></a>충돌 감지 및 해결
직접 실행 모드에서 레코드 집합을 처리 하는 경우 동시성 문제가 발생 하는 것이 훨씬 줄어듭니다. 반면에 응용 프로그램이 일괄 처리 모드 업데이트를 사용 하는 경우 한 사용자가 동일한 레코드를 편집 하는 다른 사용자가 변경한 내용을 저장 하기 전에 레코드를 변경 하는 것이 좋을 수 있습니다. 이 경우 응용 프로그램에서 충돌을 정상적으로 처리 하는 것이 좋습니다. "Wins" 서버에 대 한 업데이트를 마지막 사용자에 게 보낼 수 있습니다. 또는 충돌 하는 두 값 중에서 선택할 수 있도록 가장 최근의 사용자에 게 우선 순위를 지정할 업데이트를 결정 하도록 할 수 있습니다.  
  
 어떤 경우 든 ADO는 이러한 유형의 충돌을 처리 하기 위해 Field 개체의 UnderlyingValue 및 OriginalValue 속성을 제공 합니다. 이러한 속성은 레코드 집합의 Resync 메서드 및 Filter 속성과 함께 사용 합니다.  
  
## <a name="remarks"></a>설명  
 일괄 처리 업데이트 중에 ADO가 충돌 하는 경우 오류 컬렉션에 경고가 추가 됩니다. 따라서 BatchUpdate를 호출한 후에도 항상 오류를 확인 하 고, 검색 된 경우 충돌이 발생 했다고 가정 하는 테스트를 시작 해야 합니다. 첫 번째 단계는 레코드 집합에서 필터 속성을 adFilterConflictingRecords로 설정 하는 것입니다. 이렇게 하면 레코드 집합의 뷰가 충돌 하는 레코드만으로 제한 됩니다. 이 단계를 수행한 후 RecordCount 속성이 0과 같을 경우 충돌이 아닌 다른 오류로 인해 오류가 발생 한 것을 알 수 있습니다.  
  
 BatchUpdate를 호출 하는 경우 ADO와 공급자는 SQL 문을 생성 하 여 데이터 원본에 대 한 업데이트를 수행 합니다. 특정 데이터 원본에는 WHERE 절에 사용할 수 있는 열 유형에 대 한 제한이 있습니다.  
  
 그런 다음 AffectRecords 인수가 adAffectGroup로 설정 되 고 ResyncValues 인수가 adResyncUnderlyingValues로 설정 된 레코드 집합에서 Resync 메서드를 호출 합니다. Resync 메서드는 기본 데이터베이스에서 현재 레코드 집합 개체의 데이터를 업데이트 합니다. AdAffectGroup를 사용 하 여 현재 필터 설정으로 표시 되는 레코드 (충돌 하는 레코드만)만 데이터베이스와 다시 동기화 되도록 합니다. 이렇게 하면 큰 레코드 집합을 처리 하는 경우 성능이 크게 향상 될 수 있습니다. Resync를 호출할 때 ResyncValues 인수를 adResyncUnderlyingValues로 설정 하면 UnderlyingValue 속성에 데이터베이스의 (충돌) 값이 포함 되 고, Value 속성은 사용자가 입력 한 값을 유지 관리 하 게 됩니다. OriginalValue 속성은 필드의 원래 값을 보유 하 게 됩니다 (마지막으로 성공한 UpdateBatch 호출이 수행 되기 전의 값). 그런 다음 이러한 값을 사용 하 여 프로그래밍 방식으로 충돌을 해결 하거나 사용자가 사용할 값을 선택 하도록 요구할 수 있습니다.  
  
 이 기술은 다음 코드 예제에 나와 있습니다. 이 예에서는 UpdateBatch를 호출 하기 전에 별도의 레코드 집합을 사용 하 여 기본 테이블의 값을 변경 함으로써 충돌을 인위적으로 만듭니다.  
  
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
  
 현재 레코드 또는 특정 필드의 Status 속성을 사용 하 여 발생 한 충돌 유형을 확인할 수 있습니다.  
  
 오류 처리에 대 한 자세한 내용은 [오류 처리](../../../ado/guide/data/error-handling.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
