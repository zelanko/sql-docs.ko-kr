---
title: sp_change_log_shipping_secondary_database (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d0bd62fe3462441d4eab9d3d89bce20cf1144131
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72909562"
---
# <a name="sp_change_log_shipping_secondary_database-transact-sql"></a>sp_change_log_shipping_secondary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보조 데이터베이스 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @restore_delay = ] 'restore_delay'`보조 서버가 지정 된 백업 파일을 복원 하기 전에 대기 하는 시간 (분)입니다. *restore_delay* 는 **int** 이며 NULL 일 수 없습니다. 기본값은 0입니다.  
  
`[ @restore_all = ] 'restore_all'`1로 설정 하면 복원 작업이 실행 될 때 보조 서버에서 사용 가능한 모든 트랜잭션 로그 백업을 복원 합니다. 그렇지 않으면 파일을 하나 복원한 후 중지합니다. *restore_all* 은 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @restore_mode = ] 'restore_mode'`보조 데이터베이스에 대 한 복원 모드입니다.  
  
 0 = NORECOVERY로 로그 복원  
  
 1 = STANDBY로 로그 복원  
  
 *restore* 는 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @disconnect_users = ] 'disconnect_users'`1로 설정 하면 복원 작업을 수행할 때 보조 데이터베이스에서 사용자 연결이 끊어집니다. 기본값 = 0 *disconnect_users* 은 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @block_size = ] 'block_size'`백업 장치의 블록 크기로 사용 되는 크기 (바이트)입니다. *block_size* 은 **int** 이며 기본값은-1입니다.  
  
`[ @buffer_count = ] 'buffer_count'`백업 또는 복원 작업에 사용 되는 버퍼의 총 수입니다. *buffer_count* 은 **int** 이며 기본값은-1입니다.  
  
`[ @max_transfer_size = ] 'max_transfer_size'`에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 장치로 발급 하는 최대 입력 또는 출력 요청의 크기 (바이트)입니다. *max_transfersize* 는 **int** 이며 NULL 일 수 있습니다.  
  
`[ @restore_threshold = ] 'restore_threshold'`복원 작업 간 허용 되는 시간 (분)으로, 경고가 생성 됩니다. *restore_threshold* 는 **int** 이며 NULL 일 수 없습니다.  
  
`[ @threshold_alert = ] 'threshold_alert'`복원 임계값을 초과할 때 발생 하는 경고입니다. *threshold_alert* 는 **int**이며 기본값은 14420입니다.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'`*Restore_threshold*를 초과할 때 경고가 발생 하는지 여부를 지정 합니다. 1 = 설정, 0 = 해제 *threshold_alert_enabled* 은 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @history_retention_period = ] 'history_retention_period'`기록이 보존 되는 시간 (분)입니다. *history_retention_period* 은 **int**입니다. 지정 된 값이 없는 경우에는 1440 값이 사용 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_change_log_shipping_secondary_database** 는 보조 서버의 **master** 데이터베이스에서 실행 해야 합니다. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  필요에 따라 **log_shipping_secondary_database** 레코드의 설정을 변경 합니다.  
  
2.  필요한 경우 제공 된 인수를 사용 하 여 보조 서버에서 **log_shipping_monitor_secondary** 의 로컬 모니터 레코드를 변경 합니다.  

## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예에서는 **sp_change_log_shipping_secondary_database** 를 사용 하 여 **logshipadventureworks**데이터베이스에 대 한 보조 데이터베이스 매개 변수를 업데이트 하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
