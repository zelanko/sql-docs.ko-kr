---
title: sp_addmergepushsubscription_agent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepushsubscription_agent_TSQL
- sp_addmergepushsubscription_agent
helpviewer_keywords:
- sp_addmergepushsubscription_agent
ms.assetid: 808a1925-be46-4999-8d69-b3a83010ec81
author: stevestein
ms.author: sstein
ms.openlocfilehash: fb74cc0887d68ea01fabe7f6168c0d23275d8f4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68769156"
---
# <a name="sp_addmergepushsubscription_agent-transact-sql"></a>sp_addmergepushsubscription_agent(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  밀어넣기 구독의 동기화를 예약하는 데 사용된 새 에이전트 작업을 병합 게시에 추가합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용 &#40;SQL Server 구성 관리자&#41;을 ](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergepushsubscription_agent [ @publication =] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password = ] 'subscriber_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
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
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`동기화 시 구독자에 연결할 때 사용 하는 보안 모드입니다. *subscriber_security_mode* 은 **int**이며 기본값은 1입니다. **0**인 경우 인증 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 지정 합니다. **1**인 경우 Windows 인증을 지정 합니다.  
  
`[ @subscriber_login = ] 'subscriber_login'`동기화 할 때 구독자에 연결 하는 데 사용할 구독자 로그인입니다. *subscriber_security_mode* 가 **0**으로 설정 된 경우 *subscriber_login* 필요 합니다. *subscriber_login* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_password = ] 'subscriber_password'`인증에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자 암호입니다. *subscriber_security_mode* 가 **0**으로 설정 된 경우 *subscriber_password* 필요 합니다. *subscriber_password* 는 **sysname**이며 기본값은 NULL입니다. 구독자 암호가 사용되는 경우에는 자동으로 암호화됩니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @publisher_security_mode = ] publisher_security_mode`동기화 시 게시자에 연결할 때 사용 하는 보안 모드입니다. *publisher_security_mode* 은 **int**이며 기본값은 1입니다. **0**인 경우 인증 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 지정 합니다. **1**인 경우 Windows 인증을 지정 합니다.  
  
`[ @publisher_login = ] 'publisher_login'`동기화 시 게시자에 연결할 때 사용 하는 로그인입니다. *publisher_login* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @publisher_password = ] 'publisher_password'`게시자에 연결할 때 사용 되는 암호입니다. *publisher_password* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @job_login = ] 'job_login'`에이전트가 실행 되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)** 이며 기본값은 NULL입니다. Windows 계정은 배포자에 대한 에이전트 연결과 Windows 통합 인증 사용 시 구독자 및 게시자에 대한 연결에 항상 사용됩니다.  
  
`[ @job_password = ] 'job_password'`에이전트를 실행 하는 Windows 계정의 암호입니다. *job_password* 는 **sysname**이며 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @job_name = ] 'job_name'`기존 에이전트 작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 구독이 동기화될 경우에만 지정됩니다. **Sysadmin** 고정 서버 역할의 멤버가 아닌 경우 *job_name*을 지정할 때 *job_login* 및 *job_password* 를 지정 해야 합니다.  
  
`[ @frequency_type = ] frequency_type`병합 에이전트 일정을 예약 하는 빈도입니다. *frequency_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|주문형|  
|**4**|매일|  
|**20cm(8**|매주|  
|**x**|매월|  
|**32**|매월 상대적|  
|**64**|자동 시작|  
|**128**|Recurring|  
|NULL(기본값)||  
  
> [!NOTE]  
>  **64** 값을 지정 하면 병합 에이전트 연속 모드로 실행 됩니다. 이는 에이전트에 대 한 **-연속** 매개 변수 설정에 해당 합니다. 자세한 내용은 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)을(를) 참조하세요.  
  
`[ @frequency_interval = ] frequency_interval`병합 에이전트 실행 되는 날짜입니다. *frequency_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|일요일|  
|**2**|월요일|  
|**3**|화요일|  
|**4**|수요일|  
|**5**|목요일|  
|**6**|금요일|  
|**일**|토요일|  
|**20cm(8**|일|  
|**되었는지**|평일|  
|**5-10**|주말|  
|NULL(기본값)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`병합 에이전트 날짜입니다. 이 매개 변수는 *frequency_type* 이 **32** (매월 상대적)로 설정 된 경우에 사용 됩니다. *frequency_relative_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|처음|  
|**2**|Second|  
|**4**|셋째|  
|**20cm(8**|넷째|  
|**x**|마지막|  
|NULL(기본값)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @frequency_subday = ] frequency_subday`정의 된 기간 동안 다시 예약 하는 빈도입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|Second|  
|**4**|분|  
|**20cm(8**|Hour|  
|NULL(기본값)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*에 대 한 간격입니다. *frequency_subday_interval* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중 병합 에이전트 처음으로 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중 병합 에이전트이 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_date = ] active_start_date`병합 에이전트 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_date = ] active_end_date`병합 에이전트가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`Windows 동기화 관리자를 통해 구독을 동기화 할 수 있는지 여부를 지정 합니다. *enabled_for_syncmgr* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **False**이면 구독이 동기화 관리자에 등록 되지 않습니다. **True**이면 구독이 동기화 관리자에 등록 되며를 시작 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]하지 않고 동기화 할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergepushsubscription_agent** 는 병합 복제에 사용 되며 [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)와 유사한 기능을 사용 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepushsubscript_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addmergepushsubscription_agent**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Transact-sql&#41;sp_addmergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [Transact-sql&#41;sp_changemergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
