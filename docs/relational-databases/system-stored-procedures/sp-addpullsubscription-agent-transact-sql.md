---
title: sp_addpullsubscription_agent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpullsubscription_agent
- sp_addpullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addpullsubscription_agent
ms.assetid: b9c2eaed-6d2d-4b78-ae9b-73633133180b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 01f076673491978739ff96d791a41d0927c4ddb6
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769125"
---
# <a name="spaddpullsubscriptionagent-transact-sql"></a>sp_addpullsubscription_agent(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
 
  끌어오기 구독을 동기화하는 데 사용하는 새로 예약된 에이전트 작업을 트랜잭션 게시에 추가합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addpullsubscription_agent [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]          , [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor = ] 'distributor' ]  
    [ , [ @distribution_db = ] 'distribution_db' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]  
    [ , [ @distributor_login = ] 'distributor_login' ]  
    [ , [ @distributor_password = ] 'distributor_password' ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
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
    [ , [ @distribution_jobid = ] distribution_jobid OUTPUT ]  
    [ , [ @encrypted_distributor_password = ] encrypted_distributor_password ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port = ] ftp_port ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]  
    [ , [ @working_directory = ] 'working_directory' ]  
    [ , [ @use_ftp = ] 'use_ftp' ]  
    [ , [ @publication_type = ] publication_type ]  
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @offloadagent = ] 'remote_agent_activation' ]  
    [ , [ @offloadserver = ] 'remote_agent_server_name']  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'_`게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 NULL입니다. *publisher_db* 는 Oracle 게시자가 무시 합니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`동기화 시 구독자에 연결할 때 사용 하는 보안 모드입니다. *subscriber_security_mode* 은 **int** 이며 기본값은 NULL입니다. **0** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지정 합니다. **1** 은 Windows 인증을 지정 합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 배포 에이전트는 항상 Windows 인증을 사용하여 로컬 구독자에 연결합니다. 이 매개 변수에 NULL 또는 **1** 이 아닌 값을 지정 하면 경고 메시지가 반환 됩니다.  
  
`[ @subscriber_login = ] 'subscriber_login'`동기화 할 때 구독자에 연결 하는 데 사용할 구독자 로그인입니다. *subscriber_login* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
`[ @subscriber_password = ] 'subscriber_password'`구독자 암호입니다. *subscriber_security_mode* 가 **0**으로 설정 된 경우 *subscriber_password* 가 필요 합니다. *subscriber_password* 는 **sysname**이며 기본값은 NULL입니다. 구독자 암호가 사용되는 경우에는 자동으로 암호화됩니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
`[ @distributor = ] 'distributor'`배포자의 이름입니다. *배포자* 는 **sysname**이며 기본값은 *게시자*가 지정한 값입니다.  
  
`[ @distribution_db = ] 'distribution_db'`배포 데이터베이스의 이름입니다. *distribution_db* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @distributor_security_mode = ] distributor_security_mode`동기화 할 때 배포자에 연결할 때 사용 하는 보안 모드입니다. *distributor_security_mode* 은 **int**이며 기본값은 **1**입니다. **0** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지정 합니다. **1** 은 Windows 인증을 지정 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`동기화 할 때 배포자에 연결 하는 데 사용 하는 배포자 로그인입니다. *distributor_security_mode* 가 **0**으로 설정 된 경우 *distributor_login* 가 필요 합니다. *distributor_login* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @distributor_password = ] 'distributor_password'`배포자 암호입니다. *distributor_security_mode* 가 **0**으로 설정 된 경우 *distributor_password* 가 필요 합니다. *distributor_password* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요. 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @optional_command_line = ] 'optional_command_line'`배포 에이전트에 제공 되는 선택적 명령 프롬프트입니다. 예를 들어 **-definitionfile** C:\distdef.txt 또는 **-commitbatchsize** 10입니다. *optional_command_line* 는 **nvarchar (4000)** 이며 기본값은 빈 문자열입니다.  
  
`[ @frequency_type = ] frequency_type`배포 에이전트 일정을 예약 하는 빈도입니다. *frequency_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2** (기본값)|요청 시|  
|**4**|일별|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월 상대적|  
|**64**|자동 시작|  
|**128**|되풀이|  
  
> [!NOTE]  
>  **64** 값을 지정 하면 배포 에이전트 연속 모드로 실행 됩니다. 이는 에이전트에 대 한 **-연속** 매개 변수 설정에 해당 합니다. 자세한 내용은 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)을 참조하세요.  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*에 의해 설정 된 빈도에 적용 되는 값입니다. *frequency_interval* 은 **int**이며 기본값은 1입니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`배포 에이전트 날짜입니다. 이 매개 변수는 *frequency_type* 이 **32** (매월 상대적)로 설정 된 경우에 사용 됩니다. *frequency_relative_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1** (기본값)|첫째|  
|**2**|Second|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 **1**입니다.  
  
`[ @frequency_subday = ] frequency_subday`정의 된 기간 동안 다시 예약 하는 빈도입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1** (기본값)|한 번|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*에 대 한 간격입니다. *frequency_subday_interval* 은 **int**이며 기본값은 **1**입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중 배포 에이전트 처음으로 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중 배포 에이전트이 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @active_start_date = ] active_start_date`배포 에이전트 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @active_end_date = ] active_end_date`배포 에이전트가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @distribution_jobid = ] _distribution_jobidOUTPUT`이 작업에 대 한 배포 에이전트 ID입니다. *distribution_jobid* 는 **binary (16)** 이며 기본값은 NULL이 고 출력 매개 변수입니다.  
  
`[ @encrypted_distributor_password = ] encrypted_distributor_password`*Encrypted_distributor_password* 설정은 더 이상 지원 되지 않습니다. 이 **비트** 매개 변수를 **1** 로 설정 하려고 하면 오류가 발생 합니다.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`동기화 관리자를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 구독을 동기화 할 수 있는지 여부입니다. *enabled_for_syncmgr* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **False**이면 구독이 동기화 관리자에 등록 되지 않습니다. **True**이면 구독이 동기화 관리자에 등록 되며를 시작 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]하지 않고 동기화 할 수 있습니다.  
  
`[ @ftp_address = ] 'ftp_address'`이전 버전과의 호환성을 위한 것입니다.  
  
`[ @ftp_port = ] ftp_port`이전 버전과의 호환성을 위한 것입니다.  
  
`[ @ftp_login = ] 'ftp_login'`이전 버전과의 호환성을 위한 것입니다.  
  
`[ @ftp_password = ] 'ftp_password'`이전 버전과의 호환성을 위한 것입니다.  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'_`스냅숏에 대 한 대체 폴더의 위치를 지정 합니다. *alternate_snapshot_folder* 는 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @working_directory = ] 'working_director'`게시에 대 한 데이터 및 스키마 파일을 저장 하는 데 사용 되는 작업 디렉터리의 이름입니다. *working_directory* 는 **nvarchar (255)** 이며 기본값은 NULL입니다. 이름은 UNC 형식으로 지정해야 합니다.  
  
`[ @use_ftp = ] 'use_ftp'`일반 프로토콜 대신 FTP를 사용 하 여 스냅숏을 검색 하도록 지정 합니다. *use_ftp* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다.  
  
`[ @publication_type = ] publication_type`게시의 복제 유형을 지정 합니다. *publication_type* 은 **tinyint** 이며 기본값은 **0**입니다. **0**인 경우 게시는 트랜잭션 유형입니다. **1**인 경우 게시는 스냅숏 유형입니다. **2**인 경우 게시가 병합 유형입니다.  
  
`[ @dts_package_name = ] 'dts_package_name'`DTS 패키지의 이름을 지정 합니다. *dts_package_name* 는 **sysname** 이며 기본값은 NULL입니다. 예를 들어 `DTSPub_Package`의 패키지를 지정하려면 매개 변수가 `@dts_package_name = N'DTSPub_Package'`여야 합니다.  
  
`[ @dts_package_password = ] 'dts_package_password'`패키지에 대 한 암호를 지정 합니다 (있는 경우). *dts_package_password* 는 **sysname** 이며 기본값은 NULL입니다. 즉, 암호는 패키지에 없습니다.  
  
> [!NOTE]  
>  *Dts_package_name* 가 지정 된 경우 암호를 지정 해야 합니다.  
  
`[ @dts_package_location = ] 'dts_package_location'`패키지 위치를 지정 합니다. *dts_package_location* 은 **nvarchar (12)** 이며 기본값은 **subscriber**입니다. 패키지의 위치는 **배포자** 또는 **구독자**일 수 있습니다.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. *Remote_agent_activation* 를 **false** 이외의 값으로 설정 하면 오류가 발생 합니다.  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. *Remote_agent_server_name* 를 NULL이 아닌 값으로 설정 하면 오류가 발생 합니다.  
  
`[ @job_name = ] 'job_name'`기존 에이전트 작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 구독이 동기화될 경우에만 지정됩니다. **Sysadmin** 고정 서버 역할의 멤버가 아닌 경우 *job_name*을 지정할 때 *job_login* 및 *job_password* 를 지정 해야 합니다.  
  
`[ @job_login = ] 'job_login'`에이전트가 실행 되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)** 이며 기본값은 없습니다. 이 Windows 계정은 에이전트가 구독자에 연결할 때 항상 사용됩니다.  
  
`[ @job_password = ] 'job_password'`에이전트를 실행 하는 Windows 계정의 암호입니다. *job_password* 는 **sysname**이며 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addpullsubscription_agent** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-a_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만이 **sp_addpullsubscription_agent**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
