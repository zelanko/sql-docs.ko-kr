---
title: '4 단계: 세부 정보 텍스트 상자 채우기 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5bb2a49043857cfe9278862efd9e540e4597808
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706842"
---
# <a name="step-4-populate-the-details-text-box"></a>4단계: 세부 정보 텍스트 상자 채우기
정보 텍스트 상자를 채우려면 라는 새 서브루틴을 만들려면 **recFields** 다음 코드를 삽입 합니다.  
  
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
  
 이 코드 채웁니다 `lstDetails` 전달할 간단한 레코드의 값 필드와 `recFields`합니다. 리소스를 텍스트 파일에서 텍스트 Stream 리소스 레코드에서 열립니다. 코드와 문자 집합은 ASCII Stream 콘텐츠를 복사 하는지 여부를 결정 `txtDetails`합니다.  
  
## <a name="see-also"></a>관련 항목  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [3단계: 필드 목록 상자 채우기](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
