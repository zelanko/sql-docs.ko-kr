---
title: 업데이트됨 - SQL Server용 SSMS 문서 | Microsoft Docs
description: Microsoft SQL Server용 SSMS(SQL Server Management Studio) 설명서에서 최근에 변경된 내용에 대해 업데이트된 콘텐츠의 코드 조각을 표시합니다.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssms
ms.date: 04/28/2018
ms.openlocfilehash: 1ce446219f71baca0f4cdedc835fca929b572a0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>새로 추가되었거나 최근에 업데이트됨: SQL Server용 SSMS(SQL Server Management Studio)



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- 업데이트 날짜 범위: &nbsp; **2018-02-03**&nbsp; - &nbsp;**2018-04-28**
- *주제 영역:* &nbsp; **SSMS(SQL Server Management Studio)**.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [자습서: SQL Server Management Studio를 사용하여 SQL Server 인스턴스에 연결 및 쿼리](tutorials/connect-query-sql-server.md)
2. [자습서: SQL Server Management Studio에서 개체 스크립팅](tutorials/scripting-ssms.md)
3. [자습서: SQL Server Management Studio 구성 요소 및 구성](tutorials/ssms-configuration.md)
4. [자습서: SSMS 사용을 위한 추가 팁과 요령](tutorials/ssms-tricks.md)
5. [자습서: SQL Server Management Studio 내에서 템플릿 사용](tutorials/templates-ssms.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [SQL Server Management Studio - 변경 로그(SSMS)](#TitleNum_1)를 참조하세요.
2. [SSMS(SQL Server Management Studio) 자습서](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>1. &nbsp; [SQL Server Management Studio - 변경 로그(SSMS)](sql-server-management-studio-changelog-ssms.md)

*업데이트됨: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 eb641ac39386a26a76dc303f5bd55eb3f9f4c78d f560f09b51ea30b255c10f7eb86857c3090881d9  (PR=5676  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**[SSMS 17.6]**


릴리스 번호: 17.6<br>
빌드 번호: 14.0.17230.0<br>
릴리스 날짜: 2018년 3월 20일

**새로운 기능**


**일반 SSMS**

SQL Database 관리되는 인스턴스:

- [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에 대한 지원을 추가했습니다. Azure SQL Database 관리되는 인스턴스(미리 보기)는 SQL Server 온-프레미스로 100%에 가까운 호환성, 일반적인 보안 문제를 해결하는 네이티브 [VNet(가상 네트워크)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 구현 및 온-프레미스 SQL Server 고객에 대한 편리한 [비즈니스 모델](https://azure.microsoft.com/pricing/details/sql-database/)을 제공하는 Azure SQL Database의 새로운 특성입니다.
- 다음과 같은 일반적인 관리 시나리오에 대한 지원:
   - 데이터베이스 만들기 및 변경
   - 데이터베이스 백업 및 복원
   - 데이터 계층 응용 프로그램 가져오기, 내보내기, 추출 및 게시
   - 서버 속성 보기 및 변경
   - 전체 개체 탐색기 지원
   - 데이터베이스 개체 스크립팅
   - SQL 에이전트 작업에 대한 지원
   - 연결된 서버에 대한 지원
- [여기에서](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/) 관리되는 인스턴스에 대해 자세히 알아봅니다.

개체 탐색기:
- 개체 탐색기에서 쿼리 창으로 끌어다 놓을 때 이름 주변에 괄호를 적용하지 않도록 추가된 설정 (사용자 제안 [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) 및 [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051))

데이터 분류:
- 일반 개선 사항 및 버그 수정

**IS(Integration Services)**

- [SQL Database 관리되는 인스턴스](docs/ssms/https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)로 패키지 배포에 대한 추가된 지원



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tutorials-for-sql-server-management-studio-ssmstutorialstutorial-sql-server-management-studiomd"></a>2. &nbsp; [SSMS(SQL Server Management Studio) 자습서](tutorials/tutorial-sql-server-management-studio.md)

*업데이트됨: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1))

<!-- Source markdown line 49.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b272c75bab04912ebb706098cf6b6a6c80d9e2b8 d453ebc8251fb83ffcb1af58c9a08bb65b3e9fa2  (PR=5676  ,  Filename=tutorial-sql-server-management-studio.md  ,  Dirpath=docs\ssms\tutorials\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- 자습서: SSMS를 사용하여 SQL Server 연결 및 쿼리

    이 자습서에서는 SQL Server 인스턴스에 연결하는 방법을 알아봅니다. 또한 새 데이터베이스를 만든 다음, 쿼리하는 몇 가지 기본 T-SQL(Transact-SQL) 명령을 알아봅니다.

- 자습서: SSMS에서 개체 스크립팅

    이 자습서에서는 데이터베이스 및 쿼리를 포함하여 SSMS에서 다양한 개체를 스크립팅하는 방법을 알아봅니다.

- 자습서: SSMS에서 템플릿 사용

    이 자습서에서는 SSMS 내에서 미리 작성된 템플릿으로 작업하는 방법을 알아봅니다. 템플릿은 다양한 데이터베이스 관리 작업을 위해 많은 Transact-SQL 코드 조각을 저장하는 잘 알려지지 않은 기능입니다.

- 자습서: SSMS 구성

    이 자습서에서는 환경 레이아웃 변경 등, SSMS 환경 구성의 기본 사항을 학습합니다. 이 자습서는 다양한 SSMS 구성 요소에 대해서도 설명합니다.


- 자습서: SSMS 사용을 위한 추가 팁과 요령

    이 자습서에서는 SSMS 사용을 위한 추가 팁과 요령을 알아봅니다. 자습서에는 다음이 포함되어 있습니다.
    - 텍스트 주석 처리 및 주석 처리 제거
    - 텍스트 들여쓰기
    - 개체 탐색기에서 개체 필터링
    - SQL Server 오류 로그에 액세스
    - 인스턴스 이름 찾기








## <a name="similar-articles-about-new-or-updated-articles"></a>신규 문서 또는 업데이트된 문서에 대한 유사 문서

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *있는* 주제 영역

- [새로 추가되었거나 업데이트됨(11+6):&nbsp; &nbsp;**SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(18+0): &nbsp; &nbsp;**SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(218+14):  **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(14+0): &nbsp; &nbsp;**SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(3+2): &nbsp; &nbsp; **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(3+3): &nbsp; &nbsp; **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(7+10): &nbsp; &nbsp;**SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(0+2): &nbsp; &nbsp; **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(1+3): &nbsp; &nbsp; **SQL Operations Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(2+3): &nbsp; &nbsp; **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(1+1): &nbsp; &nbsp; **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(5+2): &nbsp; &nbsp; **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2): &nbsp; &nbsp; **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)
- [새로 추가되었거나 업데이트됨(1+1): &nbsp; &nbsp; **SQL용 도구** 문서](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *없는* 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 분석 플랫폼 시스템** 문서](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../samples/new-updated-samples.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)

