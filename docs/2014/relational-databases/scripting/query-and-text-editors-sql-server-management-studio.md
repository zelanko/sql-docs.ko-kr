---
title: 쿼리 및 텍스트 편집기
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio]
- Code Editor [SQL Server Management Studio], about Query Editor
- Query Editor [SQL Server Management Studio], full screen mode
- Query Editor [Database Engine], templates
- full screen mode [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], templates
- writing scripts
- modifying scripts
- SQL Server Management Studio [SQL Server], query editor
- Query Editor [SQL Server Management Studio], about Query Editor
- writing queries
- SQL Server Management Studio [SQL Server], editor
- scripts [SQL Server], SQL Server Management Studio
- queries [SQL Server], SQL Server Management Studio
ms.assetid: 062051e4-4b77-4969-98ae-d2547c24ce3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd16879f512bf1529bec8dab6679880cd0a6b8dd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243334"
---
# <a name="query-and-text-editors-sql-server-management-studio"></a>쿼리 및 텍스트 편집기(SQL Server Management Studio)
  
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 편집기 중 하나를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)], MDX, DMX 또는 XML/A 스크립트를 대화식으로 편집 및 테스트하거나 XML 또는 일반 텍스트 파일을 편집할 수 있습니다. 각 편집기에서는 키워드에 색을 지정하고 구문 및 사용법 오류를 검사하는 언어 관련 서비스가 지원됩니다. 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드 문제를 수정하는 데 도움이 되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거가 포함되어 있습니다.  
  
## <a name="sql-server-management-studio-editors"></a>SQL Server Management Studio 편집기  
 
  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 의 네 가지 편집기는 공통 아키텍처를 공유합니다. 텍스트 편집기는 기본 수준의 기능을 구현하며 텍스트 파일의 기본 편집기로 사용될 수 있습니다. 다른 세 개의 편집기인 쿼리 편집기는 SQL Server에서 지원되는 언어 중 하나의 구문을 정의하는 언어 서비스를 포함하여 이 기본 기능을 확장합니다. 또한 쿼리 편집기는 IntelliSense 및 디버깅 같은 편집기 기능을 다양한 수준으로 지원합니다. 쿼리 편집기에는 Transact-SQL 및 XQuery 문을 포함하는 스크립트를 작성하는 데 사용되는 데이터베이스 엔진 쿼리 편집기, MDX 언어용 MDX 편집기, DMX 언어용 DMX 편집기 및 XML for Analysis 언어용 XML/A 편집기가 포함됩니다.  
  
## <a name="common-components"></a>공통 구성 요소  
 
  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 의 모든 편집기는 다음 구성 요소를 공유합니다.  
  
 **코드 창**  
 쿼리 또는 텍스트를 입력하는 영역입니다. 쿼리 편집기의 코드 창에는 해당 언어에 사용할 수 있는 문 작성기 기능이 포함되어 있습니다. 텍스트 편집기 환경에서는 찾기 및 바꾸기, 대량 주석 달기, 사용자 지정 글꼴 및 색 등을 지원합니다.  
  
 텍스트 들여쓰기, 탭 이동, 끌어 놓기 등 코드 창에서 텍스트 작업에 영향을 주는 옵션을 설정할 수 있습니다. 쿼리 창은 문서 창이나 개별 문서에서 탭으로 사용하도록 구성할 수 있습니다.  
  
 **선택 영역 여백**  
 텍스트 줄을 선택할 때 클릭할 수 있는 여백 표시 막대와 코드 텍스트 사이의 공백 부분입니다. 선택 영역 여백을 숨기거나 표시할 수 있습니다.  
  
 **가로 및 세로 스크롤 막대**  
 코드 창을 가로 및 세로로 스크롤하여 코드 창에 표시되는 테두리 밖에 위치한 코드를 볼 수 있도록 합니다.  
  
 **줄 번호 매기기**  
 편집기에서 텍스트나 코드의 왼쪽에 줄 번호를 표시합니다. 특정 줄 번호로 이동할 수 있습니다.  
  
 **자동 줄 바꿈**  
 긴 줄의 텍스트나 코드를 여러 줄로 표시하여 해당 줄의 모든 텍스트를 볼 수 있게 합니다. 자동 줄 바꿈은 텍스트가 실행 또는 출력 시에 표시되는 방법에는 영향을 주지 않습니다. 
  **도구 옵션**, **옵션** 대화 상자의 텍스트 편집기, 모든 언어, 일반 페이지나 특정 편집기 페이지에서 자동 줄 바꿈을 설정할 수 있습니다.  
  
## <a name="code-editor-components"></a>코드 편집기 구성 요소  
 코드 편집기에는 텍스트 편집기 및 XML 편집기와 공유되는 기능 이외에 다음과 같은 기능이 포함되어 있습니다.  
  
 **검색**  
 이 창은 쿼리 결과를 보는 데 사용됩니다. 이 창에서는 표 형태나 텍스트로 결과를 표시하거나, 결과를 파일로 전달할 수 있습니다. 결과 표를 개별 탭 창으로 표시할 수 있습니다.  
  
 **메서드가**  
 편집기의 **편집** 메뉴에서 **IntelliSense**를 가리키면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 옵션이 표시됩니다.  
  
 **색 구분**  
 각 구문 요소 유형을 서로 다른 색으로 표시하여 복잡한 문의 가독성을 향상시킬 수 있습니다.  
  
 **코드 개요**  
 코드 왼쪽의 개요 줄과 함께 코드 그룹을 표시합니다. 코드를 더 간편하게 검토하기 위해 코드 그룹을 축소 및 확장할 수 있습니다.  
  
 **템플릿**  
 템플릿은 데이터베이스에 개체를 만드는 데 필요한 문의 기본 구조가 들어 있는 파일입니다. 템플릿을 사용하여 스크립트를 빠르게 작성할 수 있습니다.  
  
 **메시지가**  
 스크립트가 실행될 때 서버에서 반환하는 오류, 경고 및 정보 메시지가 표시됩니다. 메시지 목록은 스크립트가 다시 실행되기 전에는 변경되지 않습니다.  
  
 **상태 표시줄**  
 쿼리 편집기가 연결되는 인스턴스와 같이 쿼리 편집기 창과 관련된 시스템 정보를 표시합니다.  
  
## <a name="database-engine-query-editor-components"></a>데이터베이스 엔진 쿼리 편집기 구성 요소  
 다음은 데이터베이스 엔진 쿼리 편집기에서만 사용할 수 있는 구성 요소입니다.  
  
 **디버거**  
 특정 문에서의 코드 실행을 일시 중지할 수 있습니다. 그리고 나서 데이터 및 시스템 정보를 검토하여 코드 오류를 찾을 수 있습니다.  
  
 **오류 목록**  
 Intellisense에서 발견된 구문 및 의미 오류를 표시합니다. 이 오류 목록은 사용자가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 편집할 때 동적으로 변경됩니다.  
  
 **그래픽 실행 계획**  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 실행 계획에 따라 제공되는 논리 단계를 표시합니다.  
  
 **클라이언트 통계**  
 범주로 그룹화된 쿼리 실행에 대한 정보를 표시합니다. 
  **쿼리** 메뉴의 **클라이언트 통계 포함** 이 선택된 경우 쿼리 실행 시 **클라이언트 통계** 창이 표시됩니다. 연속된 쿼리 실행의 통계는 평균값과 함께 나열됩니다. 
  **쿼리** 메뉴의 **클라이언트 통계 다시 설정** 을 선택하여 평균을 다시 설정합니다.  
  
 **코드 조각**  
 데이터베이스 엔진 쿼리 편집기에서 문을 추가할 때 시작 지점으로 사용할 수 있는 템플릿입니다. SQL Server와 함께 제공되는 미리 정의된 코드 조각을 삽입하거나 사용자가 작성한 코드 조각을 추가할 수 있습니다.  
  
 **SQLCMD 모드**  
 sqlcmd 유틸리티에서 지원되는 명령 집합을 포함하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 실행합니다. 자세한 내용은 [sqlcmd 방법 도움말 항목](../../database-engine/sqlcmd-how-to-topics.md)을 참조하세요.  
  
## <a name="editor-tasks"></a>편집기 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서 기본 기능을 보거나 사용하는 방법에 대해 설명합니다.|[데이터베이스 엔진 쿼리 편집기 &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)|  
|MDX 쿼리 편집기에서 기본 기능을 보거나 사용하는 방법에 대해 설명합니다.|[MDX 쿼리 편집기 &#40;Analysis Services 다차원 데이터&#41;](../../analysis-services/mdx-query-editor-analysis-services-multidimensional-data.md)|  
|DMX 쿼리 편집기에서 기본 기능을 보거나 사용하는 방법에 대해 설명합니다.|[DMX 쿼리 편집기 &#40;Analysis Services 데이터 마이닝&#41;](../../analysis-services/dmx-query-editor-analysis-services-data-mining.md)|  
|XML/A 편집기에서 기본 기능을 보거나 사용하는 방법에 대해 설명합니다.|[XML 편집기 &#40;SQL Server Management Studio&#41;](xml-editor-sql-server-management-studio.md)|  
|줄 번호 매기기 및 IntelliSense 옵션과 같은 다양한 편집기 옵션을 구성하는 방법을 설명합니다.|[편집기 &#40;SQL Server Management Studio 구성&#41;](configure-editors-sql-server-management-studio.md)|  
|
  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 편집기를 여는 다양한 방법에 대해 설명합니다.|[편집기 &#40;SQL Server Management Studio를 엽니다&#41;](open-an-editor-sql-server-management-studio.md)|  
|자동 줄 바꿈, 창 분할, 탭 등과 같은 뷰 모드 관리 방법에 대해 설명합니다.|[편집기 및 보기 모드 관리](manage-the-editor-and-view-mode.md)|  
|숨겨진 텍스트 또는 들여쓰기 같은 서식 옵션을 설정하는 방법에 대해 설명합니다.|[코드 서식 관리](manage-code-formatting.md)|  
|증분 검색, 이동 등과 같은 기능을 사용하여 편집기 창에서 편집기를 탐색하는 방법에 대해 설명합니다.|[코드 및 텍스트 이동](navigate-code-and-text.md)|  
|복잡한 문을 쉽게 읽을 수 있도록 다양한 구문에 대한 색 구분 옵션을 설정하는 방법에 대해 설명합니다.|[쿼리 편집기의 색 구분](color-coding-in-query-editors.md)|  
|코드 윤곽을 사용하여 현재 사용하지 않는 복잡한 스크립트 부분을 숨기는 방법에 대해 설명합니다.|[코드 개요](code-outlining.md)|  
|텍스트를 스크립트의 한 위치에서 다른 위치로 끌어서 놓는 방법에 대해 설명합니다.|[텍스트 끌어서 놓기](drag-and-drop-text.md)|  
|열 이름을 변경할 때처럼 전역 검색 및 바꾸기를 수행하는 방법에 대해 설명합니다.|[검색 및 바꾸기](search-and-replace.md)|  
|코드의 중요 한 부분을 더 쉽게 찾기 위해 책갈피를 설정하는 방법에 대해 설명합니다.|[책갈피 관리](../native-client-ole-db-rowsets/bookmarks.md)|  
|창 또는 표에서 스크립트 또는 결과를 인쇄하는 방법에 대해 설명합니다.|[코드 및 결과 인쇄](print-code-and-results.md)|  
|
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서 sqlcmd 기능을 사용하는 방법에 대해 설명합니다.|[쿼리 편집기를 사용 하 여 SQLCMD 스크립트 편집](edit-sqlcmd-scripts-with-query-editor.md)|  
|사용자가 입력하는 개체 이름 자동 완성, 유효한 위치에 중단점 배치 등과 같은 IntelliSense 기능을 사용하는 방법에 대해 설명합니다.|[IntelliSense &#40;SQL Server Management Studio&#41;](intellisense-sql-server-management-studio.md)|  
|
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서 코드 조각을 사용하는 방법에 대해 설명합니다. 코드 조각은 일반적으로 사용되는 문 또는 블록에 대한 템플릿이며, 사이트별 코드 조각을 포함하도록 사용자 지정하거나 확장할 수 있습니다.|[Transact-sql 코드 조각](transact-sql-code-snippets.md)|  
|
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거를 사용하여 코드를 단계별로 처리하고 변수 및 매개 변수 값과 같은 디버깅 정보를 보는 방법에 대해 설명합니다.|[Transact-sql 디버거](transact-sql-debugger.md)|  
|
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스별로 사용자 지정 색을 설정하고 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창에서 상태 표시줄의 배경색을 설정하는 방법에 대해 설명합니다.|[상태 표시줄 &#40;데이터베이스 엔진 쿼리 편집기&#41;](status-bar-database-engine-query-editor.md)|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Management Studio 바로 가기 키](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
