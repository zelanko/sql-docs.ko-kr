---
title: "업데이트됨 - SQL Server용 SSDT 문서 | Microsoft Docs"
description: "Microsoft SQL Server용 SSDT(SQL Server Data Tools) 설명서에서 최근에 변경된 내용에 대해 업데이트된 콘텐츠의 코드 조각을 표시합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: ssdt
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.openlocfilehash: 07bfbac52cdd7d118ffd58842fe2085d52265e6f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>새로 추가되었거나 최근에 업데이트됨: SSDT(SQL Server Data Tools)



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-09-28** &nbsp;부터 &nbsp; **2017-12-02**
- *주제 영역:* &nbsp; **SSDT(SQL Server Data Tools)**.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


***지금은 나열할 새 문서가 없습니다.***



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

*업데이트됨: 2017-11-20* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 28.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7700cae7cafe1dac95c240b014f14d9c83e32be4 6416949beaee91da2f77dfebb9eb5ed363db4cb7  (PR=4032  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->




**Visual Studio 2017용 SSDT(15.4.0 미리 보기)**

빌드 번호: 14.0.16134.0

**새로운 기능**


이 릴리스에서는 Visual Studio 2017 15.4 이상의 SQL Server Database, Analysis Services, Reporting Services 및 Integration Services 프로젝트에 대한 독립 실행형 웹 설치 관리자를 제공합니다.

**설치 관리자**


- 사용자가 VS2017 인스턴스에 대한 새로운 SSDT를 설치할 때 애칭을 설정하도록 허용합니다.
- VS 인스턴스가 선택되지 않는 경우 설치 관리자의 기능 선택 확인란을 숨깁니다.
- 고객 의견에 따라 설치 관리자의 일부 메시지를 구체화합니다.
- 설치 관리자가 업그레이드를 지원하지 않는 문제를 해결했습니다.


**SSIS**


- Azure 기능 팩을 설치할 때 가져오기/내보내기 마법사에서 데이터 원본을 나열할 수 없는 문제를 해결했습니다.
- 연결을 변환하는 동안 SSIS Analysis 프로세스 태스크를 편집하면 예외가 throw되는 문제를 해결했습니다.
- __$command_id 열을 추가하는 SQL 수정 프로그램을 적용한 후 CDC 구성 요소가 손상되는 문제를 해결했습니다.
- 이전 SQL Server를 대상으로 타사 패키지를 편집 및 실행할 수 없는 문제를 해결했습니다.
- DTSWizard.exe를 두 번 클릭하고 플랫 파일 원본을 선택하면 플랫 파일 원본 구성 대화 상자가 올바르게 표시되지 않는 문제를 해결했습니다.
- SQL Server 2017을 대상으로 Azure 기능 팩 태스크/구성 요소가 포함된 패키지를 실행할 수 없는 문제를 해결했습니다.


**알려진 문제**

- 설치 프로그램이 지역화되지 않았습니다.
- SSIS 패키지 실행 태스크는 *ExecuteOutOfProcess*가 True로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.


**Visual Studio 2015용 SSDT 17.3**

빌드 번호: 14.0.61709.290

**새로운 기능**


**AS(Analysis Services)**

- Cosmos DB 및 HDI Spark는 1400 모델에서 활성화됩니다.
- 표 형식 데이터 원본 속성
- 이제 "빈 쿼리"는 1400 호환성 수준인 모델의 쿼리 편집기에서 새 쿼리를 만들기 위해 지원되는 옵션입니다.
- 이제 1400 모드 모델의 쿼리 편집기를 사용하면 새 테이블을 자동으로 처리하지 않고 쿼리를 저장할 수 있습니다.







## <a name="similar-articles"></a>유사한 문서

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새로 추가되었거나 업데이트됨(3+14): **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(87 + 0): **SQL용 분석 플랫폼 시스템** 문서](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새로 추가되었거나 업데이트됨(5+4): **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(0+1): **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(2+2): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(10+9): **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(2+4): **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(4+2): **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(0+1): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(21+0): **SQL 작업 Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(5+1): **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(1+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2): **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMA(Data Migration Assistant)** 문서](../dma/new-updated-dma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


