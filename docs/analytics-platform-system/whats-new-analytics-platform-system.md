---
title: 분석 플랫폼 시스템 확장 데이터 웨어하우스의에서 새로운 기능
description: Microsoft® 분석 플랫폼 시스템, MPP SQL Server 병렬 데이터 웨어하우스를 호스팅하는 확장 온-프레미스 어플라이언스의에서 새로운 기능을 참조 하십시오.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c2408e84e7ff81f54ad00a98f85cd8dce7b04131
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34550644"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>확장 MPP 데이터 웨어하우스 분석 플랫폼 시스템의 새로운 기능
최신 어플라이언스 업데이트에 대 한 Microsoft® Analytics Platform System (APS)의 새로운 기능을 참조 하십시오. APS는 MPP SQL Server 병렬 데이터 웨어하우스를 호스트 하는 확장 온-프레미스 어플라이언스입니다. 


## <a name="aps-au7"></a>APS AU7
APS2016은 AU7로 업그레이드 하는 필수 구성 요소입니다. 다음은 AU7 APS에 대 한 새로운 기능:

### <a name="auto-create-and-auto-update-statistics"></a>자동 작성 및 통계 자동 업데이트 합니다.
APS AU7 만들고 기본적으로 자동으로 통계를 업데이트 합니다. 설정을 통계를 업데이트 하려면 관리자의 새로운 기능 스위치 메뉴 항목을 사용할 수 있습니다는 [Configuration Manager](appliance-configuration.md#CMTasks)합니다. [기능 스위치가](appliance-feature-switch.md) auto-create, 자동 업데이트 및 통계의 비동기 업데이트 동작을 제어 합니다. 사용 하 여 설정 통계를 업데이트할 수도 있습니다는 [ALTER DATABASE (병렬 데이터 웨어하우스)](/sql/t-sql/statements/alter-database-parallel-data-warehouse) 문.

### <a name="t-sql"></a>T-SQL
선택 @var 이제 지원 됩니다. 자세한 내용은 [지역 변수 선택]을 참조 하십시오. (/ sql/t-sql/language-elements/select-local-variable-transact-sql) 

해시 및 ORDER GROUP 쿼리 힌트 이제 지원 됩니다. 자세한 내용은 [Hints(Transact-SQL)-쿼리]을 참조 하십시오. (/ sql/t-sql/쿼리/힌트-transact-sql-쿼리)

### <a name="feature-switch"></a>기능 스위치
APS AU7의 스위치 기능을 소개 [Configuration Manager](launch-the-configuration-manager.md)합니다. AutoStatsEnabled와 DmsProcessStopMessageTimeoutInSeconds 관리자가 변경 될 수 있는 구성 가능한 옵션은 이제 합니다.

### <a name="known-issues"></a>알려진 문제
패키징 및 (즉, "추론 실행 사이드 채널 공격"를 해결 하는 Intel BIOS 업데이트를 제공 하는 APS AU7 소프트웨어와 함께. 유령 및 Meltdown 취약점)입니다. 그러나 함께 패키지 BIOS 업데이트가 수동으로 설치 되 고 APS AU7 소프트웨어의 일부가 아닌 설치 합니다. Microsoft 복사가 BIOS 업데이트가 설치 하는 모든 고객 합니다. Microsoft가 커널 가상 주소 섀도잉 (KVAS), 커널 페이지 테이블 간접 참조 (KPTI) 및 간접 분기 예측 완화 (IBP) 다양 한 환경에서 다양 한 SQL 작업에 미치는 영향을 측정 하 고 일부에 크게 저하 됨을 찾을 수합니다 워크 로드 합니다. 프로덕션 환경에 배포 하기 전에 BIOS 업데이트 사용의 성능 효과 테스트 하는 것이 좋습니다. 이러한 기능 사용의 성능 효과 기존 응용 프로그램에 비해 너무 높거나 경우 실행 되는 신뢰할 수 없는 코드에서 APS 어플라이언스 격리 응용 프로그램에 대 한 더 나은 완화 인지 여부를 고려할 수 있습니다. SQL Server 설명서를 참조 하십시오. [여기](https://support.microsoft.com/en-us/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)합니다.

## <a name="aps-2016"></a>APS 2016
다음은 APS 2016에 대 한 새로운 기능입니다.

### <a name="sql-server-2016"></a>SQL Server 2016

APS 2016 최신 SQL Server 2016 버전에서 실행 하 고 기본 데이터베이스 호환성 수준 130을 사용 합니다.  SQL Server 2016을 사용 하면 PolyBase에 대 한 클러스터형된 columnstore 인덱스 및 Kerberos에 대 한 지원 보조 인덱스와 같은 새로운 기능 중 일부를 수 있습니다. 


### <a name="t-sql"></a>T-SQL
APS 2016 T-SQL 호환성 향상 된 기능을 지원합니다.  이러한 추가 언어 요소 쉽게에서 SQL Server 및 기타 데이터 소스를 마이그레이션합니다. 

- [열 수준 SQL 데이터 정렬][] Windows 데이터 정렬 이외에 이제 지원 됩니다.
- [클러스터형된 columnstore 인덱스의 비클러스터형 인덱스][] 클러스터형된 columnstore 인덱스에 있는 특정 값을 검색 하는 쿼리의 성능을 개선 합니다. 
- [SELECT...INTO][] 
- [sp_spaceused()][] 디스크 공간 사용 또는 테이블이 나 데이터베이스에서 예약 된이 표시 됩니다.
- [넓은 테이블][] 지원은 SQL Server 2016으로 동일 합니다. 행 크기에 대 한 이전 제한인 32 K 더 이상 없습니다. 

**데이터 형식**

- [VARCHAR(MAX)][], [NVARCHAR(MAX)][] 및 [varbinary (max)][]합니다. 이러한 LOB 데이터 형식이 있는 최대 크기는 2GB입니다. 로드 하는 이러한 개체가 사용 [bcp 유틸리티][]합니다. Polybase 및 dwloader 지원 하지 않습니다 현재 이러한 데이터 형식입니다. 
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

- [CHECKSUM()][] 및 [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**추가 기능**

- [NEWID()][]
- [RAND)][]

### <a name="polybasehadoop-enhancements"></a>PolyBase Hadoop/향상 된 기능

- Hortonworks HDP 2.4 및 HDP 2.5와의 호환성
- 데이터베이스 범위 자격 증명을 통해 Kerberos 지원
- Azure 저장소 Blob을 사용한 자격 증명 지원

### <a name="install-and-upgrade-enhancements"></a>설치 및 업그레이드의 향상 된 기능

**엔터프라이즈 아키텍처 업데이트** 최신 펌웨어 및 보안 픽스를 포함 하는 드라이버 업데이트 설치 기존 어플라이언스 APS 2016으로 업그레이드 합니다. 

새로운 어플라이언스 HPE 또는 DELL에서 최신 업데이트를 모두 포함 및:

- 최신 세대 프로세서 지원 (Broadwell)
- DDR4 Dimm를 업데이트 합니다.
- DIMM 처리량 향상된

**통합**

- 완전히 정규화 된 도메인 이름 (FQDN) 지원을 통해 기기에 도메인 트러스트를 설정할 수 있습니다. 
- FQDN을 사용 하려면 전체 업그레이드를 수행 하 고 업그레이드 하는 동안 옵트인 해야 합니다. 

**가동 중지 시간 감소** APS 2016으로 업그레이드 하거나 설치는 버퍼 및 이전 버전 보다 덜 가동 중지 시간이 필요 합니다. 설치 또는 업그레이드, 가동 중지 시간을 줄입니다. 

 - 2016 년 6 월을 통해 업데이트를 모두 포함 된 이미지를 사용 하 여 WSUS 업데이트를 적용 하는 간소화
 - 드라이버 및 펌웨어 업데이트와 보안 업데이트 적용
 - 다운로드 하려면 필요 없이 설치할 수 있도록 어플라이언스 최신 핫픽스 및 어플라이언스 확인 유틸리티 (PAV)를 배치 합니다.


<!--MSDN references-->
[database compatibility level 130]:/sql/t-sql/statements/alter-database-transact-sql-compatibility-level
[열 수준 SQL 데이터 정렬]:/sql/relational-databases/collations/collation-and-unicode-support
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


  

  


