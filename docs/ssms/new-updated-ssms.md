---
title: 업데이트됨 - SQL Server용 SSMS 문서 | Microsoft Docs
description: Microsoft SQL Server용 SSMS(SQL Server Management Studio) 설명서에서 최근에 변경된 내용에 대해 업데이트된 콘텐츠의 코드 조각을 표시합니다.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql
ms.component: ssms
ms.date: 02/03/2018
ms.openlocfilehash: 8f2ad52b9741a3220a8c5db0a60924a41cc62d27
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>새로 추가되었거나 최근에 업데이트됨: SQL Server용 SSMS(SQL Server Management Studio)



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-12-03** &nbsp;부터 &nbsp; **2018-02-03**까지
- *주제 영역:* &nbsp; **SSMS(SQL Server Management Studio)**.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [영어가 아닌 언어 버전의 SSMS(SQL Server Management Studio) 설치](install-other-languages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [SSMS(SQL Server Management Studio) 다운로드](#TitleNum_1)
2. [SQL Server Management Studio - 변경 로그(SSMS)](#TitleNum_2)를 참조하세요.




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1. &nbsp; [SSMS(SQL Server Management Studio) 다운로드](download-sql-server-management-studio-ssms.md)

*업데이트됨: 2018-01-18* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 83.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0e123e7bdf04f02fcd26ac31fa30ed5f31b19c7d 924246b55d3cad6a5d068da8a41f4be23dcfeb2b  (PR=4652  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



SSMS 17.4는 최신 버전의 SQL Server Management Studio입니다. 17.X 세대의 SSMS는 SQL Server 2017을 통해 SQL Server 2008의 거의 모든 기능 영역을 지원합니다. 버전 17.x는 SQL Analysis Service PaaS도 지원합니다.

17.4 버전에는 다음이 포함됩니다.

취약성 평가:
- 데이터베이스를 검색하여 구성 오류, 과도한 사용 권한, 중요한 데이터 노출 등의 잠재적 취약성 및 모범 사례와의 차이점을 발견하는 새로운 SQL Vulnerability Assessment 서비스가 추가되었습니다.
- 평가 결과에는 각 문제를 해결하는 실행 가능한 단계와 사용자 정의 재구성 스크립트(해당하는 경우)가 포함됩니다. 평가 보고서는 각 환경에 맞게 사용자 지정하고 특정 요구 사항에 맞게 조정할 수 있습니다. [SQL Vulnerability Assessment](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment)에서 자세히 알아보세요.

SMO:
- *HasMemoryOptimizedObjects*가 Azure에서 예외를 throw하는 문제를 수정했습니다.
- 새로운 CATALOG_COLLATION 기능에 대한 지원이 추가되었습니다.

Always On 대시보드:
- 가용성 그룹의 대기 시간 분석 기능이 향상되었습니다.
- 두 개의 새 보고서 *AlwaysOn\_대기 시간\_기본* 및 *AlwaysOn\_대기 시간\_보조* 보고서가 추가되었습니다.

실행 계획:
- 올바른 설명서를 가리키도록 링크가 업데이트되었습니다.
- 생성된 실제 계획에서 바로 단일 계획 분석을 수행할 수 있습니다.
- 새 아이콘 집합이 추가되었습니다.
- GbApply, InnerApply처럼 "논리 연산자 적용"을 인식하는 지원이 추가되었습니다.

XE 프로파일러:
- 이름이 XEvent 프로파일러로 변경되었습니다.
- 이제 중지/시작 메뉴가 기본적으로 세션을 중지/시작합니다.
- 바로 가기 키를 사용할 수 있습니다(예: CTRL + F 키를 누르면 검색).
- XEvent 프로파일러 세션의 적절한 이벤트에 데이터베이스\_이름 및 클라이언트\_호스트 이름 작업이 추가되었습니다. 변경 내용을 적용하려면 서버에서 기존 QuickSessionStandard 또는 QuickSessionTSQL 세션 인스턴스를 삭제해야 할 수도 있습니다 - [3142981 연결](https://connect.microsoft.com/SQLServer/feedback/details/3142981).



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>2. &nbsp; [SQL Server Management Studio - 변경 로그(SSMS)](sql-server-management-studio-changelog-ssms.md)

*업데이트됨: 2018-01-29* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5096fa8f1ae3f2e4bc040f43cb8810d96f2c69c eb641ac39386a26a76dc303f5bd55eb3f9f4c78d  (PR=0  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=ba4b1c2e5200f2f78786b710da18fd38fedde6c9) -->



**[SSMS 17.4](download-sql-server-management-studio-ssms.md)**

일반 공급 | 빌드 번호: 14.0.17213.0

**새로운 기능**


**일반 SSMS**

취약성 평가:
- 데이터베이스를 검색하여 구성 오류, 과도한 사용 권한, 중요한 데이터 노출 등의 잠재적 취약성 및 모범 사례와의 차이점을 발견하는 새로운 SQL Vulnerability Assessment 서비스가 추가되었습니다.
- 평가 결과에는 각 문제를 해결하는 실행 가능한 단계와 사용자 정의 재구성 스크립트(해당하는 경우)가 포함됩니다. 평가 보고서는 각 환경에 맞게 사용자 지정하고 특정 요구 사항에 맞게 조정할 수 있습니다. [SQL Vulnerability Assessment](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment)에서 자세히 알아보세요.

SMO:
- *HasMemoryOptimizedObjects*가 Azure에서 예외를 throw하는 문제를 수정했습니다.
- 새로운 CATALOG_COLLATION 기능에 대한 지원이 추가되었습니다.

Always On 대시보드:
- 가용성 그룹의 대기 시간 분석 기능이 향상되었습니다.
- 두 개의 새 보고서 *AlwaysOn\_대기 시간\_기본* 및 *AlwaysOn\_대기 시간\_보조* 보고서가 추가되었습니다.

실행 계획:
- 올바른 설명서를 가리키도록 링크가 업데이트되었습니다.
- 생성된 실제 계획에서 바로 단일 계획 분석을 수행할 수 있습니다.
- 새 아이콘 집합이 추가되었습니다.
- GbApply, InnerApply처럼 "논리 연산자 적용"을 인식하는 지원이 추가되었습니다.

XE 프로파일러:
- 이름이 XEvent 프로파일러로 변경되었습니다.
- 이제 중지/시작 메뉴가 기본적으로 세션을 중지/시작합니다.
- 바로 가기 키를 사용할 수 있습니다(예: CTRL + F 키를 누르면 검색).
- XEvent 프로파일러 세션의 적절한 이벤트에 데이터베이스\_이름 및 클라이언트\_호스트 이름 작업이 추가되었습니다. 변경 내용을 적용하려면 서버에서 기존 QuickSessionStandard 또는 QuickSessionTSQL 세션 인스턴스를 삭제해야 할 수도 있습니다 - [3142981 연결](https://connect.microsoft.com/SQLServer/feedback/details/3142981).

명령줄:
- SSMS가 Active Directory 인증('통합' 또는 '암호')을 사용하여 자동으로 서버/데이터베이스에 연결하도록 하는 새로운 명령줄 옵션("-G")이 추가되었습니다. 자세한 내용은 [Ssms 유틸리티](ssms-utility.md)를 참조하세요.







## <a name="similar-articles-about-new-or-updated-articles"></a>신규 문서 또는 업데이트된 문서에 대한 유사 문서

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *있는* 주제 영역


- [새로 추가되었거나 업데이트됨(1+3):&nbsp; **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SQL용 분석 플랫폼 시스템** 문서](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(12+1): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(6+2):&nbsp; **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(15+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(2+9):&nbsp; **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(1+0):&nbsp; **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **SQL Operations
 Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(1+2):&nbsp; **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2):&nbsp; **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *없는* 주제 영역


- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMA(Data Migration Assistant)** 문서](../dma/new-updated-dma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../samples/new-updated-samples.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


