---
title: "Linux에서 SQL Server에 대 한 always On 가용성 그룹 | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.workload: On Demand
ms.openlocfilehash: 2b9d80b92fd189340c5c15504ab37a8c0022df85
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="availability-groups-for-sql-server-on-linux"></a>Linux에서 SQL Server에 대 한 가용성 그룹

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server Always On 가용성 그룹은 고가용성 (HA), 재해 복구 (DR) 및 확장 솔루션입니다. 데이터베이스에 직접 연결 된 저장소 그룹에 대 한 HA를 제공합니다. 통합 된 HA 및 DR, 자동 실패 감지, 빠른 투명 한 장애 조치 및 읽기 부하 분산에 대 한 여러 개의 보조 복제본을 지원합니다. 이 광범위 한 기능을 사용 하면 작업에 대 한 최적의 가용성 Sla를 달성 수 있습니다.

SQL Server 가용성 그룹 SQL Server 2012에서 처음으로 도입 하 고 각 릴리스마다 향상 되었습니다. 이제이 기능은 Linux에서 사용할 수 있습니다. SQL Server 작업과 엄격한 비즈니스 연속성 요구를 수용 하기 위해 가용성 그룹에서 지원 되는 모든 실행 [Linux 운영 체제 배포판](sql-server-linux-release-notes.md)합니다. 또한 가용성 그룹 유연 하 고 효율적인 통합 HA DR 솔루션을 구성 하는 기능을 모두 사용할 수 있는 Linux 도입니다. 이러한 개체는 다음과 같습니다. 

- **다중 데이터베이스 장애 조치** 가용성 그룹의 가용성 데이터베이스 라고 하는 사용자 데이터베이스 집합에 대 한 장애 조치 환경을 지원 합니다.
- **빠른 오류 검색 및 장애 조치** 항상 사용 가능한 클러스터에 리소스로 가용성 그룹에서 즉각적인 장애 조치가 감지 및 장애 조치 작업에 대 한 기본 제공 클러스터 인텔리전스 유리 합니다.
- **가상 IP 리소스를 사용 하 여 투명 한 장애 조치** 장애 조치 시 기본 단일 연결 문자열을 사용 하도록 클라이언트 수 있습니다. 클러스터 관리자와 통합이 필요 합니다.
- **여러 동기 및 비동기 보조** 가용성 그룹은 최대 8 개의 보조 복제본을 지원 합니다. 동기 복제본과 주 복제본이 주 복제본이 트랜잭션을 디스크에 트랜잭션 로그에 쓸 수에 대 한 기다리는 트랜잭션을 커밋하지 기다리는 합니다. 주 복제본에서 동기 복제본이 비동기 쓰기 작업에 대해 기다리지 않습니다.  
- **자동 또는 수동 장애 조치** 동기 보조 복제본으로 장애 조치도 트리거할 수 있는 자동으로 클러스터에서 또는 요청 시 데이터베이스 관리자입니다.
- **읽기 및 백업 작업에 대해 사용할 수 있는 활성 보조** 보조 데이터베이스에 대 한 읽기 전용 액세스를 지원 하도록 및/또는 보조 데이터베이스에서 백업을 허용 하기 위해 하나 이상의 보조 복제본을 구성할 수 있습니다.
- **자동 시드** SQL Server 가용성 그룹의 모든 데이터베이스에 대 한 보조 복제본을 자동으로 만듭니다.
- **읽기 전용 라우팅** SQL Server는 읽기 전용 작업을 허용 하도록 구성 된 보조 복제본을 가용성 그룹 수신기에 들어오는 연결을 라우팅합니다. 
- **데이터베이스 수준 상태 모니터링 및 장애 조치 트리거** 향상 된 데이터베이스 수준 모니터링 및 진단 합니다. 
- **재해 복구 구성** 분산된 된 가용성 그룹 또는 다중 서브넷 가용성 그룹 설정 합니다. 
- **읽기 확장 기능** 에서 SQL Server 2017 HA 유무 확장 읽기 전용 작업에 대 한 가용성 그룹을 만들 수 있습니다. 


SQL Server 가용성 그룹에 대 한 세부 정보를 참조 하십시오. [SQL Server Always On 가용성 그룹](http://msdn.microsoft.com/library/hh510230.aspx)합니다.

## <a name="availability-group-terminology"></a>가용성 그룹 용어

가용성 그룹-가용성 데이터베이스-함께 장애 조치 하는 사용자 데이터베이스의 불연속 집합에 대 한 장애 조치 환경을 지원 합니다. 가용성 그룹 하나 집합이 읽기 / 쓰기 주 데이터베이스 집합과 1 ~ 8 개의 해당 보조 데이터베이스를 지원합니다. 필요한 경우 보조 데이터베이스에 대해 읽기 전용 액세스를 설정하거나 일부 백업 작업에 사용되도록 설정할 수 있습니다. 가용성 그룹에 가용성 복제본 이라는 두 개 이상의 장애 조치 파트너의 집합을 정의 합니다. 가용성 복제본은 가용성 그룹의 구성 요소입니다. 자세한 내용은 [개요의 Always On 가용성 그룹 (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)합니다.

SQL Server 가용성 그룹 솔루션의 주요 부분을 설명 하는 다음 조건:

 가용성 그룹  
 함께 장애 조치(failover)되는 데이터베이스의 집합인 *가용성 데이터베이스*의 컨테이너입니다.  
  
 가용성 데이터베이스  
 가용성 그룹에 속하는 데이터베이스입니다. 가용성 그룹은 각 가용성 데이터베이스에 대해 하나의 읽기/쓰기 복사본( *주 데이터베이스*)과 1~8개의 읽기 전용 복사본(*보조 데이터베이스*)을 유지 관리합니다.  
  
 주 데이터베이스  
 가용성 데이터베이스의 읽기/쓰기 복사본입니다.  
  
 보조 데이터베이스  
 가용성 데이터베이스의 읽기 전용 복사본입니다.  
  
 가용성 복제본  
 SQL Server의 특정 인스턴스에 의해 호스팅되고 가용성 그룹에 속하는 각 가용성 데이터베이스의 로컬 복사본을 유지 하는 가용성 그룹 인스턴스화입니다. 가용성 복제본은 하나의 *주 복제본* 과 1~8개의 *보조 복제본*이라는 두 가지 유형이 있습니다.  
  
 주 복제본  
 클라이언트에서 주 데이터베이스에 읽기/쓰기 연결을 할 수 있도록 주 데이터베이스를 설정하고 각 주 데이터베이스에 대한 트랜잭션 로그 레코드를 모든 보조 복제본에 보내는 가용성 복제본입니다.  
  
 보조 복제본  
 각 가용성 데이터베이스의 보조 복사본을 유지 관리하고 가용성 그룹에 대한 잠재적인 장애 조치(Failover) 대상 역할을 하는 가용성 복제본입니다. 필요에 따라 보조 복제본은 보조 데이터베이스에 대한 읽기 전용 액세스와 보조 데이터베이스에 백업을 만드는 것을 지원할 수 있습니다.  
  
 가용성 그룹 수신기  
 가용성 그룹의 주 또는 보조 복제본에 있는 데이터베이스에 액세스하기 위해 클라이언트가 연결할 수 있는 서버 이름입니다. 가용성 그룹 수신기는 들어오는 연결을 주 복제본이나 읽기 전용 보조 복제본에 전달합니다.  


## <a name="new-in-sql-server-2017-for-availability-groups"></a>가용성 그룹에 대 한 SQL Server 2017의 새로운

SQL Server 2017에 가용성 그룹에 대 한 새로운 기능이 도입 되었습니다.

**CLUSTER_TYPE** 사용 `CREATE AVAILABILITY GROUP`합니다. 가용성 그룹을 관리 하는 서버 클러스터 관리자의 형식을 나타냅니다. 다음 형식 중 하나일 수 있습니다.

   - **WSFC** Winows 서버 장애 조치 클러스터입니다. Windows에서는 CLUSTER_TYPE에 대 한 기본 값입니다.
   - **외부** 켜져 있는 하지 Windows server 장애 조치 클러스터-예를 들어 Pacemaker 있는 Linux 클러스터 관리자입니다.
   - **NONE** 클러스터 관리자가 없습니다. 읽기 확장성이 가용성 그룹에 사용 합니다.

이러한 옵션에 대 한 자세한 내용은 참조 [CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx) 또는 [ALTER AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878601.aspx)합니다.

**동기 보조 복제본에서 커밋 보장**

Use `required_synchronized_secondaries_to_commit`with `CREATE AVAILABILITY GROUP` or `ALTER AVAILABILITY GROUP`. 때 `required_synchronized_secondaries_to_commit` 데이터베이스는 지정된 된 수의에서 트랜잭션이 커밋된 때까지 대기 하는 주 복제본에서 트랜잭션 0 보다 큰 값으로 설정 되어 **동기 보조 데이터베이스** 복제본 데이터베이스 트랜잭션 로그입니다. 충분 한 동기 보조 복제본이 온라인 상태인 경우에 충분 한 보조 복제본으로 통신이 다시 시작 될 때까지 주 복제본에 대 한 모든 연결 거부 됩니다.

**읽기 확장성이 가용성 그룹**

확장성이 읽기 작업을 지원 하기 위해 클러스터에 없는 가용성 그룹을 만듭니다. 참조 [읽기 확장성이 가용성 그룹](../database-engine/availability-groups/windows/read-scale-availability-groups.md)합니다.

## <a name="next-steps"></a>다음 단계

[Linux에서 SQL Server에 대 한 가용성 그룹을 구성 합니다.](sql-server-linux-availability-group-configure-ha.md)

[Linux에서 SQL Server에 대 한 읽기 확장성이 가용성 그룹을 구성 합니다.](sql-server-linux-availability-group-configure-rs.md)

[RHEL에서 가용성 그룹 클러스터 리소스를 추가 합니다.](sql-server-linux-availability-group-cluster-rhel.md)

[SLES에 가용성 그룹 클러스터 리소스를 추가 합니다.](sql-server-linux-availability-group-cluster-sles.md)

[Ubuntu 가용성 그룹 클러스터 리소스를 추가 합니다.](sql-server-linux-availability-group-cluster-ubuntu.md)
