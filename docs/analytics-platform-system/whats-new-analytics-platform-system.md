---
title: Analytics Platform System – 수평 확장 데이터 웨어하우스의에서 새로운 기능
description: Microsoft® Analytics Platform System에서는 MPP SQL Server 병렬 데이터 웨어하우스를 호스트 하는 스케일 아웃 온-프레미스 어플라이언스의에서 새로운 기능을 참조 하세요.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b1eee6b3ca692c7935b061696b37842cda0f8326
ms.sourcegitcommit: 1d81c645dd4fb2f0a6f090711719528995a34583
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/30/2018
ms.locfileid: "37137892"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>Analytics Platform System에서는 스케일 아웃 MPP 데이터 웨어하우스의에서 새로운 기능
최신 어플라이언스 업데이트에 대 한 Microsoft® Analytics Platform System (APS)의 새로운 기능을 참조 하세요. AP는 MPP SQL Server 병렬 데이터 웨어하우스를 호스트 하는 스케일 아웃 온-프레미스 어플라이언스입니다. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"

## <a name="aps-au7"></a>AP AU7
APS 2016은 AU7로 업그레이드 하는 필수 구성 요소입니다. 다음은 AP AU7의 새로운 기능:

### <a name="auto-create-and-auto-update-statistics"></a>자동 생성 및 자동 업데이트 통계
AP AU7 만들고 기본적으로 통계를 자동으로 업데이트 합니다. 관리자 수의 새 기능 스위치 메뉴 항목을 사용 하는 데 통계 설정을 업데이트 하는 [Configuration Manager](appliance-configuration.md#CMTasks)합니다. 합니다 [기능 스위치가](appliance-feature-switch.md) auto-create, 자동 업데이트 및 통계의 비동기 업데이트 동작을 제어 합니다. 사용 하 여 통계 설정을 업데이트할 수도 있습니다는 [ALTER DATABASE (병렬 데이터 웨어하우스)](/sql/t-sql/statements/alter-database-parallel-data-warehouse) 문입니다.

### <a name="t-sql"></a>T-SQL
선택 @var 이제 지원 됩니다. 자세한 내용은 [지역 변수 선택]을 참조 하세요. (/ sql/t-sql/language-elements/select-local-variable-transact-sql) 

해시 및 ORDER GROUP 쿼리 힌트는 이제 지원 됩니다. 자세한 내용은 [Hints(Transact-SQL)-쿼리]을 참조 하세요. (/ sql/t-sql/쿼리/힌트-transact-sql-쿼리)

### <a name="feature-switch"></a>기능 스위치
AP AU7 소개에서 기능 스위치 [Configuration Manager](launch-the-configuration-manager.md)합니다. AutoStatsEnabled DmsProcessStopMessageTimeoutInSeconds와 이제 관리자가 변경 될 수 있는 구성 가능한 옵션입니다.

### <a name="known-issues"></a>알려진 문제
으로 설명 하는 문제를 해결 하는 Intel BIOS 업데이트는 제공 하는 AP AU7 소프트웨어로 *투기적 실행 사이드 채널 공격*합니다. 공격 이라는 것을 악용 하는 것을 목표로 *스펙터와 멜트다운 취약점으로 인 한*합니다. BIOS 업데이트를 수동으로 설치 하 고 있지만 AP와 함께 패키지 AP AU7 소프트웨어 설치의 일부로 없습니다.

Microsoft는 BIOS 업데이트를 설치 하려면 모든 고객에 게 권고 합니다. Microsoft 다양 한 환경에서 다양 한 SQL 워크 로드에서 커널 가상 주소 숨기기 (KVAS), 커널 페이지 테이블 간접 참조 (KPTI) 및 간접 분기 예측 완화 (IBP)의 효과 측정 합니다. 측정값에 일부 워크 로드를 크게 저하 됨. 프로덕션 환경에 배포 하기 전에 BIOS 업데이트 사용의 성능 효과 테스트 하는 것이 좋습니다는 결과 따라 합니다. SQL Server 지침을 참조 하세요 [여기](https://support.microsoft.com/en-us/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)합니다.

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"

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

- [VARCHAR(MAX)][]하십시오 [NVARCHAR(MAX)][] 하 고 [varbinary (max)][]합니다. 이러한 LOB 데이터 형식에 최대 크기는 2GB입니다. 이러한 로드를 사용 하 여 개체 [bcp 유틸리티][]합니다. Polybase 및 dwloader 지원 하지 않습니다 현재 다음 데이터 형식. 
- [SYSNAME][]
- [고유 식별자][]
- [NUMERIC][] 및 DECIMAL 데이터 형식입니다.

**창 함수**

- [ROWS 또는 RANGE][] SELECT 문의 OVER 절에 있습니다.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**보안 함수**

- [CHECKSUM()][] 고 [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**추가 기능**

- [NEWID()][]
- [RAND)][]

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
[VARBINARY (MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[넓은 테이블]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp 유틸리티]:/sql/tools/bcp-utility
[고유 식별자]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
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
[RAND)]:/sql/t-sql/functions/rand-transact-sql


  

  


