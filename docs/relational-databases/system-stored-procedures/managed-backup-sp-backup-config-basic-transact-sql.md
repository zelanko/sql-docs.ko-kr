---
description: managed_backup.sp_backup_config_basic(Transact-SQL)
title: managed_backup managed_backup.sp_backup_config_basic (transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_basic_TSQL
- sp_backup_config_basic
- managed_backup.sp_backup_config_basic
- managed_backup.sp_backup_config_basic_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_basic
- sp_backup_config_basic
ms.assetid: 3ad73051-ae9a-4e41-a889-166146e5508f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 428dff3f22b5a924f7a208a988334c14ece752a3
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753737"
---
# <a name="managed_backupsp_backup_config_basic-transact-sql"></a>managed_backup.sp_backup_config_basic(Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]특정 데이터베이스 또는 인스턴스에 대 한 기본 설정을 구성 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  이 절차를 자체적으로 호출 하 여 기본 관리 되는 백업 구성을 만들 수 있습니다. 그러나 고급 기능 또는 사용자 지정 일정을 추가 하려는 경우 먼저 [managed_backup. sp_backup_config_advanced ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) [&#41;&#40;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)&#41;&#40;사용 하 여이 절차를 통해 관리 되는 백업을 사용 하도록 설정 하기 전에 해당 설정을 구성 합니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 인수  
 @enable_backup  
 지정한 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하거나 사용하지 않습니다. 는 @enable_backup **BIT**입니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]의 첫 번째 인스턴스를 구성할 때 필요한 매개 변수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 입니다. 기존 구성을 변경 하는 경우 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 매개 변수는 선택 사항입니다. 이 경우 지정 되지 않은 모든 구성 값은 기존 값을 유지 합니다.  
  
 @database_name  
 특정 데이터베이스에서 관리 되는 백업을 사용 하도록 설정 하기 위한 데이터베이스 이름입니다.  
  
 @container_url  
 백업 위치를 나타내는 URL입니다. @credential_name가 NULL 인 경우이 url은 Azure Storage blob 컨테이너에 대 한 SAS (공유 액세스 서명) url이 고, 백업에서는 새 백업을 사용 하 여 blob 기능을 차단 합니다. 자세한 내용은 [SAS 이해](/azure/storage/common/storage-sas-overview)를 참조 하세요. @credential_name이 지정 된 경우이는 저장소 계정 URL 이며 백업은 사용 되지 않는 백업 페이지 blob 기능을 사용 합니다.  
  
> [!NOTE]  
>  지금은이 매개 변수에 SAS URL만 지원 됩니다.  
  
 @retention_days  
 백업 파일의 보존 기간(일)입니다. 는 @storage_url INT입니다. 이 매개 변수는 인스턴스에서 처음으로를 구성할 때 필수 매개 변수입니다 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 구성을 변경 하는 동안 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 매개 변수는 선택 사항입니다. 지정하지 않은 경우 기존 구성 값이 유지됩니다.  
  
 @credential_name  
 Azure 저장소 계정에 인증 하는 데 사용 되는 SQL 자격 증명의 이름입니다. @credentail_name 는 **SYSNAME**입니다. 이를 지정 하면 백업이 페이지 blob에 저장 됩니다. 이 매개 변수가 NULL 이면 백업은 블록 blob으로 저장 됩니다. 페이지 blob에 대 한 백업은 더 이상 사용 되지 않으므로 새 블록 blob 백업 기능을 사용 하는 것이 좋습니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성 변경에 사용하는 경우 이 매개 변수는 선택 사항입니다. 지정 하지 않으면 기존 구성 값이 유지 됩니다.  
  
> [!WARNING]
>  지금은 ** \@ credential_name** 매개 변수가 지원 되지 않습니다. 블록 blob에 대 한 백업만 지원 됩니다 .이 매개 변수는 NULL 이어야 합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 **ALTER ANY CREDENTIAL** 권한 및 **sp_delete_backuphistory** 저장 프로시저에 대 한 **EXECUTE** 권한이 있는 **db_backupoperator** 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예  
 최신 Azure PowerShell 명령을 사용 하 여 저장소 계정 컨테이너와 SAS URL을 모두 만들 수 있습니다. 다음 예제에서는 mystorageaccount 저장소 계정에 새 컨테이너 mycontainer를 만든 다음 모든 권한을 사용 하 여이 컨테이너에 대 한 SAS URL을 가져옵니다.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 다음 예에서는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서 실행 되는 SQL Server 인스턴스를 사용 하도록 설정 하 고, 보존 정책을 30 일로 설정 하 고, 대상을 ' mystorageaccount ' 라는 저장소 계정에서 ' mycontainer ' 라는 컨테이너로 설정 합니다.  
  
```Transact-SQL 
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=1  
                ,@container_url = 'https://mystorageaccount.blob.core.windows.net/mycontainer'  
                ,@retention_days=30;   
GO  
  
```
  
 다음 예에서는 실행 중인 SQL Server 인스턴스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하지 않도록 설정합니다.  
  
```Transact-SQL  
Use msdb;  
Go  
EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=0;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [transact-sql&#41;&#40;managed_backup.sp_backup_config_advanced managed_backup ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
