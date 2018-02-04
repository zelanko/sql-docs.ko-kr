---
title: sp_add_log_shipping_secondary_primary (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c83d0a0062f7f7affc19e91b929bb16831a8946d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spaddlogshippingsecondaryprimary-transact-sql"></a>sp_add_log_shipping_secondary_primary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 주 데이터베이스에 대한 보조 서버에서 주 정보를 설정하고, 로컬 및 원격 모니터 링크를 추가하며, 복사본을 만들고 작업을 복원합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@primary_server** = ] '*primary_server*'  
 기본 인스턴스 이름을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성의 합니다. *primary_server* 은 **sysname** NULL 일 수 없습니다.  
  
 [  **@primary_database**  =] '*primary_database*'  
 주 서버의 데이터베이스 이름입니다. *primary_database* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@backup_source_directory**  =] '*backup_source_directory*'  
 주 서버의 트랜잭션 로그 백업 파일이 저장되는 디렉터리입니다. *backup_source_directory* 은 **nvarchar (500)** NULL 일 수 없습니다.  
  
 [  **@backup_destination_directory**  =] '*backup_destination_directory*'  
 백업 파일이 복사되는 보조 서버의 디렉터리입니다. *backup_destination_directory* 은 **nvarchar (500)** NULL 일 수 없습니다.  
  
 [ **@copy_job_name** = ] '*copy_job_name*'  
 트랜잭션 로그 백업을 보조 서버에 복사하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 생성하는 데 사용할 이름입니다. *copy_job_name* 은 **sysname** NULL 일 수 없습니다.  
  
 [ **@restore_job_name** = ] '*restore_job_name*'  
 이름인는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보조 데이터베이스에 백업을 복원 하는 보조 서버의 에이전트 작업입니다. *restore_job_name* 은 **sysname** NULL 일 수 없습니다.  
  
 [  **@file_retention_period**  =] '*file_retention_period*'  
 시간 (분)로 지정 된 경로에서 보조 서버에서 유지 되는 백업 파일의 길이 @backup_destination_directory 삭제 하기 전에 매개 변수입니다. *history_retention_period* 은 **int**, 기본값은 NULL입니다. 값이 지정되지 않으면 14420이 사용됩니다.  
  
 [  **@monitor_server**  =] '*monitor_server*'  
 모니터 서버의 이름입니다. *Monitor_server* 은 **sysname**, 기본값은 없고 NULL 일 수 없습니다.  
  
 [  **@monitor_server_security_mode**  =] '*monitor_server_security_mode*'  
 모니터 서버 연결에 사용되는 보안 모드입니다.  
  
 1 = Windows 인증  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증  
  
 *monitor_server_security_mode* 은 **비트** NULL 일 수 없습니다.  
  
 [ **@monitor_server_login** = ] '*monitor_server_login*'  
 모니터 서버에 액세스하는 데 사용되는 계정의 사용자 이름입니다.  
  
 [ **@monitor_server_password** = ] '*monitor_server_password*'  
 모니터 서버에 액세스하는 데 사용되는 계정의 암호입니다.  
  
 [ **@copy_job_id** = ] '*copy_job_id*' OUTPUT  
 보조 서버의 복사 작업과 연관된 ID입니다. *copy_job_id* 은 **uniqueidentifier** NULL 일 수 없습니다.  
  
 [ **@restore_job_id** = ] '*restore_job_id*' OUTPUT  
 보조 서버의 복원 작업과 연관된 ID입니다. *restore_job_id* 은 **uniqueidentifier** NULL 일 수 없습니다.  
  
 [  **@secondary_id**  =] '*secondary_id*' 출력  
 로그 전달 구성의 보조 서버의 ID입니다. *secondary_id* 은 **uniqueidentifier** NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_add_log_shipping_secondary_primary** 에서 실행 되어야 합니다는 **마스터** 보조 서버에서 데이터베이스. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  지정한 주 서버 및 주 데이터베이스의 보조 ID를 생성합니다.  
  
2.  다음을 수행합니다.  
  
    1.  보조 ID에 대 한 항목을 추가 **log_shipping_secondary** 제공 된 인수를 사용 하 여 합니다.  
  
    2.  비활성화되어 있는 보조 ID에 대해 복사 작업을 만듭니다.  
  
    3.  복사 작업 ID를 설정의 **log_shipping_secondary** 복사 작업의 작업 ID 입력 합니다.  
  
    4.  비활성화되어 있는 보조 ID에 대해 복원 작업을 만듭니다.  
  
    5.  복원 작업 ID를 설정의 **log_shipping_secondary** 복원 작업의 작업 ID 입력 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 사용 하 여 보여 주는이 예제는 **sp_add_log_shipping_secondary_primary** 저장 프로시저는 주 데이터베이스에 대 한 정보를 설정 하려면 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 보조 서버.  
  
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
 [로그 전달 &#40;에 대 한 SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
