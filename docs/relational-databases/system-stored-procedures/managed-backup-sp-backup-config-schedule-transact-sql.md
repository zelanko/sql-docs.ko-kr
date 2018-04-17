---
title: managed_backup.sp_backup_config_schedule (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_backup_config_schedule_TSQL
- managed_backup.sp_backup_config_schedule
- managed_backup.sp_backup_config_schedule_TSQL
- sp_backup_config_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_schedule
- sp_backup_config_schedule
ms.assetid: 82541160-d1df-4061-91a5-6868dd85743a
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1749de4fc4791416ddbac8421ff6a4bfe774a772
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="managedbackupspbackupconfigschedule-transact-sql"></a>managed_backup.sp_backup_config_schedule (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  자동 또는 사용자 지정 일정 옵션을 구성 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]합니다.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'    ,[@scheduling_option = ] {'Custom' | 'System'}  
    ,[@full_backup_freq_type = ] {'Daily' | 'Weekly'}  
    ,[@days_of_week = ] 'days_of_the_week'  
    ,[@backup_begin_time = ] 'begin time of the backup window'  
    ,[@backup_duration = ] 'backup window length'  
    ,[@log_backup_freq = ] 'frequency of log backup'  
```  
  
##  <a name="Arguments"></a> 인수  
 @database_name  
 특정 데이터베이스에서 관리 되는 백업에 대 한 데이터베이스 이름입니다. Null 인 경우 또는 *, 관리 되는이 백업 서버에 모든 데이터베이스에 적용 됩니다.  
  
 @scheduling_option  
 백업 일정 예약 제어 시스템에 대 한 'System'를 지정 합니다. 다른 paratmeters 정의한 사용자 지정 일정에 대 한 'Custom'를 지정 합니다.  
  
 @full_backup_freq_type  
 '매일' 또는 '매주'로 설정 될 수 있는 관리 되는 백업 작업에 대 한 주파수 형식입니다.  
  
 @days_of_week  
 백업에 대해 주 중 일 때 @full_backup_freq_type 매주로 설정 합니다. '월요일'와 같은 완전 한 문자열 이름을 지정 합니다.  표시할 파이프로 구분 되는 1 일 이름 보다 더 합니다. 예를 들어 N'Monday | 수요일 | 금요일 '.  
  
 @backup_begin_time  
 백업 창 시작 시간입니다. 백업의 조합으로 정의 되는 시간 창 외부에서 시작 되지 것입니다. @backup_begin_time 및 @backup_duration합니다.  
  
 @backup_duration  
 백업 시간 창의 기간입니다. 에 정의 된 특정 기간 동안 백업을 완료 하지 않을 수도 있다는 점에 주의 @backup_begin_time 및 @backup_duration합니다. 이 기간에 시작 되지만 창의 기간을 초과 하는 백업 작업 취소 되지 않습니다.  
  
 @log_backup_freq  
 트랜잭션 로그 백업의 빈도 결정합니다. 이러한 백업은 데이터베이스 백업에 대해 지정 된 일정에 따라이 아니라 정기적으로 발생 합니다. @log_backup_freq 분 단위 또는 시간 수이 고 0은 유효 로그 백업이 수행 되지 나타냅니다. 로그 백업을 사용 하지 않도록 설정 게만 되는 단순 복구 모델을 사용 하 여 데이터베이스에 대 한 합니다.  
  
> [!NOTE]  
>  복구 모델이 simple에서 full로 변경 되 면 0이 아닌 값으로 0에서 log_backup_freq를 다시 구성 해야 합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 멤버 자격이 필요 **db_backupoperator** 와 데이터베이스 역할 **ALTER ANY CREDENTIAL** 사용 권한 및 **EXECUTE** 에 대 한 권한을 **sp_delete_ backuphistory** 저장 프로시저입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [managed_backup.sp_backup_config_basic (Transact SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
