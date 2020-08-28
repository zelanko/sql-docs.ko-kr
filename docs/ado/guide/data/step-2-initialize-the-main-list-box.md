---
description: '2단계: 기본 목록 상자 초기화'
title: '2 단계: 기본 목록 상자 초기화 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: rothja
ms.author: jroth
ms.openlocfilehash: 63dd3524ddd70885495c116ff875369ac34784ef
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979534"
---
# <a name="step-2-initialize-the-main-list-box"></a>2단계: 기본 목록 상자 초기화
전역 레코드 및 레코드 집합 개체를 선언 하려면 Form1의 (일반) (선언)에 다음 코드를 삽입 합니다.  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 이 코드는이 시나리오에서 나중에 사용 될 레코드 및 레코드 집합 개체에 대 한 전역 개체 참조를 선언 합니다.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>URL에 연결 하 고 lstMain을 채우려면  
 Form1의 폼 로드 이벤트 처리기에 다음 코드를 삽입 합니다.  
  
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
  
 이 코드는 전역 레코드 및 레코드 집합 개체를 인스턴스화합니다. `grec`ActiveConnection로 지정 된 URL이 있는 Record 개체가 열립니다. URL이 있는 경우 열립니다. 아직 존재 하지 않는 경우 생성 됩니다. 를 `https://servername/foldername/` 사용자 환경의 올바른 URL로 바꾸어야 합니다.  
  
 레코드 집합 개체는 `grs` 레코드의 자식에 대해 열립니다 `grec` . 그런 다음 `lstMain` URL에 게시 된 리소스의 파일 이름으로 채워집니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [1 단계: Visual Basic 프로젝트 설정](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [3단계: 필드 목록 상자 채우기](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
