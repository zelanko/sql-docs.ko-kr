---
title: "업데이트 됨-SQL Server 문서 | Microsoft Docs"
description: "가져온 조각을 for SQL Server에서 최근에 변경된 된 설명서에 대 한 업데이트 된 콘텐츠를 표시 합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 7fba3b05943b93c0a2c0e76c2d0d5f2696a48d1c
ms.contentlocale: ko-kr
ms.lasthandoff: 06/23/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>신규 / 최근에 업데이트: SQL 서버 문서



거의 매일 Microsoft 업데이트 기존 아티클 중 일부에 해당 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트입니다. 이 문서에는 최근에 업데이트 된 문서에서 발췌 한 내용 표시 됩니다. 새 문서와 연결도 나열 되어 있습니다.

이 문서는 주기적으로 다시 실행 하는 프로그램에서 생성 됩니다. 경우에 따라 발췌 한 구문을 소스 문서에서 불완전 한 서식을 사용 하 여 또는 마크 다운으로 나타날 수 있습니다. 이미지는 여기에 표시 되지 않습니다.

다음 날짜 범위 및 주체에 대 한 최신 업데이트가 보고 됩니다.



- *날짜 범위 업데이트:* &nbsp; **2017-05-01** &nbsp; 을 아래와 같이 &nbsp; **2017-05-23**
- *주제 영역:* &nbsp; **SQL Server**합니다.




&nbsp;

## <a name="updated-articles-with-excerpts"></a>부분 업데이트 되는 문서

이 섹션에는 최근에 발견 된 대규모 업데이트를 문서에서 수집 하는 업데이트의 발췌 한 내용 표시 됩니다.

여기에 표시 된 부분 적절 한 의미 체계 컨텍스트에서 분리 된 나타납니다. 또한 때로는 실제 문서의 주위에 있는 중요 한 마크 다운 구문에서 발췌 한 구문을 분리 됩니다. 따라서 이러한 발췌 한이 내용에 대 한 일반적인 지침만 됩니다. 발췌 한 내용 관심 분야를 클릭 하 고 실제 문서를 참조 하는 데 시간이 걸리는 보증 있는지 여부를 알 수 있습니다에 사용 합니다.

이러한 및 기타 이유로 이러한 부분에서 코드를 복사 하지 않으려면 및 사용 하지 않습니다 정확한 진리도 모든 텍스트 발췌문 합니다. 대신 실제 문서를 참조 합니다.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2017-release-notessql-server-2017-release-notesmd"></a>1. &nbsp;[SQL Server 2017 릴리스 정보](sql-server-2017-release-notes.md)

*Updated: 2017-05-17* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 28.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 84e7a2a49f2893d49380db1ad75695d9a4fd59b2 27a145ad30c10fd667f926d2e092b88c0ba586c5 -->



**SQL Server 2017 CTP 2.1 (2017 년 5 월)**

**설명서 (CTP 2.1)**

- **문제 및 고객 미치는 영향:** 설명서에 대 한 [! INCLUDE [ssSQLv14_md... /includes/sssqlv14-md.md)] 제한 되며 콘텐츠는에 포함 된 [! INCLUDE [ssSQL15_md... /includes/sssql15-md.md)] 설명서 집합입니다.  관련 된 문서에 콘텐츠 [! INCLUDE [ssSQLv14_md... /includes/sssqlv14-md.md)]로 표시 되어 **에 적용 됩니다.**합니다. 
- **문제 및 고객 미치는 영향:** 오프 라인 콘텐츠 ´ ü ± [! INCLUDE [ssSQLv14_md... /includes/sssqlv14-md.md)]입니다.

**SQL Server Reporting Services (CTP 2.1)**


- **문제 및 고객 미치는 영향:** SQL Server Reporting Services와 Power BI의 보고서 서버에 동일한 컴퓨터와 그 중 하나를 제거 하는 경우 더 이상 됩니다 나머지 보고서 서버 구성 관리자와 보고서 서버에 연결할 수 없습니다.
- **해결 방법** 이 문제를 해결 하려면 서버 중 하나를 제거한 후 다음 작업을 수행 해야 합니다.

    1. 관리자 모드에서 명령 프롬프트를 시작 합니다.
    2. 나머지 보고서 서버를 설치한 디렉터리로 이동 합니다.

        *기본 Power BI 보고서 서버에 대 한 위치: C:\Program Files\Microsoft Power BI 보고서 서버*

        *SQL Server Reporting Services의 기본 위치: C:\Program Files\Microsoft SQL Server Reporting Services*

    3. 다음 폴더로 이동 합니다. 이거나 *SSRS* 또는 *PBIRS* 남은 기능에 따라 합니다.
    4. WMI 폴더로 이동 합니다.
    5. 다음 명령을 실행합니다.

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        표시 경우 다음 오류를 무시할 수 있습니다.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

**TSqlLanguageService.msi (CTP 2.1)**


- **문제 및 고객 미치는 영향:** 의 2016 버전이 있는 컴퓨터에 설치한 후 *TSqlLanguageService.msi* (SQL 설치 프로그램을 통해 또는 독립 실행형 재배포 가능 패키지) v13.* (SQL 2016) 버전을 설치 *Microsoft.SqlServer.Management.SqlParser.dll* 및 *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* 제거 됩니다. 2016 버전의 이러한 어셈블리에 종속 되어 있는 모든 응용 프로그램은 다음 작동이 중단, 유사한 오류가 제공: *오류: 파일 또는 어셈블리를 로드할 수 없습니다 ' Microsoft.SqlServer.Management.SqlParser, 버전 13.0.0.0, Culture = neutral, PublicKeyToken = 89845dcd8080cc91 =' 또는 해당 종속성 중 하나입니다. 지정 된 파일을 찾을 수 없습니다.*




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-what39s-new-in-sql-server-2017what-s-new-in-sql-server-2017md"></a>2. &nbsp;[기능 &#39;의 새로운 SQL Server 2017](what-s-new-in-sql-server-2017.md)

*Updated: 2017-05-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 31.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b3e965f62414af06d42f88497958a4bca67befce 82ad09ae9a917f26db3e2210b5cf89585e0e4c4e -->



**SQL Server 2017 CTP 2.1 (2017 년 5 월)의 새로운 기능**

* * SQL Server 데이터베이스 엔진 * *

- 새 DMF, [sys.dm_db_log_stats... / relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), 요약 수준 특성 및 트랜잭션 로그 파일;에 대 한 정보를 노출 하는 도입 되었습니다. 트랜잭션 로그의 상태를 모니터링 하는 데 유용 합니다.  
- 이 CTP에는 버그 수정 및 데이터베이스 엔진에 대 한 성능 향상 기능이 포함 되어 있습니다.
- 자세한 목록은 2017 이전 CTP 릴리스에서 CTP의 향상 된 기능 [새로운 기능 참조 (데이터베이스 엔진)-SQL Server 2017에... / database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

**SQL Server Reporting Services (SSRS)**

- SQL Server Reporting Services는 더 이상 CTP 2.1을 기준으로 SQL Server 설치 프로그램을 통해 설치할 수 없습니다.
- 주석은 보고서에 사용할 수 있습니다. 메모를 사용 하 여 보고서에 포함 된 내용에 큐브 뷰를 추가 하 고 다른 사용자와 조직에서 공동 작업을 수행할 수 있습니다. 또한 사용자 메모와 함께 첨부 파일을 포함할 수 있습니다.
- 더 자세한 SSRS에 대 한 기능에서 이전 버전 정보를 포함 한 새 정보를, [새로운 기능 보기에서 Reporting Services... / reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 
- Power BI 보고서 서버에 대 한 정보를 참조 하십시오. [Power BI 보고서 서버와 함께 시작](https://powerbi.microsoft.com/documentation/reportserver-get-started/)합니다.

**SQL Server 컴퓨터 학습 서비스**

- 이 CTP의 새로운 컴퓨터 학습 서비스 기능이 없는 있습니다.
- 더 자세한 컴퓨터 학습 서비스에 대 한 기능에 이전 Ctp 세부 정보 등 새로운 정보, [새로운 기능 참조에서 SQL Server 컴퓨터 학습 서비스... / advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).  

**SQL Server Analysis Services (SSAS)**

- 이 CTP에는 새로운 SSAS 기능이 없습니다.  
- 향상 된 기능 및 버그 수정이 릴리스에 대 한 자세한 내용은 [새로운 기능 참조에서 SQL Server 2017 Analysis Services... / analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact를 최근에 업데이트 하는 문서 목록

이 압축 목록 이전 섹션에 나열 된 모든 업데이트 된 문서에 대 한 링크를 제공 합니다.

1. [SQL Server 2017 릴리스 정보](#TitleNum_1)
2. [기능 &#39;의 새로운 SQL Server 2017](#TitleNum_2)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>대체 문서

이 섹션 동일한 GitHub 리포지토리 내에서 다른 주제 영역에서 최근에 업데이트 된 아티클에 대 한 매우 유사한 문서를 나열합니다.


&nbsp;

[Microsoft /**sql-docs pr** ](https://github.com/microsoftdocs/sql-docs-pr/) GitHub.com에 리포지토리:

- [최근 업데이트: **관계형 데이터베이스 및 Microsoft SQL Server** docs](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [최근 업데이트: **Microsoft SQL Server** docs](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [최근 업데이트: **SQL Server에서 TRANSACT-SQL** docs](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



