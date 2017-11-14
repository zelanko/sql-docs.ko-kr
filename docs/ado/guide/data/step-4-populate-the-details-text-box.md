---
title: "4 단계: 세부 정보 텍스트 상자 채우기 | Microsoft Docs"
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
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 512ad22b6529adcf065cacb219d1f0acc025c306
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="step-4-populate-the-details-text-box"></a>4 단계: 세부 정보 텍스트 상자 채우기
정보 텍스트 상자를 채우려면 라는 새 서브루틴을 만들 **recFields** 하 고 다음 코드를 삽입 합니다.  
  
```  
Sub recFields(r As Record, l As ListBox, t As TextBox)  
    Dim f As Field  
    Dim s As Stream  
    Set s = New Stream  
    Dim str As String  
  
    For Each f In r.Fields  
        l.AddItem f.Name & ": " & f.Value  
    Next  
    t.Text = ""  
    If r!RESOURCE_CONTENTCLASS = "text/plain" Then  
        s.Open r, adModeRead, adOpenStreamFromRecord  
        str = s.ReadText(1)  
        s.Position = 0  
        If Asc(Mid(str, 1, 1)) = 63 Then '//63 = "?"  
            s.Charset = "ascii"  
            s.Type = adTypeText  
        End If  
        t.Text = s.ReadText(adReadAll)  
    End If  
End Sub  
```  
  
 이 코드 채웁니다 `lstDetails` 에 전달 되는 간단한 레코드의 값 필드와 `recFields`합니다. 리소스는 텍스트 파일 이면 텍스트 스트림에 리소스 레코드에서 열립니다. 코드 인지 결정 문자 집합은 ASCII에 스트림 내용을 복사 `txtDetails`합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [3단계: 필드 목록 상자 채우기](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)

