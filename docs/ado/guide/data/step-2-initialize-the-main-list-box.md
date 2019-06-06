---
title: '2단계: 기본 목록 상자를 초기화 합니다. | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0df631ccaa9cd3a6177cb4e4e8e63c65286ad361
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700367"
---
# <a name="step-2-initialize-the-main-list-box"></a>2단계: 기본 목록 상자 초기화
전역 레코드 및 레코드 집합 개체를 선언 하려면 (일반) (선언) form1에 다음 코드를 삽입 합니다.  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 이 코드는이 시나리오에서는 나중에 사용할 레코드 및 레코드 집합 개체에 대 한 전역 개체 참조를 선언 합니다.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>URL에 연결한 lstMain 채우기  
 Form1에 대 한 폼 로드 이벤트 처리기에 다음 코드를 삽입 합니다.  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=https://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 이 코드는 전역 레코드 및 레코드 집합 개체를 인스턴스화합니다. 레코드 개체 `grec`는 ActiveConnection로 지정 된 URL로 열립니다. URL에서 볼 수 있으면 열; 아직 존재 하지 않는 경우 만들어집니다. 교체 해야 하는 "<https://servername/foldername/>" 환경에서 올바른 URL을 사용 하 여 합니다.  
  
 레코드 집합 개체 `grs`, 레코드의 자식에 대해 열려 `grec`합니다. 그런 다음 `lstMain` URL에 게시 된 리소스 파일 이름으로 채워집니다.  
  
## <a name="see-also"></a>관련 항목  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [1단계: Visual Basic 프로젝트 설정](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [3단계: 필드 목록 상자 채우기](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
