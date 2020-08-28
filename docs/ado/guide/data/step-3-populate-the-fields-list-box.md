---
description: '3단계: 필드 목록 상자 채우기'
title: '3 단계: 필드 목록 상자 채우기 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: rothja
ms.author: jroth
ms.openlocfilehash: acb2572accc19937f7f4ad278fc01aa0e5760a8a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979524"
---
# <a name="step-3-populate-the-fields-list-box"></a>3단계: 필드 목록 상자 채우기
필드 목록 상자를 채우려면 다음 코드를의 Click 이벤트 처리기에 삽입 합니다 `lstMain` .  
  
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
  
 이 코드는 로컬 레코드 및 레코드 집합 개체를 각각 선언 하 고 인스턴스화합니다 `rec` `rs` .  
  
 에서 선택한 리소스에 해당 하는 행을 `lstMain` 의 현재 행으로 설정 합니다 `grs` . 그런 다음 세부 정보 목록 상자가 지워지고 `rec` 의 현재 행을 원본으로 사용 하 여 열립니다 `grs` .  
  
 [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)에 지정 된 대로 리소스가 컬렉션 레코드 이면 로컬 레코드 집합이 `rs` rec의 자식에서 열립니다. 그런 다음 `lstDetails` 는의 행 값으로 채워집니다 `rs` .  
  
 리소스가 단순 레코드 이면 `recFields` 가 호출 됩니다. 에 대 한 자세한 내용은 `recFields` 다음 단계를 참조 하세요.  
  
 리소스가 구조적 문서인 경우 코드는 구현 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [2 단계: 기본 목록 상자 초기화](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [4단계: 세부 정보 텍스트 상자 채우기](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
