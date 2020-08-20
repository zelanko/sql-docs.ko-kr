---
description: managed_backup. sp_backup_config_schedule (Transact-sql)
title: managed_backup. sp_backup_config_schedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/20/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 23f1f96ff6d41412e8606e67aacfdc42d9afabc4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486307"
---
# <a name="managed_backupsp_backup_config_schedule-transact-sql"></a>managed_backup. sp_backup_config_schedule (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  의 자동 또는 사용자 지정 일정 옵션을 구성 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 합니다.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'
    ,[@scheduling_option = ] {'Custom' | 'System'}  
    ,[@full_backup_freq_type = ] {'Daily' | 'Weekly'}  
    ,[@days_of_week = ] 'days_of_the_week'  
    ,[@backup_begin_time = ] 'begin time of the backup window'  
    ,[@backup_duration = ] 'backup window length'  
    ,[@log_backup_freq = ] 'frequency of log backup'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 인수  
 @database_name  
 특정 데이터베이스에서 관리 되는 백업을 사용 하도록 설정 하기 위한 데이터베이스 이름입니다. NULL 또는 * 인 경우이 관리 되는 백업은 서버의 모든 데이터베이스에 적용 됩니다.  
  
 @scheduling_option  
 시스템 제어 백업 일정에 대해 ' 시스템 '을 지정 합니다. 다른 매개 변수가 올바른지에서 정의한 사용자 지정 일정에 대해 ' 사용자 지정 '을 지정 합니다.  
  
 @full_backup_freq_type  
 ' 매일 ' 또는 ' 매주 '로 설정할 수 있는 관리 되는 백업 작업의 빈도 유형입니다.  
  
 @days_of_week  
 가 주별로 설정 된 경우 백업에 대 한 요일입니다 @full_backup_freq_type . ' 월요일 '과 같은 전체 문자열 이름을 지정 합니다.  또한 파이프로 구분 된 두 개 이상의 일 이름을 지정할 수 있습니다. 예: N'Monday | 수요일 | 금요일 '.  
  
 @backup_begin_time  
 백업 기간의 시작 시간입니다. 및를 조합 하 여 정의 하는 시간 창 외부에서는 백업이 시작 되지 않습니다 @backup_begin_time @backup_duration .  
  
 @backup_duration  
 백업 시간 기간의 기간입니다. 및에 정의 된 기간 동안에는 백업이 완료 될 수도 없습니다 @backup_begin_time @backup_duration . 이 기간에 시작 되었지만 기간을 초과 하는 백업 작업은 취소 되지 않습니다.  
  
 @log_backup_freq  
 이는 트랜잭션 로그 백업의 빈도를 결정 합니다. 이러한 백업은 데이터베이스 백업에 지정 된 일정 대신 정기적으로 수행 됩니다. @log_backup_freq 는 분 또는 시간 일 수 있으며 `0:00` 로그 백업이 없음을 나타내는 유효 합니다. 로그 백업을 사용 하지 않도록 설정 하는 것은 단순 복구 모델을 사용 하는 데이터베이스에만 적합 합니다.  
  
> [!NOTE]  
>  복구 모델이 단순에서 전체로 변경 되는 경우의 log_backup_freq을 `0:00` 0이 아닌 값으로 다시 구성 해야 합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 **ALTER ANY CREDENTIAL** 권한 및 **sp_delete_backuphistory** 저장 프로시저에 대 한 **EXECUTE** 권한이 있는 **db_backupoperator** 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [managed_backup. sp_backup_config_basic (Transact-sql)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
