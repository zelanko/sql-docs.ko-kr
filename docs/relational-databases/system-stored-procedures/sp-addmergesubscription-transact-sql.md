---
title: sp_addmergesubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addmergesubscription_TSQL
- sp_addmergesubscription
helpviewer_keywords:
- sp_addmergesubscription
ms.assetid: a191d817-0132-49ff-93ca-76f13e609b38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5b319f6065c31a33f30469a73286491c1d641dc3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601121"
---
# <a name="spaddmergesubscription-transact-sql"></a>sp_addmergesubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  밀어넣기 또는 끌어오기 병합 구독을 만듭니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다. 반드시 게시가 이미 존재해야 합니다.  
  
 [  **@subscriber =**] **'***구독자***'**  
 구독자의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 구독 데이터베이스의 이름입니다. *subscriber_db*됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 구독 유형입니다. *subscription_type*됩니다 **nvarchar(15)**, 기본값은 PUSH 사용 하 여 합니다. 하는 경우 **푸시**밀어넣기 구독이 추가 되 고 병합 에이전트가 배포자에서 추가 됩니다. 하는 경우 **끌어오기**, 배포자에서 병합 에이전트를 추가 하지 않고 끌어오기 구독이 추가 됩니다.  
  
> [!NOTE]  
>  익명 구독은 이 저장 프로시저를 사용할 필요가 없습니다.  
  
 [  **@subscriber_type=**] **'***subscriber_type***'**  
 구독자의 유형입니다. *subscriber_type*됩니다 **nvarchar(15)**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**로컬** (기본값)|게시자에게만 알려진 구독자입니다.|  
|**전역**|모든 서버에 알려진 구독자입니다.|  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 로컬 구독은 클라이언트 구독이라고 하며 전역 구독은 서버 구독이라고 합니다.  
  
 [  **@subscription_priority=**] *subscription_priority*  
 구독의 우선 순위를 나타내는 숫자입니다. *subscription_priority*됩니다 **실제**, 기본값은 NULL입니다. 로컬 및 익명 구독의 경우에는 우선 순위가 0.0입니다. 전역 구독의 경우에는 우선 순위가 100.0 미만이어야 합니다.  
  
 [  **@sync_type=**] **'***sync_type***'**  
 구독 동기화 유형입니다. *sync_type*됩니다 **nvarchar(15)**, 기본값은 **자동**합니다. 일 수 있습니다 **자동** 하거나 **none**합니다. 하는 경우 **자동**, 스키마 및 게시 된 테이블의 초기 데이터가 먼저 구독자에 전송 됩니다. 하는 경우 **none**를 구독자에 이미 게시 된 테이블에 대 한 초기 데이터 및 스키마를 가정 합니다. 시스템 테이블 및 데이터는 항상 전송됩니다.  
  
> [!NOTE]  
>  값을 지정 하지 않는 것이 좋습니다 **none**합니다.  
  
 [  **@frequency_type=**] *frequency_type*  
 병합 에이전트가 실행될 시기를 나타내는 값입니다. *frequency_type* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**4**|일별|  
|**8**|매주|  
|**10**|매월|  
|**20**|매월(frequency_interval에 상대적임)|  
|**40**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 시작될 때|  
|NULL(기본값)||  
  
 [  **@frequency_interval=**] *frequency_interval*  
 병합 에이전트가 실행되는 요일입니다. *frequency_interval* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|일요일|  
|**2**|월요일|  
|**3**|화요일|  
|**4**|수요일|  
|**5**|목요일|  
|**6**|금요일|  
|**7**|토요일|  
|**8**|Day|  
|**9**|평일|  
|**10**|주말|  
|NULL(기본값)||  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 예약된 병합이 빈도 간격에 따라 매월 실행되는 시기입니다. *frequency_relative_interval* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|첫째|  
|**2**|둘째|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
|NULL(기본값)||  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor*됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 단위입니다 *frequency_subday_interval*합니다. *frequency_subday* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|둘째|  
|**4**|Minute|  
|**8**|Hour|  
|NULL(기본값)||  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 에 대 한 빈도로 *frequency_subday* 각 병합 간에 발생 합니다. *frequency_subday_interval* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 하루 중에서 병합 에이전트가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 하루 중에서 병합 에이전트가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_start_date=**] *active_start_date*  
 병합 에이전트가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_end_date=**] *active_end_date*  
 병합 에이전트가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 실행할 선택적 명령 프롬프트입니다. *optional_command_line*됩니다 **nvarchar(4000)**, 기본값은 NULL입니다. 이 매개 변수는 출력을 캡처하여 파일로 저장하는 명령을 추가하거나 구성 파일 또는 특성을 지정하는 데 사용됩니다.  
  
 [  **@description=**] **'***설명***'**  
 해당 병합 구독에 대한 간단한 설명입니다. *설명*됩니다 **nvarchar(255)**, 기본값은 NULL입니다. 이 값의 복제 모니터에 의해 표시 됩니다는 **이름을** 모니터링 되는 게시에 대 한 구독을 정렬 하는 열입니다.  
  
 [  **@enabled_for_syncmgr=**] **'***enabled_for_syncmgr***'**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 동기화 관리자를 통해 구독을 동기화할 수 있는지 여부를 지정합니다. *enabled_for_syncmgr* 됩니다 **nvarchar(5)**, 기본값은 FALSE입니다. 하는 경우 **false**의 구독이 동기화 관리자에 등록 되지 않았습니다. 하는 경우 **true**, 구독이 동기화 관리자에 등록 및 시작 하지 않고 동기화 할 수 있습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
 [  **@offloadagent=** ] *remote_agent_activation*  
 에이전트를 원격으로 활성화할 수 있음을 나타냅니다. *remote_agent_activation* 됩니다 **bit** 이며 기본값은 **0**합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전의 스크립트와의 호환성을 위해서만 유지 관리됩니다.  
  
 [  **@offloadserver=** ] **'***remote_agent_server_name***'**  
 원격 에이전트 활성화에 사용할 서버의 네트워크 이름을 지정합니다. *remote_agent_server_name*됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@use_interactive_resolver=** ] **'***use_interactive_resolver***'**  
 대화형 해결을 허용하는 모든 아티클에 대해 충돌을 대화형으로 해결할 수 있도록 합니다. *use_interactive_resolver* 됩니다 **nvarchar(5)**, 기본값은 FALSE입니다.  
  
 [  **@merge_job_name=** ] **'***merge_job_name***'**  
 합니다 *@merge_job_name* 매개 변수는 사용 되지 않으며 설정할 수 없습니다. *merge_job_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [ **@hostname**=] **'***hostname***'**  
 반환 된 값을 재정의 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 매개 변수가 있는 필터의 WHERE 절에이 함수는 사용 하는 경우. *호스트 이름* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  성능상의 이유로 `LEFT([MyColumn]) = SUSER_SNAME()`과 같은 매개 변수가 있는 행 필터 절의 열 이름에는 함수를 적용하지 않는 것이 좋습니다. 사용 하는 경우 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 는 필터 절에 HOST_NAME 값을 재정의 사용 하 여 데이터 형식을 변환 해야 할 수 있습니다 [변환](../../t-sql/functions/cast-and-convert-transact-sql.md)합니다. 이를 위한 최선의 구현 방법은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)로 확장합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergesubscription** 병합 복제에 사용 됩니다.  
  
 때 **sp_addmergesubscription** 의 멤버에 의해 실행 되는 **sysadmin** 고정 서버 역할을 밀어넣기 구독을 만들려면 병합 에이전트 작업이 암시적으로 생성 됩니다 및 실행 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정입니다. 실행 하는 것이 좋습니다 [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) 계정의 다른 에이전트 특정 Windows에 대 한 자격 증명을 지정 하 고 **@job_login** 고 **@job_password**. 자세한 내용은 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergesubscription-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_addmergesubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [대화형 충돌 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_changemergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
