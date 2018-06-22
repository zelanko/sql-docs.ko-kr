---
title: 서버 인스턴스 업그레이드 시 미러된 데이터베이스에 대 한 작동 중단을 최소화 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- upgrading SQL Server, rolling upgrade of mirrored databases
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
ms.assetid: 0e73bd23-497d-42f1-9e81-8d5314bcd597
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fc5bea207d824c860d197ca75eff788f6794ecc0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079625"
---
# <a name="minimize-downtime-for-mirrored-databases-when-upgrading-server-instances"></a>서버 인스턴스 업그레이드 시 미러된 데이터베이스의 작동 중단 최소화
  서버 인스턴스를 업그레이드 하는 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]는 순차적 업그레이드를 수행 하 여 단일 수동 장애 조치만에 미러된 각 데이터베이스에 대 한 가동 중지 시간을 줄일 수 있습니다 라고는 *롤링 업그레이드*합니다. 롤링 업그레이드란 간단히 말해서 현재 미러링 세션에서 미러 서버 역할을 하고 있는 서버 인스턴스를 업그레이드한 다음 미러된 데이터베이스를 수동으로 장애 조치(Failover)하고, 이전 주 서버를 업그레이드하고, 미러링을 다시 시작하는 여러 단계로 이루어진 프로세스입니다. 실제로 정확한 프로세스는 업그레이드 중인 서버 인스턴스에서 실행되는 미러링 세션의 개수 및 레이아웃과 운영 모드에 따라 달라집니다.  
  
> [!NOTE]  
>  서비스 팩 이나 핫픽스를 설치 하려면 롤링 업그레이드를 수행 하는 방법에 대 한 정보를 참조 하십시오. [System with Minimal Downtime에 미러된 데이터베이스에 대 한 서비스 팩을 설치할](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md)합니다.  
  
 **권장된 준비 (모범 사례)**  
  
 롤링 업그레이드를 시작하기 전에 다음과 같이 하는 것이 좋습니다.  
  
1.  미러링 세션 중 하나 이상에서 수동 장애 조치(Failover)를 연습해 봅니다.  
  
    -   [데이터베이스 미러링 세션 수동 장애 조치(failover)&#40;SQL Server Management Studio&#41;](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [데이터베이스 미러링 세션 수동 장애 조치(failover)&#40;Transact-SQL&#41;](manually-fail-over-a-database-mirroring-session-transact-sql.md).  
  
    > [!NOTE]  
    >  수동 장애 조치(failover)의 작동 방식에 대한 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)을 참조하세요.  
  
2.  데이터를 보호합니다.  
  
    1.  모든 주 데이터베이스에 대해 전체 데이터베이스 백업을 수행합니다.  
  
         [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
    2.  모든 주 데이터베이스에서 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 명령을 실행합니다.  
  
 **롤링 업그레이드 단계**  
  
 세부적인 롤링 업그레이드 단계는 미러링 구성의 운영 모드에 따라 다릅니다. 그러나 기본 단계는 동일합니다.  
  
> [!NOTE]  
>  운영 모드에 대한 자세한 내용은 [데이터베이스 미러링 운영 모드](database-mirroring-operating-modes.md)를 참조하세요.  
  
 다음 그림은 각 운영 모드별로 롤링 업그레이드의 기본 단계를 보여 주는 순서도입니다. 단계별 절차는 이 그림 다음에 설명되어 있습니다.  
  
 ![롤링 업그레이드 단계를 보여 주는 순서도](../media/dbm-rolling-upgrade.gif "롤링 업그레이드 단계를 보여 주는 순서도")  
  
> [!IMPORTANT]  
>  동시 미러링 세션에서는 서버 인스턴스가 다른 역할(주 서버, 미러 서버 또는 미러링 모니터)을 수행할 수 있습니다. 이 경우 기본 롤링 업그레이드 프로세스를 적절히 조정해야 합니다. 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)에서만 사용할 수 있습니다.  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>세션을 성능 우선 모드에서 보호 우선 모드로 변경하려면  
  
1.  미러링 세션이 보호 우선 모드에서 실행되고 있을 경우 롤링 업그레이드를 수행하기 전에 자동 장애 조치가 없는 보호 우선 모드로 운영 모드를 변경하십시오.  
  
    > [!IMPORTANT]  
    >  미러 서버가 주 서버와 지리적으로 먼 거리에 있는 경우에는 롤링 업그레이드가 적합하지 않을 수 있습니다.  
  
    -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 경우: **데이터베이스 속성** 대화 상자의 [미러링 페이지](../../relational-databases/databases/database-properties-mirroring-page.md)를 사용하여 **운영 모드** 옵션을 **자동 장애 조치(Failover) 없는 보호 우선(동기)** 으로 변경합니다. 이 페이지에 액세스하는 방법은 [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)을 참조하세요.  
  
    -   [!INCLUDE[tsql](../../includes/tsql-md.md)]의 경우: 트랜잭션 보안을 FULL로 설정합니다. 자세한 내용은 [데이터베이스 미러링 세션에서 트랜잭션 보안 변경&#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)을 참조하세요.  
  
### <a name="to-remove-a-witness-from-a-session"></a>세션에서 미러링 모니터를 제거하려면  
  
1.  미러링 세션에 미러링 모니터가 있을 경우 롤링 업그레이드를 수행하기 전에 미러링 모니터를 제거하는 것이 좋습니다. 미러링 모니터를 제거하지 않으면 미러 서버 인스턴스를 업그레이드할 때 주 서버 인스턴스에 연결된 채로 남아있는 미러링 모니터에 의해 데이터베이스의 가용성이 결정됩니다. 미러링 모니터를 제거하고 나면 데이터베이스 가동 중단의 위험 없이 롤링 업그레이드 프로세스 도중 언제라도 업그레이드할 수 있습니다.  
  
    > [!NOTE]  
    >  자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
    -   [데이터베이스 미러링 세션에서 미러링 모니터 서버 제거&#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-perform-the-rolling-upgrade"></a>롤링 업그레이드를 수행하려면  
  
1.  작동 중단을 최소화하려면 롤링 업그레이드를 시작할 때 모든 자체 미러링 세션 내에서 현재 미러 서버인 모든 미러링 파트너를 업데이트하는 것이 좋습니다. 이때 여러 서버 인스턴스를 업데이트해야 할 수도 있습니다.  
  
    > [!NOTE]  
    >  미러링 모니터는 롤링 업그레이드 프로세스 도중 언제라도 업그레이드할 수 있습니다. 예를 들어 서버 인스턴스가 Session 1의 미러 서버이고 미러링 모니터가 Session 2에 있을 경우 지금 서버 인스턴스를 업그레이드할 수 있습니다.  
  
     처음 업그레이드할 서버 인스턴스는 다음과 같이 미러링 세션의 현재 구성에 따라 달라집니다.  
  
    -   서버 인스턴스가 자체 미러링 세션의 미러 서버인 경우 서버 인스턴스를 새 버전으로 업그레이드합니다.  
  
    -   현재 모든 서버 인스턴스가 미러링 세션의 주 서버일 경우 처음 업그레이드할 서버 인스턴스 하나를 선택합니다. 그런 다음 각각의 주 데이터베이스를 수동으로 장애 조치(Failover)하고 서버 인스턴스를 업그레이드합니다.  
  
     업그레이드가 끝나면 서버 인스턴스는 자동으로 자체 미러링 세션에 다시 참여합니다.  
  
2.  미러 서버 인스턴스가 업그레이드된 각 미러링 세션이 동기화될 때까지 대기합니다. 그런 다음 주 서버 인스턴스에 연결하여 세션을 수동으로 장애 조치(Failover)합니다. 장애 조치(Failover)를 수행하면 업그레이드된 서버 인스턴스는 해당 세션의 주 서버가 되고 이전 주 서버는 미러 서버가 됩니다.  
  
     이 단계의 목적은 업그레이드된 서버 인스턴스가 파트너로 참여하는 모든 미러링 세션에서 다른 서버 인스턴스를 미러 서버로 만드는 것입니다.  
  
     **업그레이드된 서버 인스턴스를 장애 조치(Failover)한 후의 제한 사항**  
  
     이전 서버 인스턴스에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 서버 인스턴스로 장애 조치(Failover)한 후에는 데이터베이스 세션이 일시 중지되며 다른 파트너가 업그레이드되기 전에는 재개할 수 없습니다. 그러나 주 서버에는 계속 연결할 수 있으며 주 서버에 있는 데이터에 액세스하고 수정하는 것도 가능합니다.  
  
    > [!NOTE]  
    >  새 미러링 세션을 시작하려면 모든 서버 인스턴스가 같은 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행해야 합니다.  
  
3.  장애 조치 후 실행 하는 것이 좋습니다는 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) theprincipal 데이터베이스에서 명령을 합니다.  
  
4.  파트너로 참여하는 모든 미러링 세션에서 이제 미러 서버가 된 각 서버 인스턴스를 업그레이드합니다. 이때 여러 서버를 업데이트해야 할 수도 있습니다.  
  
    > [!IMPORTANT]  
    >  미러링 구성이 복잡할 경우 일부 서버 인스턴스가 하나 이상의 미러링 세션에서 원래의 주 서버로 남아 있을 수 있습니다. 이러한 서버 인스턴스에 대해 2-4단계를 반복하여 관련된 모든 인스턴스를 업그레이드하십시오.  
  
5.  미러링 세션을 재개합니다.  
  
    > [!NOTE]  
    >  자동 장애 조치(Failover)는 미러링 모니터가 업그레이드되고 미러링 세션에 다시 추가되기 전까지 작동하지 않습니다.  
  
6.  모든 미러링 세션에서 미러링 모니터로 남아 있는 나머지 서버 인스턴스를 업그레이드합니다. 업그레이드된 미러링 모니터가 미러링 세션에 다시 참여한 후에는 자동 장애 조치(Failover)가 다시 가능해집니다. 이때 여러 서버를 업데이트해야 할 수도 있습니다.  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>세션을 성능 우선 모드로 되돌리려면  
  
1.  선택적으로, 다음 중 한 가지 방법을 사용하여 성능 우선 모드로 되돌릴 수 있습니다.  
  
    -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 경우: **데이터베이스 속성** 대화 상자의 **미러링 페이지** 를 사용하여 [운영 모드](../../relational-databases/databases/database-properties-mirroring-page.md) 옵션을 **성능 우선(동기)** 으로 변경합니다.  
  
    -   [!INCLUDE[tsql](../../includes/tsql-md.md)]의 경우: [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)를 사용하여 트랜잭션 보안을 OFF로 설정합니다.  
  
### <a name="to-add-a-witness-back-into-a-mirroring-session"></a>미러링 모니터를 미러링 세션에 다시 추가하려면  
  
1.  보호 우선 모드의 경우 선택적으로 미러링 모니터를 각 미러링 세션에 다시 연결합니다.  
  
     **미러링 모니터를 추가하려면**  
  
    -   [데이터베이스 미러링 모니터 서버 추가 또는 바꾸기&#40;SQL Server Management Studio&#41;](add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가&#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE 데이터베이스 미러링&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [미러된 데이터베이스 상태 보기&#40;SQL Server Management Studio&#41;](view-the-state-of-a-mirrored-database-sql-server-management-studio.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [미러된 데이터베이스에 대 한 on a System with Minimal Downtime 서비스 팩 설치](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md)   
 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [데이터베이스 미러링 세션에 서비스 강제 수행&#40;Transact-SQL&#41;](force-service-in-a-database-mirroring-session-transact-sql.md)   
 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](start-database-mirroring-monitor-sql-server-management-studio.md)   
 [데이터베이스 미러링 운영 모드](database-mirroring-operating-modes.md)  
  
  
