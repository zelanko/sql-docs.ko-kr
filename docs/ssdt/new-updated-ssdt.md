---
title: 업데이트됨 - SQL Server용 SSDT 문서 | Microsoft Docs
description: Microsoft SQL Server용 SSDT(SQL Server Data Tools) 설명서에서 최근에 변경된 내용에 대해 업데이트된 콘텐츠의 코드 조각을 표시합니다.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssdt
ms.date: 04/28/2018
ms.openlocfilehash: 99b0844803e1ce95bd6f73b0d45a2baf867428ba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>새로 추가되었거나 최근에 업데이트됨: SSDT(SQL Server Data Tools)



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- 업데이트 날짜 범위: &nbsp; **2018-02-03**&nbsp; - &nbsp;**2018-04-28**
- *주제 영역:* &nbsp; **SSDT(SQL Server Data Tools)**.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SSDT(SQL Server Data Tools)의 Azure Active Directory 지원](azure-active-directory.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [SSDT(SQL Server Data Tools)에 대한 변경 로그](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1. &nbsp; [SSDT(SQL Server Data Tools)에 대한 변경 로그](changelog-for-sql-server-data-tools-ssdt.md)

업데이트한 날짜: 2018년 4월 25일 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 29.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 de18314845cffa197b3fd2ed868f2c330760bedb 5487de1ed57c16a6517a3a8849f412c208f1889f  (PR=5676  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->





**Visual Studio 2017용 SSDT(15.6.0)**

빌드 번호: 14.0.16162.0, 릴리스 날짜: 2018년 4월 10일

**새로운 기능**


**SSIS:**

1.  SQLServer2016 및 SQLServer2017을 대상으로 할 때 AS 처리 작업이 처리 단계를 기록하지 않는 문제 해결
2.  SSDT에서 매우 긴 영어 외 작업 이름으로 dtsx를 열 때 액세스 위반이 발생하는 문제를 해결합니다.
3.  작업 UI에서 간혹 ScriptTask 변수 목록이 사라지는 문제를 해결합니다.
4.  패키지 위치가 SQL Server일 때 기존 패키지 사본 추가가 실패하는 문제 해결
5.  일부 편집기 대화 상자에서 콤보 상자에 액세스할 때 포커스가 멈추는 문제를 해결합니다.
6.  VS 테마를 전환하는 동안 배경이 변경되지 않는 문제를 해결합니다.
7.  어두운 테마에서 주석 및 로드 레이블이 보이지 않는 문제 해결
8.  SSIS 도구 상자 항목에 대해 상태 속성이 올바르게 정의되지 않는 문제를 해결합니다.
9.  WebServiceTask 실행에 항상 실패하는 문제를 해결합니다.
10. 연결 문자열이 프로젝트 매개 변수에 종속적인 변수로 설정된 경우 패키지 배포가 실패하는 문제를 해결합니다.

**설치 관리자:**

1.  개인정보 보호 고지 사항에 "SQL Server Data Tools에 대한 사용자 환경 개선 프로그램" 링크를 추가합니다.
2.  "Visual Studio 2017 인스턴스에 대한 새 SQL Server Data Tools 설치"를 선택할 때 VS 설치 관리자 창이 표시되는 문제 해결

**알려진 문제:**

1.  SSIS 패키지 실행 태스크는 ExecuteOutOfProcess가 True로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.



**Visual Studio 2017용 SSDT(15.5.2)**

빌드 번호: 14.0.16156.0

**새로운 기능**


**SSIS**
1.  SSAS와 SSIS가 동일한 VS 2017 인스턴스에 설치된 경우 SSIS 2008 프로젝트 마이그레이션이 실패하는 문제를 수정합니다.
2.  Rdlc 보고서 디자이너와 SSIS가 동일한 VS 2017 인스턴스에 설치된 경우 Rdlc 프로젝트를 작성할 수 없는 문제를 수정합니다.







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

