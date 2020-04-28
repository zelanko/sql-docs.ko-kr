---
title: sp_addsubscriber (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 278af2ca1bd6abdb84cdf2371628c6b95662e46e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73962408"
---
# <a name="sp_addsubscriber-transact-sql"></a>sp_addsubscriber(Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  새 구독자를 게시자에 추가하여 게시한 내용을 받을 수 있도록 합니다. 이 저장 프로시저는 스냅샷 및 트랜잭션 게시를 위한 게시 데이터베이스의 게시자에서 실행됩니다. 원격 배포자를 사용하는 병합 게시의 경우에는 이 저장 프로시저가 배포자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  이 저장 프로시저는 더 이상 사용되지 않습니다. 더 이상 게시자에서 구독자를 명시적으로 등록할 필요가 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addsubscriber [ @subscriber = ] 'subscriber'  
    [ , [ @type = ] type ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @commit_batch_size = ] commit_batch_size ]  
    [ , [ @status_batch_size = ] status_batch_size ]  
    [ , [ @flush_frequency = ] flush_frequency ]  
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
    [ , [ @description = ] 'description' ]  
    [ , [ @security_mode = ] security_mode ]  
    [ , [ @encrypted_password = ] encrypted_password ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @subscriber = ] 'subscriber'`이 서버의 게시에 유효한 구독자로 추가 되는 서버의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @type = ] type`구독자의 유형입니다. *type* 은 **tinyint**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0** (기본값)|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자|  
|**1**|ODBC 데이터 원본 서버|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet 데이터베이스|  
|**3**|OLE DB 공급자|  
  
`[ @login = ] 'login'`인증에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 ID입니다. *login*은 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @password = ] 'password'`인증에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호입니다. *password* 는 **nvarchar (524)** 이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @commit_batch_size = ] commit_batch_size`이 매개 변수는 더 이상 사용 되지 않으며 스크립트의 이전 버전과의 호환성을 위해 유지 관리 됩니다.  
  
> [!NOTE]  
>  값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @status_batch_size = ] status_batch_size`이 매개 변수는 더 이상 사용 되지 않으며 스크립트의 이전 버전과의 호환성을 위해 유지 관리 됩니다.  
  
> [!NOTE]  
>  값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @flush_frequency = ] flush_frequency`이 매개 변수는 더 이상 사용 되지 않으며 스크립트의 이전 버전과의 호환성을 위해 유지 관리 됩니다.  
  
> [!NOTE]  
>  값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @frequency_type = ] frequency_type`복제 에이전트를 예약 하는 빈도입니다. *frequency_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|주문형|  
|**4**|매일|  
|**20cm(8**|매주|  
|**x**|매월|  
|**32**|매월 상대적|  
|**64** (기본값)|자동 시작|  
|**128**|되풀이|  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*에 의해 설정 된 빈도에 적용 되는 값입니다. *frequency_interval* 은 **int**이며 기본값은 1입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`복제 에이전트의 날짜입니다. 이 매개 변수는 *frequency_type* 이 **32** (매월 상대적)로 설정 된 경우에 사용 됩니다. *frequency_relative_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1** (기본값)|처음|  
|**2**|초|  
|**4**|셋째|  
|**20cm(8**|넷째|  
|**x**|마지막|  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 **0**입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @frequency_subday = ] frequency_subday`정의 된 기간 동안 다시 예약 하는 빈도입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|초|  
|**4** (기본값)|Minute|  
|**20cm(8**|Hour|  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*에 대 한 간격입니다. *frequency_subday_interval* 은 **int**이며 기본값은 **5**입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중에서 복제 에이전트가 처음으로 시작 되도록 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 **0**입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중에서 복제 에이전트가 중지 되도록 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day*은 **int**이며 기본값은 235959입니다 .이는 11:59:59 오후을 의미 합니다. 235959입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @active_start_date = ] active_start_date`복제 에이전트가 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 0입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @active_end_date = ] active_end_date`복제 에이전트가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 는 **int**이며 기본값은 9999 년 12 월 31 일을 의미 하는 99991231입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @description = ] 'description'`구독자에 대 한 텍스트 설명입니다. *description* 은 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @security_mode = ] security_mode`는 구현 된 보안 모드입니다. *security_mode* 은 **int**이며 기본값은 1입니다. **0** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지정 합니다. **1** 은 Windows 인증을 지정 합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)를 실행할 때 구독 별로 지정 됩니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
`[ @encrypted_password = ] encrypted_password`이 매개 변수는 더 이상 사용 되지 않으며 이전 버전과의 호환성을 위해서만 *encrypted_password* 값에 대해 제공 되지만 **0** 으로 설정 하면 오류가 발생 합니다.  
  
`[ @publisher = ] 'publisher'`이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정 합니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *publisher* 게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시할 때는 게시자를 사용 하면 안 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addsubscriber** 는 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 구독자에 병합 게시에 대 한 익명 구독만 있는 경우에는 **sp_addsubscriber** 필요 하지 않습니다.  
  
 **sp_addsubscriber** **배포** 데이터베이스의 [MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md) 테이블에 기록 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_addsubscriber**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Transact-sql&#41;sp_changesubscriber &#40;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [Transact-sql&#41;sp_dropsubscriber &#40;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
