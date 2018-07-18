---
title: managed_backup.sp_backup_config_schedule (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
ms.openlocfilehash: 8ebeca4b0a1c9079f8786303207bcbae4dfe74c3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38035281"
---
# <a name="managedbackupspbackupconfigschedule-transact-sql"></a>managed_backup.sp_backup_config_schedule (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  자동화 된 또는 사용자 지정 일정 옵션에 대 한 구성 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]합니다.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
##  <a name="Arguments"></a> 인수  
 @database_name  
 특정 데이터베이스에 대 한 managed backup을 사용 하도록 설정 하는 것에 대 한 데이터베이스 이름입니다. Null 인 경우 또는 *, 관리 되는 backup이 서버의 모든 데이터베이스에 적용 됩니다.  
  
 @scheduling_option  
 백업 예약 시스템 제어 방식의 'System'를 지정 합니다. 'Custom' 다른 paratmeters 정의한 사용자 지정 일정을 지정 합니다.  
  
 @full_backup_freq_type  
 관리 되는 백업 작업의 경우 'Daily' 또는 '주별'로 설정할 수 있습니다는 주파수 형식입니다.  
  
 @days_of_week  
 백업에 대 한 요일 때 @full_backup_freq_type 를 매주로 설정 합니다. '월요일 부터'와 같은 전체 문자열 이름을 지정 합니다.  지정할 수도 있습니다 보다 하루 이름, 파이프로 구분 합니다. 예를 들어 N'Monday | 수요일 | 금요일 '.  
  
 @backup_begin_time  
 백업 창 시작 시간입니다. 백업 조합으로 정의 되는 시간 창 외부에서 시작 되지 것입니다 @backup_begin_time 고 @backup_duration입니다.  
  
 @backup_duration  
 백업 시간 기간 정의한 기간 동안 백업 완료 될는 보장 되지 않습니다 있다는 점에 주의 @backup_begin_time 고 @backup_duration입니다. 이 기간에서 시작 되었지만 창의 기간을 초과 하는 백업 작업이 취소 되지 않습니다.  
  
 @log_backup_freq  
 트랜잭션 로그 백업의 빈도 결정합니다. 이러한 백업이 정기적으로 대신 데이터베이스 백업에 지정 된 일정에 따라 수행 됩니다. @log_backup_freq 몇 분 또는 시간에 있을 수 있습니다 하 고 0은 로그 백업이 수행 되지 않음을 유효 합니다. 로그 백업을 사용 하지 않도록 설정 게만 되는 단순 복구 모델을 사용 하 여 데이터베이스에 대 한 합니다.  
  
> [!NOTE]  
>  복구 모델을 simple에서 full로 변경 되 면 0이 아닌 값으로 0에서 log_backup_freq를 다시 구성 해야 합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 **db_backupoperator** 사용 하 여 데이터베이스 역할 **ALTER ANY CREDENTIAL** 권한 및 **EXECUTE** 에 대 한 권한을 **sp_delete_ backuphistory** 저장 프로시저입니다.  
  
## <a name="see-also"></a>관련 항목  
 [managed_backup.sp_backup_config_basic (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
