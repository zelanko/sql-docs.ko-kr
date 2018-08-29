---
title: sp_add_log_shipping_primary_database (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_database
- sp_add_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_primary_database
ms.assetid: 69531611-113f-46b5-81a6-7bf496d0353c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b73ec62b6b0abc8ab8334efdc5f26c5bd2748605
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43034741"
---
# <a name="spaddlogshippingprimarydatabase-transact-sql"></a>sp_add_log_shipping_primary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  백업 작업, 로컬 모니터 레코드 및 원격 모니터 레코드를 포함하여 로그 전달 구성에 대한 주 데이터베이스를 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_log_shipping_primary_database [ @database = ] 'database',   
[ @backup_directory = ] 'backup_directory',   
[ @backup_share = ] 'backup_share',   
[ @backup_job_name = ] 'backup_job_name',   
[, [ @backup_retention_period = ] backup_retention_period]  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] backup_threshold ]   
[, [ @threshold_alert = ] threshold_alert ]   
[, [ @threshold_alert_enabled = ] threshold_alert_enabled ]   
[, [ @history_retention_period = ] history_retention_period ]  
[, [ @backup_job_id = ] backup_job_id OUTPUT ]  
[, [ @primary_id = ] primary_id OUTPUT]  
[, [ @backup_compression = ] backup_compression_option ]  
  
```  
  
## <a name="arguments"></a>인수  
 [  **@database=** ] '*데이터베이스*'  
 로그 전달 주 데이터베이스의 이름입니다. *데이터베이스* 됩니다 **sysname**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [  **@backup_directory=** ] '*backup_directory*'  
 주 서버의 백업 폴더에 대한 경로입니다. *backup_directory* 됩니다 **nvarchar(500)**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [  **@backup_share=** ] '*backup_share*'  
 주 서버의 백업 디렉터리에 대한 네트워크 경로입니다. *backup_share* 됩니다 **nvarchar(500)**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [ **@backup_job_name=** ] '*backup_job_name*'  
 주 서버에서 백업 폴더에 백업을 복사하는 SQL Server 에이전트 작업의 이름입니다. *backup_job_name* 됩니다 **sysname** NULL 일 수 없습니다.  
  
 [ **@backup_retention_period=** ] *backup_retention_period*  
 주 서버에서 백업 디렉터리에 로그 백업 파일이 보관되는 시간(분)입니다. *backup_retention_period* 됩니다 **int**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [  **@monitor_server=** ] '*monitor_server*'  
 모니터 서버의 이름입니다. *Monitor_server* 됩니다 **sysname**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [ **@monitor_server_security_mode=** ] *monitor_server_security_mode*  
 모니터 서버 연결에 사용되는 보안 모드입니다.  
  
 1 = Windows 인증  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. *monitor_server_security_mode* 됩니다 **비트** NULL 일 수 없습니다.  
  
 [ **@monitor_server_login=** ] '*monitor_server_login*'  
 모니터 서버에 액세스하는 데 사용되는 계정의 사용자 이름입니다.  
  
 [ **@monitor_server_password=** ] '*monitor_server_password*'  
 모니터 서버에 액세스하는 데 사용되는 계정의 암호입니다.  
  
 [ **@backup_threshold=** ] *backup_threshold*  
 시간 (분) 하기 전에 마지막 백업 후의 길이 *threshold_alert* 오류가 발생 합니다. *backup_threshold* 됩니다 **int**, 기본값은 60 분입니다.  
  
 [ **@threshold_alert=** ] *threshold_alert*  
 백업 임계값이 초과될 때 발생하는 경고입니다. *threshold_alert* 됩니다 **int**, 기본값은 14,420입니다.  
  
 [ **@threshold_alert_enabled=** ] *threshold_alert_enabled*  
 경고 않을 것인지 여부를 지정 될 때 발생 *backup_threshold* 를 초과 합니다. 기본값(숫자 0)인 경우 경고를 사용하지 않으므로 경고는 발생하지 않습니다. *threshold_alert_enabled* 됩니다 **비트**합니다.  
  
 [ **@history_retention_period=** ] *history_retention_period*  
 기록이 보존되는 기간(분)입니다. *history_retention_period* 됩니다 **int**, 기본값은 NULL입니다. 값이 지정되지 않으면 14420이 사용됩니다.  
  
 [ **@backup_job_id=** ] *backup_job_id* OUTPUT  
 주 서버의 백업 작업과 연관된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 작업 ID입니다. *backup_job_id* 됩니다 **uniqueidentifier** NULL 일 수 없습니다.  
  
 [ **@primary_id=** ] *primary_id* OUTPUT  
 로그 전달 구성의 주 데이터베이스의 ID입니다. *primary_id* 됩니다 **uniqueidentifier** NULL 일 수 없습니다.  
  
 [ **@backup_compression**=] *backup_compression_option*  
 로그 전달 구성을 사용할지 여부를 지정 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)합니다. 이 매개 변수는 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서만 지원됩니다.  
  
 0 = 사용 안 함. 로그 백업을 압축하지 않습니다.  
  
 1 = 사용. 항상 로그 백업을 압축합니다.  
  
 2 =의 설정을 사용 합니다 [보거나 backup compression default 서버 구성 옵션 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)합니다. 이것은 기본값입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 **sp_add_log_shipping_primary_database** 에서 실행 해야 합니다 **마스터** 주 서버의 데이터베이스입니다. 이 저장 프로시저는 다음 기능을 수행합니다.  
  
1.  주 ID를 생성 하 고 테이블의 주 데이터베이스에 대 한 항목을 추가 **log_shipping_primary_databases** 제공된 된 인수를 사용 하 여 합니다.  
  
2.  비활성화되어 있는 주 데이터베이스에 대해 백업 작업을 만듭니다.  
  
3.  백업 작업 ID를 설정 합니다 **log_shipping_primary_databases** 백업 작업의 작업 ID로 입력 합니다.  
  
4.  테이블에서 로컬 모니터 레코드를 추가 **log_shipping_monitor_primary** 주 서버에서 사용 하 여 제공 된 인수입니다.  
  
5.  모니터 서버가 주 서버에서 다른 경우에서 모니터 레코드를 추가 합니다 **log_shipping_monitor_primary** 모니터 서버를 사용 하 여 제공 된 인수입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 로그 전달 구성의 주 데이터베이스로 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 추가합니다.  
  
```  
DECLARE @LS_BackupJobId AS uniqueidentifier ;  
DECLARE @LS_PrimaryId AS uniqueidentifier ;  
  
EXEC master.dbo.sp_add_log_shipping_primary_database   
@database = N'AdventureWorks'   
,@backup_directory = N'c:\lsbackup'   
,@backup_share = N'\\tribeca\lsbackup'   
,@backup_job_name = N'LSBackup_AdventureWorks'   
,@backup_retention_period = 1440  
,@monitor_server = N'rockaway'   
,@monitor_server_security_mode = 1   
,@backup_threshold = 60   
,@threshold_alert = 0   
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440   
,@backup_job_id = @LS_BackupJobId OUTPUT   
,@primary_id = @LS_PrimaryId OUTPUT   
,@overwrite = 1   
,@backup_compression = 0;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
