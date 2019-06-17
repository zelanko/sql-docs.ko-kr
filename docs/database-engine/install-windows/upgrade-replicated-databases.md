---
title: 복제된 데이터베이스 업그레이드 또는 패치 | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- merge replication database upgrades [SQL Server replication]
- replication [SQL Server], upgrading
- transactional replication, upgrading databases
- snapshot replication [SQL Server], upgrading databases
- upgrading replicated databases
ms.assetid: 9926a4f7-bcd8-4b9b-9dcf-5426a5857116
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 3b311514c90045042dcb6a62f163d5fe08ef9549
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794715"
---
# <a name="upgrade-or-patch-replicated-databases"></a>복제된 데이터베이스 업그레이드 또는 패치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복제된 데이터베이스를 업그레이드할 수 있도록 지원합니다. 따라서 노드 업그레이드 중에 다른 노드의 작업을 중지할 필요가 없으며 한 토폴로지 내에서 지원되는 버전과 관련된 규칙만 잘 지키면 됩니다.  
  
-   배포자는 게시자 버전 이상인 모든 버전일 수 있습니다. 많은 경우에 배포자는 게시자와 동일한 인스턴스에 있습니다.    
-   게시자는 배포자 버전 이하인 모든 버전일 수 있습니다.    
-   구독자 버전은 게시 유형에 따라 달라집니다.    
    - 트랜잭션 게시에 대한 구독자는 게시자의 두 가지 버전 중 어떤 버전이든 될 수 있습니다. 예를 들어 SQL Server 2012(11.x) 게시자에는 SQL Server 2014(12.x) 및 SQL Server 2016(13.x) 구독자가 있을 수 있으며, SQL Server 2016(13.x) 게시자에는 SQL Server 2014(12.x) 및 SQL Server 2012(11.x) 구독자가 있을 수 있습니다.     
    - 병합 게시에 대한 구독자는 버전 수명 주기 지원 주기에 따라 지원되는 게시자 버전과 같거나 낮은 모든 버전이 될 수 있습니다.  
 
SQL Server로의 업그레이드 경로는 배포 패턴에 따라 다릅니다. SQL Server는 일반적으로 다음 두 가지 업그레이드 경로를 제공합니다.
- 함께 실행: 병렬 환경을 배포하고 로그인, 작업 등 연결된 인스턴스 수준 개체와 함께 데이터베이스를 새 환경으로 이동합니다. 
- 현재 위치 업그레이드: SQL Server 설치 미디어를 통해 SQL Server 비트를 바꾸고 데이터베이스 개체를 업그레이드하여 기존 SQL Server 설치를 업그레이드하도록 허용합니다. Always On 가용성 그룹 또는 장애 조치 클러스터 인스턴스를 실행하는 환경의 경우 현재 위치 업그레이드는 [롤링 업그레이드](choose-a-database-engine-upgrade-method.md#rolling-upgrade)와 결합되어 가동 중지 시간을 최소화합니다. 

복제 토폴로지를 병렬로 업그레이드하기 위해 채택된 일반적인 방법은 전체 토폴로지의 이동과 달리 일부 게시자-구독자 쌍을 새 병렬 새 환경으로 이동하는 것입니다. 이러한 단계별 방법은 가동 중지 시간을 제어하고 복제를 사용하는 비즈니스에 미치는 영향을 어느 정도 최소화할 수 있습니다.  

이 문서의 대부분은 SQL Server 버전 업그레이드에 대한 것입니다. 그러나 SQL Server를 서비스 팩 또는 누적 업데이트로 패치할 때도 적절한 업그레이드 프로세스를 사용해야 합니다. 

 >[!WARNING]
 > 복제 토폴로지를 업그레이드하는 작업은 다단계 프로세스입니다. 실제 프로덕션 환경에서 업그레이드를 실행하기 전에 테스트 환경에서 복제 토폴로지의 복제본을 업그레이드해 보는 것이 좋습니다. 이렇게 하면 실제 업그레이드 프로세스 중에 많은 비용이 들지 않고 오랫동안 가동 중지하지 않고 원활하게 업그레이드하는 데 필요한 모든 운영 설명서를 바로잡을 수 있습니다. 고객이 복제 토폴로지를 업그레이드하는 동안 프로덕션 환경에 Always On 가용성 그룹 및/또는 SQL Server 장애 조치 클러스터 인스턴스를 사용하면 가동 중지 시간을 크게 줄일 수 있음을 확인했습니다. 또한 업그레이드를 시도하기 전에 MSDB, 마스터, 배포 데이터베이스 및 복제에 참여하는 사용자 데이터베이스를 포함한 모든 데이터베이스의 백업을 수행하는 것이 좋습니다.


## <a name="replication-matrix"></a>복제 매트릭스

[!INCLUDE[repl matrix](../../includes/replication-compat-matrix.md)]
  
## <a name="run-the-log-reader-agent-for-transactional-replication-before-upgrade"></a>업그레이드 전에 트랜잭션 복제용 로그 판독기 에이전트 실행  
 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]로 업그레이드하기 전에 로그 판독기 에이전트에서 게시된 테이블의 커밋된 모든 트랜잭션을 처리했는지 확인해야 합니다. 모든 트랜잭션이 처리되었는지 확인하려면 트랜잭션 게시를 포함하는 각 데이터베이스에 대해 다음 단계를 수행하십시오.  
  
1.  데이터베이스에서 로그 판독기 에이전트가 실행 중인지 확인합니다. 기본적으로 에이전트는 계속 실행됩니다.    
2.  게시된 테이블에 대한 사용자 동작을 중지합니다.  
3.  로그 판독기 에이전트가 배포 데이터베이스로 트랜잭션을 복사할 때까지 기다린 다음 에이전트를 중지합니다.  
4.  [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 를 실행하여 모든 트랜잭션이 처리되었는지 확인합니다. 이 프로시저의 결과 집합은 비어 있어야 합니다.   
5.  [sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) 를 실행하여 sp_replcmds의 연결을 닫습니다.   
6.  서버를 최신 버전의 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]로 업그레이드합니다.   
7.  업그레이드 후에 자동으로 시작되지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 및 로그 판독기 에이전트를 다시 시작합니다.  
  
## <a name="run-agents-for-merge-replication-after-upgrade"></a>업그레이드 후 병합 복제를 위한 에이전트 실행  
 업그레이드 후에 각 병합 게시에 대해 스냅숏 에이전트를 실행하고 각 구독에 대해 병합 에이전트를 실행하여 복제 메타데이터를 업데이트합니다. 구독을 다시 초기화할 필요가 없으므로 새 스냅숏을 적용하지 않아도 됩니다. 구독 메타데이터는 업그레이드 후에 병합 에이전트가 처음 실행될 때 업데이트됩니다. 즉, 게시자를 업그레이드하는 동안 구독 데이터베이스를 온라인 활성 상태로 유지할 수 있습니다.  
  
 병합 복제는 게시 및 구독 데이터베이스의 많은 시스템 테이블에 게시 및 구독 메타데이터를 저장합니다. 스냅숏 에이전트를 실행하면 게시 메타데이터가 업데이트되고 병합 에이전트를 실행하면 구독 메타데이터가 업데이트됩니다. 따라서 게시 스냅숏을 생성하기만 하면 됩니다. 병합 게시에 매개 변수가 있는 필터가 사용되면 각 파티션은 스냅숏도 갖게 됩니다. 이러한 분할된 스냅숏은 업데이트하지 않아도 됩니다.  
  
 에이전트는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 복제 모니터 또는 명령줄에서 실행합니다. 스냅숏 에이전트를 실행하는 방법은 다음 문서를 참조하세요.  
  
-   [초기 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)
-   [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)
-   [초기 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)
-   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  

병합 에이전트를 실행하는 방법은 다음 문서를 참조하세요.
-   [끌어오기 구독 동기화](../../relational-databases/replication/synchronize-a-pull-subscription.md)
-   [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  

병합 복제를 사용하는 토폴로지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 업그레이드한 후에 새 기능을 사용하려면 모든 게시의 게시 호환성 수준을 변경합니다.  
  
## <a name="upgrading-to-standard-workgroup-or-express-editions"></a>Standard, Workgroup 또는 Express Edition으로 업그레이드  
한 에디션의 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 에서 다른 에디션으로 업그레이드하기 전에 현재 사용 중인 기능이 업그레이드할 에디션에서 지원되는지 확인하십시오. 자세한 내용은 [SQL Server의 버전 및 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)의 복제 섹션을 참조하세요.  

## <a name="steps-to-upgrade-a-replication-topology"></a>복제 토폴로지를 업그레이드하는 단계
다음 단계에서는 복제 토폴로지의 서버를 업그레이드하는 순서를 간략하게 설명합니다. 트랜잭션 복제 또는 병합 복제 중 어느 것을 실행하든 동일한 단계가 적용됩니다. 그러나 이러한 단계는 피어 투 피어 복제, 큐 대기 업데이트 구독 또는 즉시 업데이트 구독에는 적용되지 않습니다. 

### <a name="in-place-upgrade"></a>내부 업그레이드 
1. 배포자를 업그레이드합니다. 
2. 게시자와 구독자를 업그레이드합니다. 순서에 관계없이 업그레이드할 수 있습니다. 

 >[!NOTE]
 > SQL 2008 및 2008 R2의 경우 복제 토폴로지 매트릭스에 맞게 게시자와 구독자를 동시에 업그레이드해야 합니다. SQL 2008/2008R2 게시자 또는 구독자에는 SQL 2016 이상 게시자 또는 구독자가 있을 수 없습니다. 동시에 업그레이드할 수 없는 경우 중간 업그레이드를 사용하여 SQL 인스턴스를 SQL 2014로 업그레이드한 다음, SQL 2016 이상으로 다시 업그레이드합니다.  

### <a name="side-by-side-upgrade"></a>병렬 업그레이드
1. 배포자를 업그레이드합니다.
1. 새 SQL Server 인스턴스에서 [배포](../../relational-databases/replication/configure-distribution.md)를 다시 구성합니다.
1. 게시자를 업그레이드합니다.
1. 구독자를 업그레이드합니다.
1. 구독자의 다시 초기화를 포함하여 모든 게시자-구독자 쌍을 다시 구성합니다. 


## <a name="steps-for-side-by-side-migration-of-the-distributor-to-windows-server-2012-r2"></a>배포자를 Windows Server 2012 R2로 병렬 마이그레이션하는 단계
SQL Server 인스턴스를 SQL 2016 이상으로 업그레이드하려고 하고 현재 OS가 Windows 2008(또는 2008 R2)이면 OS를 Windows Server 2012 R2 이상으로 병렬 업그레이드해야 합니다. 이 중간 OS 업그레이드에 대한 이유는 SQL Server 2016을 Windows Server 2008/2008 R2에 설치할 수 없고, Windows Server 2008/20008 R2에서 장애 조치 클러스터에 대한 현재 위치 업그레이드를 허용하지 않기 때문입니다. 다음 단계는 독립 실행형 SQL 서버 인스턴스 또는 Always On FCI(장애 조치 클러스터 인스턴스) 내에서 수행할 수 있습니다.

1. Windows Server 2012 R2/2016에서 다른 Windows 클러스터 및 SQL Server FCI 이름 또는 독립 실행형 호스트 이름을 사용하여 새 SQL Server 인스턴스(독립 실행형 또는 Always On 장애 조치 클러스터), 에디션 및 버전을 배포자로 설정합니다. 복제 에이전트 실행 파일, 복제 폴더 및 데이터베이스 파일 경로가 새 환경의 동일한 경로에 있도록 이전 배포자와 동일한 디렉터리 구조를 유지해야 합니다. 이렇게 하면 필요한 사후 마이그레이션/업그레이드 단계가 줄어듭니다.
1. 복제가 동기화되었는지 확인한 다음, 모든 복제 에이전트를 종료합니다. 
1. 현재 SQL Server 배포자 인스턴스를 종료합니다. 독립 실행형 인스턴스인 경우 서버를 종료합니다. SQL FCI인 경우 네트워크 이름을 포함하여 클러스터 관리자에서 전체 SQL 서버 역할을 오프라인으로 전환합니다. 
1. 이전(현재 배포자 인스턴스) 환경에 대한 DNS 및 AD 컴퓨터 개체 항목을 제거합니다. 
1. 새 서버의 호스트 이름이 이전 서버의 호스트 이름과 일치하도록 변경합니다.
    1. SQL FCI인 경우 새 SQL FCI의 이름을 이전 인스턴스와 동일한 가상 서버 이름으로 바꿉니다. 
1. SAN 리디렉션, 스토리지 복사본 또는 파일 복사본을 사용하여 이전 인스턴스의 데이터베이스 파일을 복사합니다. 
1. 새 SQL 서버 인스턴스를 온라인으로 전환합니다. 
1. 모든 복제 에이전트를 다시 시작하고, 에이전트가 제대로 실행되는지 확인합니다.
1. 복제가 예상대로 작동하는지 확인합니다. 
1. SQL Server 설치 미디어를 사용하여 SQL Server 인스턴스에서 새 SQL Server 버전으로의 현재 위치 업그레이드를 실행합니다. 


  >[!NOTE]
  > 가동 중지 시간을 줄이려면 배포자의 *병렬 마이그레이션*을 하나의 작업으로 수행하고, *SQL Server 2016으로의 현재 위치 업그레이드*를 다른 하나의 작업으로 수행하는 것이 좋습니다. 이렇게 하면 단계별 방법을 수행하고, 위험을 줄이며, 가동 중지 시간을 최소화할 수 있습니다.

## <a name="web-synchronization-for-merge-replication"></a>병합 복제에 대한 웹 동기화  
 병합 복제에 대한 웹 동기화 옵션을 사용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기(replisapi.dll)를 동기화에 사용되는 인터넷 정보 서비스(IIS) 서버의 가상 디렉터리에 복사해야 합니다. 웹 동기화를 구성할 때는 웹 동기화 구성 마법사를 실행하여 가상 디렉터리에 파일을 복사합니다. IIS 서버에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 업그레이드하는 경우에는 COM 디렉터리의 replisapi.dll을 IIS 서버의 가상 디렉터리에 수동으로 복사해야 합니다. 웹 동기화를 구성하는 방법은 [웹 동기화 구성](../../relational-databases/replication/configure-web-synchronization.md)을 참조하세요.  
  
## <a name="restoring-a-replicated-database-from-an-earlier-version"></a>이전 버전에서 복제된 데이터베이스 복원  
 이전 버전에서 복제된 데이터베이스의 백업을 복원할 때 복제 설정이 유지되게 하려면 백업 당시의 서버 및 데이터베이스와 같은 이름의 서버 및 데이터베이스에 복원합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 복제](../../relational-databases/replication/sql-server-replication.md)  
 [복제 관리 FAQ](../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [복제의 이전 버전과의 호환성](../../relational-databases/replication/replication-backward-compatibility.md)   
 [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)  
 [SQL Server 2016으로 복제 토폴로지 업그레이드](https://blogs.msdn.microsoft.com/sql_server_team/upgrading-a-replication-topology-to-sql-server-2016/)
