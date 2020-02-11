---
title: 새로운 기능
description: MPP SQL Server 병렬 데이터 웨어하우스를 호스트 하는 확장 온-프레미스 어플라이언스 인 Microsoft Analytics Platform System의 새로운 기능을 참조 하세요.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3845470668e4cffeda7a48ed01c144eb53f671b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399426"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>확장 MPP 데이터 웨어하우스의 분석 플랫폼 시스템의 새로운 기능
최신 어플라이언스 업데이트 Microsoft Analytics Platform System (APS)의 새로운 기능을 참조 하세요. APS는 MPP SQL Server 병렬 데이터 웨어하우스를 호스팅하는 스케일 아웃 온-프레미스 어플라이언스입니다. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.5"></a>
## <a name="aps-cu75"></a>APS CU7.5
릴리스 날짜-9 월 2019

### <a name="alter-external-data-source"></a>외부 데이터 원본 변경
고객은 CU 7.5 업데이트를 사용 하 여 외부 데이터 원본 정의를 변경할 수 있습니다. Hadoop 이름 노드 고가용성을 사용 하는 고객은 이제 장애 조치 (failover) 발생 시 인수를 변경 하도록 데이터 원본을 변경할 수 있습니다. APS의 경우 위치, RESOURCE_MANAGER_LOCATION 및 자격 증명만 변경할 수 있습니다. 자세한 내용은 [alter external data source](https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql?view=sql-server-2017) 를 참조 하세요.

### <a name="cdh-515-and-516-support-with-polybase"></a>PolyBase를 사용한 CDH 5.15 및 5.16 지원
CU 7.5 업데이트를 사용 하는 APS의 PolyBase는 이제 Cloudera에서 CDH 5.15 및 5.16 버전의 Hadoop 배포를 지원 합니다. Cdh .x 버전의 경우 옵션 6을 사용 합니다. 

### <a name="try_convert-and-try_cast-support"></a>Try_Convert 및 Try_Cast 지원
CU 7.5 AP는 이제 [TRY_CAST](https://docs.microsoft.com/sql/t-sql/functions/try-cast-transact-sql?view=sql-server-2017) 및 [TRY_CONVERT](https://docs.microsoft.com/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-2017) tsql 함수를 지원 합니다. 이러한 함수는 모두 변환이 성공 하는 경우 지정 된 데이터 형식으로 변환 된 값을 반환 합니다. 그렇지 않으면 null을 반환 합니다.

<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
릴리스 날짜-2019 년 5 월

### <a name="loading-large-rows-with-dwloader"></a>Dwloader를 사용 하 여 많은 행 로드
APS CU 7.4부터 고객은 새 dwloader를 사용 하 여 32 KB (32768 바이트) 보다 큰 테이블에 행을 로드할 수 있습니다. 새 dwloader는 32768과 33554432 (바이트) 사이의 정수 값을 사용 하 여 32 KB 보다 큰 행을 로드 하는-l 스위치를 지원 합니다. 이 스위치는 클라이언트와 서버에 더 많은 메모리를 할당 하 고 부하를 늦출 수 있으므로 큰 행 (32 이상)을 로드 하는 경우에만이 옵션을 사용 합니다. [다운로드 사이트](https://www.microsoft.com/download/details.aspx?id=57472)에서 새 dwloader를 다운로드할 수 있습니다.  

### <a name="hdp-30-and-31-support-with-polybase"></a>PolyBase를 사용 하는 HDP 3.0 및 3.1 지원
이제 APS의 PolyBase는이 업데이트와 함께 HDP 3.0 및 3.1을 지원 합니다. HDP 3.x 버전에는 option 7을 사용 합니다. 자세한 내용은 [PolyBase 연결](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql) 페이지를 참조 하세요.

### <a name="utf16-file-support-with-polybase"></a>PolyBase를 사용 하 여 UTF16 파일 지원
이제 PolyBase는 UTF16 (LE) 인코딩에 있는 구분 된 텍스트 파일 읽기를 지원 합니다. 설치에 대 한 자세한 내용은 [외부 파일 형식 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql) 를 참조 하세요. 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
릴리스 날짜-12 월 2018

### <a name="common-subexpression-elimination"></a>일반 하위 식 제거
APS CU 7.3은 SQL 쿼리 최적화 프로그램에서 일반적인 하위 식 제거를 사용 하 여 쿼리 성능을 향상 시킵니다. 향상 된 기능은 두 가지 방법으로 쿼리를 향상 시킵니다. 첫 번째 혜택은 이러한 식을 확인 하 고 제거 하는 기능을 통해 SQL 컴파일 시간을 단축 하는 것입니다. 두 번째와 더 중요 한 혜택은 이러한 중복 부분식에 대 한 데이터 이동 작업은 제거 되므로 쿼리의 실행 시간이 더 빨라집니다. 이 기능에 대 한 자세한 설명은 [여기](common-sub-expression-elimination.md)를 참조 하십시오.

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>Informatica 10.2.0 게시 된 APS Informatica 커넥터
Informatica 버전 10.2.0 및 10.2.0 핫픽스 1에서 작동 하는 AP 용 Informatica 커넥터의 새 버전을 릴리스 했습니다. 새 커넥터는 [다운로드 사이트](https://www.microsoft.com/download/details.aspx?id=57472)에서 다운로드할 수 있습니다.

#### <a name="supported-versions"></a>지원되는 버전

| APS 버전 | Informatica PowerCenter | 드라이버 |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 11.x |
| APS 2016 이상 | 10.2.0, 10.2.0 핫픽스 1 | SQL Server Native Client 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
릴리스 날짜-10 월 2018

### <a name="support-for-tls-12"></a>TLS 1.2에 대 한 지원
APS CU 7.2는 TLS 1.2를 지원 합니다. 클라이언트 컴퓨터와 APS 간 통신은 이제 TLS 1.2를 통해서만 통신 하도록 설정할 수 있습니다. TLS 1.2을 통해서만 통신 하도록 설정 된 클라이언트 컴퓨터에 설치 된 SSDT, SSIS 및 Dwloader와 같은 도구는 이제 TLS 1.2을 사용 하 여 AP에 연결할 수 있습니다. 기본적으로 APS는 이전 버전과의 호환성을 위해 모든 TLS (1.0, 1.1 및 1.2) 버전을 지원 합니다. TLS 1.2를 엄격 하 게 사용 하도록 APS 어플라이언스를 설정 하려는 경우 레지스트리 설정을 변경 하 여 수행할 수 있습니다. 

자세한 내용은 [ap에서 tls 1.2 구성](configure-tls12-aps.md)을 참조 하세요.

### <a name="hadoop-encryption-zone-support-for-polybase"></a>PolyBase에 대 한 Hadoop 암호화 영역 지원
이제 PolyBase에서 Hadoop 암호화 영역과 통신할 수 있습니다. [Hadoop 보안 구성](polybase-configure-hadoop-security.md#encryptionzone)에 필요한 APS 구성 변경을 참조 하세요.

### <a name="insert-select-maxdop-options"></a>Maxdop 옵션 삽입-선택
삽입 선택 작업에 대해 1 보다 큰 maxdop 설정을 선택할 수 있는 [기능 스위치](appliance-feature-switch.md) 를 추가 했습니다. 이제 maxdop 설정을 0, 1, 2 또는 4로 설정할 수 있습니다. 기본값은 1입니다.

> [!IMPORTANT]  
> Maxdop를 높이면 때때로 작업 또는 교착 상태 오류가 발생할 수 있습니다. 이 경우 설정을 다시 maxdop 1로 변경 하 고 작업을 다시 시도 하세요.

### <a name="columnstore-index-health-dmv"></a>ColumnStore 인덱스 상태 DMV
**Dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv를 사용 하 여 columnstore 인덱스 상태 정보를 볼 수 있습니다. 다음 뷰를 사용 하 여 조각화를 확인 하 고 columnstore 인덱스를 다시 작성 하거나 다시 구성할 시기를 결정 합니다.

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
이제 PolyBase를 사용 하 여 날짜 데이터 형식 읽기, 가져오기 및 내보내기는 1970-01-01 이전 날짜와 ORC 및 Parquet 파일 형식에 대해 2038-01-20 이후 날짜를 지원 합니다.

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>대상으로 SQL Server 2017 용 SSIS 대상 어댑터
배포 대상으로 SQL Server 2017를 지 원하는 새 APS SSIS 대상 어댑터는 [다운로드 사이트](https://www.microsoft.com/download/details.aspx?id=57472)에서 다운로드할 수 있습니다.

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
릴리스 날짜-7 월 2018

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>DBCC 명령은 동시성 슬롯을 사용 하지 않습니다 (동작 변경).
APS는 [DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql)와 같은 t-sql [DBCC 명령의](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) 하위 집합을 지원 합니다. 이러한 명령은 이전에 실행될 수 있는 사용자 로드/쿼리 수를 줄이는 [동시성 슬롯](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots)을 사용했습니다. 그러면 `DBCC` 전체 쿼리 실행 성능을 향상 시키는 사용자 동시성 슬롯을 사용 하지 않는 로컬 큐에서 명령이 실행 됩니다.

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>일부 메타 데이터 호출을 카탈로그 개체로 바꿉니다.
SMO를 사용 하는 대신 메타 데이터 호출에 대해 카탈로그 개체를 사용 하는 경우 APS의 성능이 개선 되었습니다. CU 7.1부터 이러한 메타 데이터 호출 중 일부는 이제 기본적으로 카탈로그 개체를 사용 합니다. 메타 데이터 쿼리를 사용 하는 고객이 문제를 해결 하는 경우이 동작은 [기능 전환](appliance-feature-switch.md) 에 의해 해제 될 수 있습니다.

### <a name="bug-fixes"></a>버그 수정
Microsoft는 APS CU 7.1을 사용 하 여 SQL Server 2016 SP2 CU2로 업그레이드 했습니다. 업그레이드는 아래에 설명 된 몇 가지 문제를 해결 합니다.

| 제목 | Description |
|:---|:---|
| **잠재적 튜플 이동 교착 상태** |업그레이드는 분산 트랜잭션과 튜플 이동 기 백그라운드 스레드에서 교착 상태의 긴 가능성을 수정 합니다. CU 7.1을 설치한 후 TF634를 사용 하 여 시작 매개 변수 또는 전역 추적 플래그로 SQL Server 튜플 이동 기를 중지 하는 고객은이를 안전 하 게 제거할 수 있습니다. | 
| **특정 지연/리드 쿼리 실패** |오류가 발생 하는 중첩 된 지연/리드 함수를 사용 하는 CCI 테이블의 특정 쿼리는 이제이 업그레이드로 수정 되었습니다. | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
릴리스 날짜-2018 년 5 월

APS 2016은 AU7로 업그레이드 하기 위한 필수 구성 요소입니다. 다음은 APS AU7의 새로운 기능입니다.

### <a name="auto-create-and-auto-update-statistics"></a>통계 자동 생성 및 자동 업데이트
APS AU7는 기본적으로 통계를 자동으로 만들고 업데이트 합니다. 통계 설정을 업데이트 하기 위해 관리자는 [Configuration Manager](appliance-configuration.md#CMTasks)의 새로운 기능 스위치 메뉴 항목을 사용할 수 있습니다. [기능 스위치](appliance-feature-switch.md) 는 통계의 자동 생성, 자동 업데이트 및 비동기 업데이트 동작을 제어 합니다. [ALTER DATABASE (병렬 데이터 웨어하우스)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 문을 사용 하 여 통계 설정을 업데이트할 수도 있습니다.

### <a name="t-sql"></a>T-SQL
이제 @var 선택이 지원 됩니다. 자세한 내용은 [지역 변수 선택](/sql/t-sql/language-elements/select-local-variable-transact-sql) 을 참조 하세요. 

이제 쿼리 힌트 해시 및 순서 그룹이 지원 됩니다. 자세한 내용은 [힌트 (transact-sql)-쿼리](/sql/t-sql/queries/hints-transact-sql-query) 를 참조 하세요.

### <a name="feature-switch"></a>기능 스위치
APS AU7 [Configuration Manager](launch-the-configuration-manager.md)의 기능 스위치를 소개 합니다. AutoStatsEnabled 및 DmsProcessStopMessageTimeoutInSeconds는 이제 관리자가 변경할 수 있는 구성 가능한 옵션입니다.

### <a name="known-issues"></a>알려진 문제
APS AU7 소프트웨어를 사용 하면 잘못 된 *실행 측 채널 공격*으로 설명 된 문제를 해결 하는 Intel BIOS 업데이트가 제공 됩니다. 이 공격은 *스펙터 및 멜트다운 취약성*을 악용 하는 것을 목표로 합니다. AP와 함께 패키지 되기는 하지만, AP AU7 소프트웨어 설치의 일부가 아니라 수동으로 BIOS 업데이트가 설치 됩니다.

Microsoft는 모든 고객에 게 BIOS 업데이트를 설치 하도록 조언 합니다. Microsoft는 다양 한 환경에서 다양 한 SQL 작업에 대 한 커널 KVAS (가상 주소 숨김), KPTI (커널 페이지 테이블 간접 참조) 및 IBP (간접 분기 예측 완화)의 효과를 측정 했습니다. 측정값이 일부 워크 로드에서 상당한 저하를 발견 했습니다. 결과에 따라 프로덕션 환경에 배포 하기 전에 BIOS 업데이트를 사용 하도록 설정 하는 성능 효과를 테스트 하는 것이 좋습니다. SQL Server 지침은 [여기](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)를 참조 하세요.

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
이 섹션에서는 AP 2016-AU6의 새로운 기능에 대해 설명 했습니다.

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6는 최신 SQL Server 2016 릴리스에서 실행 되며 기본 데이터베이스 호환성 수준 130을 사용 합니다. SQL Server 2016에서는 다음과 같은 새로운 기능을 지원 합니다.

- 클러스터형 columnstore 인덱스에 대 한 보조 인덱스입니다.
- PolyBase 용 Kerberos.

### <a name="t-sql"></a>T-SQL
APS AU6는 이러한 T-sql 호환성 개선 사항을 지원 합니다.  이러한 추가 언어 요소를 사용 하 여 SQL Server 및 기타 데이터 원본에서 쉽게 마이그레이션할 수 있습니다. 

- 이제 Windows 데이터 정렬과 더불어 [열 수준 SQL 데이터 정렬이][] 지원 됩니다.
- [클러스터형 columnstore 인덱스의 비클러스터형 인덱스][] 는 클러스터형 columnstore 인덱스에서 특정 값을 검색 하는 쿼리 성능을 향상 시킵니다. 
- [...를 선택 합니다. 범주로][] 
- [sp_spaceused ()][] 는 테이블이 나 데이터베이스에서 사용 되거나 예약 된 디스크 공간을 표시 합니다.
- [넓은 테이블][] 지원 SQL Server 2016와 동일 합니다. 행 크기의 이전 제한인 32 K가 더 이상 존재 하지 않습니다. 

**데이터 형식**

- [VARCHAR (max)][], [NVARCHAR (Max)][] 및 [VARBINARY (max)][]입니다. 이러한 LOB 데이터 형식의 최대 크기는 2gb입니다. 이러한 개체를 로드 하려면 [Bcp 유틸리티][]를 사용 합니다. PolyBase 및 dwloader는 현재 이러한 데이터 형식을 지원 하지 않습니다. 
- [SYSNAME 이며][]
- [없으면][]
- [NUMERIC][] 및 DECIMAL 데이터 형식입니다.

**창 함수**

- SELECT 문의 OVER 절에 있는 [행 또는 범위][]
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**보안 함수**

- [CHECKSUM ()][] 및 [BINARY_CHECKSUM ()][]
- [HAS_PERMS_BY_NAME ()][]

**추가 함수**

- [NEWID ()][]
- [RAND ()][]

### <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop 향상 된 기능

- Hortonworks HDP 2.4 및 HDP 2.5와의 호환성
- 데이터베이스 범위 자격 증명을 통한 Kerberos 지원
- Azure Storage Blob을 사용 하 여 자격 증명 지원

### <a name="install-and-upgrade-enhancements"></a>향상 된 설치 및 업그레이드

**엔터프라이즈 아키텍처 업데이트** 기존 어플라이언스를 APS AU6로 업그레이드 하면 보안 픽스를 포함 하는 최신 펌웨어 및 드라이버 업데이트가 설치 됩니다. 

HPE 또는 DELL의 새 어플라이언스에는 모든 최신 업데이트 plus가 포함 됩니다.

- 최신 세대 프로세서 지원 (Broadwell)
- DDR4 Dimm 업데이트
- 향상 된 DIMM 처리량

**통합**

- FQDN (정규화 된 도메인 이름)을 지원 하면 어플라이언스에 대 한 도메인 트러스트를 설정할 수 있습니다. 
- FQDN을 사용 하려면 업그레이드 하는 동안 전체 업그레이드 및 옵트인 (opt in) 해야 합니다. 

**가동 중지 시간 감소** APS AU6를 설치 하거나 업그레이드 하는 것이 더 빠르며 이전 릴리스 보다 가동 중지 시간이 짧습니다. 설치 또는 업그레이드의 가동 중지 시간을 줄이려면 다음을 수행 합니다. 

 - 6 월 2016까지 모든 업데이트가 포함 된 이미지를 사용 하 여 WSUS 업데이트 적용 간소화
 - 드라이버 및 펌웨어 업데이트를 사용 하 여 보안 업데이트 적용
 - 최신 핫픽스와 PAV (어플라이언스 확인 유틸리티)를 어플라이언스에 배치 하 여 다운로드할 필요 없이 설치할 수 있습니다.

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[열 수준 SQL 데이터 정렬]: ~/relational-databases/collations/collation-and-unicode-support.md

[클러스터형 columnstore 인덱스의 비클러스터형 인덱스]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR (MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR (MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY (MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME 이며]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[...를 선택 합니다. 범주로]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused ()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[넓은 테이블]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp 유틸리티]:/sql/tools/bcp-utility
[없으면]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[번호]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[행 또는 범위]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM ()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM ()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME ()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID ()]:/sql/t-sql/functions/newid-transact-sql
[RAND ()]:/sql/t-sql/functions/rand-transact-sql


  

  


