---
title: sp_changesubscriber (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1f31a00e0c42bc56dffac191ff9a934bb77b95df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62997804"
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  구독자에 대한 옵션을 변경합니다. 구독자에 대한 모든 배포 태스크가 이 게시자로 업데이트됩니다. 이 저장된 프로시저를 기록 합니다 **MSsubscriber_info** 배포 데이터베이스의 테이블입니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @subscriber = ] 'subscriber'` 옵션을 변경 하는 구독자의 이름이입니다. *구독자* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @type = ] type` 구독자 유형이입니다. *형식* 됩니다 **tinyint**, 기본값은 NULL입니다. **0** 나타냅니다는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다. **1** 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 기타 ODBC 데이터 원본 서버 구독자입니다.  
  
`[ @login = ] 'login'` 가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 id입니다. *login*은 **sysname**이며 기본값은 NULL입니다.  
  
`[ @password = ] 'password'` 가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 암호입니다. *암호* 됩니다 **sysname**, 기본값은 **%** 합니다. **%** 암호 속성이 변경 사항이 없는 것을 나타냅니다.  
  
`[ @commit_batch_size = ] commit_batch_size` 이전 버전과 호환성을 위해서만 지원 합니다.  
  
`[ @status_batch_size = ] status_batch_size` 이전 버전과 호환성을 위해서만 지원 합니다.  
  
`[ @flush_frequency = ] flush_frequency` 이전 버전과 호환성을 위해서만 지원 합니다.  
  
`[ @frequency_type = ] frequency_type` 배포 태스크를 예약 하는 빈도입니다. *frequency_type* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|요청 시|  
|**4**|일별|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월 상대적|  
|**64**|자동 시작|  
|**128**|되풀이|  
  
`[ @frequency_interval = ] frequency_interval` 에 대 한 간격인 *frequency_type*합니다. *frequency_interval* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 배포 태스크 날짜가입니다. 이 매개 변수를 사용 하면 *frequency_type* 로 설정 된 **32** (매월 상대적)입니다. *frequency_relative_interval* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|첫째|  
|**2**|Second|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 배포 작업 기간 동안 정의 된 되풀이 되는 얼마나 자주 *frequency_type*합니다. *frequency_recurrence_factor* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @frequency_subday = ] frequency_subday` 정의 된 기간 동안 다시 예약 하는 빈도 방법이입니다. *frequency_subday* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 에 대 한 간격인 *frequence_subday*합니다. *frequency_subday_interval* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 배포 태스크가 처음 하루 중 시간 예약 됩니다, hhmmss 형식. *active_start_time_of_day* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 배포 태스크가 중지 되 면 시간 예약 된 형식은 HHMMSS입니다. *active_end_time_of_day*됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @active_start_date = ] active_start_date` 배포 태스크의 경우 첫 번째 예약 된 날짜 이며 YYYYMMDD 형식으로. *active_start_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @active_end_date = ] active_end_date` 배포 태스크가 중지 되 면 날짜 예약 된 형식은 YYYYMMDD입니다. *active_end_date*됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @description = ] 'description'` 선택적인 텍스트 설명이입니다. *설명* 됩니다 **nvarchar(255)**, 기본값은 NULL입니다.  
  
`[ @security_mode = ] security_mode` 구현 된 보안 모드가입니다. *security_mode* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증|  
|**1**|Windows 인증|  
  
`[ @publisher = ] 'publisher'` 지정 된 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에서 아티클 속성을 변경 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_changesubscriber** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_changesubscriber**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_addsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
