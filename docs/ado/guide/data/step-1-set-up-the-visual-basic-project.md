---
title: '1 단계: Visual Basic 프로젝트 설정 | Microsoft Docs'
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
ms.openlocfilehash: bd44990c38a30f26e682fbb7f1f6aef642043215
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924080"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>1단계: Visual Basic 프로젝트 설정
이 시나리오에서는 Microsoft Visual Basic 6.0, ADO 2.5 이상 및 Microsoft OLE DB Provider for Internet Publishing이 시스템에 설치 되어 있다고 가정 합니다. 먼저 새 프로젝트를 만든 다음 일부 컨트롤을 프로젝트의 기본 폼에 추가 합니다.  
  
### <a name="to-create-an-ado-project"></a>ADO 프로젝트를 만들려면 다음을 수행 합니다.  
  
1.  Microsoft Visual Basic에서 새 표준 EXE 프로젝트를 만듭니다.  
  
2.  프로젝트 메뉴에서 참조를 선택 합니다.  
  
3.  "Microsoft ADO(ActiveX Data Objects) 2.5 Library"를 선택 하 고 확인을 클릭 합니다.  
  
### <a name="to-insert-controls-on-the-main-form"></a>기본 폼에 컨트롤을 삽입 하려면:  
  
1.  ListBox 컨트롤을 Form1에 추가 합니다. Name 속성을 **Lstmain**으로 설정 합니다.  
  
2.  다른 ListBox 컨트롤을 Form1에 추가 합니다. Name 속성을 **Lstdetails**로 설정 합니다.  
  
3.  텍스트 상자 컨트롤을 Form1에 추가 합니다. Name 속성을 **Txtdetails**로 설정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)   
 [2단계: 기본 목록 상자 초기화](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
