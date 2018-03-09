---
title: "2 단계: 기본 목록 상자를 초기화 합니다. | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60ece26fab2c6f691614b609d1dd3f07f42231e4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="step-2-initialize-the-main-list-box"></a>2 단계: 기본 목록 상자를 초기화 합니다.
전역 레코드 및 레코드 집합 개체를 선언 하려면 (일반) (선언) form1에 다음 코드를 삽입:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 이 코드에서는이 시나리오에서는 나중에 사용할 수 있는 레코드와 레코드 집합 개체에 대 한 전역 개체 참조를 선언 합니다.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>URL에 연결 하 고 lstMain 채우기  
 Form1 폼을 로드 이벤트 처리기에 다음 코드를 삽입 합니다.  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=http://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 이 코드는 전역 레코드 및 레코드 집합 개체를 인스턴스화합니다. Record 개체 `grec`는 ActiveConnection로 지정 된 URL로 열립니다. URL이 있으면 열. 이미 존재 하지 않는 경우 자동으로 만들어집니다. 사용자 환경에서 "http://servername/foldername/"는 올바른 url을 바꿔야 함을 note 합니다.  
  
 레코드 집합 개체 `grs`, 레코드의 자식에서 열릴 `grec`합니다. 그런 다음 `lstMain` URL에 게시 된 리소스의 파일 이름으로 채워집니다.  
  
## <a name="see-also"></a>관련 항목:  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [1 단계: Visual Basic 프로젝트 설정](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [3단계: 필드 목록 상자 채우기](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
