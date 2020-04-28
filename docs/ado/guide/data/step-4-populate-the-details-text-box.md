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
ms.openlocfilehash: 90748ca7f725ddbf947d9686b846695da0c6626c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924062"
---
# <a name="step-4-populate-the-details-text-box"></a>4단계: 세부 정보 텍스트 상자 채우기
세부 정보 텍스트 상자를 채우려면 새 **서브루틴 이라는 새 서브루틴을 만들고** 다음 코드를 삽입 합니다.  
  
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
  
 이 코드는 `lstDetails` 에 `recFields`전달 된 단순 레코드의 필드 및 값으로 채워집니다. 리소스가 텍스트 파일이 면 리소스 레코드에서 텍스트 스트림이 열립니다. 이 코드는 문자 집합이 ASCII 인지 확인 하 고 스트림 내용을에 `txtDetails`복사 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [3단계: 필드 목록 상자 채우기](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
