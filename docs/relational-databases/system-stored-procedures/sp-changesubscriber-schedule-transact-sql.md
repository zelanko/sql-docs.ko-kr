---
title: sp_changesubscriber_schedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber_schedule
- sp_changesubscriber_schedule_TSQL
helpviewer_keywords:
- sp_changesubscriber_schedule
ms.assetid: ff84e8e2-d496-482c-b23e-38a6626596e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 22ecb1601108562607d1fdc550daaa945fe72910
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68770729"
---
# <a name="sp_changesubscriber_schedule-transact-sql"></a>sp_changesubscriber_schedule(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  구독자에 대해 배포 에이전트 또는 병합 에이전트 일정을 변경합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changesubscriber_schedule [ @subscriber = ] 'subscriber', [ @agent_type = ] type  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**입니다. 구독자의 이름은 데이터베이스에서 고유해야 하고 이미 존재해서는 안 되며 NULL일 수 없습니다.  
  
`[ @agent_type = ] type`에이전트의 유형입니다. *type* 은 **smallint**이며 기본값은 **0**입니다. **0** 은 배포 에이전트를 나타냅니다. **1** 은 병합 에이전트를 나타냅니다.  
  
`[ @frequency_type = ] frequency_type`배포 태스크를 예약 하는 빈도입니다. *frequency_type* 는 **int**이며 기본값은 **64**입니다. 10개의 일정 열이 있습니다.  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*에 의해 설정 된 빈도에 적용 되는 값입니다. *frequency_interval* 은 **int**이며 기본값은 **1**입니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`배포 작업의 날짜입니다. *frequency_relative_interval* 은 **int**이며 기본값은 **1**입니다.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @frequency_subday = ] frequency_subday`정의 된 기간 동안 다시 예약 하는 빈도 (분)입니다. *frequency_subday* 은 **int**이며 기본값은 **4**입니다.  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*에 대 한 간격입니다. *frequency_subday_interval* 은 **int**이며 기본값은 **5**입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중에서 배포 태스크가 처음으로 예약 된 시간입니다. *active_start_time_of_day* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중에서 배포 태스크가 중지 되도록 예약 된 시간입니다. *active_end_time_of_day* 은 **int**이며 기본값은 **235959**입니다 .이는 11:59:59 오후을 의미 합니다. 24시간제를 기준으로 오후 11:59:59를 나타냅니다.  
  
`[ @active_start_date = ] active_start_date`배포 태스크가 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @active_end_date = ] active_end_date`배포 태스크가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 는 **int**이며 기본값은 9999 년 12 월 31 일을 의미 하는 **99991231**입니다.  
  
`[ @publisher = ] 'publisher'`이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정 합니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  ** 게시자에 대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한 아티클 속성을 변경할 때는 게시자를 사용 하면 안 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changesubscriber_schedule** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_changesubscriber_schedule**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addsubscriber_schedule &#40;](../../relational-databases/system-stored-procedures/sp-addsubscriber-schedule-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
