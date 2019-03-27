---
title: sp_add_log_shipping_secondary_database (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_database
- sp_add_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_database
ms.assetid: d29e1c24-3a3c-47a4-a726-4584afa6038a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c7dab148af9d8c3db8a9b1503ad33975c790120
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493225"
---
# <a name="spaddlogshippingsecondarydatabase-transact-sql"></a>sp_add_log_shipping_secondary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그 전달을 위한 보조 데이터베이스를 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>인수  
`[ @secondary_database = ] 'secondary_database'` 보조 데이터베이스의 이름이입니다. *secondary_database* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @primary_server = ] 'primary_server'` 기본 인스턴스 이름을 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성에서 합니다. *primary_server* 됩니다 **sysname** NULL 일 수 없습니다.  
  
`[ @primary_database = ] 'primary_database'` 주 서버에서 데이터베이스의 이름이입니다. *primary_database* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @restore_delay = ] 'restore_delay'` 시간 (분) 보조 서버가 지정된 된 백업 파일을 복원 하기 전에 대기 하는 양입니다. *restore_delay* 됩니다 **int** NULL 일 수 없습니다. 기본값은 0입니다.  
  
`[ @restore_all = ] 'restore_all'` 복원 작업을 실행 하면 모든 사용 가능한 트랜잭션 로그 백업을 복원 하는 보조 서버 1로 설정 합니다. 그렇지 않으면 파일 한 개를 복원한 후 중지됩니다. *restore_all* 됩니다 **비트** NULL 일 수 없습니다.  
  
`[ @restore_mode = ] 'restore_mode'` 보조 데이터베이스에 대 한 복원 모드입니다.  
  
 0 = NORECOVERY로 로그 복원  
  
 1 = STANDBY로 로그 복원  
  
 *복원할* 됩니다 **비트** NULL 일 수 없습니다.  
  
`[ @disconnect_users = ] 'disconnect_users'` 하는 경우 1로 설정 된 사용자의 연결이 끊어집니다 보조 데이터베이스에서 복원 작업을 수행할 때. 기본값 = 0 *연결 끊기* 사용자는 **비트** NULL 일 수 없습니다.  
  
`[ @block_size = ] 'block_size'` 크기 (바이트), 백업 장치의 블록 크기로 사용 되는 합니다. *block_size* 됩니다 **int** 기본값인-1입니다.  
  
`[ @buffer_count = ] 'buffer_count'` 백업 또는 복원 작업에 사용 되는 버퍼의 총 수입니다. *buffer_count* 됩니다 **int** 기본값인-1입니다.  
  
`[ @max_transfer_size = ] 'max_transfer_size'` 크기 (바이트), 최대 입력 또는 출력 요청의에서 발급 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 장치에 있습니다. *max_transfersize* 됩니다 **int** 이며 NULL 일 수 있습니다.  
  
`[ @restore_threshold = ] 'restore_threshold'` 간의 시간 경과 허용 하는 시간 (분). 복원 작업 전에 경고가 생성 됩니다. *restore_threshold* 됩니다 **int** NULL 일 수 없습니다.  
  
`[ @threshold_alert = ] 'threshold_alert'` 백업 임계값이 초과 하는 경우 발생 하는 경고 이며 *threshold_alert* 됩니다 **int**, 기본값은 14,420입니다.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` 경고가 발생 하는지 여부를 지정 하면 *backup_threshold* 를 초과 합니다. 기본값인 1은 경고가 발생된다는 의미입니다. *threshold_alert_enabled* 됩니다 **비트**합니다.  
  
`[ @history_retention_period = ] 'history_retention_period'` 기록이 보존 되는 몇 분 안에 시간의 길이입니다. *history_retention_period* 됩니다 **int**, 기본값은 NULL입니다. 지정된 값이 없으면 14420을 사용합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 **sp_add_log_shipping_secondary_database** 에서 실행 해야 합니다 **마스터** 보조 서버의 데이터베이스. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  **sp_add_log_shipping_secondary_primary** 이전 주 로그 전달 보조 서버에서 데이터베이스 정보를 초기화 하려면이 저장된 프로시저를 호출 해야 합니다.  
  
2.  보조 데이터베이스의 항목을 추가 **log_shipping_secondary_databases** 제공된 된 인수를 사용 하 여 합니다.  
  
3.  로컬 모니터 레코드를 추가 **log_shipping_monitor_secondary** 보조 서버에서 사용 하 여 제공 된 인수입니다.  
  
4.  모니터 서버가 보조 서버에서 다른 경우에서 모니터 레코드를 추가 합니다 **log_shipping_monitor_secondary** 모니터 서버를 사용 하 여 제공 된 인수입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예제를 사용 하 여 **sp_add_log_shipping_secondary_database** 저장 프로시저는 데이터베이스를 추가 하려면 **LogShipAdventureWorks** 로그 전달 구성에서 보조 데이터베이스로 주 데이터베이스와 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 주 서버 TRIBECA에 상주 합니다.  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_database   
@secondary_database = N'LogShipAdventureWorks'   
,@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks2012'   
,@restore_delay = 0   
,@restore_mode = 1   
,@disconnect_users = 0   
,@restore_threshold = 45     
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440 ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
