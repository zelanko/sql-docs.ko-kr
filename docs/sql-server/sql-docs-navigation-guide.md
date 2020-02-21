---
title: SQL Server 설명서 탐색 팁
description: SQL Server 기술 문서 탐색을 위한 팁과 트릭 - 허브 페이지, 목차, 헤더, 이동 경로 사용 방법 및 버전 필터 사용 방법 등을 설명합니다.
ms.date: 10/15/2019
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 5492b4ff50baa805989df3521b01856eb028328e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "76831622"
---
# <a name="sql-server-docs-navigation-guide"></a>SQL Server 설명서 탐색 가이드 

이 항목에서는 SQL Server 기술 설명서 공간을 탐색하기 위한 몇 가지 팁과 요령을 제공합니다.  

## <a name="hub-page"></a>허브 페이지

SQL Server 허브 페이지는에서 [https://aka.ms/sqldocs](https://aka.ms/sqldocs)에서 찾을 수 있으며 관련 SQL Server 콘텐츠를 찾기 위한 진입점입니다.

SQL Server 기술 설명서 내의 모든 페이지 상단에 있는 헤더에서 **SQL 설명서**를 선택하여 이 페이지로 언제든지 다시 이동할 수 있습니다. 

![헤더의 SQL 설명서](media/sql-server-docs-navigation-guide/sql-docs-in-header.png)

## <a name="offline-documentation"></a>오프라인 설명서

SQL Server 설명서를 오프라인 시스템에서 보려는 경우 두 가지 옵션이 있습니다. SQL Server 기술 설명서의 어느 부분이든 PDF로 만들거나 [SQL Server 오프라인 도움말 뷰어](sql-server-help-installation.md)를 사용하여 오프라인 콘텐츠를 다운로드할 수 있습니다. 

PDF를 만들려는 경우 모든 목차의 맨 아래에 있는 **PDF 다운로드** 링크를 선택합니다.


![PDF 다운로드](media/sql-server-docs-navigation-guide/download-pdf.png)

## <a name="toc-symbols"></a>TOC 기호 

항목 끝에 `>` 표시가 있는 TOC(목차)의 항목은 사용자가 다른 목차가 있는 기술 설명서로 이동하게 된다는 의미입니다. 

![목차의 단일 표시](media/sql-server-docs-navigation-guide/single-carrots-in-sql-docs-toc.png)

`>>` 표시가 있는 TOC의 항목은 사용자가 docs.microsoft.com에서 제거된다는 의미입니다. 

![목차 탐색 마커](media/sql-server-docs-navigation-guide/double-carrots-in-sql-docs-toc.png)

이러한 페이지 중 하나를 탐색하는 경우 각 목차의 맨 위에 있는 "SQL Server 시작 >>" 항목을 선택하여 기본 SQL Server 기술 페이지와 목차로 돌아갈 수 있습니다. 

![SQL 목차로 다시 이동](media/sql-server-docs-navigation-guide/navigate-back-to-sql-toc.png)

## <a name="toc-search"></a>TOC 검색 
docs.microsoft.com에서 맨 위에 있는 필터 검색 상자를 사용하여 목차의 내용을 검색할 수 있습니다. 

![필터 상자 사용](media/sql-server-docs-navigation-guide/sql-docs-toc-filter.gif)

## <a name="version-filter"></a>버전 필터
SQL Server 기술 설명서에서는 지원되는 여러 SQL Server 버전에 대한 콘텐츠를 제공합니다. 기능은 SQL Server의 버전에 따라 달라질 수 있으며, 경우에 따라 콘텐츠 자체가 달라질 수 있습니다. 

[버전 필터](versioning-system-monikers-ui-sql-server.md)를 사용하여 SQL Server의 적절한 버전에 대한 콘텐츠를 볼 수 있습니다. 

![SQL 설명서 버전 필터](media/sql-server-docs-navigation-guide/sql-docs-version-filter.gif)

**모든 SQL** \> **모두 표시**를 선택하면 모든 콘텐츠가 표시되고 버전 필터 뒤에 숨겨진 내용이 없습니다. **모두 표시** 옵션은 같은 문서 내에 여러 다른 버전의 SQL Server와 관련된 콘텐츠를 표시할 수 있으며 이는 모순되거나 명확하지 않거나 혼동될 수 있습니다. 이러한 [**모두 표시** 옵션은 일반적인 경우에는 권장되지 않습니다](versioning-system-monikers-ui-sql-server.md#anchor-allsql-hidenothing). 

## <a name="breadcrumbs"></a>이동 경로

이동 경로는 헤더 아래와 목차 위에 있으며 현재 문서가 목차에서 어느 부분에 있는지 나타냅니다.  이를 통해 컨텍스트를 현재 읽고 있는 콘텐츠 형식으로 설정할 수 있으며 목차 트리를 다시 탐색할 수도 있습니다.

![SQL 설명서 이동 경로](media/sql-server-docs-navigation-guide/sql-docs-bread-crumbs.gif)

## <a name="article-section-navigation"></a>문서 섹션 탐색

오른쪽 탐색 창을 사용하면 문서 내의 섹션을 빠르게 탐색하고 문서 내 위치를 파악할 수 있습니다.  

![오른쪽 탐색](media/sql-server-docs-navigation-guide/sql-docs-right-hand-navigation.gif)


## <a name="submit-docs-feedback"></a>설명서 피드백 제출

설명서 내에서 잘못된 점을 발견하면 페이지 맨 아래로 스크롤하고 **콘텐츠 피드백**을 선택하여 해당 설명서에 대해 SQL 콘텐츠 팀에 피드백을 제출할 수 있습니다.

![Git 문제 콘텐츠 피드백](media/sql-server-get-help/git-issues.png)

[https://aka.ms/sqldocsfeedback](https://aka.ms/sqldocsfeedback)에서 일반 설명서 피드백 및 제안을 제출할 수도 있습니다. 

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![SQL 설명서 편집](media/sql-server-docs-navigation-guide/edit-sql-docs.gif)

## <a name="next-steps"></a>다음 단계

- [SQL Server 기술 설명서](index.yml)를 시작하세요.
- SQL Server에 대한 피드백 제출 또는 도움말에 대한 자세한 내용은 [도움말 보기](sql-server-get-help.md) 페이지를 참조하세요. 
- 모든 빠른 시작 및 자습서에 빠르게 액세스하려면 [교육용 SQL 리소스](../sql-server/educational-sql-resources.yml)를 참조하세요.
