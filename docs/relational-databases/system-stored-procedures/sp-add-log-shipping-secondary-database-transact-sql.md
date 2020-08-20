---
description: sp_add_log_shipping_secondary_database(Transact-SQL)
title: sp_add_log_shipping_secondary_database (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 384884e2b2b076b20cb9c679c3494a7c292f77a1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464670"
---
# <a name="sp_add_log_shipping_secondary_database-transact-sql"></a>sp_add_log_shipping_secondary_database(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  로그 전달을 위한 보조 데이터베이스를 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @secondary_database = ] 'secondary_database'` 보조 데이터베이스의 이름입니다. *secondary_database* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @primary_server = ] 'primary_server'`[!INCLUDE[msCoName](../../includes/msconame-md.md)]로그 전달 구성에 있는의 주 인스턴스 이름입니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . *primary_server* 는 **sysname** 이며 NULL 일 수 없습니다.  
  
`[ @primary_database = ] 'primary_database'` 주 서버에 있는 데이터베이스의 이름입니다. *primary_database* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @restore_delay = ] 'restore_delay'` 보조 서버가 지정 된 백업 파일을 복원 하기 전에 대기 하는 시간 (분)입니다. *restore_delay* 는 **int** 이며 NULL 일 수 없습니다. 기본값은 0입니다.  
  
`[ @restore_all = ] 'restore_all'` 1로 설정 하면 복원 작업이 실행 될 때 보조 서버에서 사용 가능한 모든 트랜잭션 로그 백업을 복원 합니다. 그렇지 않으면 파일 한 개를 복원한 후 중지됩니다. *restore_all* 은 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @restore_mode = ] 'restore_mode'` 보조 데이터베이스에 대 한 복원 모드입니다.  
  
 0 = NORECOVERY로 로그 복원  
  
 1 = STANDBY로 로그 복원  
  
 *restore* 는 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @disconnect_users = ] 'disconnect_users'` 1로 설정 하면 복원 작업을 수행할 때 보조 데이터베이스에서 사용자 연결이 끊어집니다. 기본값 = 0 *연결 끊기* 사용자는 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @block_size = ] 'block_size'` 백업 장치의 블록 크기로 사용 되는 크기 (바이트)입니다. *block_size* 은 **int** 이며 기본값은-1입니다.  
  
`[ @buffer_count = ] 'buffer_count'` 백업 또는 복원 작업에 사용 되는 버퍼의 총 수입니다. *buffer_count* 은 **int** 이며 기본값은-1입니다.  
  
`[ @max_transfer_size = ] 'max_transfer_size'` 에서 백업 장치로 발급 하는 최대 입력 또는 출력 요청의 크기 (바이트)입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *max_transfersize* 는 **int** 이며 NULL 일 수 있습니다.  
  
`[ @restore_threshold = ] 'restore_threshold'` 복원 작업 간 허용 되는 시간 (분)으로, 경고가 생성 됩니다. *restore_threshold* 는 **int** 이며 NULL 일 수 없습니다.  
  
`[ @threshold_alert = ] 'threshold_alert'` 백업 임계값이 초과 될 때 발생 하는 경고입니다. *threshold_alert* 는 **int**이며 기본값은 14420입니다.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'`*Backup_threshold* 를 초과할 때 경고가 발생 하는지 여부를 지정 합니다. 기본값인 1은 경고가 발생된다는 의미입니다. *threshold_alert_enabled* **비트**입니다.  
  
`[ @history_retention_period = ] 'history_retention_period'` 기록이 보존 되는 시간 (분)입니다. *history_retention_period* 은 **int**이며 기본값은 NULL입니다. 지정된 값이 없으면 14420을 사용합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_add_log_shipping_secondary_database** 는 보조 서버의 **master** 데이터베이스에서 실행 해야 합니다. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  보조 서버에서 주 로그 전달 데이터베이스 정보를 초기화 하려면이 저장 프로시저 보다 먼저 **sp_add_log_shipping_secondary_primary** 를 호출 해야 합니다.  
  
2.  제공 된 인수를 사용 하 여 **log_shipping_secondary_databases** 에서 보조 데이터베이스에 대 한 항목을 추가 합니다.  
  
3.  제공 된 인수를 사용 하 여 보조 서버의 **log_shipping_monitor_secondary** 에 로컬 모니터 레코드를 추가 합니다.  
  
4.  모니터 서버가 보조 서버와 다른 경우 제공 된 인수를 사용 하 여 모니터 서버에 **log_shipping_monitor_secondary** 모니터 레코드를 추가 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예제  
 이 예에서는 **sp_add_log_shipping_secondary_database** 저장 프로시저를 사용 하 여 주 서버 TRIBECA에 있는 주 데이터베이스를 사용 하 여 로그 전달 구성에서 데이터베이스 **로깅할 adventureworks** 를 보조 데이터베이스로 추가 하는 방법을 보여 줍니다 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
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
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
