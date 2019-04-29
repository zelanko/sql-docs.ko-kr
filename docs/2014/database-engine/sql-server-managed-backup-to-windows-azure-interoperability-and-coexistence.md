---
title: 'Microsoft Azure에 대한 SQL Server 관리되는 백업: 상호 운용성 및 공존 성 | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 78fb78ed-653f-45fe-a02a-a66519bfee1b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d4d883d54a1ad933d4e248f292d9b6a222915a00
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62842910"
---
# <a name="sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence"></a>Microsoft Azure에 대한 SQL Server 관리되는 백업: 상호 운용성 및 공존성
  이 항목에서는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 의 몇 가지 기능에 대한 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 상호 운용성 및 공존성에 대해 설명합니다. 이러한 기능에는 AlwaysOn 가용성 그룹, 데이터베이스 미러링, 백업 유지 관리 계획, 로그 전달, 임시 백업, 데이터베이스 분리 및 데이터베이스 삭제가 있습니다.  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn 가용성 그룹  
 Windows Azure 전용 솔루션에 대 한 지원으로 구성 된 AlwaysOn 가용성 그룹 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]합니다. 온-프레미스 전용 또는 혼합 AlwaysOn 가용성 그룹 구성은 지원되지 않습니다. 자세한 내용 및 기타 고려 사항에 대 한 참조 [가용성 그룹에 대 한 SQL Server Managed Backup to Windows Azure 설정](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)  
  
### <a name="database-mirroring"></a>데이터베이스 미러링  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]은 주 데이터베이스에서만 지원됩니다. 주 데이터베이스와 미러 데이터베이스 모두 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 사용하도록 구성된 경우 미러된 데이터베이스를 건너뛰고 백업하지 않습니다. 그러나 장애 조치(Failover) 시 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 은 미러가 역할 전환을 완료했거나 온라인 상태가 된 이후 백업 프로세스를 시작합니다. 이 경우 백업이 새 컨테이너에 저장됩니다. 미러가 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]을 사용하도록 구성되지 않은 경우에는 장애 조치 시에 백업이 수행되지 않습니다. 백업이 장애 조치 시에 계속되도록 주 데이터베이스와 미러 데이터베이스 모두에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성하는 것이 좋습니다.  
  
> [!TIP]  
>  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 기본 설정을 사용하는 인스턴스에서 미러된 데이터베이스를 만드는 경우, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 인스턴스 기본값을 해제하여 미러된 데이터베이스에 적용되지 않도록 한 다음 주 데이터베이스와 미러 데이터베이스를 구성한 후에 인스턴스 기본값을 다시 사용하도록 설정하는 것이 적합할 수 있습니다.  
  
### <a name="maintenance-plan"></a>유지 관리 계획  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 설정되었을 때 데이터베이스에 대한 백업을 만드는 데 유지 관리 계획을 사용하는 기능은 지원되지 않습니다. 유지 관리 계획은 로그 체인을 끊어지게 하며 복원 시 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 에서 데이터베이스의 보장된 복구를 지원하지 않습니다. 이는 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 설정된 경우에도 적용됩니다.  
  
> [!TIP]  
>  복사 전용 백업을 사용한 유지 관리 계획이 동일한 데이터베이스 또는 인스턴스에 대해 구성된 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 에서 지원됩니다.  
  
### <a name="log-shipping"></a>로그 전달  
 동일한 데이터베이스에 대해 로그 전달 및 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 동시에 구성할 수 없습니다. 이렇게 하면 둘 중 한 기능을 사용하는 데이터베이스 복구가 영향을 받습니다.  
  
### <a name="ad-hoc-backups-using-transact-sql-and-sql-server-management-studio"></a>Transact-SQL 및 SQL Server Management Studio를 사용하는 임시 백업  
 Transact-SQL 또는 SQL Server Management Studio를 사용하여 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 외부에서 만든 임시 또는 한 번 백업은 사용되는 백업 및 스토리지 미디어 유형에 따라 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 프로세스에 영향을 줄 수 있습니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 에서 사용하는 것과 다른 Windows Azure 저장소 계정 또는 Windows Azure Blob 저장소 서비스 이외의 다른 모든 대상으로 로그를 백업하면 로그 체인이 끊어집니다. 사용 하는 것이 좋습니다 합니다 [smart_admin.sp_backup_on_demand &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) 저장 프로시저는 데이터베이스에서 백업을 시작 하려면 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 사용 하도록 설정 합니다. 이 저장 프로시저를 사용하여 전체 데이터베이스 또는 로그 백업을 시작할 수 있습니다.  
  
### <a name="drop-database-and-detach-database"></a>데이터베이스 삭제 및 데이터베이스 분리  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 설정된 데이터베이스가 분리되거나 삭제되면 가능한 추가 백업이 없어도 보존 기간이 경과될 때까지 이전 백업이 저장소에 그대로 있는데 이때 백업이 제거됩니다.  
  
### <a name="changes-to-recovery-model"></a>복구 모델 변경  
  
-   데이터베이스의 복구 모델을 **Simple** 에서 **Full** 또는 **Bulk-Logged**로 변경하는 경우 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] f또는 the database. 이는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 관점에서 새 데이터베이스로 간주됩니다.  
  
-   데이터베이스의 복구 모델을 **Full** 또는 **Bulk-Logged** 에서 **Simple**에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 로 변경하는 경우 백업 작업이 더 이상 예약되지 않습니다. 보존 기간이 경과될 때까지 보존 기간 설정이 계속 활성 상태이며 백업 파일이 스토리지 계정에 남아 있습니다. 백업을 보존하려는 경우 파일을 다른 스토리지 계정 또는 온-프레미스 위치로 다운로드하는 것이 좋습니다. 구성 설정은 보존되며 복구 모델이 다시 **Full** 또는 **Bulk-Logged** 로 설정되는 경우 다시 사용될 수 있습니다.  
  
### <a name="log-backups-using-other-backup-tools-or-custom-scripts"></a>다른 백업 도구 또는 사용자 지정 스크립트를 사용한 로그 백업  
 동일한 데이터베이스에서 로그 백업을 수행하도록 구성된 두 백업은 백업 로그 체인을 끊어지게 합니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 이 백업 체인이 끊어진 것을 검색하면 전체 백업을 예약하여 체인이 끊어진 문제를 해결하려고 시도하지만, 이는 경쟁하는 두 도구에서 수행하는 주기적 로그 백업과 체인이 끊어지는 문제를 지속적으로 파악해야 함을 의미합니다. 또한 어떤 도구도 전체 백업 집합을 순서대로 보유할 것으로 기대할 수 없으므로 데이터베이스의 복구 기능도 영향을 받을 수 있습니다. 이 문제는 로그 백업을 수행하는 어떠한 두 기능이나 도구에도 적용되지만 아래에 설명된 특정 예를 살펴보면 도움이 될 수 있습니다. 또한 이 문제는 이 항목의 이전 섹션에서 설명한 유지 관리 계획 또는 로그 전달 구성 문제의 기초가 됩니다.  
  
 **Data Protection Manager (DPM) 기반 백업:** Microsoft Data Protection Manager를 통해 전체 및 증분 백업을 수행할 수 있습니다. 증분 백업은 T-로그 백업을 만든 후 로그 잘림을 수행하는 로그 백업입니다. 따라서 동일한 데이터베이스에 대해 DPM과 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 둘 다 구성하는 것은 지원되지 않습니다.  
  
 **타사 도구 또는 스크립트:** 로그 잘림을 유발하는 로그 백업을 수행하는 모든 타사 도구 또는 스크립트는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]과 호환되지 않으며 지원되지 않습니다.  
  
 있다면 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 데이터베이스 인스턴스에 대해 사용 하도록 설정 하 고 사용 하 여 임시 백업을 수행 하려는 합니다 [smart_admin.sp_backup_on_demand &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) 이전에 설명 된 대로 저장 프로시저 섹션입니다. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]외부에서 주기적으로 백업을 예약하거나 실행해야 하는 경우에는 복사 전용 백업을 사용할 수 있습니다.  자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](../relational-databases/backup-restore/copy-only-backups-sql-server.md)를 참조하세요.  
  
  
