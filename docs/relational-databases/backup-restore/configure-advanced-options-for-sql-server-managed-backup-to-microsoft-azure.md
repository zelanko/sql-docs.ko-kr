---
title: Microsoft Azure에 대한 SQL Server Managed Backup용 고급 옵션 구성 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ffd28159-8de8-4d40-87da-1586bfef3315
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f64010973cd54bee7723668c861ca515e818bce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure"></a>Microsoft Azure에 대한 SQL Server Managed Backup용 고급 옵션 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  다음 자습서는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에 대한 고급 옵션 설정 방법을 설명합니다. 이러한 절차는 제공되는 기능에서 필요한 경우에만 필요합니다. 그렇지 않으면 기본 동작에 따라 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을(를) 사용할 수 있습니다.  
  
 각 시나리오에서 백업은 `database_name` 매개 변수를 사용하여 지정됩니다. `database_name` 이 NULL 또는 *인 경우 변경하면 인스턴스 수준의 기본 설정에 영향을 줍니다. 또한, 인스턴스 수준 설정은 변경 이후 생성된 새로운 데이터베이스에도 영향을 줍니다.  
  
 이러한 설정을 지정하면 시스템 저장 프로시저 [managed_backup.sp_backup_config_basic(Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)을 사용하여 데이터베이스 또는 인스턴스에서 Managed Backup을 사용하도록 설정할 수 있습니다. 자세한 내용은 [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)을(를) 참조하십시오.  
  
> [!WARNING]  
>  항상 고급 옵션 및 사용자 지정 일정 옵션을 구성한 후에 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]와 [managed_backup.sp_backup_config_basic(Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)을 사용하도록 설정해야 합니다. 그렇지 않은 경우 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을(를) 활성화하고 이러한 설정을 구성하는 시간 기간 동안에 예기치 않은 백업 작업이 발생할 수 있습니다.  
  
## <a name="configure-encryption"></a>암호화 구성  
 다음 단계는 저장 프로시저 [managed_backup.sp_backup_config_advanced&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)를 사용하여 암호화 설정을 지정하는 방법을 설명합니다.  
  
1.  **암호화 알고리즘 결정:** 먼저 사용할 암호화 알고리즘의 이름을 결정합니다. 다음 알고리즘 중 하나 선택:  
  
    -   AES_128  
  
    -   AES_192  
  
    -   AES_256  
  
    -   TRIPLE_DES_3KEY  
  
    -   NO_ENCRYPTION  
  
2.  **데이터베이스 마스터 키 생성:** 데이터베이스에 저장되는 마스터 키의 복사본을 암호화하기 위한 암호를 선택합니다.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
       CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
    ```  
  
3.  **백업 인증서 또는 비대칭 키 생성:** 암호화에서 사용할 CERTIFICATE 또는 ASYMMETRIC KEY를 사용할 수 있습니다. 다음 예제에서는 백업 암호화에 사용할 백업 인증서를 만듭니다.  
  
    ```sql  
    USE Master;  
    GO  
       CREATE CERTIFICATE MyTestDBBackupEncryptCert  
          WITH SUBJECT = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
4.  **Managed Backup 암호화 설정:** 해당 값과 함께 **managed_backup.sp_backup_config_advanced** 저장 프로시저를 호출합니다. 예를 들어, 다음 예제에서는 이름이 `MyDB` 인 인증서와 `MyTestDBBackupEncryptCert` 암호화 알고리즘을 사용하여 암호화에서 사용할 `AES_128` 데이터베이스를 구성합니다.  
  
    ```  
    USE msdb;  
    GO  
       EXEC managed_backup.sp_backup_config_advanced  
          @database_name = 'MyDB'                
          ,@encryption_algorithm ='AES_128'  
          ,@encryptor_type = 'CERTIFICATE'  
          ,@encryptor_name = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
    > [!WARNING]  
    >  이전 예제에서 `@database_name` 이 NULL인 경우 설정은 SQL Server 인스턴스에 적용됩니다.  
  
## <a name="configure-a-custom-backup-schedule"></a>사용자 지정 백업 일정 구성  
 다음 단계는 저장 프로시저 [managed_backup.sp_backup_config_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)을 사용하여 사용자 지정 일정을 설정하는 방법을 설명합니다.  
  
1.  **전체 백업을 위한 빈도 결정:** 데이터베이스의 전체 백업을 수행하는 빈도를 결정합니다. '매일' 및 '매주' 전체 백업을 선택할 수 있습니다.  
  
2.  **로그 백업을 위한 빈도 결정:** 로그 백업을 수행하는 빈도를 결정합니다. 이 값은 분 단위 또는 시간 단위입니다.  
  
3.  **주별 백업에 대한 요일 결정:** 주별로 백업하는 경우 전체 백업을 수행할 요일을 결정합니다.  
  
4.  **백업 시작 시간 결정:** 24시간 표시법을 사용하여 백업을 시작할 시간을 선택합니다.  
  
5.  **백업에서 허용되는 시간 길이 결정:** 백업이 완료되어야 하는 시간의 양을 지정합니다.  
  
6.  **사용자 지정 백업 일정 설정:** 다음 저장 프로시저는 `MyDB` 데이터베이스에 대한 사용자 지정 일정을 정의합니다. 전체 백업은 `Monday` `17:30`시에 매주 수행됩니다. 로그 백업은 `5` 분마다 수행됩니다. 백업은 두 시간 내에 완료됩니다.  
  
    ```  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_backup_config_schedule   
         @database_name =  'MyDB'  
        ,@scheduling_option = 'Custom'  
        ,@full_backup_freq_type = 'Weekly'  
        ,@days_of_week = 'Monday'  
        ,@backup_begin_time =  '17:30'  
        ,@backup_duration = '02:00'  
        ,@log_backup_freq = '00:05'  
    GO  
  
    ```  
  
## <a name="next-steps"></a>Next Steps  
 고급 옵션 및 사용자 지정 일정을 구성한 후 대상 데이터베이스 또는 SQL Server 인스턴스에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을(를) 활성화해야 합니다. 자세한 내용은 [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)을(를) 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Azure에 대한 SQL Server Managed Backup](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
