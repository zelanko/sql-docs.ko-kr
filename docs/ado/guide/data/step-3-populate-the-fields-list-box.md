---
title: '3단계: 필드 목록 상자 채우기 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f69ab97a522e148d8027042ff7e2c6b09a690424
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704831"
---
# <a name="step-3-populate-the-fields-list-box"></a>3단계: 필드 목록 상자 채우기
필드 목록 상자를 채우려면 Click 이벤트 처리기에 다음 코드를 삽입 `lstMain`:  
  
```  
Private Sub lstMain_Click()  
    Dim rec As Record  
    Dim rs As Recordset  
    Set rec = New Record  
    Set rs = New Recordset  
    grs.MoveFirst  
    grs.Move lstMain.ListIndex  
    lstDetails.Clear  
    rec.Open grs  
    Select Case rec.RecordType  
        Case adCollectionRecord:  
            Set rs = rec.GetChildren  
            While Not rs.EOF  
                lstDetails.AddItem rs(0)  
                rs.MoveNext  
            Wend  
        Case adSimpleRecord:  
            recFields rec, lstDetails, txtDetails  
  
        Case adStructDoc:  
    End Select  
  
End Sub  
```  
  
 이 코드는 선언 하 고 로컬 레코드 및 레코드 집합 개체를 인스턴스화합니다 `rec` 고 `rs`, 각각.  
  
 선택한 리소스에 해당 하는 행 `lstMain` 의 현재 행 이루어집니다 `grs`합니다. 세부 정보 목록 상자를 지우고 다음 하 고 `rec` 의 현재 행과 열은 `grs` 원본으로 합니다.  
  
 리소스 컬렉션 레코드인 경우, 지정 된 대로 [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), 로컬 레코드 집합 `rs` rec의 자식에 대해 열려 있습니다. 그런 다음 `lstDetails` 행의 값으로 채워지는 `rs`합니다.  
  
 리소스 레코드를 간단한 경우 `recFields` 라고 합니다. 에 대 한 자세한 내용은 `recFields`, 다음 단계를 참조 하세요.  
  
 코드가 없는 경우 리소스는 구조화 된 문서에 구현 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [2단계: 기본 목록 상자를 초기화 합니다.](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [4단계: 정보 텍스트 상자 채우기](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
