---
title: SQL Database Projects 확장
description: Azure Data Studio용 SQL Database Projects 확장을 설치하고 사용합니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: ''
ms.date: 10/22/2020
ms.openlocfilehash: bd361913ac7f094e217b6b75163a0dd96d97d7e2
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496741"
---
# <a name="sql-database-projects-extension-preview"></a>SQL Database Projects 확장(미리 보기)

SQL Database 프로젝트 확장(미리 보기)은 프로젝트 기반 개발 환경에서 SQL 데이터베이스를 개발하는 확장입니다. 


## <a name="features"></a>기능

1. 연결된 데이터베이스에서 프로젝트 만들기
2. 비어 있는 새 프로젝트 만들기
3. 이전의 [Azure Data Studio](sql-database-project-extension-getting-started.md) 또는 [SQL Server Data Tools](../../ssdt/sql-server-data-tools.md)에서 만든 프로젝트 열기
4. 프로젝트에서 테이블, 뷰, 저장 프로시저 또는 사용자 지정 스크립트를 추가하거나 제거하여 프로젝트 편집
5. 폴더의 파일/스크립트 구성
6. 시스템 데이터베이스 또는 사용자 dacpac에 대한 참조 추가
7. 단일 프로젝트 빌드
8. 단일 프로젝트 배포
9. 배포 프로필에서 연결 세부 정보(SQL Windows 인증) 및 SQLCMD 변수 로드

Azure Data Studio의 SQL Database Projects 확장을 소개하는 10분 분량의 다음 동영상을 시청하세요.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Build-SQL-Database-Projects-Easily-in-Azure-Data-Studio/player?WT.mc_id=dataexposed-c9-niner]

## <a name="install-the-sql-database-projects-extension"></a>SQL Database Projects 확장 설치

1. 확장 관리자를 열어 사용 가능한 확장에 액세스합니다.  이렇게 하려면 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장** 을 선택합니다.
2. 확장 검색 상자에 이름 전부 또는 일부를 입력하여 *SQL Database Projects* 확장을 식별합니다. 세부 정보를 보려면 사용 가능한 확장을 선택합니다.

   ![확장 설치](media/sql-database-projects-extension/install-database-projects.png)

3. 원하는 확장을 선택하고 **설치** 합니다.
4. **다시 로드** 를 선택하여 확장을 사용하도록 설정합니다(확장을 처음 설치할 때만 필요).
5. 작업 표시줄에서 파일 아이콘을 선택하거나 **보기** 메뉴에서 **탐색기** 를 선택합니다. 이제 **Projects** 의 새 뷰렛을 사용할 수 있습니다.

   > [!NOTE]
   > .NET Core SDK는 프로젝트 빌드 기능에 필수이며 확장에서 검색할 수 없는 경우 .NET Core SDK를 설치하라는 메시지가 표시됩니다.  .NET Core SDK(v3.1 이상)는 [https://dotnet.microsoft.com/download/dotnet-core/3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1)에서 다운로드하여 설치할 수 있습니다.

   > [!NOTE]
   > 모든 기능을 사용할 수 있도록 [스키마 비교 확장](schema-compare-extension.md)을 SQL Database Projects 확장과 함께 설치하는 것이 좋습니다.

## <a name="known-limitations"></a>알려진 제한 사항

1. Azure Data Studio 뷰렛에서 프로젝트 참조를 추가하고 기존 프로젝트 참조를 로드하는 기능이 현재 지원되지 않습니다.
2. Azure Data Studio 뷰렛에서 파일을 링크로 로드하는 기능이 현재 지원되지 않지만 파일은 트리의 최상위 수준에서 로드되고 빌드는 이러한 파일을 문제 없이 통합합니다.
3. 뷰렛에서 사전/사후 배포 스크립트를 추가하고 로드하는 기능이 현재 지원되지 않지만 이러한 파일이 프로젝트에서 수동으로 추가되면 빌드 시에 적용됩니다.
4. 프로젝트의 SQLCLR 개체는 DacFx의 .NET Core 버전에서 지원되지 않습니다.
5. 작업(빌드/게시)이 사용자 정의되지 않습니다.
6. DacFx에 의해 정의된 대상을 게시합니다.
7. 원본 제어 통합 및 새 프로젝트 만들기에서 .gitignore 파일을 자동으로 만들지 않습니다.
8. WSL 환경 지원이 제한됩니다.

## <a name="next-steps"></a>다음 단계

- [SQL Database Projects 확장 시작](sql-database-project-extension-getting-started.md)
- [Azure Data Studio용 SQL Database Projects 확장을 사용하여 프로젝트 빌드 및 게시](sql-database-project-extension-build.md)
