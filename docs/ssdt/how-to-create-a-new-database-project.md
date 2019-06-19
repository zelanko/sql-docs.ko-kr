---
title: '방법: 새 데이터베이스 프로젝트 만들기 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbprojectwizard.importschema
- sql.data.tools.SqlProjectImportDatabaseDialog.dialog
- sql.data.tools.importscriptwizard.welcome
- sql.data.tools.importscriptwizard.summary
- sql.data.tools.SqlProjectImportDatabaseSummaryDialog.dialog
- sql.data.tools.importscriptwizard.fileselection
ms.assetid: 0b7883fa-b6e1-4ccf-b1d8-f522fd03a59d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5861f16d20d95ae6ba9d2024d2199b853934d355
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098113"
---
# <a name="how-to-create-a-new-database-project"></a>방법: 새 데이터베이스 프로젝트 만들기
새 데이터베이스 프로젝트를 만들고 기존 데이터베이스, .sql 스크립트 파일 또는 데이터 계층 응용 프로그램(.dacpac)에서 데이터베이스 스키마를 가져올 수 있습니다. 그런 다음 연결된 데이터베이스 개발에 사용할 수 있는 것과 동일한 비주얼 디자이너 도구(Transact\-SQL 편집기, 테이블 디자이너)를 호출하여 오프라인 데이터베이스 프로젝트를 변경하고 변경 내용을 다시 프로덕션 데이터베이스에 게시할 수 있습니다. 변경 내용을 스크립트로 저장하여 나중에 게시할 수도 있습니다. **프로젝트 속성** 창을 사용하면 대상 플랫폼을 SQL Azure를 포함한 다른 버전의 SQL Server로 변경할 수 있습니다.  
  
다음 두 절차에서는 본질적으로 새 데이터베이스 프로젝트를 만들고 기존 데이터베이스에서 스키마를 가져오는 방법으로 동일한 목적을 달성합니다. 각 데이터베이스 개체는 **솔루션 탐색기**에 SQL 스크립트 파일(.sql)로 표시됩니다. 스냅숏에서 데이터베이스 스키마 가져오기에 대한 자세한 내용은 [방법: 프로젝트의 스냅숏 만들기](../ssdt/how-to-create-a-snapshot-of-a-project.md)를 참조하세요.  
  
> [!WARNING]  
> 다음 절차에서는 이전의 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 섹션에 나오는 절차에서 만든 엔터티를 활용합니다.  
  
### <a name="to-create-a-new-database-project-off-a-connected-database"></a>연결된 데이터베이스에서 새 데이터베이스 프로젝트를 만들려면  
  
1.  **SQL Server 개체 탐색기**에서 **TradeDev** 노드를 마우스 오른쪽 단추로 클릭하고 **새 프로젝트 만들기**를 선택합니다.  
  
2.  **데이터베이스 가져오기** 대화 상자에서 **원본 데이터베이스 연결** 설정이 **SQL Server 개체 탐색기**에서 선택한 데이터베이스에 의해 미리 정의되어 있는지 확인합니다. **대상 프로젝트** 설정에서 프로젝트 이름을 **TradeDev**로 변경합니다.  
  
3.  **설정 가져오기** 섹션에서 특정 개체 및 설정을 가져오고 각 스키마 및/또는 개체 유형의 폴더를 만들기 위한 옵션을 살펴봅니다. 모든 데이터베이스 개체로 구성된 계층에 대해 모든 기본 설정을 그대로 사용하고 **시작**을 클릭합니다.  
  
4.  **데이터베이스 가져오기** 대화 상자에는 진행률 표시줄과 SSDT에서 가져오고 있는 개체의 목록이 표시됩니다. 가져오기 작업이 완료되면 **마침**을 클릭하여 최종 화면을 종료합니다.  
  
5.  **솔루션 탐색기**에서 계층 구조를 검사합니다. **dbo** 폴더를 확장하면 개별 **함수**, **테이블** 및 **뷰** 폴더가 표시됩니다. 테이블과 함수는 해당 스키마 폴더 아래에 그룹화됩니다.  
  
6.  **테이블** 아래의 **Products.sql**을 두 번 클릭합니다. **테이블 디자이너**가 열리고, 열 표에 테이블의 시각적 해석이 표시되며 스크립트 창에 테이블의 스크립트 정의가 표시됩니다. 이는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 섹션에서 본 것과 동일합니다.  
  
7.  **CustomerId** 열에 대한 **Null 허용** 상자의 선택을 취소합니다. Ctrl+S를 눌러 파일을 저장합니다.  
  
8.  **솔루션 탐색기**에서 **TradeDev** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **빌드**를 선택하여 데이터베이스 프로젝트를 빌드합니다.  
  
    빌드 작업 결과는 출력 창에서 볼 수 있습니다.  
  
### <a name="to-create-a-new-project-and-import-existing-database-schema"></a>새 프로젝트를 만들고 기존 데이터베이스 스키마를 가져오려면  
  
1.  **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭합니다. **새 프로젝트** 대화 상자의 왼쪽 창에서 **SQL Server**를 선택합니다. 그러면 데이터베이스 프로젝트 형식으로 **SQL Server 데이터베이스 프로젝트** 하나만 표시됩니다. 이전 버전의 Visual Studio와 마찬가지로 플랫폼 관련 프로젝트는 없습니다. 프로젝트를 만든 후 **프로젝트 설정** 대화 상자에서 대상 플랫폼을 설정할 수 있습니다. 이러한 작업은 [방법: 대상 플랫폼 변경 및 데이터베이스 프로젝트 게시](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md) 항목에서 설명합니다.  
  
2.  프로젝트의 이름을 **TradeDev**로 변경하고 **확인**을 클릭하여 새 프로젝트를 만듭니다.  
  
3.  **솔루션 탐색기**에서 새로 만든 **TradeDev** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **가져오기**를 선택한 후 **데이터베이스**를 선택합니다.  
  
    **데이터베이스 가져오기** 대화 상자가 열립니다. **원본 데이터베이스 연결** 섹션에서 **데이터베이스 선택**을 클릭하고 **TradeDev**를 선택합니다. **TradeDev**가 드롭다운 목록에 표시되지 않으면 **새 연결** 단추를 사용하여 연결 속성을 편집합니다.  
  
4.  **설정 가져오기** 섹션에서 특정 개체 및 설정을 가져오고 각 스키마 및/또는 개체 유형의 폴더를 만들기 위한 옵션을 살펴봅니다. 모든 데이터베이스 개체로 구성된 계층에 대해 모든 기본 설정을 그대로 사용하고 **시작**을 클릭합니다.  
  
5.  **데이터베이스 가져오기** 대화 상자에는 진행률 표시줄과 SSDT에서 가져오고 있는 개체의 목록이 표시됩니다. 가져오기 작업이 완료되면 **마침**을 클릭하여 최종 화면을 종료합니다.  
  
6.  **솔루션 탐색기**에서 계층 구조를 검사합니다. **dbo** 폴더를 확장하면 개별 **함수**, **테이블** 및 **뷰** 폴더가 표시됩니다. 테이블과 함수는 해당 스키마 폴더 아래에 그룹화됩니다.  
  
7.  **테이블** 아래의 **Products.sql**을 두 번 클릭합니다. **테이블 디자이너**가 열리고, 열 표에 테이블의 시각적 해석이 표시되며 스크립트 창에 테이블의 스크립트 정의가 표시됩니다. 이는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 섹션에서 본 것과 동일합니다.  
  
8.  **CustomerId** 열에 대한 **Null 허용** 상자의 선택을 취소합니다. Ctrl+S를 눌러 파일을 저장합니다.  
  
9. **솔루션 탐색기**에서 **TradeDev** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **빌드**를 선택하여 데이터베이스 프로젝트를 빌드합니다.  
  
## <a name="see-also"></a>참고 항목  
[방법: 대상 플랫폼 변경 및 데이터베이스 프로젝트 게시](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)  
  
