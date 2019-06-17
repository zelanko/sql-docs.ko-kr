---
title: 미러된 데이터베이스에 대 한 서비스 팩을 System with Minimal Downtime 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- hotfixes [SQL Server]
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
- service packs [SQL Server]
- upgrading mirrored database systems
- upgrading SQL Server, mirrored databases
ms.assetid: bdc63142-027d-4ead-9d3e-147331387ef5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 821fd05e94ac820dff50bd08c70c75e7e9cc653d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779597"
---
# <a name="install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases"></a>미러된 데이터베이스 작동 중단을 최소화하면서 시스템에 서비스 팩 설치
  이 항목에서는 서비스 팩과 핫픽스를 설치할 때 미러된 데이터베이스의 작동 중단을 최소화하는 방법에 대해 설명합니다. 이 프로세스에는 데이터베이스 미러링에 참여하는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 인스턴스를 순차적으로 업그레이드하는 과정이 포함됩니다. 이러한 형태의 업데이트 라고도 함를 *롤링 업데이트*만 단일 장애 조치를 가동 중지 시간을 줄입니다. Note는 미러 서버는 지리적으로 먼 거리에서에 있는 주 서버는 성능 우선 모드 세션에 대 한 업데이트가 적합 하지 않습니다.  
  
 롤링 업데이트는 다음과 같은 여러 단계로 구성되는 프로세스입니다.  
  
-   데이터를 보호합니다.  
  
-   세션에 미러링 모니터가 포함되어 있는 경우 미러링 모니터를 제거하는 것이 좋습니다. 미러링 모니터를 제거하지 않으면 미러 서버 인스턴스를 업데이트할 때 주 서버 인스턴스에 연결된 채로 남아있는 미러링 모니터에 의해 데이터베이스의 가용성이 결정됩니다. 미러링 모니터를 제거하고 나면 데이터베이스 가동 중단의 위험 없이 롤링 업데이트 프로세스 도중 언제라도 업데이트할 수 있습니다.  
  
    > [!NOTE]  
    >  자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
-   세션이 성능 우선 모드에서 실행되는 경우 운영 모드를 보호 우선 모드로 변경하십시오.  
  
-   데이터베이스 미러링에 관련된 각 서버 인스턴스를 업데이트합니다. 롤링 업데이트는 현재 미러 서버인 서버 인스턴스를 업그레이드하고, 이 서버 인스턴스의 미러된 각 데이터베이스를 수동으로 장애 조치(failover)하고, 처음에 주 서버였으며 현재는 새 미러 서버인 서버 인스턴스를 업그레이드하는 과정으로 진행됩니다. 이때 미러링을 재개해야 합니다.  
  
    > [!NOTE]  
    >  롤링 업데이트를 시작하기 전에 미러링 세션 중 적어도 하나에 대해 수동 장애 조치(failover)를 수행하는 과정을 연습해 보는 것이 좋습니다.  
  
-   필요할 경우 성능 우선 모드로 되돌립니다.  
  
-   필요할 경우 미러링 모니터를 미러링 세션에 다시 추가합니다.  
  
 이러한 각 단계를 수행하는 절차는 다음과 같습니다.  
  
> [!IMPORTANT]  
>  동시 미러링 세션에서는 서버 인스턴스가 다른 역할(주 서버, 미러 서버 또는 미러링 모니터)을 수행할 수 있습니다. 이 경우 기본 롤링 업데이트 프로세스를 적절히 조정해야 합니다.  
  
### <a name="to-protect-your-data-before-an-update-a-best-practice"></a>업데이트 전에 데이터를 보호하려면(최상의 방법)  
  
1.  모든 주 데이터베이스에 대해 전체 데이터베이스 백업을 수행합니다.  
  
     **데이터베이스를 백업하려면**  
  
    -   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
2.  모든 주 데이터베이스에서 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 명령을 실행합니다.  
  
### <a name="to-remove-a-witness-from-a-session"></a>세션에서 미러링 모니터를 제거하려면  
  
1.  미러링 세션에 미러링 모니터 서버가 있을 경우 롤링 업데이트를 수행하기 전에 미러링 모니터 서버를 제거하는 것이 좋습니다.  
  
     **미러링 모니터를 제거하려면**  
  
    -   [데이터베이스 미러링 세션에서 미러링 모니터 서버 제거&#40;SQL Server&#41;](database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>세션을 성능 우선 모드에서 보호 우선 모드로 변경하려면  
  
1.  미러링 세션이 성능 우선 모드에서 실행되고 있을 경우 롤링 업데이트를 수행하기 전에 자동 장애 조치(Failover)가 없는 보호 우선 모드로 운영 모드를 변경하십시오. 다음 방법 중 하나를 사용합니다.  
  
    -   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 경우: **데이터베이스 속성** 대화 상자의 [미러링 페이지](../relational-databases/databases/database-properties-mirroring-page.md)를 사용하여 **운영 모드** 옵션을 **자동 장애 조치(Failover) 없는 보호 우선(동기)** 으로 변경합니다. 이 페이지에 액세스하는 방법은 [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)을 참조하세요.  
  
    -   [!INCLUDE[tsql](../includes/tsql-md.md)]의 경우: 트랜잭션 보안을 FULL로 설정합니다. 자세한 내용은 [데이터베이스 미러링 세션에서 트랜잭션 보안 변경&#40;Transact-SQL&#41;](database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)을 참조하세요.  
  
### <a name="to-perform-the-rolling-update"></a>롤링 업데이트를 수행하려면  
  
1.  가동 중단을 최소화하려면 다음 방법을 사용하는 것이 좋습니다. 모든 미러링 세션에는 현재 미러 서버인 모든 미러링 파트너를 업데이트 하 여 롤링 업데이트를 시작 합니다. 이때 여러 서버 인스턴스를 업데이트해야 할 수도 있습니다.  
  
    > [!NOTE]  
    >  미러링 모니터는 롤링 업데이트 프로세스 도중 언제라도 업데이트할 수 있습니다. 예를 들어 서버 인스턴스가 Session 1의 미러 서버이고 미러링 모니터가 Session 2에 있을 경우 지금 서버 인스턴스를 업데이트할 수 있습니다.  
  
     처음 업데이트할 서버 인스턴스는 다음과 같이 미러링 세션의 현재 구성에 따라 달라집니다.  
  
    -   서버 인스턴스가 자체 모든 미러링 세션의 미러 서버인 경우 서버 인스턴스에 서비스 팩이나 핫픽스를 설치합니다.  
  
    -   현재 모든 서버 인스턴스가 미러링 세션의 주 서버일 경우 처음 업데이트할 서버 인스턴스 하나를 선택합니다. 그런 다음 서비스 팩이나 핫픽스를 설치하여 각각의 주 데이터베이스를 수동으로 장애 조치(failover)하고 서버 인스턴스를 업데이트합니다.  
  
     업데이트가 끝나면 서버 인스턴스는 자동으로 자체 미러링 세션에 다시 참여합니다.  
  
     **수동 장애 조치(failover)를 수행하려면**  
  
    -   [데이터베이스 미러링 세션 수동 장애 조치(failover)&#40;SQL Server Management Studio&#41;](database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [데이터베이스 미러링 세션 수동 장애 조치(failover)&#40;Transact-SQL&#41;](database-mirroring/manually-fail-over-a-database-mirroring-session-transact-sql.md).  
  
     수동 장애 조치(failover)의 작동 방식에 대한 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)을 참조하세요.  
  
2.  미러 서버 인스턴스가 업데이트된 각 미러링 세션이 동기화될 때까지 대기합니다. 그런 다음 주 서버 인스턴스에 연결하여 세션을 수동으로 장애 조치(Failover)합니다. 장애 조치(Failover)를 수행하면 업데이트된 서버 인스턴스는 해당 세션의 주 서버가 되고 이전 주 서버는 미러 서버가 됩니다.  
  
     이 단계의 목적은 업그레이드된 서버 인스턴스가 파트너로 참여하는 모든 미러링 세션에서 다른 서버 인스턴스를 미러 서버로 만드는 것입니다.  
  
3.  장애 조치(failover)를 수행한 후에는 주 데이터베이스에서 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 명령을 실행하는 것이 좋습니다.  
  
4.  파트너로 참여하는 모든 미러링 세션에서 이제 미러 서버가 된 각 서버 인스턴스에 서비스 팩이나 핫픽스를 설치합니다. 이때 여러 서버를 업데이트해야 할 수도 있습니다.  
  
    > [!IMPORTANT]  
    >  미러링 구성이 복잡할 경우 일부 서버 인스턴스가 하나 이상의 미러링 세션에서 원래의 주 서버로 남아 있을 수 있습니다. 관련 된 모든 인스턴스에 업데이트 될 때까지 이러한 서버 인스턴스에 대해 2-4 단계를 반복 합니다.  
  
5.  미러링 세션을 재개합니다.  
  
    > [!NOTE]  
    >  미러링 모니터가 업데이트되기 전까지 자동 장애 조치(failover)는 작동하지 않습니다.  
  
6.  모든 미러링 세션에서 미러링 모니터가 된 나머지 서버 인스턴스에 서비스 팩이나 핫픽스를 설치합니다. 업데이트된 미러링 모니터가 미러링 세션에 다시 참여한 후에는 자동 장애 조치(Failover)가 다시 가능해집니다. 이때 여러 서버를 업데이트해야 할 수도 있습니다.  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>세션을 성능 우선 모드로 되돌리려면  
  
1.  선택적으로, 다음 중 한 가지 방법을 사용하여 성능 우선 모드로 되돌릴 수 있습니다.  
  
    -   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 경우: **데이터베이스 속성** 대화 상자의 **미러링 페이지**를 사용하여 [운영 모드](../relational-databases/databases/database-properties-mirroring-page.md) 옵션을 **성능 우선(동기)** 으로 변경합니다.  
  
    -   [!INCLUDE[tsql](../includes/tsql-md.md)]의 경우: 사용 하 여 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) 트랜잭션 보안을 OFF로 설정 합니다.  
  
### <a name="to-return-a-witness-to-a-mirroring-session"></a>미러링 모니터를 미러링 세션에 다시 추가하려면  
  
1.  보호 우선 모드의 경우 선택적으로 미러링 모니터를 각 미러링 세션에 다시 연결합니다.  
  
     **미러링 모니터 서버를 다시 설정 하려면**  
  
    -   [데이터베이스 미러링 모니터 서버 추가 또는 바꾸기&#40;SQL Server Management Studio&#41;](database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가&#40;Transact-SQL&#41;](database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE 데이터베이스 미러링&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [데이터베이스 미러링&#40;SQL Server&#41;](database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 운영 모드](database-mirroring/database-mirroring-operating-modes.md)   
 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [미러된 데이터베이스의 상태 보기&#40;SQL Server Management Studio&#41;](database-mirroring/view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
  
