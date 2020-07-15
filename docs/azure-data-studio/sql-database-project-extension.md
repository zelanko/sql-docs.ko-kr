---
title: SQL Database Projects 확장
description: Azure Data Studio에 대한 SQL Database Projects 확장(미리 보기) 설치 및 사용
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 609af04cec2f6eaaaf1890e19c6d85fbd4bd5b8a
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519172"
---
# <a name="sql-database-projects-extension-preview"></a>SQL Database Projects 확장(미리 보기)

SQL Database 프로젝트 확장(미리 보기)은 프로젝트 기반 개발 환경에서 SQL 데이터베이스를 개발하는 확장입니다. 이 확장은 현재 미리 보기 상태이며 [Azure Data Studio 참가자 빌드](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main)에서 사용할 수 있습니다.


## <a name="install-the-sql-database-projects-extension"></a>SQL Database Projects 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스하려면 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장**을 선택합니다.
2. 확장 검색 상자에 이름 전부 또는 일부를 입력하여 *SQL Database Projects* 확장을 식별합니다. 세부 정보를 보려면 사용 가능한 확장을 선택합니다.

   ![확장 설치](media/extensions/sql-database-projects-extension/install-database-projects.png)

3. 원하는 확장을 선택하고 **설치**합니다.
4. **다시 로드**를 선택하여 확장을 사용하도록 설정합니다(확장을 처음 설치할 때만 필요).
5. 작업 표시줄에서 파일 아이콘을 선택하거나 **보기** 메뉴에서 **탐색기**를 선택합니다. 이제 **Projects**의 새 뷰렛을 사용할 수 있습니다.

   > [!NOTE]
   > 모든 기능을 사용할 수 있도록 [스키마 비교 확장](schema-compare-extension.md)을 SQL Database Projects 확장과 함께 설치하는 것이 좋습니다.

## <a name="getting-started-with-database-projects"></a>Database Projects 시작

* 탐색기에서 **프로젝트** 뷰렛으로 이동하거나 명령 팔레트에서 **새 데이터베이스 프로젝트**를 검색하여 새 데이터베이스 프로젝트를 만듭니다.
* 기존 데이터베이스 프로젝트는 명령 팔레트의 **데이터베이스 프로젝트 열기**에서 열 수 있습니다.
* 명령 팔레트에서 **새 데이터베이스 프로젝트 가져오기**를 사용하여 기존 데이터베이스에서 시작합니다.

   ![새 뷰렛](media/extensions/sql-database-projects-extension/projects-viewlet.png)


### <a name="create-an-empty-database-project"></a>빈 데이터베이스 프로젝트 만들기

 **탐색기**의 **프로젝트** 뷰렛에서 **새 프로젝트** 버튼을 클릭하고 표시되는 텍스트 입력란에 프로젝트 이름을 입력합니다.  표시되는 "폴더 선택" 대화상자에서 프로젝트의 폴더, .sqlproj 파일 및 기타 콘텐츠가 상주할 디렉터리를 선택합니다.
빈 프로젝트가 열리고 **프로젝트** 뷰렛에서 표시되어 편집할 수 있게 됩니다.

### <a name="open-an-existing-project"></a>기존 프로젝트 열기

**프로젝트** 뷰렛에서 **프로젝트 열기** 버튼을 클릭하고 표시되는 파일 선택기에서 기존 *.sqlproj* 파일을 엽니다. Azure Data Studio 또는 [Visual Studio SQL Server Data Tools](../ssdt/sql-server-data-tools.md)에서 기존 프로젝트를 가져올 수 있습니다.

기존 프로젝트가 열리고 콘텐츠가 **프로젝트** 뷰렛에 콘텐츠가 표시되어 편집할 수 있게 됩니다.

### <a name="create-a-database-project-from-an-existing-database"></a>기존 데이터베이스에서 데이터베이스 프로젝트 만들기

**프로젝트** 뷰렛에서 **데이터베이스에서 프로젝트 가져오기** 버튼을 클릭하고 SQL Server에 연결합니다.  연결이 설정되면 사용 가능한 데이터베이스 목록에서 데이터베이스를 선택하고 프로젝트 이름을 설정합니다.

마지막으로 추출의 대상 구조를 선택합니다.  새 프로젝트가 열리고 선택한 데이터베이스의 콘텐츠에 대한 SQL 스크립트가 포함됩니다.

## <a name="build-and-publish"></a>빌드 및 게시

데이터베이스 프로젝트 배포는 [데이터 계층 애플리케이션 파일](../relational-databases/data-tier-applications/data-tier-applications.md)(DACPAC)로 프로젝트를 빌드하고 지원되는 플랫폼에 게시하여 Azure Data Studio용 SQL Database Projects 확장에서 구현됩니다. 이 프로세스에 대한 자세한 내용은 [프로젝트 빌드 및 게시](sql-database-project-extension-build.md)를 참조하세요.

## <a name="schema-compare"></a>스키마 비교
SQL Database Projects 확장은 [스키마 비교 확장](schema-compare-extension.md)이 설치되어 있다면 상호작용하여 프로젝트의 콘텐츠를 dacpac 또는 기존 데이터베이스와 비교합니다.  이러한 스키마 비교를 사용하여 원본과 대상의 차이를 확인하고 대상에 적용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Azure Data Studio용 SQL Database Projects 확장을 사용하여 프로젝트 빌드 및 게시](sql-database-project-extension-build.md)
- [데이터 계층 애플리케이션](../relational-databases/data-tier-applications/data-tier-applications.md)