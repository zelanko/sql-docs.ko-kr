---
title: sp_change_log_shipping_secondary_database (Transact SQL) | Microsoft Docs
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
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5e4ee6324e92130f3f887fe3a36ecd5469cd9d99
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spchangelogshippingsecondarydatabase-transact-sql"></a>sp_change_log_shipping_secondary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보조 데이터베이스 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
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
 [  **@restore_delay =** ] '*restore_delay*'  
 보조 서버가 지정된 백업 파일을 복원하기 전에 대기하는 시간(분)입니다. *restore_delay* 은 **int** NULL 일 수 없습니다. 기본값은 0입니다.  
  
 [  **@restore_all =** ] '*restore_all*'  
 1로 설정될 경우 보조 서버는 복원 작업 실행 시 모든 사용 가능한 트랜잭션 백업을 복원합니다. 그렇지 않으면 파일을 하나 복원한 후 중지합니다. *restore_all* 은 **비트** NULL 일 수 없습니다.  
  
 [  **@restore_mode =** ] '*restore_mode*'  
 보조 데이터베이스의 복원 모드입니다.  
  
 0 = NORECOVERY로 로그 복원  
  
 1 = STANDBY로 로그 복원  
  
 *복원* 은 **비트** NULL 일 수 없습니다.  
  
 [  **@disconnect_users =** ] '*disconnect_users*'  
 1로 설정될 경우 복원 작업 수행 시 보조 데이터베이스에서 사용자 연결이 끊어집니다. 기본값 = 0 *disconnect_users* 은 **비트** NULL 일 수 없습니다.  
  
 [  **@block_size =** ] '*block_size*'  
 백업 장치의 블록 크기로 사용되는 크기(바이트)입니다. *block_size* 은 **int** 기본값은-1입니다.  
  
 [ **@buffer_count =** ] '*buffer_count*'  
 백업 또는 복원 작업에 사용되는 버퍼의 총 개수입니다. *buffer_count* 은 **int** 기본값은-1입니다.  
  
 [ **@max_transfer_size =** ] '*max_transfer_size*'  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 백업 장치로 발급하는 최대 입력 또는 출력 요청의 크기(바이트)입니다. *max_transfersize* 은 **int** NULL 일 수 있습니다.  
  
 [  **@restore_threshold =** ] '*restore_threshold*'  
 복원 작업 간 허용되는 시간(분)입니다. 이 시간이 지나면 경고가 발생합니다. *restore_threshold* 은 **int** NULL 일 수 없습니다.  
  
 [  **@threshold_alert =** ] '*threshold_alert*'  
 복원 임계값을 초과할 경우 발생하는 경고입니다. *threshold_alert* 은 **int**, 14420이 기본값입니다.  
  
 [  **@threshold_alert_enabled =** ] '*threshold_alert_enabled*'  
 경고는 되는지 여부를 지정 발생 시기 *restore_threshold*을 초과 합니다. 1 = 설정, 0 = 해제 *threshold_alert_enabled* 은 **비트** NULL 일 수 없습니다.  
  
 [  **@history_retention_period =** ] '*history_retention_period*'  
 기록이 보존되는 기간(분)입니다. *history_retention_period* 은 **int**합니다. 1440 값은 지정 되지 않은 경우에 사용 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_change_log_shipping_secondary_database** 에서 실행 되어야 합니다는 **마스터** 보조 서버에서 데이터베이스. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  설정을 변경는 **log_shipping_secondary_database** 필요에 따라 기록 합니다.  
  
2.  로컬 모니터 레코드를 변경 **log_shipping_monitor_secondary** 보조 서버에서 사용 하 여 제공 된 인수를 필요한 경우.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예제에서는 사용 하 여 **sp_change_log_shipping_secondary_database** 보조 데이터베이스 매개 변수는 데이터베이스에 대 한 업데이트 **LogShipAdventureWorks**합니다.  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 & #40;에 대 한 SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
