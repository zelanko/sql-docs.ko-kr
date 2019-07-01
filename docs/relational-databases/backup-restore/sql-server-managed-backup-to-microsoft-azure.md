---
title: Microsoft Azure에 대한 SQL Server Managed Backup 해제 | Microsoft 문서
ms.custom: ''
ms.date: 10/18/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5c041ee4a56b2df2190eabb0da0ef472f0b8ee49
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63008565"
---
# <a name="sql-server-managed-backup-to-microsoft-azure"></a>Microsoft Azure에 대한 SQL Server Managed Backup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 Microsoft Azure Blob Storage에 대한 SQL Server 백업을 관리하고 자동화합니다. SQL Server에서 데이터베이스의 트랜잭션 작업에 따라 백업 일정을 결정하도록 선택할 수 있습니다. 또는 고급 옵션을 사용하여 일정을 정의할 수 있습니다. 보존 설정은 백업이 Azure Blob 스토리지에 저장되는 기간을 결정합니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 지정한 보존 기간 동안 지정 시간 복원을 지원합니다.  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 의 프로시저 및 기본 동작이 변경되었습니다. 자세한 내용은 [Migrate SQL Server 2014 Managed Backup Settings to SQL Server 2016](../../relational-databases/backup-restore/migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016.md)을 참조하세요.  
  
> [!TIP]  
>  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 Microsoft Azure 가상 컴퓨터에서 실행되는 SQL Server 인스턴스에 사용하는 것이 좋습니다.  
  
## <a name="benefits"></a>이점  
 현재 여러 데이터베이스에 대한 백업을 자동화하려면 백업 전략 개발, 사용자 지정 코드 작성, 백업 예약 등이 필요하지만, [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하여 보존 기간 및 스토리지 위치만을 지정함으로써 백업 계획을 만들 수 있습니다. 고급 설정을 사용할 수 있지만 필요하지 않습니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 백업의 예약, 실행 및 유지 관리를 모두 처리합니다.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 데이터베이스 수준 또는 SQL Server 인스턴스 수준에서 구성할 수 있습니다. 인스턴스 수준에서 구성할 경우 새로운 데이터베이스도 자동으로 백업됩니다. 데이터베이스 수준에서 설정을 사용하여 개별 사례에서 인스턴스 수준 기본값을 재정의할 수 있습니다.  
  
 또한, 추가 보안에 대한 백업을 암호화하고, 사용자 지정 일정을 설정하여 백업 실행 시기를 관리할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 위한 Microsoft Azure Blob Storage 서비스의 이점에 대한 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.  
  
##  <a name="Prereqs"></a> 필수 구성 요소  
 Microsoft Azure Storage는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에서 백업 파일을 저장하는 데 사용합니다. 필요한 필수 구성 요소는 다음과 같습니다.  
  
|사전 요구 사항|설명|  
|------------------|-----------------|  
|**Microsoft Azure 계정**|[무료 평가판](https://azure.microsoft.com/pricing/free-trial/) 으로 Azure를 시작한 후에 [구매 옵션](https://azure.microsoft.com/pricing/purchase-options/)을 살펴볼 수 있습니다.|  
|**Azure Storage 계정**|백업은 Azure 스토리지 계정에 연결된 Azure Blob 스토리지에 저장됩니다. 스토리지 계정을 만드는 단계별 지침은 [Azure Storage 계정 정보](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)를 참조하세요.|  
|**Blob 컨테이너**|Blob은 컨테이너에 구성됩니다. 백업 파일에 대한 대상 컨테이너를 지정합니다. [Azure 관리 포털](https://manage.windowsazure.com/)에서 컨테이너를 만들거나 **New-AzureStorageContainer**[Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) 명령을 사용할 수 있습니다.|  
|**공유 액세스 서명(SAS)**|대상 컨테이너에 대한 액세스는 공유 액세스 서명(SAS)으로 제어됩니다. SAS에 대한 개요는 [공유 액세스 서명, 1부: SAS 모델 이해](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)를 참조하세요. 코드 또는 **New-AzureStorageContainerSASToken** PowerShell 명령으로 SAS 토큰을 만들 수 있습니다. 이 프로세스를 간소화하는 PowerShell 스크립트는 [Powershell 포함 Azure Storage에서 SAS(공유 액세스 서명) 토큰으로 SQL 자격 증명 만들기 간소화](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)를 참조하세요. SAS 토큰은 **에 사용할 수 있도록** SQL 자격 증명 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에 저장할 수 있습니다.|  
|**SQL Server 에이전트**|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 작동하려면 SQL Server 에이전트가 실행되고 있어야 합니다. 자동으로 시작 옵션을 설정하는 것이 좋습니다.|  
  
## <a name="components"></a>구성 요소  
 Transact-SQL은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]과 상호 작용하는 주 인터페이스입니다. 시스템 저장 프로시저는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하도록 설정하고 구성 및 모니터링하는 데 사용됩니다. 시스템 함수는 기존 구성 설정, 매개 변수 값 및 백업 파일 정보를 검색하는 데 사용됩니다. 확장 이벤트는 오류 및 경고를 노출하는 데 사용됩니다. 경고 메커니즘은 SQL 에이전트 작업 및 SQL Server 정책 기반의 관리를 통해 설정됩니다 다음은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]과 관련된 개체와 해당 기능에 대한 설명 목록입니다.  
  
 PowerShell cmdlet도 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 구성하는 데 사용할 수 있습니다. SQL Server Management Studio는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서 **데이터베이스 복원** 태스크를 사용하여 만든 백업 복원을 지원합니다.  
  
|||  
|-|-|  
|시스템 개체|설명|  
|**MSDB**|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에서 만든 모든 백업에 대한 메타데이터, 백업 기록을 저장합니다.|  
|[managed_backup.sp_backup_config_basic(Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]를 사용합니다.|  
|[managed_backup.sp_backup_config_advanced&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에 대한 고급 설정(예: 암호화)을 구성합니다.|  
|[managed_backup.sp_backup_config_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]의 사용자 지정 일정을 만듭니다.|  
|[managed_backup.sp_ backup_master_switch&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 일시 중지하고 다시 시작합니다.|  
|[managed_backup.sp_set_parameter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에 대한 모니터링을 사용하고 구성합니다. 예제: 알림을 위한 메일 설정, 확장 이벤트 설정입니다.|  
|[managed_backup.sp_backup_on_demand&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql.md)|로그 체인을 끊지 않고 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 사용하기 위해 설정된 데이터베이스의 임시 백업을 수행합니다.|  
|[managed_backup.fn_backup_db_config&#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql.md)|데이터베이스 또는 인스턴스에 있는 모든 데이터베이스의 현재 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 상태 및 구성 값을 반환합니다.|  
|[managed_backup.fn_is_master_switch_on&#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql.md)|마스터 스위치의 상태를 반환합니다.|  
|[managed_backup.sp_get_backup_diagnostics&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql.md)|확장 이벤트에 기록된 이벤트를 반환합니다.|  
|[managed_backup.fn_get_parameter&#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql.md)|경고의 메일 설정 및 모니터링 등 백업 시스템 설정의 현재 값을 반환합니다.|  
|[managed_backup.fn_available_backups&#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md)|지정한 데이터베이스 또는 인스턴스의 모든 데이터베이스에 대해 사용 가능한 백업을 검색합니다.|  
|[managed_backup.fn_get_current_xevent_settings&#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql.md)|현재 확장 이벤트 설정을 반환합니다.|  
|[managed_backup.fn_get_health_status&#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql.md)|지정한 기간 동안 확장 이벤트에서 기록한 집계된 오류 수를 반환합니다.|  
  
## <a name="backup-strategy"></a>백업 전략  
  
### <a name="backup-scheduling"></a>백업 일정 예약  
 시스템 저장 프로시저 [managed_backup.sp_backup_config_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)을 참조하세요. 사용자 지정 일정을 지정하지 않을 경우 예약된 백업 유형 및 백업 주기는 데이터베이스 작업을 기준으로 결정됩니다. 보존 기간 설정은 보존 기간 내 지정 시간에 데이터베이스를 복구하는 기능과 스토리지에 보존할 백업 파일의 시간을 결정하는 데 사용됩니다.  
  
### <a name="backup-file-naming-conventions"></a>백업 파일 명명 규칙  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 사용자가 지정하는 컨테이너를 사용하므로, 컨테이너 이름을 제어할 수 있습니다. 백업 파일의 경우 다음 규칙을 사용하여 비가용성 데이터베이스의 이름을 지정합니다. 이름은 데이터베이스 이름의 첫 40자, '-'를 제외한 데이터베이스 GUID 및 타임스탬프를 사용하여 만들어집니다. 밑줄 문자는 구분 기호로 세그먼트 사이에 삽입됩니다. **.bak** 파일 확장명은 전체 백업에 사용되고 **.log** 파일 확장명은 로그 백업에 사용됩니다. 가용성 그룹 데이터베이스의 경우 위에서 설명한 파일 명명 규칙 외에도 가용성 그룹 데이터베이스 GUID가 40자의 데이터베이스 이름 뒤에 추가됩니다. 가용성 그룹 데이터베이스 GUID 값은 sys.databases의 group_database_id 값입니다.  
  
### <a name="full-database-backup"></a>전체 데이터베이스 백업  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에이전트는 다음을 만족할 경우 전체 데이터베이스 백업을 예약합니다.  
  
-   데이터베이스에 처음으로 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 설정되거나 인스턴스 수준에서 기본 설정과 함께 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 설정된 경우  
  
-   마지막 전체 데이터베이스 백업 이후 증가한 로그가 1GB 이상인 경우  
  
-   마지막 전체 데이터베이스 백업 이후 최대 시간 간격인 일주일이 지난 경우  
  
-   로그 체인이 끊어진 경우. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 주기적으로 백업 파일의 첫 번째 LSN과 마지막 LSN을 비교하여 로그 체인의 변경 여부를 확인합니다. 이유에 관계없이 로그 체인이 끊어진 경우 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 전체 데이터베이스 백업을 예약합니다. 로그 체인이 끊어지는 가장 일반적인 이유는 Transact-SQL을 사용하거나 SQL Server Management Studio의 백업 태스크를 통해 실행되는 백업 명령 때문입니다.  그 외에 실수로 백업 로그 파일을 삭제하거나 백업을 덮어쓰는 경우가 있을 수 있습니다.  
  
### <a name="transaction-log-backup"></a>트랜잭션 로그 백업  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 다음 중 하나에 해당하는 경우 로그 백업을 예약합니다.  
  
-   로그 백업 기록을 찾을 수 없는 경우. 이는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 처음으로 설정된 경우 발생합니다.  
  
-   사용된 트랜잭션 로그 공간이 5MB 이상인 경우  
  
-   마지막 로그 백업 후 최대 시간 간격인 2시간이 경과한 경우  
  
-   트랜잭션 로그 백업이 전체 데이터베이스 백업보다 뒤처지는 경우. 목표는 로그 체인이 전체 백업을 앞서도록 유지하는 것입니다.  
  
## <a name="retention-period-settings"></a>보존 기간 설정  
 백업을 사용하도록 설정할 때는 일 단위로 보존 기간을 설정해야 합니다. 최솟값은 1일이고 최댓값은 30일입니다.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 지정한 시간 내 지정 시간에 복구하는 기능을 평가하여 보존해야 할 백업 파일과 삭제할 백업 파일을 결정합니다. 백업의 backup_finish_date는 보존 기간 설정에서 지정한 시간을 확인하고 일치시키는 데 사용됩니다.  
  
## <a name="important-considerations"></a>중요 고려 사항  
 특정 데이터베이스의 경우 기존의 전체 데이터베이스 백업 작업이 실행 중이면 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 는 현재 작업이 완료될 때까지 기다린 다음 동일한 데이터베이스에 대해 다른 전체 데이터베이스 백업을 수행합니다. 마찬가지로 한 번에 한 트랜잭션 로그 백업만 실행할 수 있습니다. 그러나 전체 데이터베이스 백업 및 트랜잭션 로그 백업은 동시에 실행할 수 있습니다. 실패는 확장 이벤트로 기록됩니다.  
  
 10개 이상의 전체 데이터베이스 백업이 동시에 예약된 경우 확장 이벤트의 디버그 채널을 통해 경고가 발생합니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 백업이 필요한 나머지 데이터베이스의 우선 순위 큐를 관리합니다.  

> [!NOTE]
> 프록시 서버에서 SQL Server Managed Backup이 지원되지 않습니다.
>
  
##  <a name="support_limits"></a> 지원 가능성  
 다음 지원 제한 사항 및 고려 사항은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 특정한 것입니다.  
  
-   **마스터**, **모델**및 **msdb** 시스템 데이터베이스는 백업할 수 있습니다. **tempdb** 는 백업할 수 없습니다. 
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 경우 모든 복구 모델이 지원됩니다(전체, 대량 로그 및 단순).  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에이전트는 데이터베이스 전체 및 로그 백업만 지원합니다. 파일 백업 자동화는 지원되지 않습니다.  
  
-   Microsoft Azure Blob Storage service는 유일하게 지원되는 백업 스토리지 옵션입니다. 디스크 또는 테이프 백업은 지원되지 않습니다.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 블록 Blob에 백업 기능을 사용합니다. 블록 Blob의 최대 크기는 200GB입니다. 그러나 스트라이프를 활용하여 개별 백업의 최대 크기를 최대 12TB가 될 수 있습니다. 백업 요구 사항이 이 크기를 초과하는 경우 압축을 사용해 보고 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 설정하기 전에 백업 파일 크기를 테스트하세요. 로컬 디스크에 백업하거나 **BACKUP TO URL** Transact-SQL 문을 사용하여 Microsoft Azure Storage에 수동으로 백업하여 테스트할 수 있습니다. 자세한 내용은 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)을 참조하세요.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 구성한 경우 일부 제한 사항이 있을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
- [Microsoft Azure에 대한 SQL Server Managed Backup 설정](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)   
- [Microsoft Azure에 대한 SQL Server Managed Backup용 고급 옵션 구성](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)   
- [Microsoft Azure에 대한 SQL Server Managed Backup 해제](../../relational-databases/backup-restore/disable-sql-server-managed-backup-to-microsoft-azure.md)
- [시스템 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)
- [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
  
  
