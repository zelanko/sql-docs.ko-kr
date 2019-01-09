---
title: 옵션 (환경-일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Environment.SQLEnvironmentOptions
ms.assetid: c32ccdb8-2cf8-4c78-b474-a3abd3dbbd13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a96b77c3f1243bc3d95cf38242463724348134b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764345"
---
# <a name="options-environment-general-page"></a>옵션(환경-일반 페이지)
   **옵션** 대화 상자를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 시작 동작, 일반 창 관리 옵션 및 기타 일반 설정을 구성할 수 있습니다. **도구** 메뉴에서 **옵션**을 클릭하고 **환경** 폴더를 확장한 다음 **일반**을 클릭합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **시작 시**  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 시작할 때 수행할 동작을 선택합니다. 다음 옵션을 사용할 수 있습니다.  
  
-   **개체 탐색기 열기** 를 선택하면 연결 설정 대화 상자를 표시한 다음 개체 탐색기를 엽니다.  
  
-   **새 쿼리 창 열기** 를 선택하면 연결 설정 대화 상자를 표시한 다음 SQL 쿼리 편집기를 엽니다.  
  
-   **개체 탐색기 및 새 쿼리 열기** 를 선택하면 연결 설정 대화 상자를 표시한 다음 해당 연결을 사용하여 개체 탐색기와 SQL 쿼리 편집기를 엽니다.  
  
-   **빈 환경 열기** 를 선택하면 SQL 쿼리 편집기 창을 열거나 개체 편집기를 서버에 연결하지 않고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 엽니다.  
  
 **개체 탐색기에서 시스템 개체 숨기기**  
 개체 탐색기의 트리 뷰에서 시스템 데이터베이스, 시스템 테이블, 시스템 뷰 및 시스템 저장 프로시저를 제거하려면 이 확인란을 선택합니다. 시스템 함수와 시스템 데이터 형식은 숨겨지지 않습니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에만 적용되고 개체 탐색기에 이미 연결되어 있는 서버에는 영향을 주지 않습니다.  
  
## <a name="environment-layout"></a>환경 레이아웃  
 탭 문서 및 MDI(다중 문서 인터페이스) 환경 모드 간에 전환하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 닫은 다음 다시 열어야 합니다.  
  
 **탭 문서**  
 편집기에서 탭으로 분류되어 있는 문서 창을 표시하려면 이 옵션을 선택합니다. 탭 문서 창은 열려 있는 여러 문서를 구성하거나 여러 문서 간에 전환하려는 경우에 유용합니다.  
  
 **MDI 환경**  
 MDI 환경에서 문서를 열려면 이 옵션을 선택합니다. MDI 문서 창을 사용하면 탭 문서 환경에서 탭이 차지하는 화면 공간을 확보할 수 있습니다. MDI 모드로 작업하는 경우 Ctrl+Tab을 눌러 문서 간에 전환하거나 **창** 메뉴에 있는 바둑판식 배열 옵션을 사용할 수 있습니다.  
  
## <a name="docked-tool-window-behavior"></a>도킹된 도구 창 동작  
 **[닫기] 단추를 누르면 활성 탭만 닫힘**  
 이 확인란을 선택하면 도킹된 집합의 모든 도구 창을 닫는 것이 아니라 현재 포커스가 있는 도구 창만 닫습니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **[자동 숨기기] 단추를 누르면 활성 탭만 숨김**  
 이 확인란을 선택하면 도킹된 집합의 모든 도구 창을 숨기는 것이 아니라 현재 포커스가 있는 도구 창만 자동으로 숨깁니다. 이 확인란은 기본적으로 선택되어 있지 않습니다.  
  
## <a name="display"></a>표시  
 **최근 사용 목록에 n개 파일 표시**  
 **파일** 메뉴에 표시할 최근 프로젝트 및 최근 파일 수를 지정합니다. 1과 24 사이의 숫자를 입력하며 기본값은 4입니다. 이 옵션을 사용하면 최근에 사용한 스크립트 프로젝트 및 파일은 물론 다른 스크립트 프로젝트도 쉽게 검색할 수 있습니다.  
  
  
