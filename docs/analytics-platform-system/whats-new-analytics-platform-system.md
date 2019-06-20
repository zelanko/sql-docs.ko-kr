---
title: Analytics Platform System-수평 확장 데이터 웨어하우스의에서 새로운 기능
description: Microsoft Analytics Platform System에서는 MPP SQL Server 병렬 데이터 웨어하우스를 호스트 하는 스케일 아웃 온-프레미스 어플라이언스의에서 새로운 기능을 참조 하세요.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b56791e9fd59aef57c2d107e21eb76896ebb4910
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175048"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>Analytics Platform System에서는 스케일 아웃 MPP 데이터 웨어하우스의에서 새로운 기능
Microsoft Analytics Platform System (APS)에 대 한 최신 어플라이언스 업데이트의 새로운 기능을 참조 하세요. AP는 MPP SQL Server 병렬 데이터 웨어하우스를 호스트 하는 스케일 아웃 온-프레미스 어플라이언스입니다. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
릴리스 날짜-2019 년 5 월

### <a name="loading-large-rows-with-dwloader"></a>Dwloader 사용 하 여 대용량 행의 로드
AP CU7.4에서 시작 하며, 고객에 게 새 dwloader 32KB (32,768 바이트) 보다 큰 경우에 테이블에 행을 로드 하는 데 할 수 됩니다. 새 dwloader 32KB 보다 큰 행을 로드 하려면 32768 및 33554432 (메가바이트) 사이의 정수 값을 사용 하는-l 스위치를 지원 합니다. 이 스위치는 클라이언트와 서버에서 더 많은 메모리를 할당 하 고 로드 느려질 수 있습니다 (32KB 보다 큼) 큰 행을 로드 하는 경우에이 옵션을 사용 합니다. 새 dwloader를 다운로드할 수 있습니다 [다운로드 사이트](https://www.microsoft.com/download/details.aspx?id=57472)합니다.  

### <a name="hdp-30-and-31-support-with-polybase"></a>HDP 3.0 및 3.1 지원 PolyBase 사용 하 여
AP에서 PolyBase는 HDP 3.0 및 3.1이이 업데이트를 사용 하 여 이제 지원합니다. HDP 3.x 버전에 대 한 옵션 7을 사용 합니다. 자세한 내용은 [PolyBase 연결](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql) 페이지입니다.

### <a name="utf16-file-support-with-polybase"></a>PolyBase 사용 하 여 UTF16 파일 지원
PolyBase는 이제 UTF16 (LE) 인코딩에 있는 구분 기호로 분리 된 텍스트 파일 읽기 지원 합니다. 참조 [외부 파일 형식 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql) 설정 세부 정보에 대 한 합니다. 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
릴리스 날짜-2018 년 12 월

### <a name="common-subexpression-elimination"></a>일반 하위 식 제거
AP CU7.3 SQL 쿼리 최적화 프로그램의 공용 부분식 제거를 사용 하 여 쿼리 성능을 향상 시킵니다. 향상 두 가지 방법으로 쿼리를 개선합니다. 첫 번째 이점은 식별 하 고 제거 하는 등 있다는 점입니다 식 SQL 컴파일 시간을 줄이는 데 도움이 됩니다. 두 번째 및 더 중요 한 장점은 쿼리가 더 빠르게 됩니다에 대 한 이러한 중복 하위 식에 대 한 데이터 이동 작업 실행 시간에 따라서 제거 됩니다. 자세한 설명은이 기능을 찾을 수 있습니다 [여기](common-sub-expression-elimination.md)합니다.

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>APS Informatica connector informatica 10.2.0 게시
APS Informatica 10.2.0 및 10.2.0 버전을 사용 하 여 작동 하는 대 한 Informatica 커넥터의 새 버전을 출시 되었음을 핫픽스 1입니다. 새 커넥터에서 다운로드할 수 있습니다 [다운로드 사이트](https://www.microsoft.com/download/details.aspx?id=57472)합니다.

#### <a name="supported-versions"></a>Supported Versions

| AP 버전 | Informatica PowerCenter | 드라이버 |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 11.x |
| APS 2016 이상 | 10.2.0, 10.2.0 Hotfix 1 | SQL Server Native Client 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
릴리스 날짜-2018 년 10 월

### <a name="support-for-tls-12"></a>TLS 1.2에 대 한 지원
AP CU7.2 TLS 1.2를 지원합니다. 클라이언트 컴퓨터 AP AP를 노드 간 통신 설정할 수 있는 이제 TLS1.2를 통해서만 통신 합니다. SSDT, SSIS 및 TLS 1.2를 통해서만 통신 하도록 설정 된 클라이언트 컴퓨터에 설치 된 Dwloader와 같은 도구 이제 TLS 1.2를 사용 하 여 AP를 연결할 수 있습니다. 기본적으로 AP는 이전 버전과 호환성에 대 한 모든 TLS (1.0, 1.1 및 1.2) 버전을 지원 합니다. APS 어플라이언스 엄격 하 게 TLS 1.2를 사용 하도록 설정 하려면 레지스트리 설정을 변경 하 여 할 수 있습니다. 

자세한 내용은 [TLS1.2 AP에 구성](configure-tls12-aps.md)합니다.

### <a name="hadoop-encryption-zone-support-for-polybase"></a>Polybase Hadoop 암호화 영역을 지원 합니다.
PolyBase는 이제 Hadoop 암호화 영역 통신할 수 있습니다. 에 필요한 AP 구성 변경 내용을 확인할 [Hadoop 보안 구성](polybase-configure-hadoop-security.md#encryptionzone)합니다.

### <a name="insert-select-maxdop-options"></a>Insert Select maxdop 옵션
추가한 것을 [기능 스위치가](appliance-feature-switch.md) insert select 작업에 대해 1 보다 큰 maxdop 설정을 선택할 수 있습니다. 이제 0, 1, 2 또는 4 maxdop 설정을 설정할 수 있습니다. 기본값은 1입니다.

> [!IMPORTANT]  
> Maxdop 증가 유발 하는 경우도 느린 작업 또는 교착 상태 오류가 발생 합니다. 발생 하는 경우 maxdop 1로 다시 설정을 변경 하 고 작업을 다시 시도 합니다.

### <a name="columnstore-index-health-dmv"></a>ColumnStore 인덱스 상태 DMV
Columnstore 인덱스 상태 정보를 사용 하 여 볼 수 있습니다 **dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv 합니다. 조각화를 확인 하 고 다시 만들거나 columnstore 인덱스를 다시 구성할 시기를 결정 하려면 다음 보기를 사용 합니다.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[pdw_node_id]    = nt.[pdw_node_id]                                          
)
select *
from cte;
```

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>ORC 및 Parquet 파일에 대 한 PolyBase 날짜 범위 증가
읽기, 가져오기 및 내보내기 이제 PolyBase를 사용 하 여 날짜 데이터 형식 ORC 및 Parquet 파일 형식에 대 한 날짜 1970-01-01 전후 2038-01-20을 지원 합니다.

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>대상으로 SQL Server 2017에 대 한 SSIS 대상 어댑터
SQL Server 2017 배포 대상에서 다운로드할 수 있습니다 하는 대로를 지 원하는 새 AP SSIS 대상 어댑터 [다운로드 사이트](https://www.microsoft.com/download/details.aspx?id=57472)합니다.

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
릴리스 날짜-2018 년 7 월

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>동시성 슬롯 (동작 변경 내용)를 사용 하지 않는 DBCC 명령
AP는 T-SQL의 하위 집합을 지원 [DBCC 명령을](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) 와 같은 [DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql)합니다. 다음이 명령을 사용 하는 이전에 [동시성 슬롯](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots) 사용자 쿼리의 로드/실행 될 수 있는 수를 줄입니다. `DBCC` 명령은 전반적인 쿼리 실행 성능을 향상 시킵니다 사용자 동시성 슬롯을 사용 하지 않는 로컬 큐의 이제 실행 됩니다.

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>카탈로그 개체를 사용 하 여 일부 메타 데이터 호출을 대체합니다.
카탈로그 개체를 사용 하 여 SMO를 사용 하는 대신 호출 메타 데이터에 대 한 성능 향상을 AP에서 주었습니다. CU7.1에서 시작 하며, 이러한 메타 데이터 호출의 일부 이제 카탈로그 개체 기본적으로 사용 합니다. 이 동작을 해제할 수 있습니다 [기능 스위치가](appliance-feature-switch.md) 메타 데이터 쿼리를 사용 하 여 고객에 게 문제가 발생 하는 경우.

### <a name="bug-fixes"></a>버그 수정
AP CU7.1를 사용 하 여 SQL Server 2016 SP2 CU2를 업그레이드 했습니다. 업그레이드는 아래에 설명 된 몇 가지 문제를 해결 합니다.

| Title | Description |
|:---|:---|
| **튜플 이동 기 교착 상태가 발생할** |업그레이드는 분산 트랜잭션 및 튜플 이동 기 백그라운드 스레드에서 교착 상태를 오래 가능성을 해결합니다. CU7.1를 설치한 후 SQL Server 시작 매개 변수 또는 전역 추적 플래그가 튜플 이동 기를 중지 하려면 TF634를 사용한 고객 안전 하 게 제거할 수 있습니다. | 
| **특정 lag/잠재 고객 쿼리 실패** |이 업그레이드를 사용 하 여 오류가 발생 하는 지연/잠재 고객의 중첩 된 함수를 사용 하 여 CCI 테이블에 대 한 특정 쿼리 고정 됩니다. | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
릴리스 날짜-2018 년 5 월

APS 2016은 AU7로 업그레이드 하는 필수 구성 요소입니다. 다음은 AP AU7의 새로운 기능입니다.

### <a name="auto-create-and-auto-update-statistics"></a>자동 생성 및 자동 업데이트 통계
AP AU7 만들고 기본적으로 통계를 자동으로 업데이트 합니다. 관리자 수의 새 기능 스위치 메뉴 항목을 사용 하는 데 통계 설정을 업데이트 하는 [Configuration Manager](appliance-configuration.md#CMTasks)합니다. 합니다 [기능 스위치가](appliance-feature-switch.md) auto-create, 자동 업데이트 및 통계의 비동기 업데이트 동작을 제어 합니다. 사용 하 여 통계 설정을 업데이트할 수도 있습니다는 [ALTER DATABASE (병렬 데이터 웨어하우스)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 문입니다.

### <a name="t-sql"></a>T-SQL
선택 @var 이제 지원 됩니다. 자세한 내용은 참조 하세요. [지역 변수를 선택 합니다.](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

해시 및 ORDER GROUP 쿼리 힌트는 이제 지원 됩니다. 자세한 내용은 참조 하세요. [Hints(Transact-SQL)-쿼리](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>기능 스위치
AP AU7 소개에서 기능 스위치 [Configuration Manager](launch-the-configuration-manager.md)합니다. AutoStatsEnabled DmsProcessStopMessageTimeoutInSeconds와 이제 관리자가 변경 될 수 있는 구성 가능한 옵션입니다.

### <a name="known-issues"></a>알려진 문제
으로 설명 하는 문제를 해결 하는 Intel BIOS 업데이트는 제공 하는 AP AU7 소프트웨어로 *투기적 실행 사이드 채널 공격*합니다. 공격 이라는 것을 악용 하는 것을 목표로 *스펙터와 멜트다운 취약점으로 인 한*합니다. BIOS 업데이트를 수동으로 설치 하 고 있지만 AP와 함께 패키지 AP AU7 소프트웨어 설치의 일부로 없습니다.

Microsoft는 BIOS 업데이트를 설치 하려면 모든 고객에 게 권고 합니다. Microsoft 다양 한 환경에서 다양 한 SQL 워크 로드에서 커널 가상 주소 숨기기 (KVAS), 커널 페이지 테이블 간접 참조 (KPTI) 및 간접 분기 예측 완화 (IBP)의 효과 측정 합니다. 측정값에 일부 워크 로드를 크게 저하 됨. 프로덕션 환경에 배포 하기 전에 BIOS 업데이트 사용의 성능 효과 테스트 하는 것이 좋습니다는 결과 따라 합니다. SQL Server 지침을 참조 하세요 [여기](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)합니다.

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
이 섹션에서는 AU6 APS 2016에 대 한 새로운 기능을 설명합니다.

### <a name="sql-server-2016"></a>SQL Server 2016

AP AU6 최신 SQL Server 2016 릴리스를 실행 하 고 기본 데이터베이스 호환성 수준 130을 사용 합니다. SQL Server 2016와 같은 새로운 기능에 대 한 지원을 활성화합니다.

- 클러스터형된 columnstore 인덱스에 대 한 보조 인덱스입니다.
- PolyBase에 대 한 Kerberos입니다.

### <a name="t-sql"></a>T-SQL
AP AU6 T-SQL 호환성 향상 된 기능을 지원합니다.  이러한 추가 언어 요소 쉽게 SQL Server 및 기타 데이터 원본에서 마이그레이션. 

- [SQL 데이터 정렬은 열 수준][] Windows 데이터 정렬 하는 것 외에도 이제 지원 됩니다.
- [클러스터형된 columnstore 인덱스의 비클러스터형 인덱스][] 클러스터형된 columnstore 인덱스에 있는 특정 값을 검색 하는 쿼리의 성능을 향상 합니다. 
- [SELECT...INTO][] 
- [sp_spaceused()][] 디스크 공간을 사용 하거나 테이블 또는 데이터베이스에서 예약 된 표시 됩니다.
- [넓은 테이블][] 지원은 SQL Server 2016와 동일 합니다. 행 크기는 32k 한 이전의 제한이 더 이상 없습니다. 

**데이터 형식**

- [VARCHAR(MAX)][]하십시오 [NVARCHAR(MAX)][] 하 고 [VARBINARY(MAX)][]합니다. 이러한 LOB 데이터 형식에 최대 크기는 2GB입니다. 이러한 로드를 사용 하 여 개체 [bcp 유틸리티][]합니다. PolyBase 및 dwloader 지원 하지 않습니다 현재 다음 데이터 형식. 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [NUMERIC][] 및 DECIMAL 데이터 형식입니다.

**창 함수**

- [ROWS 또는 RANGE][] SELECT 문의 OVER 절에 있습니다.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**보안 함수**

- [CHECKSUM()][] and [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**추가 기능**

- [NEWID()][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>PolyBase Hadoop/향상 된 기능

- Hortonworks HDP 2.4 및 HDP 2.5 사용 하 여 호환성
- 데이터베이스 범위 자격 증명을 통해 Kerberos 지원
- Azure Storage Blob을 사용 하 여 자격 증명 지원

### <a name="install-and-upgrade-enhancements"></a>설치 및 업그레이드 향상 된 기능

**엔터프라이즈 아키텍처 업데이트** 는 최신 펌웨어 및 드라이버 업데이트, 보안 수정 사항을 포함 하는 설치 기존 어플라이언스 AP AU6로 업그레이드 합니다. 

최신 업데이트를 포함 하는 HPE 또는 DELL 새 어플라이언스 및:

- 최신 세대 프로세서 지원 (Broadwell)
- DDR4 Dimm 업데이트
- DIMM 처리량이 향상된

**통합**

- 완전히 정규화 된 도메인 이름 (FQDN) 지원을 통해 어플라이언스에 도메인 트러스트를 설정할 수 있습니다. 
- FQDN을 사용 하려면 전체 업그레이드를 수행 하 고 업그레이드 하는 동안 옵트인 해야 합니다. 

**가동 중지 시간 감소** 설치 또는 업그레이드 AP AU6 빠릅니다 및 이전 버전 보다 적은 가동 중지 시간이 필요 합니다. 가동 중지 시간, 설치 또는 업그레이드를 줄이려면: 

 - 2016 년 6 월을 통해 업데이트를 모두 포함 된 이미지를 사용 하 여 WSUS 업데이트를 적용 하는 간소화
 - 드라이버 및 펌웨어 업데이트를 사용 하 여 보안 업데이트 적용
 - 다운로드할 필요가 없습니다를 사용 하 여 설치 준비 완료 되므로 어플라이언스에서 최신 핫픽스 및 어플라이언스 확인 유틸리티 (PAV)를 배치 합니다.

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[SQL 데이터 정렬은 열 수준]: ~/relational-databases/collations/collation-and-unicode-support.md

[클러스터형된 columnstore 인덱스의 비클러스터형 인덱스]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY(MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[넓은 테이블]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp 유틸리티]:/sql/tools/bcp-utility
[UNIQUEIDENTIFIER]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[NUMERIC]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[ROWS 또는 RANGE]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID()]:/sql/t-sql/functions/newid-transact-sql
[RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


