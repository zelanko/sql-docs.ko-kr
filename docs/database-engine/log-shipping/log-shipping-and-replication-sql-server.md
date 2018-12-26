---
title: 로그 전달 및 복제(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], log shipping and
- log shipping [SQL Server], replication and
ms.assetid: 132bebfd-0206-4d23-829a-b38e5ed17bc9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9970c01b1af46287c9438b2b731af6a1c9e1f44
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655951"
---
# <a name="log-shipping-and-replication-sql-server"></a>로그 전달 및 복제(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  로그 전달에는 일반적으로 서로 다른 컴퓨터에 있는 두 개의 단일 데이터베이스 복사본이 사용됩니다. 클라이언트는 항상 하나의 데이터베이스 복사본만 사용할 수 있습니다. 이 복사본을 주 데이터베이스라고 합니다. 클라이언트가 주 데이터베이스에 업데이트한 내용은 로그 전달을 사용하여 보조 데이터베이스라고 부르는 다른 데이터베이스 복사본에 전달됩니다. 로그 전달에는 주 데이터베이스에 대해 수행된 모든 삽입, 업데이트 또는 삭제 작업의 트랜잭션 로그를 보조 데이터베이스에 적용하는 작업이 포함됩니다.  
  
 로그 전달은 다음과 같은 동작의 경우 복제와 함께 사용될 수 있습니다.  
  
-   로그 전달 장애 조치(Failover) 이후에는 복제가 계속되지 않습니다. 장애 조치가 발생하면 복제 에이전트가 보조 데이터베이스에 연결하지 않기 때문에 트랜잭션이 구독자에 복제되지 않습니다. 주 서버에 대한 장애 복구(Failback)가 발생하면 복제가 다시 시작됩니다. 로그 전달이 보조 서버에서 주 서버로 복사하는 모든 트랜잭션이 구독자에 복제됩니다.  
  
-   주 서버가 영구적으로 손실되면 보조 서버 이름을 바꿔서 복제를 계속할 수 있습니다. 이 항목의 남은 부분에서는 이러한 경우를 처리하기 위한 요구 사항과 절차에 대해 설명합니다. 제공된 예는 로그 전달에서 가장 일반적인 게시 데이터베이스이지만 구독 및 배포 데이터베이스에 더 간단한 프로세스를 적용할 수도 있습니다.  
  
 복제를 다시 구성할 필요 없이 복제에 관련된 데이터베이스를 복구하는 방법은 [복제된 데이터베이스 백업 및 복원](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)을 참조하세요.  
  
> [!NOTE]  
>  게시 데이터베이스의 가용성을 높이기 위해서는 로그 전달 대신 데이터베이스 미러링을 사용하는 것이 좋습니다. 자세한 내용은 [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)을 참조하세요.  
  
## <a name="requirements-and-procedures-for-replicating-from-the-secondary-if-the-primary-is-lost"></a>주 서버가 손실된 경우 보조 서버로부터 복제하기 위한 요구 사항 및 절차  
 다음 요구 사항과 고려 사항에 주의하십시오.  
  
-   주 서버에 하나 이상의 게시 데이터베이스가 포함된 경우 모든 게시 데이터베이스의 로그를 동일한 보조 서버로 전달합니다.  
  
-   보조 서버 인스턴스의 설치 경로는 주 서버와 동일해야 합니다. 보조 서버의 사용자 데이터베이스 위치는 주 서버와 동일해야 합니다.  
  
-   주 서버에서 서비스 마스터 키를 백업합니다. 이 키는 보조 서버에서 복원됩니다. 자세한 내용은 [BACKUP SERVICE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)를 참조하세요.  
  
-   로그 전달은 데이터 손실 방지를 보장하지 않습니다. 보조 데이터베이스에 오류가 발생하면 아직 백업되지 않은 데이터가 손실되거나 오류 중에 손실된 백업의 데이터가 손실될 수 있습니다.  
  
### <a name="log-shipping-with-transactional-replication"></a>트랜잭션 복제의 로그 전달  
 트랜잭션 복제의 경우 로그 전달의 동작은 **sync with backup** 옵션에 따라 달라집니다. 이 옵션은 게시 데이터베이스 및 배포 데이터베이스에 설정될 수 있으며, 게시자의 로드 전달의 경우에는 게시 데이터베이스의 설정만 관련이 있습니다.  
  
 게시 데이터베이스에 이 옵션을 설정하면 트랜잭션은 게시 데이터베이스에서 백업될 때까지 배포 데이터베이스로 배달되지 않습니다. 그러면 복원된 게시 데이터베이스에 없는 트랜잭션이 배포 데이터베이스에 있을 수 없으므로 보조 서버에서 마지막 게시 데이터베이스 백업을 복원할 수 있습니다. 이 옵션은 게시자가 보조 서버로 장애 조치되는 경우 게시자, 배포자 및 구독자 간의 일관성이 유지되도록 보장합니다. 트랜잭션이 게시자에서 백업되기 전까지는 배포 데이터베이스로 트랜잭션을 전달할 수 없으므로 지연이 발생하거나 처리량이 줄어들 수 있습니다. 애플리케이션에서 이러한 지연이 허용되는 경우 게시 데이터베이스에 이 옵션을 설정하는 것이 좋습니다. **sync with backup** 옵션을 설정하지 않으면 보조 서버에서 복구된 데이터베이스에는 포함되지 않는 변경 내용을 구독자가 받을 수 있습니다. 자세한 내용은 [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)을(를) 참조하세요.  
  
 **sync with backup 옵션으로 트랜잭션 게시 및 로그 전달을 구성하려면**  
  
1.  게시 데이터베이스에 sync with backup 옵션이 설정되어 있지 않으면 `sp_replicationdboption '<publicationdatabasename>', 'sync with backup', 'true'`를 실행합니다. 자세한 내용은 [sp_replicationdboption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)을 참조하세요.  
  
2.  게시 데이터베이스에 대한 로그 전달을 구성합니다. 자세한 내용은 [로그 전달 구성&#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)을 참조하세요.  
  
3.  게시자에서 오류가 발생하면 RESTORE LOG의 KEEP_REPLICATION 옵션을 사용하여 데이터베이스의 마지막 로그를 보조 서버로 복원합니다. 이렇게 하면 데이터베이스에 대한 모든 복제 설정이 유지됩니다. 자세한 내용은 [로그 전달 보조 데이터베이스로 장애 조치(Failover)&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md) 및 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)를 참조하세요.  
  
4.  주 서버에서 보조 서버로 **msdb** 데이터베이스와 **master** 데이터베이스를 복원합니다. 자세한 내용은 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)를 참조하세요. 주 서버가 배포자이기도 한 경우 배포 데이터베이스를 주 서버에서 보조 서버로 복원합니다.  
  
     이러한 데이터베이스의 복제 구성 및 설정은 주 서버의 게시 데이터베이스와 일치해야 합니다.  
  
5.  보조 서버에서 컴퓨터의 이름을 바꾼 후 주 서버 이름과 일치하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 바꿉니다. 컴퓨터의 이름을 바꾸는 방법은 Windows 설명서를 참조하십시오. 서버 이름을 바꾸는 방법은 [SQL Server의 독립 실행형 인스턴스를 호스팅하는 컴퓨터 이름 바꾸기](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) 및 [SQL Server 장애 조치(Failover) 클러스터 인스턴스 이름 변경](../../sql-server/failover-clusters/install/rename-a-sql-server-failover-cluster-instance.md)을 참조하세요.  
  
6.  보조 서버에서 주 서버로부터 백업한 서비스 마스터 키를 복원합니다. 자세한 내용은 [RESTORE SERVICE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)를 참조하세요.  
  
 **sync with backup 옵션을 사용하지 않고 트랜잭션 게시 및 로그 전달을 구성하려면**  
  
1.  게시 데이터베이스에 대한 로그 전달을 구성합니다. 자세한 내용은 [로그 전달 구성&#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)을 참조하세요.  
  
2.  게시자에서 오류가 발생하면 RESTORE LOG의 KEEP_REPLICATION 옵션을 사용하여 데이터베이스의 마지막 로그를 보조 서버로 복원합니다. 이렇게 하면 데이터베이스에 대한 모든 복제 설정이 유지됩니다. 자세한 내용은 [로그 전달 보조 데이터베이스로 장애 조치(Failover)&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md) 및 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)를 참조하세요.  
  
3.  주 서버에서 보조 서버로 **msdb** 데이터베이스와 **master** 데이터베이스를 복원합니다. 자세한 내용은 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)를 참조하세요. 주 서버가 배포자이기도 한 경우 배포 데이터베이스를 주 서버에서 보조 서버로 복원합니다.  
  
     이러한 데이터베이스의 복제 구성 및 설정은 주 서버의 게시 데이터베이스와 일치해야 합니다.  
  
4.  보조 서버에서 컴퓨터의 이름을 바꾼 후 주 서버 이름과 일치하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 바꿉니다. 컴퓨터의 이름을 바꾸는 방법은 Windows 설명서를 참조하십시오. 서버 이름을 바꾸는 방법은 [SQL Server의 독립 실행형 인스턴스를 호스팅하는 컴퓨터 이름 바꾸기](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) 및 [SQL Server 장애 조치(Failover) 클러스터 인스턴스 이름 변경](../../sql-server/failover-clusters/install/rename-a-sql-server-failover-cluster-instance.md)을 참조하세요.  
  
     게시 데이터베이스 및 배포 데이터베이스가 동기화되지 않았다는 오류 메시지가 로그 판독기 에이전트에서 발생할 수 있습니다.  
  
5.  보조 서버에서 주 서버로부터 백업한 서비스 마스터 키를 복원합니다. 자세한 내용은 [RESTORE SERVICE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)를 참조하세요.  
  
6.  **sp_replrestart**를 실행합니다. 이 저장 프로시저를 사용하면 로그 판독기 에이전트가 게시 데이터베이스 로그에서 이전에 복제된 모든 트랜잭션을 강제로 무시하도록 할 수 있습니다. 저장 프로시저가 완료된 후에 적용된 트랜잭션은 로그 판독기 에이전트에 의해 처리됩니다. 자세한 내용은 [sp_replrestart&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md)를 참조하세요.  
  
7.  저장 프로시저가 성공적으로 실행된 후에 로그 판독기 에이전트를 다시 시작합니다. 자세한 내용은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)를 참조하세요.  
  
8.  구독자에 이미 배포된 트랜잭션은 게시자에 적용될 수 있습니다. 배포 에이전트에서 이러한 트랜잭션을 구독자에서 다시 적용할 때 오류가 발생하지 않도록 하려면 **데이터 일관성 오류가 발생했지만 계속됩니다**라는 에이전트 프로필을 지정합니다.  
  
### <a name="log-shipping-with-merge-replication"></a>병합 복제의 로그 전달  
 병합 복제와 로그 전달을 구성하려면 아래 절차의 단계를 따르십시오.  
  
 **병합 복제 및 로그 전달을 구성하려면**  
  
1.  게시 데이터베이스에 대한 로그 전달을 구성합니다. 자세한 내용은 [로그 전달 구성&#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)에서 도입되었습니다.  
  
2.  게시자가 실패하면 보조 서버에서 컴퓨터의 이름을 바꾼 후 주 서버 이름과 일치하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 바꿉니다. 컴퓨터의 이름을 바꾸는 방법은 Windows 설명서를 참조하십시오. 서버 이름을 바꾸는 방법은 [SQL Server의 독립 실행형 인스턴스를 호스팅하는 컴퓨터 이름 바꾸기](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) 및 [SQL Server 장애 조치(Failover) 클러스터 인스턴스 이름 변경](../../sql-server/failover-clusters/install/rename-a-sql-server-failover-cluster-instance.md)을 참조하세요.  
  
3.  RESTORE LOG의 KEEP_REPLICATION 옵션을 사용하여 데이터베이스의 마지막 로그를 보조 서버로 복원합니다. 이렇게 하면 데이터베이스에 대한 모든 복제 설정이 유지됩니다. 자세한 내용은 [로그 전달 보조 데이터베이스로 장애 조치(Failover)&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md) 및 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)를 참조하세요.  
  
4.  주 서버에서 보조 서버로 **msdb** 데이터베이스와 **master** 데이터베이스를 복원합니다. 자세한 내용은 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)를 참조하세요. 주 서버가 배포자이기도 한 경우 배포 데이터베이스를 주 서버에서 보조 서버로 복원합니다.  
  
     이러한 데이터베이스의 복제 구성 및 설정은 주 서버의 게시 데이터베이스와 일치해야 합니다.  
  
5.  보조 서버에서 주 서버로부터 백업한 서비스 마스터 키를 복원합니다. 자세한 내용은 [RESTORE SERVICE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)를 참조하세요.  
  
6.  하나 이상의 구독 데이터베이스와 게시 데이터베이스를 동기화합니다. 이렇게 하면 이전 게시 데이터베이스에서 변경되었지만 복원된 백업에 표시되지 않은 변경 내용을 업로드할 수 있습니다. 업로드할 수 있는 데이터는 게시가 필터링되는 방식에 따라 달라집니다.  
  
    -   게시가 필터링되지 않은 경우 최신 구독자와 동기화하여 게시 데이터베이스를 최신 상태로 만들 수 있습니다.  
  
    -   게시가 필터링된 경우 게시 데이터베이스를 최신 상태로 만들 수 없을 수도 있습니다. 각 구독이 동부, 서부, 남부 및 북부 중 한 지역에 대한 고객 데이터만 수신하도록 분할된 테이블을 고려해 봅시다. 각 데이터 파티션에 대해 최소 하나의 구독자가 있는 경우 각 파티션에 대해 구독자와 동기화하면 게시 데이터베이스가 최신 상태가 됩니다. 그러나 예를 들어 서부 파티션의 데이터가 구독자에 복제되지 않은 경우에는 게시자에서 이 데이터를 최신 상태로 만들 수 없습니다. 이 경우에는 게시자 및 구독자의 데이터가 일치하도록 모든 구독을 다시 초기화하는 것이 좋습니다. 자세한 내용은 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]를 실행하는 구독자와 동기화할 경우에 해당 구독은 익명일 수 없습니다. 구독은 클라이언트 구독 또는 서버 구독(이전 버전에서는 로컬 구독 및 전역 구독)이어야 합니다. 자세한 내용은 [데이터 동기화](../../relational-databases/replication/synchronize-data.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [복제 기능 및 태스크](../../relational-databases/replication/replication-features-and-tasks.md)   
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
  
