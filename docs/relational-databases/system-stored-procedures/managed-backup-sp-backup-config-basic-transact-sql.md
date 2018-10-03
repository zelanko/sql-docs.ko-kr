---
title: managed_backup.sp_backup_config_basic (TRANSACT-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 93e6bcfc4ec686f61672fa382d545db5a7000f96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838801"
---
# <a name="managedbackupspbackupconfigbasic-transact-sql"></a>managed_backup.sp_backup_config_basic (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  구성 된 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 특정 데이터베이스 또는 인스턴스에 대 한 기본 설정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
> [!NOTE]  
>  이 절차 호출 될 수는 기본 관리 되는 백업 구성을 만들려면 자체. 그러나 고급 기능 또는 사용자 지정 일정을 추가 하려는 경우 먼저 해당 설정을 구성를 사용 하 여 [managed_backup.sp_backup_config_advanced &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) 하 고 [managed_backup.sp_ backup_config_schedule &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) 이 절차를 사용 하 여 관리 되는 백업을 사용 하도록 설정 하기 전에 합니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> 인수  
 @enable_backup  
 지정한 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하거나 사용하지 않습니다. 합니다 @enable_backup 됩니다 **비트**합니다. 필수 매개 변수를 구성할 때 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 첫 번째 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 기존 변경 하는 경우 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성에서는이 매개 변수는 선택 사항입니다. 이 경우 모든 구성 값을 지정 하지 기존 값을 유지 합니다.  
  
 @database_name  
 특정 데이터베이스에 대 한 managed backup을 사용 하도록 설정 하는 것에 대 한 데이터베이스 이름입니다.  
  
 @container_url  
 백업의 위치를 나타내는 URL입니다. 때 @credential_name 가 null 인 경우이 URL은 Azure Storage에 blob 컨테이너에 대 한 공유 액세스 서명 (SAS) URL 및 백업을 사용 하 여 새로운 블록 blob 기능에 백업 합니다. 자세한 내용은 살펴보시기 [이해 SAS](http://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)합니다. 때 @credential_name 지정 하면 저장소 계정 URL 이며 백업은 사용 되지 않는 백업 페이지 blob 기능을 사용 합니다.  
  
> [!NOTE]  
>  이 현재가 매개이 변수에 대 한 SAS URL만 지원 됩니다.  
  
 @retention_days  
 백업 파일의 보존 기간(일)입니다. @storage_url 정수입니다. 구성 하는 경우 필수 매개 변수를 이것이 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 인스턴스에 처음으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다. 변경 하는 동안는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성에서는이 매개 변수는 선택 사항입니다. 지정하지 않은 경우 기존 구성 값이 유지됩니다.  
  
 @credential_name  
 Windows Azure 저장소 계정 인증에 사용되는 SQL 자격 증명의 이름입니다. @credentail_name 됩니다 **SYSNAME**합니다. 지정 하면 백업 페이지 blob에 저장 됩니다. 이 매개 변수가 NULL 인 경우 백업 블록 blob으로 저장 됩니다. 페이지 blob에 백업 하는 것이 좋습니다 새 블록 blob의 백업 기능을 사용 하므로 사용 되지 않습니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성 변경에 사용하는 경우 이 매개 변수는 선택 사항입니다. 지정 하지 않으면 기존 구성 값이 유지 됩니다.  
  
> [!WARNING]  
>  합니다 **@credential_name** 지금은 매개 변수를 사용할 수 없습니다. Null이이 매개 변수를 요구 하는 블록 blob에만 백업이 지원 됩니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 **db_backupoperator** 사용 하 여 데이터베이스 역할 **ALTER ANY CREDENTIAL** 권한 및 **EXECUTE** 에 대 한 권한을 **sp_delete_ backuphistory** 저장 프로시저입니다.  
  
## <a name="examples"></a>예  
 최신 Azure PowerShell 명령을 사용 하 여 저장소 계정 컨테이너 및 SAS URL을 만들 수 있습니다. 다음 예제에서는 mystorageaccount 저장소 계정에 mycontainer, 새 컨테이너를 만들고 모든 권한으로 SAS URL에 대 한를 획득 합니다.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 다음 예에서는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 실행 중인 SQL Server 인스턴스의 보존 정책을 30 일로 설정에 대 한 대상 'mycontainer' 저장소 계정에 'mystorageaccount' 라는 라는 컨테이너를 설정 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [managed_backup.sp_backup_config_advanced &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
