---
title: "3 단계: 필드 목록 상자 채우기 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6ef92cbf72ad8a8aa3a8076be7ccaf3761f51ab0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="step-3-populate-the-fields-list-box"></a>3 단계: 필드 목록 상자 채우기
필드 목록 상자를 채우려면의 Click 이벤트 처리기에 다음 코드를 삽입 `lstMain`:  
  
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
  
 이 코드는 선언 하 고 로컬 기록 및 레코드 집합 개체를 인스턴스화합니다 `rec` 및 `rs`각각.  
  
 선택한 리소스에 해당 하는 행 `lstMain` 의 현재 행 이루어집니다 `grs`합니다. 다음 세부 정보 목록 상자를 지우고 및 `rec` 의 현재 행으로 열려 `grs` 소스로 합니다.  
  
 리소스 컬렉션 레코드인 경우에 지정 된 대로 [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), 로컬 Recordset `rs` rec의 자식을에서 열릴 합니다. 그런 다음 `lstDetails` 의 행의 값으로 채워지는 `rs`합니다.  
  
 리소스가 있는 경우 단순 레코드 `recFields` 호출 됩니다. 에 대 한 자세한 내용은 `recFields`, 다음 단계를 참조 하세요.  
  
 코드가 없는 리소스가 있는 경우 구조적된 문서 구현 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [2 단계: 기본 목록 상자를 초기화 합니다.](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [4단계: 세부 정보 텍스트 상자 채우기](../../../ado/guide/data/step-4-populate-the-details-text-box.md)

