---
title: 새로운 기능
description: MPP SQL Server 병렬 데이터 웨어하우스를 호스팅하는 확장 형 온-프레미스 어플라이언스인 Microsoft 분석 플랫폼 시스템의 새로운 기능을 확인하십시오.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: faf3bd1f487fb5c850759fdde3ddecd32bdd3b1f
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625537"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>확장형 MPP 데이터 웨어하우스인 애널리틱스 플랫폼 시스템의 새로운 점
Microsoft 분석 플랫폼 시스템(APS)에 대한 최신 어플라이언스 업데이트의 새로운 기능을 확인하세요. APS는 MPP SQL Server 병렬 데이터 웨어하우스를 호스팅하는 확장-온-프레미스 어플라이언스입니다. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.6"></a>
## <a name="aps-cu76"></a>APS CU7.6
릴리스 날짜 - 2020년 4월

### <a name="rename-column"></a>열 이름 바꾸기
CU7.6으로 업그레이드한 후 고객은 사용자가 만든 테이블의 열 이름을 바꿀 수 있습니다. 구문, 예제, 제한 사항 및 자세한 내용은 [이름 바꾸기(Transact-SQL)를](https://docs.microsoft.com/sql/t-sql/statements/rename-transact-sql) 참조하십시오.

### <a name="alter-view"></a>뷰 변경
이제 고객은 보기를 변경할 수 있습니다. 자세한 내용은 [ALTER 보기(거래-SQL)를](https://docs.microsoft.com/sql/t-sql/statements/alter-view-transact-sql) 참조하십시오.

<a name="h2-aps-cu7.5"></a>
## <a name="aps-cu75"></a>APS CU7.5
릴리스 날짜 - 2019년 9월

### <a name="alter-external-data-source"></a>외부 데이터 원본 변경
고객은 CU7.5 업데이트를 통해 외부 데이터 원본 정의를 변경할 수 있습니다. Hadoop 이름 노드 고가용성을 가진 고객은 이제 장애 조치(failover)가 발생할 때 인수를 변경하기 위해 데이터 원본을 변경할 수 있습니다. APS의 경우 위치, RESOURCE_MANAGER_LOCATION 및 자격 증명만 변경할 수 있습니다. 자세한 내용은 [외부 데이터 원본 변경을](https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql?view=sql-server-2017) 참조하십시오.

### <a name="cdh-515-and-516-support-with-polybase"></a>폴리베이스를 지원하는 CDH 5.15 및 5.16 지원
CU7.5 업데이트가 있는 APS의 폴리베이스는 이제 Cloudera의 하두프 배포판CDH 5.15 및 5.16 버전을 지원합니다. CDH 5.x 버전의 경우 옵션 6을 사용합니다. 

### <a name="try_convert-and-try_cast-support"></a>Try_Convert 및 Try_Cast 지원
CU7.5 APS는 이제 [TRY_CAST](https://docs.microsoft.com/sql/t-sql/functions/try-cast-transact-sql?view=sql-server-2017) 및 [TRY_CONVERT](https://docs.microsoft.com/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-2017) tsql 기능을 지원합니다. 변환이 성공하면 이러한 함수 모두 지정된 데이터 유형으로 변환된 값을 반환합니다. 그렇지 않으면 null을 반환합니다.

<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
릴리스 날짜 - 2019년 5월

### <a name="loading-large-rows-with-dwloader"></a>dwloader로 큰 행 로드
APS CU7.4부터 고객은 새 dwloader를 사용하여 32KB(32,768바이트)보다 큰 테이블에 행을 로드할 수 있습니다. 새 dwloader는 32KB보다 큰 행을 로드하기 위해 32768에서 33554432(바이트) 사이의 정수 값을 사용하는 -l 스위치를 지원합니다. 이 스위치는 클라이언트와 서버에 더 많은 메모리를 할당하고 로드 속도를 늦출 수 있기 때문에 큰 행(32KB보다 큰)을 로드할 때만 이 옵션을 사용합니다. 당신은 [다운로드 사이트에서](https://www.microsoft.com/download/details.aspx?id=57472)새 dwloader를 다운로드 할 수 있습니다.  

### <a name="hdp-30-and-31-support-with-polybase"></a>폴리베이스를 지원하는 HDP 3.0 및 3.1 지원
APS의 폴리베이스는 이 업데이트로 HDP 3.0 및 3.1을 지원합니다. HDP 3.x 버전의 경우 옵션 7을 사용합니다. 자세한 내용은 [PolyBase 연결](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql) 페이지를 참조하십시오.

### <a name="utf16-file-support-with-polybase"></a>폴리베이스를 가진 UTF16 파일 지원
PolyBase는 이제 UTF16(LE) 인코딩에 있는 제한된 텍스트 파일 읽기를 지원합니다. 설정 세부 정보는 [외부 파일 형식 만들기를](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql) 참조하십시오. 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
릴리스 날짜 - 2018년 12월

### <a name="common-subexpression-elimination"></a>일반 하위 식 제거
APS CU7.3은 SQL 쿼리 최적화 에서 일반적인 하위 식 제거를 통해 쿼리 성능을 향상시킵니다. 이 개선은 두 가지 방법으로 쿼리를 향상시킵니다. 첫 번째 이점은 이러한 식을 식별하고 제거하는 기능으로 SQL 컴파일 시간을 줄이는 데 도움이 됩니다. 두 번째로 중요한 이점은 이러한 중복 하위 표현식에 대한 데이터 이동 작업이 제거되어 쿼리실행 시간이 빨라진다는 것입니다. 이 기능에 대한 자세한 설명은 [여기에서](common-sub-expression-elimination.md)찾을 수 있습니다.

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>INformatica 10.2.0에 대한 APS Informatica 커넥터 게시
우리는 Informatica 버전 10.2.0 및 10.2.0 핫픽스 1과 함께 작동하는 APS에 대한 Informatica 커넥터의 새로운 버전을 발표했다. 새 커넥터는 [다운로드 사이트에서](https://www.microsoft.com/download/details.aspx?id=57472)다운로드할 수 있습니다.

#### <a name="supported-versions"></a>지원되는 버전

| APS 버전 | Informatica PowerCenter | 드라이버 |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL 서버 네이티브 클라이언트 11.x |
| APS 2016 이상 | 10.2.0, 10.2.0 핫픽스 1 | SQL 서버 네이티브 클라이언트 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
릴리스 날짜 - 2018년 10월

### <a name="support-for-tls-12"></a>TLS 1.2에 대한 지원
APS CU7.2는 TLS 1.2를 지원합니다. 이제 클라이언트 에서 APS 및 APS 노드 내 통신을 TLS1.2를 통해만 통신하도록 설정할 수 있습니다. TLS 1.2를 통해서만 통신하도록 설정된 클라이언트 컴퓨터에 설치된 SSDT, SSIS 및 Dwloader와 같은 도구는 이제 TLS 1.2를 사용하여 APS에 연결할 수 있습니다. 기본적으로 APS는 이전 버전과의 호환성을 위해 모든 TLS(1.0, 1.1 및 1.2) 버전을 지원합니다. APS 어플라이언스를 TLS 1.2를 엄격하게 사용하도록 설정하려면 레지스트리 설정을 변경하여 사용할 수 있습니다. 

자세한 내용은 [APS에서 TLS1.2 구성을](configure-tls12-aps.md)참조하십시오.

### <a name="hadoop-encryption-zone-support-for-polybase"></a>폴리베이스에 대한 하눕 암호화 영역 지원
이제 PolyBase가 하눕 암호화 영역과 통신할 수 있습니다. [Hadoop 보안 구성에](polybase-configure-hadoop-security.md#encryptionzone)필요한 APS 구성 변경 사항을 참조하십시오.

### <a name="insert-select-maxdop-options"></a>인서삽입-최대도프 선택 옵션
인서트 선택 작업에 대해 1보다 큰 maxdop 설정을 선택할 수 있는 [기능 스위치가](appliance-feature-switch.md) 추가되었습니다. 이제 maxdop 설정을 0, 1, 2 또는 4로 설정할 수 있습니다. 기본값은 1입니다.

> [!IMPORTANT]  
> maxdop를 늘리면 작업 속도가 느려지거나 교착 상태가 발생할 수 있습니다. 이 경우 설정을 maxdop 1로 다시 변경하고 작업을 다시 시도합니다.

### <a name="columnstore-index-health-dmv"></a>컬럼스토어 인덱스 상태 DMV
**dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv를 사용하여 columnstore 인덱스 상태 정보를 볼 수 있습니다. 다음 뷰를 사용하여 조각화를 결정하고 columnstore 인덱스를 다시 작성하거나 재구성할 시기를 결정합니다.

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

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>ORC 및 마루 파일에 대한 폴리베이스 날짜 범위 증가
PolyBase를 사용하여 날짜 데이터 형식을 읽고, 가져오고 내보내기는 이제 1970-01-01 이전과 ORC 및 Parquet 파일 형식의 경우 2038-01-20 이후의 날짜를 지원합니다.

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>SQL Server 2017용 SSIS 대상 어댑터를 대상으로 합니다.
SQL Server 2017을 배포 대상으로 지원하는 새 APS SSIS 대상 어댑터는 [다운로드 사이트에서](https://www.microsoft.com/download/details.aspx?id=57472)다운로드할 수 있습니다.

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
릴리스 날짜 - 2018년 7월

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>DBCC 명령은 동시성 슬롯을 사용하지 않습니다(동작 변경)
APS는 [DBCC 드롭클린버퍼와](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql)같은 T-SQL [DBCC 명령의](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) 하위 집합을 지원합니다. 이러한 명령은 이전에 실행될 수 있는 사용자 로드/쿼리 수를 줄이는 [동시성 슬롯](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots)을 사용했습니다. 이제 `DBCC` 명령은 전체 쿼리 실행 성능을 향상시키는 사용자 동시성 슬롯을 사용하지 않는 로컬 큐에서 실행됩니다.

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>일부 메타데이터 호출을 카탈로그 개체로 바꿉
SMO를 사용하는 대신 메타데이터 호출에 카탈로그 개체를 사용하면 APS의 성능이 향상되었습니다. CU7.1부터 이러한 메타데이터 호출 중 일부는 기본적으로 카탈로그 개체를 사용합니다. 메타데이터 쿼리를 사용하는 고객이 문제가 발생하는 경우 [기능 스위치를](appliance-feature-switch.md) 통해 이 동작을 해제할 수 있습니다.

### <a name="bug-fixes"></a>버그 수정
APS CU7.1을 사용하여 SQL Server 2016 SP2 CU2로 업그레이드했습니다. 업그레이드는 아래에 설명된 몇 가지 문제를 해결합니다.

| 제목 | 설명 |
|:---|:---|
| **잠재적튜플 무버 교착 상태** |업그레이드는 분산 트랜잭션 및 튜플 무버 백그라운드 스레드에서 교착 상태의 오랜 가능성을 수정합니다. CU7.1을 설치한 후 TF634를 사용하여 튜플 무버를 SQL Server 시작 매개 변수 또는 전역 추적 플래그로 중지한 고객은 안전하게 제거할 수 있습니다. | 
| **특정 지연/잠재 고객 쿼리 실패** |이제 오류가 발생할 수 있는 중첩 된 지연/리드 함수가 있는 CCI 테이블의 특정 쿼리가 이 업그레이드로 수정되었습니다. | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
릴리스 날짜 - 2018년 5월

APS 2016은 AU7로 업그레이드하기 위한 전제 조건입니다. APS AU7의 새로운 기능은 다음과 같습니다.

### <a name="auto-create-and-auto-update-statistics"></a>통계 자동 생성 및 자동 업데이트
APS AU7은 기본적으로 통계를 자동으로 만들고 업데이트합니다. 통계 설정을 업데이트하기 위해 관리자는 [구성 관리자](appliance-configuration.md#CMTasks)의 새 기능 스위치 메뉴 항목을 사용할 수 있습니다. [기능 스위치는](appliance-feature-switch.md) 통계의 자동 생성, 자동 업데이트 및 비동기 업데이트 동작을 제어합니다. [ALTER 데이터베이스(병렬 데이터 웨어하우스)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 문을 사용하여 통계 설정을 업데이트할 수도 있습니다.

### <a name="t-sql"></a>T-SQL
이제 @var 선택이 지원됩니다. 자세한 내용은 [로컬 변수 선택을](/sql/t-sql/language-elements/select-local-variable-transact-sql) 참조하십시오. 

쿼리 힌트 해시 및 ORDER 그룹이 지원됩니다. 자세한 내용은 [힌트(거래-SQL) - 쿼리를](/sql/t-sql/queries/hints-transact-sql-query) 참조하십시오.

### <a name="feature-switch"></a>기능 스위치
APS AU7은 구성 [관리자의](launch-the-configuration-manager.md)기능 스위치를 소개합니다. AutoStatsEnabled 및 DmsProcessStopMessageTimeoutSeconds는 이제 관리자가 변경할 수 있는 구성 가능한 옵션입니다.

### <a name="known-issues"></a>알려진 문제
APS AU7 소프트웨어를 사용하면 *투기적 실행 측면 채널 공격으로*설명된 문제를 해결하는 인텔 BIOS 업데이트가 제공됩니다. 이 공격은 유령 및 *멜트다운 취약점을*악용하는 것을 목표로합니다. APS와 함께 패키징되었지만 BIOS 업데이트는 APS AU7 소프트웨어 설치의 일부가 아니라 수동으로 설치됩니다.

Microsoft는 모든 고객에게 업데이트된 BIOS를 설치할 것을 권장합니다. Microsoft는 다양한 환경에서 다양한 SQL 워크로드에 대한 커널 가상 주소 그림자(KVAS), 커널 페이지 테이블 간접(KPTI) 및 간접 분기 예측 완화(IBP)의 효과를 측정했습니다. 측정 결과 일부 워크로드가 크게 저하된 것으로 나타났습니다. 결과에 따라 프로덕션 환경에 배포하기 전에 BIOS 업데이트를 사용하도록 설정하는 성능 효과를 테스트하는 것이 좋습니다. [여기SQL](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)서버 지침을 참조하십시오.

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
이 섹션에서는 APS 2016-AU6의 새로운 기능에 대해 설명했습니다.

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6는 최신 SQL Server 2016 릴리스에서 실행되며 기본 데이터베이스 호환성 수준 130을 사용합니다. SQL Server 2016을 사용하면 다음과 같은 새로운 기능을 지원할 수 있습니다.

- 클러스터된 열 저장소 인덱스에 대한 보조 인덱스입니다.
- 폴리베이스에 대한 케르베로스.

### <a name="t-sql"></a>T-SQL
APS AU6는 이러한 T-SQL 호환성 향상을 지원합니다.  이러한 추가 언어 요소를 통해 SQL Server 및 기타 데이터 원본에서 쉽게 마이그레이션할 수 있습니다. 

- [이제 Windows][] 데이터 정렬 외에도 열 수준 SQL 데이터 정렬이 지원됩니다.
- [클러스터된 columnstore 인덱스의 클러스터되지 않은 인덱스는][] 클러스터된 columnstore 인덱스의 특정 값을 검색하는 쿼리의 성능을 향상시킵니다. 
- [SELECT...INTO][] 
- [sp_spaceused()][] 테이블 이나 데이터베이스에서 사용 하거나 예약 된 디스크 공간을 표시 합니다.
- [와이드 테이블][] 지원은 SQL Server 2016과 동일합니다. 행 크기에 대한 이전 제한 32K는 더 이상 존재하지 않습니다. 

**데이터 유형**

- [바르차르(MAX),][] [은바르차(MAX)][] 및 [바리너리(MAX)][]. 이러한 LOB 데이터 형식의 최대 크기는 2GB입니다. 이러한 개체를 로드하려면 [bcp 유틸리티][]를 사용합니다. PolyBase 및 dwloader는 현재 이러한 데이터 형식을 지원하지 않습니다. 
- [SYSNAME][]
- [고유 식별자][]
- [숫자][] 및 소수점 데이터 형식입니다.

**창 함수**

- SELECT 문의 OVER 절의 [행 또는 범위입니다.][]
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**보안 기능**

- [체크섬()][] 및 [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**추가 기능**

- [뉴이드()][]
- [랜드()][]

### <a name="polybasehadoop-enhancements"></a>폴리베이스/하두프 개선 사항

- 호튼웍스 HDP 2.4 및 HDP 2.5와의 호환성
- 데이터베이스 범위 자격 증명을 통한 Kerberos 지원
- Azure 저장소 Blob을 위한 자격 증명 지원

### <a name="install-and-upgrade-enhancements"></a>설치 및 업그레이드 개선 사항

**엔터프라이즈 아키텍처 업데이트** 기존 어플라이언스를 APS AU6로 업그레이드하면 보안 수정이 포함된 최신 펌웨어 및 드라이버 업데이트가 설치됩니다. 

HPE 또는 DELL의 새로운 어플라이언스에는 모든 최신 업데이트와 다음이 포함되어 있습니다.

- 최신 세대 프로세서 지원(브로드웰)
- DDR4 DIMM으로 업데이트
- 향상된 DIMM 처리량

**통합**

- 완전 인증된 도메인 이름(FQDN) 지원을 통해 어플라이언스에 도메인 트러스트를 설정할 수 있습니다. 
- FQDN을 사용하려면 업그레이드 중에 전체 업그레이드 및 옵트인을 수행해야 합니다. 

**가동 중지 시간 감소** APS AU6로 설치 또는 업그레이드하는 속도가 빠르며 이전 릴리스보다 가동 중지 시간이 줄어듭니다. 가동 중지 시간을 줄이려면 설치 또는 업그레이드를 수행하십시오. 

 - 2016년 6월까지 모든 업데이트가 포함된 이미지를 사용하여 WSUS 업데이트를 적용간소화
 - 드라이버 및 펌웨어 업데이트에 보안 업데이트 적용
 - 최신 핫픽스와 어플라이언스 확인 유틸리티(PAV)를 어플라이언스에 배치하여 다운로드할 필요 없이 설치할 수 있습니다.

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[열 수준 SQL 데이터 정렬]: ~/relational-databases/collations/collation-and-unicode-support.md

[클러스터된 열 저장소 인덱스에 대한 클러스터되지 않은 인덱스]:/sql/t-sql/statements/create-index-transact-sql
[바르차르(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[응바르차르 (MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[바바이너리(최대)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[넓은 테이블]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp 유틸리티]:/sql/tools/bcp-utility
[고유 식별자]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[숫자]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[행 또는 범위]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[체크섬()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[뉴이드()]:/sql/t-sql/functions/newid-transact-sql
[랜드()]:/sql/t-sql/functions/rand-transact-sql


  

  


