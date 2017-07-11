---
title: "업데이트 됨-관계형 데이터베이스 docs | Microsoft Docs"
description: "가져온 조각을 관계형 데이터베이스에 대 한 최근에 변경 된 설명서에 대 한 업데이트 된 콘텐츠를 표시 합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 06/30/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 19b664245f45ad45a4c7d1eba249858030fad718
ms.contentlocale: ko-kr
ms.lasthandoff: 07/03/2017

---
<a id="new-and-recently-updated-relational-databases-docs" class="xliff"></a>

# 신규 / 최근에 업데이트: 관계형 데이터베이스 docs



거의 매일 Microsoft 업데이트 기존 아티클 중 일부에 해당 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트입니다. 이 문서에는 최근에 업데이트 된 문서에서 발췌 한 내용 표시 됩니다. 새 문서와 연결도 나열 되어 있습니다.

이 문서는 주기적으로 다시 실행 하는 프로그램에서 생성 됩니다. 경우에 따라 발췌 한 구문을 소스 문서에서 불완전 한 서식을 사용 하 여 또는 마크 다운으로 나타날 수 있습니다. 이미지는 여기에 표시 되지 않습니다.

다음 날짜 범위 및 주체에 대 한 최신 업데이트가 보고 됩니다.



- *업데이트 날짜 범위:* &nbsp; **2017-05-17** &nbsp; ~ &nbsp; **2017-06-30**
- *주제 영역:* &nbsp; **관계형 데이터베이스**합니다.




&nbsp;

<a id="new-articles-created-recently" class="xliff"></a>

## 최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SQL Server 2016용 SQL Server 메모리 내 OLTP 내부](in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016.md)
2. [SQL 데이터베이스의 적응 쿼리 처리](performance/adaptive-query-processing.md)
3. [Microsoft SQL 플랫폼을 사용한 개인 정보 보호 향상 및 GDPR 요구 사항 해결 가이드](security/microsoft-sql-and-the-gdpr-requirements.md)
4. [sys.dm_db_log_stats(Transact-SQL)](system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)
5. [sys.dm_exec_query_parallel_workers(Transact-SQL)](system-dynamic-management-views/sys-dm-exec-query-parallel-workers-transact-sql.md)



&nbsp;

<a id="updated-articles-with-excerpts" class="xliff"></a>

## 부분 업데이트 되는 문서

이 섹션에는 최근에 발견 된 대규모 업데이트를 문서에서 수집 하는 업데이트의 발췌 한 내용 표시 됩니다.

여기에 표시 된 부분 적절 한 의미 체계 컨텍스트에서 분리 된 나타납니다. 또한 때로는 실제 문서의 주위에 있는 중요 한 마크 다운 구문에서 발췌 한 구문을 분리 됩니다. 따라서 이러한 발췌 한이 내용에 대 한 일반적인 지침만 됩니다. 발췌 한 내용 관심 분야를 클릭 하 고 실제 문서를 참조 하는 데 시간이 걸리는 보증 있는지 여부를 알 수 있습니다에 사용 합니다.

이러한 및 기타 이유로 이러한 부분에서 코드를 복사 하지 않으려면 및 사용 하지 않습니다 정확한 진리도 모든 텍스트 발췌문 합니다. 대신 실제 문서를 참조 합니다.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

<a id="1-nbsp-altering-memory-optimized-tablesin-memory-oltpaltering-memory-optimized-tablesmd" class="xliff"></a>

### 1. &nbsp; [메모리 최적화 테이블 변경](in-memory-oltp/altering-memory-optimized-tables.md)

*업데이트됨: 2017-06-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 82.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8359700b5db24838f1bb273526794c2865bbbe11 41d77cf0bbcf53a1b64d6524a24e5736c5a073da  (PR=2171  ,  Filename=altering-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**메모리 최적화 테이블에 대한 ALTER TABLE 로깅**

대부분 ALTER TABLE 시나리오는 이제 병렬로 실행되고 이를 통해 트랜잭션 로그에 대한 쓰기가 최적화됩니다. 최적화는 메타데이터 변경 내용을 트랜잭션 로그에 기록해야만 가능합니다. 그러나 다음 ALTER TABLE 작업은 단일 스레드를 실행하고 로그에 최적화되지 않습니다.

이 경우 단일 스레드 작업은 변경된 테이블의 전체 내용을 트랜잭션 로그에 기록합니다. 단일 스레드 작업 목록은 다음과 같습니다.

- 큰 개체(LOB) 형식인 nvarchar(max), varchar(max) 또는 varbinary(max)를 사용하도록 열을 변경하거나 추가합니다.

- COLUMNSTORE 인덱스를 추가하거나 삭제합니다.

- [off-row column--../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)에 영향을 주는 거의 모든 항목입니다.

    - 행 내부 열이 행 외부 열을 이동하게 합니다.

    - 행 외부 열이 행 내부 열을 이동하게 합니다.

    - 새 행 외부 열을 만듭니다.

    - *예외:* 이미 행 외부 형식인 열을 늘리면 최적화된 방식으로 기록됩니다. 
  




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

<a id="2-nbsp-table-and-row-size-in-memory-optimized-tablesin-memory-oltptable-and-row-size-in-memory-optimized-tablesmd" class="xliff"></a>

### 2. &nbsp; [메모리 최적화 테이블의 테이블 및 행 크기](in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)

*업데이트됨: 2017-06-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1) | [다음](#TitleNum_3))

<!-- Source markdown line 114.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 27ce0fa2e7bb464f9c3d6e32dd195de3b79abfcd 0a3cacd86024e2b734704ffd37e55ca0b17a0c94  (PR=2163  ,  Filename=table-and-row-size-in-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=fe6de2b16b9792a5399b1c014af72a2a5ee52377) -->



 
  
 [row body size] 계산은 다음 표에서 설명합니다.  
  
 행 본문 크기는 계산된 크기 및 실제 크기의 두 가지 방식으로 계산할 수 있습니다.  
  
-   [computed row body size]로 표시되는 계산 크기는 행 크기 제한인 8,060바이트를 초과하는지 여부를 확인하기 위해 사용됩니다.  
  
-   [actual row body size]로 표시되는 실제 크기는 메모리 및 검사점 파일에서 행 본문의 실제 저장소 크기입니다.  
  
 [computed row body size] 및 [actual row body size]는 모두 비슷하게 계산됩니다. 유일한 차이점은 다음 표의 하단에 표시된 것처럼 (n)varchar(i) 및 varbinary(i) 열의 크기에 대한 계산입니다. 계산된 행 본문 크기는 선언된 크기인 *i* 를 열 크기로 사용하고, 실제 행 본문 크기는 데이터의 실제 크기를 사용합니다.  
  
 다음 표에서는 [actual row body size] = SUM([size of shallow types]) + 2 + 2 * [number of deep type columns]와 같이 행 본문 크기의 계산에 대해 설명합니다.  
  
|섹션|크기|설명|  
|-------------|----------|--------------|  
|단순 형식 열|SUM([단순 형식의 크기]) 개별 형식의 바이트 크기는 다음과 같습니다.<br /><br /> **Bit**: 1<br /><br /> **Tinyint**: 1<br /><br /> **Smallint**: 2<br /><br /> **Int**: 4<br /><br /> **Real**: 4<br /><br /> **Smalldatetime**: 4<br /><br /> **Smallmoney**: 4<br /><br /> **Bigint**: 8<br /><br /> **Datetime**: 8<br /><br /> **Datetime2**: 8<br /><br /> **Float**: 8<br /><br /> **Money**: 8<br /><br /> **숫자**(전체 자릿수<=18): 8<br /><br /> **Time**: 8<br /><br /> **숫자**(전체 자릿수>18): 16<br /><br /> **Uniqueidentifier**: 16||  
|단순 열 패딩|가능한 값은<br /><br /> 전체 형식 열이 있고 단순 열의 총 데이터 크기가 홀수인 경우 1입니다.<br /><br /> 그렇지 않으면 0입니다.|전체 형식은 (var)binary 및 (n)(var)char 형식입니다.|  




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

<a id="3-nbsp-post-migration-validation-and-optimization-guidepost-migration-validation-and-optimization-guidemd" class="xliff"></a>

### 3. &nbsp; [마이그레이션 후 유효성 검사 및 최적화 가이드](post-migration-validation-and-optimization-guide.md)

*업데이트됨: 2017-06-21* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_2) | [다음](#TitleNum_4))

<!-- Source markdown line 27.  ms.author= "harinid".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 faa2e3dd8be3aeb475bf8c7f71617ebf17969892 f2760dfecda10baeb121929b72a4d8164e81185b  (PR=2126  ,  Filename=post-migration-validation-and-optimization-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=dcbeda6b8372b358b6497f78d6139cad91c8097c) -->



다음은 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 플랫폼으로 마이그레이션한 후 발생하는 몇 가지 일반적인 성능 시나리오 및 해결 방법입니다. 여기에는 이전 버전 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)]에서 새 버전 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)]로의 마이그레이션 및 Oracle, DB2, MySQL, Sybase 등의 외래 플랫폼에서 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)]로의 마이그레이션에 특정한 시나리오가 포함됩니다.

**<a name="CEUpgrade"></a> CE 버전 변경으로 인한 쿼리 회귀**


**적용 대상:** [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)]로의 마이그레이션.

이전 버전의 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssSQL14--../includes/sssql14-md.md)] 이상으로 마이그레이션하고 [database compatibility level--../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)을 최신 버전으로 업그레이드하는 경우 워크로드가 성능 회귀 위험에 노출될 수 있습니다.

[!INCLUDE[ssSQL14--../includes/sssql14-md.md)]부터는 쿼리 최적화 프로그램의 모든 변경 내용이 최신 [database compatibility level--../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)에 연결되므로 계획이 업그레이드 시점에 즉시 변경되지 않고 사용자가 `COMPATIBILITY_LEVEL` 데이터베이스 옵션을 최신 상태로 변경하는 경우에 변경됩니다. 이 기능은 쿼리 저장소와 함께 업그레이드 프로세스에서 쿼리 성능에 대한 뛰어난 제어 수준을 제공합니다. 

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에 도입된 쿼리 최적화 프로그램 변경 사항에 대한 자세한 내용은 [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](http://msdn.microsoft.com/library/dn673537.aspx)(SQL Server 2014 카디널리티 평가기로 쿼리 계획 최적화)를 참조하세요.




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

<a id="4-nbsp-sysquerystoreplan-transact-sqlsystem-catalog-viewssys-query-store-plan-transact-sqlmd" class="xliff"></a>

### 4. &nbsp; [sys.query_store_plan(Transact-SQL)](system-catalog-views/sys-query-store-plan-transact-sql.md)

*업데이트됨: 2017-06-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_3) | [다음](#TitleNum_5))

<!-- Source markdown line 58.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1b77e34309ba7033578b3c82ed83c8c2fbc93e24 ce4ade9ab906c35cb87068a1fb91c4e1d7549aac  (PR=1940  ,  Filename=sys-query-store-plan-transact-sql.md  ,  Dirpath=docs\relational-databases\system-catalog-views\  ,  MergeCommitSha40=1d363db8e8bd0e1460cdea3c3a7add68e48714c9) -->



**계획 강제 적용 제한 사항**

쿼리 저장소에는 쿼리 최적화 프로그램이 특정 실행 계획을 사용하도록 적용하는 메커니즘이 있습니다. 그러나 계획이 적용되지 않도록 하는 몇 가지 제한 사항이 있습니다. 

첫째, 계획에 다음과 같은 구성이 포함된 경우
* Insert bulk 문
* Insert bulk 문
* 외부 테이블에 대한 참조
* 분산 쿼리 또는 전체 텍스트 작업
* 전역 쿼리 사용 
* 커서
* 잘못된 스타 조인 사양 

둘째, 계획에 사용되는 개체를 더 이상 사용할 수 없는 경우
* 데이터베이스(계획이 발생한 데이터베이스가 더 이상 없는 경우)
* 인덱스(더 이상 없거나 사용할 수 없는 경우)

마지막으로, 계획 자체에 문제가 있는 경우
* 쿼리에 적합하지 않음
* 쿼리 최적화 프로그램이 허용되는 작업 수를 초과함
* 잘못 구성된 계획 XML




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

<a id="5-nbsp-manage-retention-of-historical-data-in-system-versioned-temporal-tablestablesmanage-retention-of-historical-data-in-system-versioned-temporal-tablesmd" class="xliff"></a>

### 5. &nbsp;[시스템 버전 임시 테이블에서 기록 데이터의 보존 관리](tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_4))

<!-- Source markdown line 425.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ee69beb6a46913934d4a322f5d95343cc86f2ec4 94da98fec4ab16636a4581c16eb4456e2d1ff66b  (PR=1777  ,  Filename=manage-retention-of-historical-data-in-system-versioned-temporal-tables.md  ,  Dirpath=docs\relational-databases\tables\  ,  MergeCommitSha40=5bd0e1d3955d898824d285d28979089e2de6f322) -->



**임시 기록 보존 정책 접근 방식 사용**

> **참고:** 임시 기록 보존 정책을 사용 하 여 접근 방식을 적용 [! INCLUDE [sqldbesa... /.. /includes/sqldbesa-md.md)] 및 SQL Server 2017 CTP 1.3에서 시작 합니다.  

임시 기록 보존 될 수 있습니다 정책은 사용자가을 유연한 에이징을 만들 수 있는 개별 테이블 수준에서 구성 합니다. 임시 보존이 적용 하는 것은 간단: 테이블 스키마를 만들거나 변경 하는 동안 설정 하려면 매개 변수는 하나만 필요 합니다.

보존 정책을 정의 하 고 나면 Azure SQL 데이터베이스는 자동 데이터 정리에 사용할 수 있는 기록 행이 있는 경우 정기적으로 검사를 시작 합니다. 일치 하는 행 식별 하 고 기록 테이블에서 해당 제거 예약 되 고 시스템에서 실행 하는 백그라운드 태스크에서 투명 하 게 발생 합니다. 기록 테이블의 행에 대 한 나이 조건은 나타내는 SYSTEM_TIME 기간 종료 열에 따라 확인 됩니다. 예를 들어 보존 기간 이후 6 개월으로 설정 된, 경우 테이블의 정리에 대 한 적격 행 다음 조건을 만족 합니다.
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
앞의 예제에서 ValidTo 열 SYSTEM_TIME 기간 종료에 해당 하는지을 가정 합니다.
**보존 정책을 구성 하려면 어떻게 하나요?**

데이터베이스 수준에서 임시 기록 보존이 사용 되는지 여부를 임시 테이블에 대 한 보존 정책을 구성 하기 전에 먼저 검사.
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
플래그 데이터베이스 **is_temporal_history_retention_enabled** 기본적으로 ON으로 설정 되어 사용자가 ALTER DATABASE 문을 사용 하 여 변경할 수 있습니다. 시간 복원 작업에서 이후에 자동으로 OFF로 설정 됩니다. 데이터베이스에 대 한 임시 기록 보존 정리를 활성화 하려면 다음 문을 실행 합니다.





&nbsp;

<a name="compactupdatedlist"/>

<a id="compact-list-of-articles-updated-recently" class="xliff"></a>

## Compact를 최근에 업데이트 하는 문서 목록

이 압축 목록 이전 섹션에 나열 된 모든 업데이트 된 문서에 대 한 링크를 제공 합니다.

1. [메모리 액세스에 최적화된 테이블 변경](#TitleNum_1)
2. [메모리 액세스에 최적화된 테이블의 테이블 및 행 크기](#TitleNum_2)
3. [마이그레이션 후 유효성 검사 및 최적화 가이드](#TitleNum_3)
4. [sys.query_store_plan(Transact-SQL)](#TitleNum_4)
5. [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](#TitleNum_5)




<a name="sisters2"/>

&nbsp;

<a id="sister-articles" class="xliff"></a>

## 대체 문서

이 섹션에는 동일한 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170630-1150  -->

<a id="subject-areas-which-do-have-new-or-recently-updated-articles" class="xliff"></a>

#### 새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새로 추가되었거나 업데이트됨(12+2): **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(0+2): **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(3+0): **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(1+2): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새 + 업데이트 (2 + 8): **SQL용 Linux** docs](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(5+5): **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(2+0): **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(0+4): **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)


<a id="subject-areas-which-have-no-new-or-recently-updated-articles" class="xliff"></a>

#### 새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


&nbsp;


