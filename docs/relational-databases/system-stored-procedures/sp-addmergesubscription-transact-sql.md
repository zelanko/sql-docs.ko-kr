---
title: sp_addmergesubscription (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergesubscription_TSQL
- sp_addmergesubscription
helpviewer_keywords:
- sp_addmergesubscription
ms.assetid: a191d817-0132-49ff-93ca-76f13e609b38
author: stevestein
ms.author: sstein
ms.openlocfilehash: b501a2c06a6d9e8e3573ef5d5814c3318c4e623b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68769131"
---
# <a name="sp_addmergesubscription-transact-sql"></a>sp_addmergesubscription(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  밀어넣기 또는 끌어오기 병합 구독을 만듭니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergesubscription [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @subscriber_type= ] 'subscriber_type' ]  
    [ , [ @subscription_priority= ] subscription_priority ]  
    [ , [ @sync_type= ] 'sync_type' ]  
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
    [ , [ @optional_command_line= ] 'optional_command_line' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @use_interactive_resolver= ] 'use_interactive_resolver' ]  
    [ , [ @merge_job_name= ] 'merge_job_name' ]  
    [ , [ @hostname = ] 'hostname'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다. 반드시 게시가 이미 존재해야 합니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscription_type = ] 'subscription_type'`구독의 유형입니다. *subscription_type*은 **nvarchar (15)** 이며 기본값은 PUSH입니다. **밀어넣기**인 경우 밀어넣기 구독을 추가 하 고 병합 에이전트를 배포자에 추가 합니다. **Pull**인 경우 배포자에 병합 에이전트를 추가 하지 않고 끌어오기 구독을 추가 합니다.  
  
> [!NOTE]  
>  익명 구독은 이 저장 프로시저를 사용할 필요가 없습니다.  
  
`[ @subscriber_type = ] 'subscriber_type'`구독자의 유형입니다. *subscriber_type*은 **nvarchar (15)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**local** (기본값)|게시자에게만 알려진 구독자입니다.|  
|**전역적**|모든 서버에 알려진 구독자입니다.|  
  
 
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 로컬 구독은 클라이언트 구독이라고 하며 전역 구독은 서버 구독이라고 합니다.  
  
`[ @subscription_priority = ] subscription_priority`구독의 우선 순위를 나타내는 숫자입니다. *subscription_priority*은 **실제**이며 기본값은 NULL입니다. 로컬 및 익명 구독의 경우에는 우선 순위가 0.0입니다. 전역 구독의 경우에는 우선 순위가 100.0 미만이어야 합니다.  
  
`[ @sync_type = ] 'sync_type'`구독 동기화 유형입니다. *sync_type*은 **nvarchar (15)** 이며 기본값은 **automatic**입니다. **자동** 또는 **없음**일 수 있습니다. **Automatic**인 경우 게시 된 테이블의 스키마 및 초기 데이터가 먼저 구독자로 전송 됩니다. 없으면 **구독자**에 게시 된 테이블에 대 한 스키마 및 초기 데이터가 이미 있다고 가정 합니다. 시스템 테이블 및 데이터는 항상 전송됩니다.  
  
> [!NOTE]  
>  **None**값을 지정 하지 않는 것이 좋습니다.  
  
`[ @frequency_type = ] frequency_type`병합 에이전트 실행 되는 시기를 나타내는 값입니다. *frequency_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**4**|매일|  
|**20cm(8**|매주|  
|**5-10**|매월|  
|**20**|매월(frequency_interval에 상대적임)|  
|**40**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 시작될 때|  
|NULL(기본값)||  
  
`[ @frequency_interval = ] frequency_interval`병합 에이전트 실행 되는 일 또는 날짜입니다. *frequency_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
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
  
`[ @frequency_relative_interval = ] frequency_relative_interval`예약 된 병합 발생 빈도 간격 (월)입니다. *frequency_relative_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|처음|  
|**2**|Second|  
|**4**|셋째|  
|**20cm(8**|넷째|  
|**x**|마지막|  
|NULL(기본값)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor*은 **int**이며 기본값은 NULL입니다.  
  
`[ @frequency_subday = ] frequency_subday`는 *frequency_subday_interval*단위입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|Second|  
|**4**|분|  
|**20cm(8**|Hour|  
|NULL(기본값)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`각 병합 사이에 *frequency_subday* 발생 하는 빈도입니다. *frequency_subday_interval* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중 병합 에이전트 처음으로 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중 병합 에이전트이 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_date = ] active_start_date`병합 에이전트 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_date = ] active_end_date`병합 에이전트가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @optional_command_line = ] 'optional_command_line'`실행할 선택적인 명령 프롬프트입니다. *optional_command_line*은 **nvarchar (4000)** 이며 기본값은 NULL입니다. 이 매개 변수는 출력을 캡처하여 파일로 저장하는 명령을 추가하거나 구성 파일 또는 특성을 지정하는 데 사용됩니다.  
  
`[ @description = ] 'description'`는이 병합 구독에 대 한 간단한 설명입니다. *description*은 **nvarchar (255)** 이며 기본값은 NULL입니다. 이 값은 모니터링 되는 게시에 대 한 구독을 정렬 하는 데 사용할 수 있는 **이름** 열의 복제 모니터에 의해 표시 됩니다.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`Windows 동기화 관리자를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 구독을 동기화 할 수 있는지 여부를 지정 합니다. *enabled_for_syncmgr* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **False**이면 구독이 동기화 관리자에 등록 되지 않습니다. **True**이면 구독이 동기화 관리자에 등록 되며를 시작 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]하지 않고 동기화 할 수 있습니다.  
  
`[ @offloadagent = ] remote_agent_activation`에이전트를 원격으로 활성화할 수 있도록 지정 합니다. *remote_agent_activation* 은 **bit** 이며 기본값은 **0**입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전의 스크립트와의 호환성을 위해서만 유지 관리됩니다.  
  
`[ @offloadserver = ] 'remote_agent_server_name'`원격 에이전트 활성화에 사용할 서버의 네트워크 이름을 지정 합니다. *remote_agent_server_name*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver'`대화형 해결을 허용 하는 모든 아티클에 대해 대화형으로 충돌을 해결할 수 있습니다. *use_interactive_resolver* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다.  
  
`[ @merge_job_name = ] 'merge_job_name'`Merge_job_name 매개 변수는 더 이상 사용 되지 않으며 설정할 수 없습니다. * \@* *merge_job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @hostname = ] 'hostname'`매개 변수가 있는 필터의 WHERE 절에서이 함수를 사용 하는 경우 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 에서 반환 하는 값을 재정의 합니다. *호스트 이름은* **sysname**이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  성능상의 이유로 `LEFT([MyColumn]) = SUSER_SNAME()`과 같은 매개 변수가 있는 행 필터 절의 열 이름에는 함수를 적용하지 않는 것이 좋습니다. 필터 절에 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 를 사용 하 고 HOST_NAME 값을 재정의 하는 경우 [convert](../../t-sql/functions/cast-and-convert-transact-sql.md)를 사용 하 여 데이터 형식을 변환 해야 할 수 있습니다. 이를 위한 최선의 구현 방법은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)항목의 "HOST_NAME() 값 재정의" 섹션을 참조하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergesubscription** 는 병합 복제에 사용 됩니다.  
  
 **Sysadmin** 고정 서버 역할의 멤버가 밀어넣기 구독을 만들기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sp_addmergesubscription** 를 실행 하면 병합 에이전트 작업이 암시적으로 만들어지고 에이전트 서비스 계정에서 실행 됩니다. [Sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) 를 실행 하 고 ** \@job_login** 및 ** \@job_password**에 대 한 다른 에이전트 특정 Windows 계정의 자격 증명을 지정 하는 것이 좋습니다. 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergesubscription-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addmergesubscription**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [대화형 충돌 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Transact-sql&#41;sp_changemergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
