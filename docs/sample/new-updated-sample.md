---
title: "SQL Server 문서에 대 한 샘플 업데이트 됨-| Microsoft Docs"
description: "코드 조각에 최근에 변경 된 설명서, Microsoft SQL Server에 대 한 샘플에 대 한 업데이트 된 콘텐츠를 표시 합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: samples
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.author: genemi
ms.workload: sample
ms.openlocfilehash: 363cb5dde93c628317a977082fe8697af890d51c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sample-for-sql-server"></a>새로 추가 되거나 최근에 업데이트 된: SQL Server에 대 한 샘플



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *날짜 범위 업데이트:* &nbsp; **2017-09-28** &nbsp; 을 아래와 같이 &nbsp; **2017-12-02**
- *주제 영역:* &nbsp; **SQL Server에 대 한 샘플**합니다.




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

1. [WideWorldImporters 데이터베이스 카탈로그](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-wideworldimporters-database-catalogworld-wide-importersdatabase-catalog-oltpmd"></a>1. &nbsp;[WideWorldImporters 데이터베이스 카탈로그](world-wide-importers/database-catalog-oltp.md)

*업데이트 됨된: 2017-11-20* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 136.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c055d0483699f06b8766ac2c999101934c14c55c 6975d5a3d1ade7b0ce34bd165bc0e9ef49299ba2  (PR=4032  ,  Filename=database-catalog-oltp.md  ,  Dirpath=docs\sample\world-wide-importers\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->



가능 하면 데이터베이스 collocates 테이블을 조인 복잡성을 최소화 하기 위해 동일한 스키마로 함께 일반적으로 쿼리 됩니다.

데이터베이스 스키마가 되었습니다 코드에서 생성 된 일련의 WWI_Preparation 다른 데이터베이스의 메타 데이터 테이블에 따라. 매우 높은 수준의 일관성 디자인, 명명 일관성 및 완결성 WideWorldImporters 제공합니다. 스키마가 생성 되었습니다 참조 소스 코드: [와이드-실제-가져오기/wwi-데이터베이스-스크립트](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

**테이블 디자인**


- 모든 테이블에는 조인 단순성에 대 한 단일 열 기본 키가 있습니다.
- 모든 스키마, 테이블, 열, 인덱스 및 check 제약 조건에는 개체 또는 열의 목적을 파악 하는 데 사용할 수 있는 속성을 확장 하는 설명이 필요 합니다. 메모리 액세스에 최적화 된 테이블 예외 되므로 현재 확장된 속성을 지원 하지 않습니다.
- 모든 외래 키를 사용 하지 않으면 다른 비클러스터형 인덱스 같은 왼쪽 구성 요소를 자동으로 인덱싱됩니다.
- 테이블에서 자동 번호 지정 시퀀스를 기반으로 합니다. 이러한 시퀀스는 연결 된 서버 및 ID 열 보다 유사한 환경에서 사용 하기 쉽습니다. 메모리 액세스에 최적화 된 테이블 ID 열을 사용 하 여 SQL Server 2016에서 지원 하지 않습니다.
- 단일 시퀀스 (트랜잭션 Id)는 이러한 테이블에 사용 됩니다: CustomerTransactions, SupplierTransactions, 및 StockItemTransactions 합니다. 이 테이블 집합 단일 시퀀스를 가질 수 있습니다는 방법을 보여 줍니다.
- 일부 열에는 적절 한 기본값이 있습니다.

**보안 스키마**


보안을 위해 WideWorldImporters 데이터 스키마에 직접 액세스 하는 외부 응용 프로그램을 허용 하지 않습니다. 액세스를 격리 하려면 WideWorldImporters 데이터를 포함 하지 않은 있지만 뷰 및 저장된 프로시저를 포함 하는 보안 액세스 스키마를 사용 합니다. 외부 응용 프로그램 보안 스키마를 사용 하 여 볼 수 있는 데이터를 검색 합니다.  이러한 방식으로 사용자가 실행할 수 있습니다 뷰 및 저장된 프로시저는 보안 액세스 스키마







## <a name="similar-articles"></a>유사한 문서

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새 + 업데이트 (3 + 14): **SQL에 대 한 고급 분석** docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새 + 업데이트 (87 + 0): **SQL에 대 한 분석 플랫폼 시스템** docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새 + 업데이트 (5 + 4): **SQL에 연결** docs](../connect/new-updated-connect.md)
- [새 + 업데이트 (0 + 1): **SQL에 대 한 데이터베이스 엔진** docs](../database-engine/new-updated-database-engine.md)
- [새 + 업데이트 (2 + 2): **sql Integration Services** docs](../integration-services/new-updated-integration-services.md)
- [새 + 업데이트 (10 + 9): **SQL에 대 한 Linux** docs](../linux/new-updated-linux.md)
- [새 + 업데이트 (2 + 4): **SQL에 대 한 관계형 데이터베이스** docs](../relational-databases/new-updated-relational-databases.md)
- [새 + 업데이트 (4 + 2): **sql Reporting Services** docs](../reporting-services/new-updated-reporting-services.md)
- [새 + 업데이트 (0 + 1): **SQL에 대 한 샘플** docs](../sample/new-updated-sample.md)
- [새 + 업데이트 (21 + 0): **SQL 작업 Studio** docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새 + 업데이트 (5 + 1): **Microsoft SQL Server** docs](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새 + 업데이트 (1 + 0): **SQL Server Migration Assistant (SSMA)** docs](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새 + 업데이트 (0 + 2): **TRANSACT-SQL** docs](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새 + 업데이트 (0 + 0): **데이터 마이그레이션 길잡이 (DMA) sql** docs](../dma/new-updated-dma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


