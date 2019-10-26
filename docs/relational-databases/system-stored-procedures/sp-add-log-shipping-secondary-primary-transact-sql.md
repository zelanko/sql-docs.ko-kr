---
title: sp_add_log_shipping_secondary_primary (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 155f59426e8167d5d888f3890089dd4b2ea3bf7c
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909691"
---
# <a name="sp_add_log_shipping_secondary_primary-transact-sql"></a>sp_add_log_shipping_secondary_primary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 주 데이터베이스에 대한 보조 서버에서 주 정보를 설정하고, 로컬 및 원격 모니터 링크를 추가하며, 복사본을 만들고 작업을 복원합니다.  
  
 ![토픽 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "토픽 링크 아이콘") [Transact-sql 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_log_shipping_secondary_primary  
 [ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[ @backup_source_directory = ] 'backup_source_directory' ,   
[ @backup_destination_directory = ] 'backup_destination_directory'  
[ @copy_job_name = ] 'copy_job_name'  
[ @restore_job_name = ] 'restore_job_name'  
[, [ @file_retention_period = ] 'file_retention_period']  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @copy_job_id = ] 'copy_job_id' OUTPUT ]  
[, [ @restore_job_id = ] 'restore_job_id' OUTPUT ]  
[, [ @secondary_id = ] 'secondary_id' OUTPUT]  
```  
  
## <a name="arguments"></a>인수  
로그 전달 구성에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 주 인스턴스의 이름을 `[ @primary_server = ] 'primary_server'` 합니다. *primary_server* 는 **sysname** 이며 NULL 일 수 없습니다.  
  
`[ @primary_database = ] 'primary_database'`는 주 서버에 있는 데이터베이스의 이름입니다. *primary_database* 는 **sysname**이며 기본값은 없습니다.  
  
주 서버의 트랜잭션 로그 백업 파일이 저장 되는 디렉터리를 `[ @backup_source_directory = ] 'backup_source_directory'` 합니다. *backup_source_directory* 는 **nvarchar (500)** 이며 NULL 일 수 없습니다.  
  
백업 파일이 복사 되는 보조 서버의 디렉터리를 `[ @backup_destination_directory = ] 'backup_destination_directory'` 합니다. *backup_destination_directory* 는 **nvarchar (500)** 이며 NULL 일 수 없습니다.  
  
트랜잭션 로그 백업을 보조 서버에 복사 하기 위해 생성 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업에 사용할 이름을 `[ @copy_job_name = ] 'copy_job_name'` 합니다. *copy_job_name* 는 **sysname** 이며 NULL 일 수 없습니다.  
  
`[ @restore_job_name = ] 'restore_job_name'` 보조 서버에서 보조 데이터베이스로 백업을 복원 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업의 이름입니다. *restore_job_name* 는 **sysname** 이며 NULL 일 수 없습니다.  
  
백업 파일이 삭제 되기 전에 @backup_destination_directory 매개 변수로 지정 된 경로에서 보조 서버에 유지 되는 시간 (분)을 `[ @file_retention_period = ] 'file_retention_period'` 합니다. *history_retention_period* 은 **int**이며 기본값은 NULL입니다. 값이 지정되지 않으면 14420이 사용됩니다.  
  
`[ @monitor_server = ] 'monitor_server'`은 모니터 서버의 이름입니다. *Monitor_server* 는 **sysname**이며 기본값은 없고 NULL 일 수 없습니다.  
  
모니터 서버에 연결 하는 데 사용 되는 보안 모드를 `[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 합니다.  
  
 1 = Windows 인증  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증  
  
 *monitor_server_security_mode* 는 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @monitor_server_login = ] 'monitor_server_login'`는 모니터 서버에 액세스 하는 데 사용 되는 계정의 사용자 이름입니다.  
  
`[ @monitor_server_password = ] 'monitor_server_password'`는 모니터 서버에 액세스 하는 데 사용 되는 계정의 암호입니다.  
  
보조 서버의 복사 작업과 연결 된 ID를 `[ @copy_job_id = ] 'copy_job_id' OUTPUT` 합니다. *copy_job_id* 은 **uniqueidentifier** 이며 NULL 일 수 없습니다.  
  
보조 서버의 복원 작업과 연결 된 ID를 `[ @restore_job_id = ] 'restore_job_id' OUTPUT` 합니다. *restore_job_id* 은 **uniqueidentifier** 이며 NULL 일 수 없습니다.  
  
로그 전달 구성에서 보조 서버의 ID를 `[ @secondary_id = ] 'secondary_id' OUTPUT` 합니다. *secondary_id* 은 **uniqueidentifier** 이며 NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>Remarks  
 **sp_add_log_shipping_secondary_primary** 는 보조 서버의 **master** 데이터베이스에서 실행 해야 합니다. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  지정한 주 서버 및 주 데이터베이스의 보조 ID를 생성합니다.  
  
2.  다음을 수행합니다.  

    1.  제공 된 인수를 사용 하 여 **log_shipping_secondary** 에서 보조 ID에 대 한 항목을 추가 합니다.  
  
    2.  비활성화되어 있는 보조 ID에 대해 복사 작업을 만듭니다.  
  
    3.  **Log_shipping_secondary** 항목의 복사 작업 id를 복사 작업의 작업 id로 설정 합니다.  
  
    4.  비활성화되어 있는 보조 ID에 대해 복원 작업을 만듭니다.  
  
    5.  **Log_shipping_secondary** 항목의 복원 작업 id를 복원 작업의 작업 id로 설정 합니다.  
  
## <a name="permissions"></a>Permissions  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예에서는 **sp_add_log_shipping_secondary_primary** 저장 프로시저를 사용 하 여 보조 서버에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 주 데이터베이스에 대 한 정보를 설정 하는 방법을 보여 줍니다.  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_primary   
@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks'   
,@backup_source_directory = N'\\tribeca\LogShipping'   
,@backup_destination_directory = N''   
,@copy_job_name = N''   
,@restore_job_name = N''   
,@file_retention_period = 1440   
,@monitor_server = N'ROCKAWAY'   
,@monitor_server_security_mode = 1   
,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT   
,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT   
,@secondary_id = @LS_Secondary__SecondaryId OUTPUT ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
