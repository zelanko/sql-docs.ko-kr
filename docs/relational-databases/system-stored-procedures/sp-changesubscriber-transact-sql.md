---
title: sp_changesubscriber (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2cd1e4126c1a9da57a6bda6195be78d996e101d7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771379"
---
# <a name="sp_changesubscriber-transact-sql"></a>sp_changesubscriber(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  구독자에 대한 옵션을 변경합니다. 구독자에 대한 모든 배포 태스크가 이 게시자로 업데이트됩니다. 이 저장 프로시저는 배포 데이터베이스의 **MSsubscriber_info** 테이블에 기록 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @subscriber = ] 'subscriber'`옵션을 변경할 구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @type = ] type`구독자 유형입니다. *type* 은 **tinyint**이며 기본값은 NULL입니다. **0** 은 구독자를 나타냅니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **1** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 그렇지 않은 ODBC 데이터 원본 서버 구독자를 지정 합니다.  
  
`[ @login = ] 'login'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인증 로그인 ID입니다. *login*은 **sysname**이며 기본값은 NULL입니다.  
  
`[ @password = ] 'password'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인증 암호입니다. *password* 는 **sysname**이며 기본값은 **%** 입니다. **%** 암호 속성이 변경 되지 않았음을 나타냅니다.  
  
`[ @commit_batch_size = ] commit_batch_size`이전 버전과의 호환성을 위해서만 지원 됩니다.  
  
`[ @status_batch_size = ] status_batch_size`이전 버전과의 호환성을 위해서만 지원 됩니다.  
  
`[ @flush_frequency = ] flush_frequency`이전 버전과의 호환성을 위해서만 지원 됩니다.  
  
`[ @frequency_type = ] frequency_type`배포 태스크를 예약 하는 빈도입니다. *frequency_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|주문형|  
|**4**|매일|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월 상대적|  
|**64**|자동 시작|  
|**128**|되풀이|  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*에 대 한 간격입니다. *frequency_interval* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`배포 작업의 날짜입니다. 이 매개 변수는 *frequency_type* 이 **32** (매월 상대적)로 설정 된 경우에 사용 됩니다. *frequency_relative_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|첫째|  
|**2**|Second|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`지정 된 *frequency_type*동안 배포 작업이 되풀이 되는 빈도입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @frequency_subday = ] frequency_subday`정의 된 기간 동안 다시 예약 하는 빈도입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|Second|  
|**4**|Minute|  
|**8**|시간|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequence_subday*에 대 한 간격입니다. *frequency_subday_interval* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중에서 배포 태스크가 처음으로 시작 되도록 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중에서 배포 태스크가 중지 되도록 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day*은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_date = ] active_start_date`배포 태스크가 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_date = ] active_end_date`배포 태스크가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date*은 **int**이며 기본값은 NULL입니다.  
  
`[ @description = ] 'description'`선택적인 텍스트 설명입니다. *description* 은 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @security_mode = ] security_mode`는 구현 된 보안 모드입니다. *security_mode* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증|  
|**1**|Windows 인증|  
  
`[ @publisher = ] 'publisher'`이외 게시자를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에 대 한 아티클 속성을 변경할 때는 *게시자* 를 사용 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changesubscriber** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_changesubscriber**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addsubscriber &#40;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [Transact-sql&#41;sp_dropsubscriber &#40;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [Transact-sql&#41;sp_helpdistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Transact-sql&#41;sp_helpserver &#40;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Transact-sql&#41;sp_helpsubscriberinfo &#40;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
