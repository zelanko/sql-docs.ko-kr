---
title: Windows Server 2008/2008 R2/2012 클러스터에서 실행 중인 SQL Server 인스턴스 업그레이드 | Microsoft Docs
ms.date: 01/25/2018
ms.prod: sql
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a73eda4fbb3898846894a4cf35de4253cffedbc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63243373"
---
# <a name="upgrade-sql-server-instances-running-on-windows-server-20082008-r22012-clusters"></a>Windows Server 2008/2008 R2/2012 클러스터에서 실행 중인 SQL Server 인스턴스 업그레이드

[!INCLUDE[nextref-longhorn-md](../../../includes/nextref-longhorn-md.md)], [!INCLUDE[winserver2008r2-md](../../../includes/winserver2008r2-md.md)], 및 [!INCLUDE[win8srv-md](../../../includes/win8srv-md.md)]에서는 Windows Server 장애 조치(failover) 클러스터가 운영 체제 바로 업그레이드를 수행하지 못하게 방지하여 클러스터에 허용되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전을 제한합니다. 클러스터가 [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] 이상으로 업그레이드되면 클러스터가 최신으로 유지될 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

-   마이그레이션 전략을 수행하기 전에 Windows Server 2016/2012 R2를 사용한 병렬 Windows Server 장애 조치(failover) 클러스터를 준비해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI(장애 조치 클러스터 인스턴스)를 구성하는 모든 노드는 병렬 FCI가 설치된 Windows 클러스터에 조인되어 있어야 합니다. 모든 독립 실행형 컴퓨터는 마이그레이션 전에 Windows Server 장애 조치 클러스터에 조인되어 있지 **않아야 합니다**. 사용자 데이터베이스는 마이그레이션 전에 새 환경에서 동기화해야 합니다.
-   모든 대상 인스턴스는 원본 환경의 병렬 인스턴스와 버전, 인스턴스 이름 및 ID가 동일하고, 동일한 기능이 설치된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]을(를) 실행 중이어야 합니다. 설치 경로 및 디렉터리 구조는 대상 컴퓨터에서 동일해야 합니다. 하지만 FCI 가상 네트워크 이름은 예외적으로 마이그레이션 전에 동일하지 않아야 합니다. 원본 인스턴스에서 활성화한 모든 기능(Always On, FILESTREAM 등)은 대상 인스턴스에서 활성화되어야 합니다.

-   마이그레이션 전에는 병렬 클러스터에 [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)]이(가) 설치되어 있지 않아야 합니다.

-   엄격하게 가용성 그룹(SQL FCI 지원 또는 미지원)을 사용하는 클러스터를 마이그레이션할 때는 분산 가용성 그룹을 사용하여 가동 중지 시간을 상당 부분 제한할 수 있지만 이를 위해서는 모든 인스턴스가 [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] RTM(또는 그 이상) 버전을 실행해야 합니다.

-   모든 마이그레이션 전략에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sysadmin 역할이 필요합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 사용하는 모든 Windows 사용자(즉, 복제 에이전트를 실행 중인 Windows 계정)는 새 환경의 각 컴퓨터에 대해 OS 수준 권한을 가지고 있어야 합니다.

-   원본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터 환경에서 사용된 네트워크 파일 공유 및 네트워크 매핑 드라이브는 계속 존재해야 하며, 대상 클러스터가 원본 인스턴스와 동일한 권한을 사용하여 액세스할 수 있어야 합니다.

-   원본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 수신 대기하는 모든 TCP/IP 포트는 사용 중이지 않아야 하며, 대상 컴퓨터에서 인바운드 트래픽을 허용해야 합니다.
-   모든 SQL 관련 서비스는 동일한 Windows 사용자가 설치하고 실행해야 합니다.

-   대상 인스턴스는 원본 인스턴스와 동일한 로캘을 사용하여 설치해야 합니다.

## <a name="migration-scenarios"></a>마이그레이션 시나리오

원본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터 토폴로지의 특정 매개 변수, 즉 [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)] 및 SQL 장애 조치(failover) 클러스터 인스턴스의 사용에 따라 올바른 마이그레이션 전략이 달라집니다. 또한 대상 환경의 요구 사항에 따라 선택하는 전략도 달라집니다. 새 환경에서 각 컴퓨터 또는 SQL FCI가 원본 가상 네트워크 이름(VNN)을 유지해야 하는 경우 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 토폴로지가 원본 인스턴스의 모든 시스템 개체를 상속하는 새로운 인스턴스에 따라 달라지는 경우 이를 마이그레이션하는 전략을 선택해야 합니다.

|                                   | 모든 서버 개체와 VNN 필요 | 모든 서버 개체와 VNN 필요 | 서버 개체/VNN이 필요하지 않음\* | 서버 개체/VNN이 필요하지 않음\* |
|-----------------------------------|--------------------------------------|--------------------------------------------------------------------|------------|------------|
| **_가용성 그룹? (예/아니요_)**                  | **_Y_**                              | **_N_**                                                            | **_Y_**    | **_N_**    |
| **클러스터에서 SQL FCI만 사용**         | [시나리오 3](#scenario-3-windows-cluster-has-both-sql-fcis-and-sql-server-availability-groups)                           | [시나리오 2](#scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis)                                                        | [시나리오 1](#scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis) | [시나리오 2](#scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis) |
| **클러스터에서 독립 실행형 인스턴스 사용** | [시나리오 5](#scenario-5-windows-cluster-with-standalone-sql-server-instances-and-availability-groups)                           | [시나리오 4](#scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups)                                                         | [시나리오 1](#scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis) | [시나리오 4](#scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups) |

\* 가용성 그룹 수신기 이름 제외

## <a name="scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis"></a>시나리오 1: SQL Server 가용성 그룹이 있고 FCI(장애 조치(Failover) 클러스터 인스턴스)가 없는 Windows 클러스터
AG(가용성 그룹)를 사용하고 장애 조치(failover) 클러스터 인스턴스를 사용하지 않는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]이 설치되어 있는 경우, Windows Server 2016/2012 R2가 설치된 다른 Windows 클러스터에 병렬 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포를 만들어서 새 클러스터로 마이그레이션할 수 있습니다. 이후에 대상 클러스터가 현재 프로덕션 클러스터에 대한 보조 클러스터인 분산 AG를 만들 수 있습니다. 이를 위해서는 사용자가 [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] 이상으로 업그레이드해야 합니다.

###  <a name="to-perform-the-upgrade"></a>업그레이드를 수행하려면

1.  필요한 경우 모든 인스턴스를 [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] 이상으로 업그레이드합니다. 병렬 인스턴스는 동일한 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]을(를) 실행 중이어야 합니다.

2.  대상 클러스터에 대한 가용성 그룹을 만듭니다. 대상 클러스터의 기본 노드가 FCI가 아닐 경우 수신기를 만듭니다.

3.  대상 클러스터가 보조 가용성 그룹인 분산 가용성 그룹을 형성합니다.

    >[!NOTE]
    >create distributed AG T-SQL에 대한 LISTENER\_URL 매개 변수는 SQL FCI가 주 인스턴스인 AG와 다르게 작동합니다. 기본 또는 보조 AG가 이런 경우라면 데이터베이스 미러링 엔드포인트 포트와 함께 주 SQL FCI의 VNN을 수신기의 네트워크 이름 대신 수신기 URL로 사용합니다.

4.  보조 가용성 그룹을 분산 AG에 조인합니다.

5.  보조 AG에서 보조 데이터베이스를 조인합니다.

    >[!NOTE]
    >이는 대상 가용성 그룹이 자동 시드를 사용하는 경우에 자동으로 수행됩니다. 이는 모든 복제본에서 데이터 및 로그 경로가 동일한 경우에만 가능합니다.

6.  기본 AG에 대한 모든 트래픽을 차단하고 보조 AG가 동기화되도록 합니다.

7.  두 가용성 그룹에 대한 커밋 정책을 SYNCHRONOUS_COMMIT으로 변경하고 상태가 SYNCHRONIZED가 되면 대상 클러스터로 장애 조치(failover)를 수행합니다.

8.  분산 AG를 삭제합니다.

9.  원본 AG의 수신기를 삭제하거나 이름을 바꿉니다.

10. 이름을 바꾸거나 원본 AG의 수신기 이름을 사용하여 새 AG 수신기를 만듭니다.

    >[!NOTE]
    >원래 AG 수신기에 대한 DNS 기록이 있으면 이 이름을 사용한 수신기 생성 시도가 실패합니다.

11. 수신기에 대한 트래픽을 다시 시작합니다.

## <a name="scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis"></a>시나리오 2: SQL Server FCI(장애 조치(Failover) 클러스터 인스턴스)가 없는 Windows 클러스터

SQL FCI 인스턴스만 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 환경의 경우, Windows Server 2016/2012 R2가 설치된 다른 Windows 클러스터에 병렬 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 환경을 만들어서 새 클러스터로 마이그레이션할 수 있습니다. 이전 SQL FCI의 VNN을 "도용"하고 새로운 클러스터에서 입수하여 대상 클러스터로 마이그레이션할 수 있습니다. 그러면 DNS 전파 시간에 따라 추가 가동 중지 시간이 발생합니다.

###  <a name="to-perform-the-upgrade"></a>업그레이드를 수행하려면

1.  전체 백업을 수행하고 원본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터에 대한 트래픽을 중지합니다.

2.  사용자 데이터베이스의 비상 로그 백업을 수행하고 새 환경에서 복구를 통해 복원합니다.

3.  대상 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI의 클러스터링된 역할을 중지 상태로 전환합니다.

4.  대상 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI가 사용하는 클러스터링된 디스크를 다시 가동 상태로 전환합니다.

5.  원본 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI의 클러스터링된 역할을 중지 상태로 전환합니다.

6.  원본 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI가 사용하는 클러스터링된 디스크를 다시 가동 상태로 전환합니다.

7.  해당 원본 컴퓨터의 시스템 데이터베이스를 병렬 대상 컴퓨터로 복사합니다.

8.  원본 환경의 장애 조치(Failover) 클러스터 관리자에서 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할의 '서버 이름' 리소스 이름을 변경합니다.

9.  이제 각 SQL FCI 역할에서 이름이 바뀐 서버 이름 리소스만 다시 온라인 상태로 전환합니다.

10. 이제 대상 클러스터의 장애 조치(failover) 클러스터 관리자에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할의 "서버 이름" 리소스 이름을 원본 클러스터에서 이전에 보유한 이름으로 변경합니다.

    >[!NOTE]
    >다른 컴퓨터에서 이미 보유하고 있는 이름으로 인해 발생하는 오류는 이름에 대한 DNS 기록이 삭제되면 중지됩니다.

11. 모든 FCI의 이름이 변경되면 새 클러스터에서 각 컴퓨터를 다시 시작합니다.

12. 재시작 후 컴퓨터가 다시 온라인 상태가 되면 장애 조치(failover) 클러스터 관리자에서 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할을 시작합니다.

## <a name="scenario-3-windows-cluster-has-both-sql-fcis-and-sql-server-availability-groups"></a>시나리오 3: SQL FCI와 SQL Server 가용성 그룹이 모두 있는 Windows 클러스터

독립 실행형 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 사용하지 않고 하나 이상의 가용성 그룹에 포함된 SQL FCI만 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램이 있는 경우 이를 "가용성 그룹 없음, 독립 실행형 인스턴스 없음" 시나리오와 유사한 방법을 사용하여 새 클러스터로 마이그레이션할 수 있습니다. 시스템 테이블을 대상 FCI 공유 디스크에 복사하기 전에 원본 환경의 모든 가용성 그룹을 삭제해야 합니다. 모든 데이터베이스가 대상 컴퓨터로 마이그레이션되면 동일한 스키마와 수신기 이름으로 가용성 그룹을 다시 만듭니다. 이렇게 하면 Windows Server 장애 조치(failover) 클러스터 리소스가 대상 클러스터에서 올바르게 형식이 지정되고 관리됩니다. **마이그레이션 전에 대상 환경의 각 컴퓨터의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager에서 Always On을 활성화해야 합니다.**

### <a name="to-perform-the-upgrade"></a>업그레이드를 수행하려면

1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 트래픽을 중지합니다.

2.  사용자 데이터베이스의 비상 로그 백업을 수행하고, 새로운 환경의 원하는 기본 노드에서 복구를 통해 복원하고, 원하는 모든 보조 노드에서 NORECOVERY를 통해 복원합니다.

3.  대상 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI의 클러스터링된 역할을 중지 상태로 전환합니다.

4.  대상 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI가 사용하는 클러스터링된 디스크를 다시 가동 상태로 전환합니다.

5.  원본 클러스터에서 가용성 그룹을 삭제합니다.

6.  원본 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI의 클러스터링된 역할을 중지 상태로 전환합니다.

7.  원본 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI가 사용하는 클러스터링된 디스크를 다시 가동 상태로 전환합니다.

8.  해당 원본 컴퓨터의 시스템 데이터베이스를 병렬 대상 컴퓨터로 복사합니다.

9.  원본 환경의 장애 조치(Failover) 클러스터 관리자에서 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할의 '서버 이름' 리소스 이름을 변경합니다.

10. 이제 각 SQL FCI 역할에서 이름이 바뀐 서버 이름 리소스만 다시 온라인 상태로 전환합니다.

11. 이제 대상 클러스터의 장애 조치(failover) 클러스터 관리자에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할의 "서버 이름" 리소스 이름을 원본 클러스터에서 이전에 보유한 이름으로 변경합니다.

12. 모든 FCI의 이름이 변경되면 새 클러스터에서 각 컴퓨터를 다시 시작합니다.

13. 재시작 후 컴퓨터가 다시 온라인 상태가 되면 장애 조치(failover) 클러스터 관리자에서 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할을 시작합니다.

14. 모든 인스턴스가 온라인 상태가 되면 복구를 통해 데이터베이스를 복원한 복제본에서 가용성 그룹을 형성합니다.

15. 모든 보조 복제본을 AG에 조인하고, 모든 보조 데이터베이스를 AG에 조인합니다.

16. 원본 가용성 그룹의 수신기 이름을 사용하여 새로운 AG에 수신기를 만듭니다.

## <a name="scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups"></a>시나리오 4: 독립 실행형 SQL Server 인스턴스가 있고 가용성 그룹이 없는 Windows 클러스터

독립 실행형 인스턴스를 사용하여 클러스터를 마이그레이션하는 것은 FCI만 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터를 마이그레이션하는 프로세스와 유사하지만 FCI의 네트워크 이름 클러스터 리소스의 VNN을 변경하지 않고 원본 독립 실행형 머신의 머신 이름을 변경한 후 대상 머신에서 이전 머신의 이름을 "도용"한다는 점이 다릅니다. 이전 머신의 네트워크 이름을 입수해야만 대상 독립 실행형 머신을 WSFC로 조인할 수 있으므로 이 시나리오는 독립 실행형이 아닌 시나리오보다 가동 중지 시간이 더 길어집니다.

###  <a name="to-perform-the-upgrade"></a>업그레이드를 수행하려면

1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 트래픽을 중지합니다.

2.  사용자 데이터베이스의 비상 로그 백업을 수행하고 각 컴퓨터의 새 환경에서 복구를 통해 복원합니다.

3.  대상 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI의 클러스터링된 역할을 중지 상태로 전환합니다.

4.  대상 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI가 사용하는 클러스터링된 디스크를 다시 가동 상태로 전환합니다.

5.  원본 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI의 클러스터링된 역할을 중지 상태로 전환하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 독립 실행형 인스턴스를 중지합니다.

6.  원본 클러스터의 각 독립 실행형 컴퓨터에서 각 컴퓨터의 이름을 고유한 새 컴퓨터 이름으로 바꿉니다. 이러한 각 컴퓨터를 지침에 따라 다시 시작합니다.

7.  원본 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI가 사용하는 클러스터링된 디스크를 다시 가동 상태로 전환합니다.

8.  시스템 데이터베이스를 대상 컴퓨터로 복사합니다.

9.  원본 환경의 장애 조치(Failover) 클러스터 관리자에서 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할의 '서버 이름' 리소스를 고유한 새 이름으로 변경합니다.

10. 이제 각 SQL FCI 역할에서 이름이 바뀐 서버 이름 리소스만 다시 온라인 상태로 전환합니다.

11. 이제 병렬 독립 실행형 인스턴스에서 컴퓨터의 이름을 원본 독립 실행형 컴퓨터 이름으로 변경합니다. (이전 서버 이름을 삭제하고 로컬 매개 변수를 사용하여 새로운 서버 이름을 추가합니다.) 지침에 따라 컴퓨터를 다시 시작합니다.

12. 재시작 후 각각의 독립 실행형 컴퓨터를 대상 Windows Server 장애 조치(failover) 클러스터에 조인합니다.

13. 이제 대상 클러스터의 장애 조치(failover) 클러스터 관리자에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할의 "서버 이름" 리소스 이름을 원본 클러스터에서 이전에 보유한 이름으로 변경합니다.

14. 모든 FCI의 이름이 변경되면 새 클러스터에서 각 컴퓨터를 다시 시작합니다.

15. 재시작 후 컴퓨터가 다시 온라인 상태가 되면 장애 조치(failover) 클러스터 관리자에서 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할을 시작합니다.

## <a name="scenario-5-windows-cluster-with-standalone-sql-server-instances-and-availability-groups"></a>시나리오 5: 독립 실행형 SQL Server 인스턴스와 가용성 그룹이 있는 Windows 클러스터

독립 실행형 복제본으로 가용성 그룹을 사용하는 클러스터를 마이그레이션하는 것은 가용성 그룹을 사용하여 FCI로 클러스터를 마이그레이션하는 프로세스와 유사합니다. 여전히 원본 가용성 그룹을 삭제하고 대상 클러스터에 재구성해야 하지만 독립 실행형 인스턴스 마이그레이션 시 추가 비용으로 인해 추가 가동 중지 시간이 발생합니다. **마이그레이션 전에 대상 환경의 각 FCI에서 Always On을 활성화해야 합니다.**

###  <a name="to-perform-the-upgrade"></a>업그레이드를 수행하려면

1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 트래픽을 중지합니다.

2.  사용자 데이터베이스의 비상 로그 백업을 수행하고, 새로운 환경의 원하는 기본 노드에서 복구를 통해 복원하고, 원하는 각 보조 노드에서 NORECOVERY를 통해 복원합니다.

3.  원본 클러스터에서 가용성 그룹을 삭제합니다.

4.  대상 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI의 클러스터링된 역할을 중지 상태로 전환합니다.

5.  대상 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI가 사용하는 클러스터링된 디스크를 다시 가동 상태로 전환합니다.

6.  원본 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI의 클러스터링된 역할을 중지 상태로 전환하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 독립 실행형 인스턴스를 중지합니다.

7.  원본 클러스터의 각 독립 실행형 컴퓨터에서 각 컴퓨터의 이름을 고유한 새 컴퓨터 이름으로 바꿉니다. 이러한 각 컴퓨터를 지침에 따라 다시 시작합니다.

8.  원본 클러스터의 장애 조치(Failover) 클러스터 관리자에서 각 SQL FCI가 사용하는 클러스터링된 디스크를 다시 가동 상태로 전환합니다.

9.  시스템 데이터베이스를 대상 컴퓨터로 복사합니다.

10. 원본 환경의 장애 조치(Failover) 클러스터 관리자에서 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할의 '서버 이름' 리소스를 고유한 새 이름으로 변경합니다.

11. 이제 각 SQL FCI 역할에서 이름이 바뀐 서버 이름 리소스만 다시 온라인 상태로 전환합니다.

12. 이제 병렬 독립 실행형 인스턴스에서 컴퓨터의 이름을 원본 독립 실행형 컴퓨터 이름으로 변경합니다. (SQL에서 서버 이름을 삭제하고 추가합니다.) 지침에 따라 컴퓨터를 다시 시작합니다.

13. 재시작 후 각각의 독립 실행형 컴퓨터를 대상 Windows Server 장애 조치(failover) 클러스터에 조인합니다.

14. 이제 대상 클러스터의 장애 조치(failover) 클러스터 관리자에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할의 "서버 이름" 리소스 이름을 원본 클러스터에서 이전에 보유한 이름으로 변경합니다.

15. 모든 FCI의 이름이 변경되면 새 클러스터에서 각 컴퓨터를 다시 시작합니다.

16. 재시작 후 컴퓨터가 다시 온라인 상태가 되면 장애 조치(failover) 클러스터 관리자에서 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI 역할을 시작합니다.

17. 모든 인스턴스가 온라인 상태가 되면 원하는 기본 노드에서 가용성 그룹을 다시 만듭니다.

18. 각 보조 복제본 및 보조 데이터베이스를 조인합니다.

19. 원본과 동일한 이름을 사용하여 가용성 그룹 수신기를 다시 만듭니다.

## <a name="specific-concerns-for-individual-features"></a>개별 기능에 대한 특정 문제

### [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)]

-   **데이터베이스 미러링 엔드포인트**

    SQL 관점에서 데이터베이스 미러링 엔드포인트는 시스템 테이블과 함께 새로운 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스로 마이그레이션됩니다. 마이그레이션 전에 방화벽에 적절한 규칙이 적용되어 있고 동일한 포트에서 다른 프로세스가 수신 대기하고 있지 않은지 확인하세요.

-   **가용성 그룹**

    가용성 그룹과 해당 수신기는 인스턴스 간에 마이그레이션할 수 없습니다. 가용성 그룹에서 만든 Windows Server 장애 조치(failover) 클러스터 리소스는 대상 환경에 쉽게 다시 만들 수 없습니다. 가용성 그룹을 마이그레이션하는 대신 대상 클러스터에서 가용성 그룹을 삭제하고 다시 만드는 것이 좋습니다.

-   **가용성 그룹 수신기**

    가용성 그룹 수신기는 가용성 그룹과 마찬가지로 바로 마이그레이션하지 않고 삭제한 후 다시 만듭니다.

### <a name="replication"></a>복제

-   **원격 배포자, 게시자, 구독자**

    배포자와 게시자 간의 관계는 새 컴퓨터로 올바르게 확인되는, 둘을 호스팅하는 컴퓨터의 VNN에만 좌우됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업도 시스템 테이블과 함께 올바르게 마이그레이션되므로 다양한 복제 에이전트가 계속 평상시처럼 실행될 수 있습니다. 마이그레이션을 수행하기 전에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 자체나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업을 실행 중인 Windows 계정은 대상 환경에서 동일한 권한을 가져야 합니다. 게시자와 구독자와의 통신은 평상시처럼 실행됩니다.

-   **스냅숏 폴더**

    마이그레이션 전에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능이 사용하는 모든 네트워크 공유는 대상 환경의 컴퓨터가 원본 환경과 동일한 권한으로 액세스할 수 있어야 합니다. 마이그레이션 전에 이 사실을 확인해야 합니다.

### <a name="service-broker"></a>Service Broker

-   **Service broker 엔드포인트**

    [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관점에서 엔드포인트와 관련된 문제는 없습니다. 마이그레이션 전에 동일한 포트에서 이미 수신 대기하고 있는 프로세스가 없고, 방화벽 규칙이 해당 포트를 차단하고 있지 않은지, 명시적으로 포트를 허용하는 방화벽 규칙이 있는지 확인해야 합니다.

-   **인증서**

    인증서를 새 컴퓨터로 복원해야 하는 경우에도 대상 컴퓨터에 인증서를 백업하고 복원해야 합니다.

-   **경로**

    경로는 대상의 가상 네트워크 이름에 따라 달라집니다. 컴퓨터 이름과 SQL FCI 네트워크 이름의 경우 새 환경의 올바른 컴퓨터로 올바르게 확인됩니다. 다른 모든 참조된 VNN도 새 컴퓨터로 리디렉션되어야 합니다.

-   **원격 서비스 바인딩**

    원격 서비스 바인딩을 사용하는 모든 사용자는 올바르게 마이그레이션되기 때문에 원격 서비스 바인딩은 마이그레이션 후에 올바르게 작동합니다.

### <a name="includessnoversionincludesssnoversion-mdmd-agent"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트

-   **작업**

    작업은 시스템 데이터베이스와 함께 올바르게 마이그레이션됩니다. SQL 에이전트 작업 또는 SQL 에이전트 자체를 실행하는 모든 사용자는 대상 컴퓨터에 대해 필수 구성 요소에 지정된 것과 동일한 사용 권한을 갖습니다.

-   **경고 및 연산자**

    경고 및 연산자는 시스템 데이터베이스와 함께 올바르게 마이그레이션됩니다.

### <a name="filestream"></a>FILESTREAM

-   **Windows 파일 공유 포트**

    Windows 파일 공유 포트 139 및 445는 인바운드 트래픽이 FILESTREAM을 사용하도록 허용하는 규칙을 가지고 있어야 합니다.

-   **Windows 공유**

    Windows 공유 경로는 `\\ServerName\ShareName`을 사용하여 액세스하므로 SQL FCI 이름 리소스에 따라 달라집니다. FILESTREAM을 마이그레이션하려면 대상 FCI의 모든 노드가 FILESTREAM을 활성화해야 하며, Windows 공유를 사용하는 경우 원본 컴퓨터와 동일한 이름을 사용하도록 구성해야 합니다. 대상 FCI가 올바른 서버 이름을 입수하면 원하는 경로를 사용하여 Windows 공유를 호스팅하게 됩니다.

-   **FILESTREAM 데이터**

    FILESTREAM 데이터는 백업에 포함됩니다.

### <a name="integration-services"></a>Integration Services

-   **SSIS 프로젝트**

    SSIS 프로젝트는 SSIS 데이터베이스와 함께 마이그레이션됩니다. SSIS 데이터베이스가 이동되면 시스템 테이블을 이동하기 전에 패키지를 즉시 실행할 수 있습니다.

-   **파일 기반 데이터 원본**

    플랫 파일, Excel 파일, XML 원본 및 기타 파일은 SSIS 패키지가 지정한 동일한 위치에서 액세스할 수 있어야 합니다.

## <a name="next-steps"></a>다음 단계
- [데이터베이스 엔진 업그레이드 완료](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)
- [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)
- [새 SQL Server 2016 기능 활용](https://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)
- [SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드](upgrade-a-sql-server-failover-cluster-instance.md)
- [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
- [SQL Server 2016 인스턴스에 기능 추가(설치 프로그램)](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)
