---
title: '1단계: Visual Basic 프로젝트 설정 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b5f6379eb6cfc1d0f9020019d543cda180d9d88b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700602"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>1단계: Visual Basic 프로젝트 설정
이 시나리오에서는 Microsoft Visual Basic 6.0, 2.5 이상 ADO 및 Microsoft OLE DB Provider for Internet Publishing 시스템에 설치 되어 있는 가정 합니다. 먼저 새 프로젝트를 만들고 일부 컨트롤은 프로젝트의 기본 폼을 추가 합니다.  
  
### <a name="to-create-an-ado-project"></a>ADO 프로젝트를 만들려면:  
  
1.  Microsoft Visual Basic의 새로운 표준 EXE 프로젝트를 만듭니다.  
  
2.  프로젝트 메뉴에서 참조를 선택 합니다.  
  
3.  "Microsoft ActiveX Data Objects 2.5 라이브러리"를 선택 하 고 확인을 클릭 합니다.  
  
### <a name="to-insert-controls-on-the-main-form"></a>기본 폼에 컨트롤 삽입:  
  
1.  Form1에 ListBox 컨트롤을 추가 합니다. 해당 이름 속성을 설정 **lstMain**합니다.  
  
2.  Form1에 다른 ListBox 컨트롤을 추가 합니다. 해당 이름 속성을 설정 **lstDetails**합니다.  
  
3.  Form1에 TextBox 컨트롤을 추가 합니다. 해당 이름 속성을 설정 **txtDetails**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [2단계: 기본 목록 상자를 초기화 합니다.](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
