---
title: SQL Server 2014으로 로그 전달 업그레이드 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], upgrading
ms.assetid: b1289cc3-f5be-40bb-8801-0e3eed40336e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 80330d03853c984cfd26100b02918eb218705085
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84931144"
---
# <a name="upgrade-log-shipping-to-sql-server-2014-transact-sql"></a>SQL Server 2014로 로그 전달 업그레이드(Transact-SQL)
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드할 때 로그 전달 구성을 유지할 수 있습니다. 이 항목에서는 로그 전달 구성을 업그레이드하기 위한 다양한 시나리오와 최선의 구현 방법에 대해 설명합니다.

> [!NOTE]
>  [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)은 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]에서 도입되었습니다. 업그레이드된 로그 전달 구성은 **백업 압축 기본값** 서버 수준 구성 옵션을 사용하여 백업 압축을 트랜잭션 로그 백업 파일에 사용할지 여부를 제어합니다. 로그 백업에 대한 백업 압축 동작은 각 로그 전달 구성에 지정할 수 있습니다. 자세한 내용은 [로그 전달 구성&#40;SQL Server&#41;](configure-log-shipping-sql-server.md)에서 도입되었습니다.


##  <a name="protect-your-data-before-the-upgrade"></a><a name="ProtectData"></a> 업그레이드하기 전에 데이터 보호
 가능하면 로그 전달 업그레이드 전에 데이터를 보호하는 것이 좋습니다.

 **데이터를 보호하려면**

1.  모든 주 데이터베이스에 대해 전체 데이터베이스 백업을 수행합니다.

     자세한 내용은 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)에서 차등 데이터베이스 백업을 만듭니다.

2.  모든 주 데이터베이스에서 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 명령을 실행합니다.

##  <a name="upgrading-the-monitor-server-instance"></a><a name="UpgradeMonitor"></a>모니터 서버 인스턴스 업그레이드
 모니터 서버 인스턴스(있는 경우)는 언제든지 업그레이드할 수 있습니다.

 모니터 서버가 업그레이드되는 동안 로그 전달 구성은 계속 작동하지만 해당 상태는 모니터 테이블에 기록되지 않습니다. 따라서 모니터 서버가 업그레이드되는 동안에는 구성된 경고가 트리거되지 않습니다. 업그레이드 후에는 [sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql) 시스템 저장 프로시저를 실행하여 모니터 테이블의 정보를 업데이트할 수 있습니다.

##  <a name="upgrading-log-shipping-configurations-with-a-single-secondary-server"></a><a name="UpgradeSingleSecondary"></a>단일 보조 서버를 사용 하 여 로그 전달 구성 업그레이드
 이 섹션에서 설명하는 업그레이드 프로세스는 구성이 주 서버와 하나의 보조 서버로 구성되었다고 가정합니다. 다음 그림에서는 주 서버 인스턴스 A와 단일 보조 서버 인스턴스 B로 구성된 이러한 구성을 보여 줍니다.

 ![보조 서버 1대, 모니터 서버 없음](../media/ls-2-wayconfig-nomonitor.gif "보조 서버 1대, 모니터 서버 없음")

 여러 보조 서버를 업그레이드하는 방법은 이 항목의 뒷부분에 나오는 [여러 보조 서버 인스턴스 업그레이드](#MultipleSecondaries)를 참조하세요.
 

###  <a name="upgrading-the-secondary-server-instance"></a><a name="UpgradeSecondary"></a>보조 서버 인스턴스 업그레이드
 업그레이드 프로세스에는 주 서버 인스턴스를 업그레이드하기 전에 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상의 로그 전달 구성의 보조 서버 인스턴스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 로 업그레이드하는 과정이 포함됩니다. 업그레이드할 때는 항상 보조 서버 인스턴스를 먼저 업그레이드해야 합니다. 주 서버를 보조 서버보다 먼저 업그레이드하면 새 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 만든 백업을 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복원할 수 없기 때문에 로그 전달이 실패합니다.

 업그레이드된 보조 서버가 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상의 주 서버에서 로그 백업을 계속 복원하기 때문에 전체 업그레이드 프로세스 동안 로그 전달은 계속됩니다. 보조 서버 인스턴스를 업그레이드하는 프로세스는 부분적으로 로그 전달 구성이 여러 보조 서버를 처리하는지 여부의 영향을 받습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [여러 보조 서버 인스턴스 업그레이드](#MultipleSecondaries)를 참조하세요.

 보조 서버 인스턴스가 업그레이드되는 동안에는 복원되지 않은 트랜잭션 로그 백업이 누적되도록 로그 전달 복사 및 복원 작업이 실행되지 않습니다. 누적되는 양은 주 서버의 예약된 백업 빈도에 따라 달라집니다. 또한 별도의 모니터 서버가 구성된 경우 지정된 간격보다 오랫동안 복원이 수행되지 않았음을 나타내는 경고가 발생할 수 있습니다.

 보조 서버가 업그레이드된 후에는 로그 전달 에이전트 작업이 다시 시작되어 주 서버 인스턴스인 서버 A의 로그 백업을 계속 복사하고 복원합니다. 보조 서버에서 보조 데이터베이스를 최신 상태로 만드는 데 필요한 시간은 보조 서버를 업그레이드하는 데 걸리는 시간과 주 서버에서 수행되는 백업 빈도에 따라 달라집니다.

> [!NOTE]
>  서버 업그레이드 도중 보조 데이터베이스는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스로 업그레이드되지 않습니다. 보조 데이터베이스는 온라인 상태가 될 경우에만 업그레이드됩니다.

> [!IMPORTANT]
>  업그레이드가 필요한 데이터베이스에는 RESTORE WITH STANDBY 옵션이 지원되지 않습니다. RESTORE WITH STANDBY를 사용하여 업그레이드된 보조 데이터베이스를 구성한 경우에는 업그레이드 후에 트랜잭션 로그를 더 이상 복원할 수 없습니다. 해당 보조 데이터베이스에서 로그 전달을 재개하려면 해당 대기 서버에서 로그 전달을 다시 설정해야 합니다. STANDBY 옵션에 대 한 자세한 내용은 [RESTORE Arguments &#40;transact-sql&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)를 참조 하세요.

###  <a name="upgrading-the-primary-server-instance"></a><a name="UpgradePrimary"></a> 주 서버 인스턴스 업그레이드
 업그레이드를 계획할 때는 데이터베이스를 사용할 수 없는 시간을 고려하는 것이 중요합니다. 가장 간단한 업그레이드 시나리오를 사용할 경우 주 서버를 업그레이드하는 동안 데이터베이스가 사용할 수 없게 됩니다(시나리오 1).

 업그레이드 프로세스가 복잡해지더라도 원래 주 서버를 업그레이드하기 전에 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상의 주 서버를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보조 서버로 장애 조치(Failover)하여 데이터베이스 가용성을 최대화할 수 있습니다(아래의 시나리오 2). 장애 조치 시나리오에는 두 가지 변형이 있는데, 하나는 원래 주 서버로 다시 전환하고 원래 로그 전달 구성을 유지하는 것이고 다른 하나는 원래 주 서버를 업그레이드하기 전에 원래 로그 전달 구성을 제거하고 나중에 새 주 서버를 사용하여 새 구성을 만드는 것입니다. 이 섹션에서는 이러한 시나리오에 대해 설명합니다.

> [!IMPORTANT]
>  주 서버 인스턴스를 업그레이드하기 전에 보조 서버 인스턴스를 업그레이드해야 합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [보조 서버 인스턴스 업그레이드](#UpgradeSecondary)를 참조하세요.


####  <a name="scenario-1-upgrade-primary-server-instance-without-failover"></a><a name="Scenario1"></a>시나리오 1: 장애 조치를 사용 하지 않고 주 서버 인스턴스 업그레이드
 이 시나리오는 간단한 반면에 장애 조치를 사용할 때보다 작동 중단 시간이 깁니다. 즉, 주 서버 인스턴스를 손쉽게 업그레이드할 수 있는 반면에 이 업그레이드 동안 데이터베이스를 사용할 수 없습니다.

 서버가 업그레이드된 후에는 데이터베이스가 자동으로 업그레이드가 가능한 온라인 상태로 다시 설정됩니다. 데이터베이스가 업그레이드되면 로그 전달 작업이 다시 시작됩니다.

#### <a name="scenario-2-upgrade-primary-server-instance-with-failover"></a>시나리오 2: 장애 조치를 사용하여 주 서버 인스턴스 업그레이드
 이 시나리오는 가용성을 최대화하고 작동 중단 시간을 최소화합니다. 즉, 보조 서버 인스턴스로의 제어된 장애 조치가 사용되기 때문에 원래 주 서버 인스턴스가 업그레이드되는 동안 데이터베이스가 사용 가능한 상태로 유지됩니다. 작동 중단 시간은 주 서버 인스턴스를 업그레이드하는 데 필요한 시간이 아니라 장애 조치하는 데 필요한 상대적으로 짧은 시간으로 제한됩니다.

 장애 조치를 사용하여 주 서버 인스턴스를 업그레이드하는 프로세스에는 보조 서버로 제어된 장애 조치를 수행하고, 원래 주 서버 인스턴스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하고, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 주 서버 인스턴스에 로그 전달을 설정하는 세 가지 일반적인 절차가 포함됩니다. 이 섹션에서는 이러한 절차에 대해 설명합니다.

> [!IMPORTANT]
>  보조 서버 인스턴스를 새 주 서버 인스턴스로 사용하려면 로그 전달 구성을 제거해야 합니다. 로그 전달은 원래 주 서버 인스턴스가 업그레이드된 후에 새 주 서버에서 새 보조 서버로 다시 구성해야 합니다. 자세한 내용은 [로그 전달 &#40;제거 SQL Server&#41;](remove-log-shipping-sql-server.md)를 참조 하세요.


#####  <a name="procedure-1-perform-a-controlled-failover-to-the-secondary-server"></a><a name="Procedure1"></a>절차 1: 보조 서버로 제어 된 장애 조치 (Failover) 수행
 보조 서버로 제어된 장애 조치를 수행하려면 다음과 같이 하세요.

1.  WITH NORECOVERY를 지정 하 여 주 데이터베이스에 대 한 트랜잭션 로그의 [비상 로그 백업을](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) 수동으로 수행 합니다. 이 로그 백업은 아직 백업되지 않은 모든 로그 레코드를 캡처하고 데이터베이스를 오프라인 상태로 만듭니다. 데이터베이스가 오프라인 상태일 때는 로그 전달 백업 작업이 실패합니다.

     다음 예에서는 주 서버에 있는 `AdventureWorks` 데이터베이스의 비상 로그 백업을 만듭니다. 백업 파일의 이름은 `Failover_AW_20080315.trn`입니다.

    ```
    BACKUP LOG AdventureWorks 
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Failover_AW_20080315.trn' 
       WITH NORECOVERY;
    GO
    ```

     고유한 파일 명명 규칙을 사용하여 수동으로 만든 백업 파일과 로그 전달 백업 작업을 통해 만들어진 백업 파일을 구분하는 것이 좋습니다.

2.  보조 서버에서 다음을 수행합니다.

    1.  로그 전달 백업 작업을 통해 자동으로 수행된 모든 백업이 적용되었는지 확인합니다. 적용 된 백업 작업을 확인 하려면 모니터 서버 또는 주 서버와 보조 서버에서 [sp_help_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql) 시스템 저장 프로시저를 사용 합니다. 동일한 파일이 **last_backup_file**, **last_copied_file**및 **last_restored_file** 열에 나열 되어야 합니다. 백업 파일 중 하나라도 복사되지 않거나 복원되지 않은 경우 수동으로 로그 전달 구성에 대한 에이전트 복사 및 복원 작업을 호출합니다.

         작업을 시작하는 방법은 [Start a Job](../../ssms/agent/start-a-job.md)을 참조하세요.

    2.  1단계에서 만든 최종 로그 백업 파일을 파일 공유에서 보조 서버의 로그 전달에 사용되는 로컬 위치로 복사합니다.

    3.  데이터베이스를 온라인 상태로 만드는 WITH RECOVERY를 지정하여 최종 로그 백업을 복원합니다. 온라인 상태로 만드는 과정에서 데이터베이스는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드됩니다.

         다음 예에서는 보조 서버에 있는 `AdventureWorks` 데이터베이스의 비상 로그 백업을 복원합니다. 이 예에서는 데이터베이스를 온라인 상태로 만드는 WITH RECOVERY 옵션을 사용합니다.

        ```
        RESTORE LOG AdventureWorks 
          FROM DISK = N'c:\logshipping\Failover_AW_20080315.trn' 
           WITH RECOVERY;
        GO
        ```

        > [!NOTE]
        >  둘 이상의 보조 서버가 있는 구성의 경우 추가로 고려해야 할 사항이 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [여러 보조 서버 인스턴스 업그레이드](#MultipleSecondaries)를 참조하세요.

    4.  클라이언트를 원래 주 서버(서버 A)에서 온라인 보조 서버(서버 B)로 리디렉션하여 데이터베이스를 장애 조치합니다.

    5.  데이터베이스가 온라인 상태일 때 보조 데이터베이스의 트랜잭션 로그가 채워지지 않도록 주의합니다. 트랜잭션 로그가 채워지지 않도록 하려면 트랜잭션 로그를 백업해야 할 수 있습니다. 이 경우 다른 서버 인스턴스에서 복원할 수 있도록 공유 위치인 *백업 공유*에 백업하는 것이 좋습니다.

#####  <a name="procedure-2-upgrade-the-original-primary-server-instance-to-sscurrent"></a><a name="Procedure2"></a>절차 2: 원래 주 서버 인스턴스를로 업그레이드[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
 원래 주 서버 인스턴스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 후에도 데이터베이스는 계속 오프라인 상태로 동일한 형식을 사용합니다.

#####  <a name="procedure-3-set-up-log-shipping-on-sscurrent"></a><a name="Procedure3"></a>절차 3:에서 로그 전달 설정[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
 업그레이드 프로세스의 나머지 부분은 다음과 같이 로그 전달이 계속 구성되어 있는지 여부에 따라 달라집니다.

-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]이상의 로그 전달 구성을 유지한 경우 원래 주 서버 인스턴스로 다시 전환합니다. 자세한 내용은 이 섹션의 뒷부분에 나오는 [원래 주 서버 인스턴스로 다시 전환하려면](#SwitchToOrigPrimary)을 참조하세요.

-   장애 조치를 수행하기 전에 로그 전달 구성을 제거한 경우 원래 보조 서버 인스턴스가 새 주 서버 인스턴스가 되는 새 로그 전달 구성을 만듭니다. 자세한 내용은 이 섹션의 뒷부분에 나오는 [이전 보조 서버 인스턴스를 새 주 서버 인스턴스로 사용하려면](#KeepOldSecondaryAsNewPrimary)을 참조하세요.

######  <a name="to-switch-back-to-the-original-primary-server-instance"></a><a name="SwitchToOrigPrimary"></a>원래 주 서버 인스턴스로 다시 전환 하려면

1.  임시 주 서버(서버 B)에서 WITH NORECOVERY를 사용하여 비상 로그를 백업하여 비상 로그 백업을 만들고 데이터베이스를 오프라인 상태로 만듭니다. 비상 로그 백업의 이름은 `Switchback_AW_20080315.trn`입니다. 예를 들면 다음과 같습니다.

    ```
    BACKUP LOG AdventureWorks 
      TO DISK = N'\\FileServer\LogShipping\AdventureWorks\Switchback_AW_20080315.trn' 
       WITH NORECOVERY;
    GO
    ```

2.  임시 주 데이터베이스에서 1단계에서 만든 비상 백업이 아니라 트랜잭션 로그 백업이 수행된 경우 WITH NORECOVERY를 사용하여 이러한 로그 백업을 원래 주 서버(서버 A)의 오프라인 데이터베이스로 복원합니다. 데이터베이스는 첫 번째 로그 백업이 복원될 때 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드됩니다.

3.  데이터베이스를 온라인 상태로 전환하는 WITH RECOVERY를 사용하여 원래 주 데이터베이스(서버 A)의 비상 로그 백업 `Switchback_AW_20080315.trn`을 복원합니다.

4.  클라이언트를 원래 주 서버에서 온라인 보조 서버로 리디렉션하여 원래 주 데이터베이스(서버 A)로 다시 장애 조치합니다.

 데이터베이스가 온라인 상태가 되면 원래 로그 전달 구성이 다시 시작됩니다.

######  <a name="to-keep-the-old-secondary-server-instance-as-the-new-primary-server-instance"></a><a name="KeepOldSecondaryAsNewPrimary"></a>이전 보조 서버 인스턴스를 새 주 서버 인스턴스로 유지 하려면
 다음과 같이 이전 보조 서버 인스턴스 B를 주 서버로 사용하고 이전 주 서버 인스턴스 A를 새 보조 서버로 사용하는 새 로그 전달 구성을 설정합니다.

> [!IMPORTANT]
>  데이터베이스를 오프라인 상태로 만드는 수동 트랜잭션 로그 백업을 수행하기 전에 원래 주 서버에서 이전 로그 전달 구성을 제거해야 합니다.

1.  새 보조 서버(서버 A)에서 데이터베이스의 전체 백업 및 복원이 수행되는 것을 방지하려면 새 주 데이터베이스의 로그 백업을 새 보조 데이터베이스에 적용합니다. 위의 구성 예에서는 이 과정에 서버 B에서 수행된 로그 백업을 서버 A의 데이터베이스로 복원하는 작업이 포함됩니다.

2.  새 주 데이터베이스(서버 B)의 로그를 백업합니다.

3.  WITH NORECOVERY를 사용하여 새 보조 서버 인스턴스(서버 A)에 로그 백업을 복원합니다. 데이터베이스는 첫 번째 복원 작업이 수행될 때 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업데이트됩니다.

4.  이전 보조 서버(서버 B)가 주 서버 인스턴스로 사용되는 로그 전달을 구성합니다.

    > [!IMPORTANT]
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하는 경우 보조 데이터베이스가 이미 초기화되어 있다고 지정하세요.

     자세한 내용은 [로그 전달 구성&#40;SQL Server&#41;](configure-log-shipping-sql-server.md)에서 도입되었습니다.

5.  클라이언트를 원래 주 서버(서버 A)에서 온라인 보조 서버(서버 B)로 리디렉션하여 데이터베이스를 장애 조치합니다.

    > [!IMPORTANT]
    >  새 주 데이터베이스로 장애 조치할 때는 해당 메타데이터가 원래 주 데이터베이스의 메타데이터와 일치하는지 확인해야 합니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)을 참조하세요.

##  <a name="upgrading-multiple-secondary-server-instances"></a><a name="MultipleSecondaries"></a>여러 보조 서버 인스턴스 업그레이드
 다음 그림에서는 주 서버 인스턴스 A와 두 개의 보조 서버 인스턴스 B와 C로 구성된 이러한 구성을 보여 줍니다.

 ![보조 서버 2대, 모니터 서버 없음](../media/ls-3-wayconfig-nomonitor.gif "보조 서버 2대, 모니터 서버 없음")

 이 섹션에서는 장애 조치(failover)를 사용한 다음 원래 주 서버로 다시 전환하여 업그레이드하는 방법에 대해 설명합니다. 보조 서버 인스턴스가 여러 개 있으면 장애 조치를 사용하여 주 인스턴스를 업그레이드하는 프로세스가 훨씬 더 복잡해집니다. 다음 절차에서는 보조 서버가 모두 업그레이드된 후에 주 서버가 업그레이드된 보조 데이터베이스 중 하나로 장애 조치됩니다. 원래 주 서버가 업그레이드되면 로그 전달은 다시 원래 주 서버로 장애 조치됩니다.

> [!IMPORTANT]
>  항상 주 서버를 업그레이드하기 전에 모든 보조 서버 인스턴스를 업그레이드하세요.

 **장애 조치를 사용한 다음 원래 주 서버로 다시 전환하여 업그레이드하려면**

1.  모든 보조 서버 인스턴스(서버 B 및 서버 C)를 업그레이드합니다.

2.  주 데이터베이스(서버 A)의 트랜잭션 비상 로그를 가져오고 데이터베이스를 오프라인 상태로 만든 다음 WITH NORECOVERY를 사용하여 트랜잭션 로그를 백업합니다.

3.  장애 조치하려는 보조 서버(서버 B)에서 보조 데이터베이스를 온라인 상태로 만들고 WITH RECOVERY를 사용하여 로그 백업을 복원합니다.

4.  다른 한 보조 서버(서버 C)에서 보조 데이터베이스를 오프라인 상태로 그대로 두고 WITH RECOVERY를 사용하여 로그 백업을 복원합니다.

    > [!NOTE]
    >  보조 서버에서 로그 전달 복사 및 복원 작업이 실행되지만 백업 공유에 새 로그 백업 파일이 저장되지 않기 때문에 이러한 작업이 실행되어도 아무런 효과가 없습니다.

5.  클라이언트를 원래 주 서버(서버 A)에서 온라인 보조 서버(서버 B)로 리디렉션하여 데이터베이스를 장애 조치합니다. 그러면 온라인 데이터베이스가 임시 주 서버가 되어 원래 주 서버(서버 A)가 오프라인 상태일 때 계속 사용 가능한 상태로 유지됩니다.

6.  원래 주 서버(서버 A)를 업그레이드합니다.

7.  장애 조치 (failover) 한 데이터베이스-중간 주 데이터베이스 (서버 B)에서 WITH NORECOVERY를 사용 하 여 트랜잭션 로그를 수동으로 백업 합니다. 그러면 데이터베이스가 오프라인 상태가 됩니다.

8.  임시 주 데이터베이스(서버 B)에서 만든 모든 트랜잭션 로그 백업을 WITH NORECOVERY를 사용하여 다른 보조 데이터베이스(서버 C)로 복원합니다. 이렇게 하면 각 보조 데이터베이스에서 전체 데이터베이스 복원을 수행하지 않고도 업그레이드 후에 원래 주 데이터베이스에서 로그 전달을 계속할 수 있습니다.

9. WITH RECOVERY를 사용하여 임시 주 서버(서버 B)에서 원래 주 데이터베이스(서버 A)로 트랜잭션 로그를 복원합니다.

##  <a name="redeploying-log-shipping"></a><a name="Redeploying"></a>로그 전달 다시 배포
 위의 절차 중 하나를 사용하여 로그 전달 구성을 마이그레이션하지 않으려는 경우 주 데이터베이스의 전체 백업 및 복원으로 보조 데이터베이스를 다시 초기화하여 로그 전달을 처음부터 다시 배포할 수 있습니다. 데이터베이스 크기가 작거나 업그레이드 절차를 수행하는 동안 고가용성이 필요 없는 경우 알맞은 방법입니다.

 로그 전달을 설정 하는 방법에 대 한 자세한 내용은 [로그 전달 &#40;구성 SQL Server&#41;](configure-log-shipping-sql-server.md)을 참조 하십시오.

## <a name="see-also"></a>참고 항목
 [트랜잭션 로그 백업은](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md) [트랜잭션 로그 백업 &#40;SQL Server](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)&#41;[로그 전달 테이블 및 저장 프로시저](log-shipping-tables-and-stored-procedures.md)&#41;적용 SQL Server &#40;합니다.
