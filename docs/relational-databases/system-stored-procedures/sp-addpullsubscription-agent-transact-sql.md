---
title: sp_addpullsubscription_agent (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addpullsubscription_agent
- sp_addpullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addpullsubscription_agent
ms.assetid: b9c2eaed-6d2d-4b78-ae9b-73633133180b
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 82689b234a6294ef4c13c801ba88a7d700b0db44
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddpullsubscriptionagent-transact-sql"></a>sp_addpullsubscription_agent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
 
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
 [ **@publisher=**] **'***publisher***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher_db=**] **' * * * publisher_db'*  
 게시자 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 NULL입니다. *publisher_db* Oracle 게시자에 의해 무시 됩니다.  
  
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@subscriber=**] **'***구독자***'**  
 구독자의 이름입니다. *구독자* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다.  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 구독 데이터베이스의 이름입니다. *subscriber_db* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다.  
  
 [  **@subscriber_security_mode=**] *subscriber_security_mode*  
 동기화 시 구독자에 연결하는 데 사용할 보안 모드입니다. *subscriber_security_mode* 은 **int,** 기본값은 NULL입니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. **1** Windows 인증을 지정 합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 배포 에이전트는 항상 Windows 인증을 사용하여 로컬 구독자에 연결합니다. NULL이 아닌 값 또는 **1** 지정이 매개 변수에 대 한 경고 메시지가 반환 됩니다.  
  
 [  **@subscriber_login =**] **'***subscriber_login***'**  
 동기화 시 구독자에 연결할 때 사용할 구독자 로그인이입니다. *subscriber_login* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
 [  **@subscriber_password=**] **'***subscriber_password***'**  
 구독자 암호입니다. *subscriber_password* 경우 필요한 *subscriber_security_mode* 로 설정 된 **0**합니다. *subscriber_password* 은 **sysname**, 기본값은 NULL입니다. 구독자 암호가 사용되는 경우에는 자동으로 암호화됩니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
 [  **@distributor=**] **'***배포자***'**  
 배포자의 이름입니다. *배포자* 은 **sysname**, 기본값에 지정 된 값은 *게시자*합니다.  
  
 [  **@distribution_db=**] **'***distribution_db***'**  
 배포 데이터베이스의 이름입니다. *distribution_db* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@distributor_security_mode=**] *distributor_security_mode*  
 동기화 시 배포자에 연결하는 데 사용할 보안 모드입니다. *distributor_security_mode* 은 **int**, 기본값은 **1**합니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. **1** Windows 인증을 지정 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login=**] **'***distributor_login***'**  
 동기화 시 배포자에 연결하는 데 사용할 배포자 로그인입니다. *distributor_login* 경우 필요한 *distributor_security_mode* 로 설정 된 **0**합니다. *distributor_login* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@distributor_password =**] **'***distributor_password***'**  
 배포자 암호입니다. *distributor_password* 경우 필요한 *distributor_security_mode* 로 설정 된 **0**합니다. *distributor_password* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요. 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 배포 에이전트에 공급되는 선택적 명령 프롬프트입니다. 예를 들어 **-DefinitionFile** C:\Distdef.txt 또는 **-CommitBatchSize** 10입니다. *optional_command_line* 은 **nvarchar (4000)**, 기본값은 빈 문자열입니다.  
  
 [  **@frequency_type=**] *frequency_type*  
 배포 에이전트를 예약하는 빈도입니다. *frequency_type* 은 **int**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|설명|  
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
>  값을 지정 **64** 하면 배포 에이전트가 연속 모드로 실행 되도록 합니다. 이 설정에 해당 하는 **-연속** 에이전트에 대 한 매개 변수입니다. 자세한 내용은 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)을 참조하세요.  
  
 [  **@frequency_interval=**] *frequency_interval*  
 값 설정 된 빈도에 적용 하려면 *frequency_type*합니다. *frequency_interval* 은 **int**, 기본값은 1입니다.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 배포 에이전트의 날짜입니다. 이 매개 변수는 때 *frequency_type* 로 설정 된 **32** (매월 상대)입니다. *frequency_relative_interval* 은 **int**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**1** (기본값)|첫째|  
|**2**|둘째|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor* 은 **int**, 기본값은 **1**합니다.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 정의된 기간 동안 다시 예약하는 빈도입니다. *frequency_subday* 은 **int**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**1** (기본값)|한 번|  
|**2**|둘째|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 에 대 한 간격인 *frequency_subday*합니다. *frequency_subday_interval* 은 **int**, 기본값은 **1**합니다.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 하루 중에서 배포 에이전트가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 은 **int**, 기본값은 **0**합니다.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 하루 중에서 배포 에이전트가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day* 은 **int**, 기본값은 **0**합니다.  
  
 [  **@active_start_date=**] *active_start_date*  
 배포 에이전트가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 은 **int**, 기본값은 **0**합니다.  
  
 [  **@active_end_date=**] *active_end_date*  
 배포 에이전트가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date* 은 **int**, 기본값은 **0**합니다.  
  
 [  **@distribution_jobid =**] *distribution_jobid * * * 출력**  
 이 작업의 배포 에이전트 ID입니다. *distribution_jobid* 은 **binary (16)**, 기본값은 null 이며 출력 매개 변수입니다.  
  
 [  **@encrypted_distributor_password=**] *encrypted_distributor_password*  
 설정 *encrypted_distributor_password* 더 이상 지원 합니다. 이 설정 하는 **비트** 매개 변수를 **1** 에서 오류가 발생 합니다.  
  
 [  **@enabled_for_syncmgr=**] **'***enabled_for_syncmgr***'**  
 구독을 통해 동기화 할 수 있는지 여부는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 동기화 관리자입니다. *enabled_for_syncmgr* 은 **nvarchar (5)**, 기본값은 FALSE입니다. 경우 **false**의 구독이 동기화 관리자에 등록 되지 않습니다. 경우 **true**, 구독이 동기화 관리자에 등록 및 시작 하지 않고 동기화 할 수 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
 [  **@ftp_address=**] **'***ftp_address***'**  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@ftp_port=**] *ftp_port*  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@ftp_login=**] **'***ftp_login***'**  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@ftp_password=**] **'***ftp_password***'**  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@alt_snapshot_folder=** ] **' * * * alternate_snapshot_folder'*  
 스냅숏의 대체 폴더 위치를 지정합니다. *alternate_snapshot_folder* 은 **nvarchar (255)**, 기본값은 NULL입니다.  
  
 [ **@working_directory**=] **'***working_director***'**  
 게시용 데이터 및 스키마 파일을 저장하기 위해 사용하는 작업 디렉터리의 이름입니다. *working_directory* 은 **nvarchar (255)**, 기본값은 NULL입니다. 이름은 UNC 형식으로 지정해야 합니다.  
  
 [ **@use_ftp**=] **'***use_ftp***'**  
 일반 프로토콜 대신 FTP를 사용하여 스냅숏을 검색하도록 지정합니다. *use_ftp* 은 **nvarchar (5)**, 기본값은 FALSE입니다.  
  
 [ **@publication_type**=] *publication_type*  
 게시의 복제 유형을 지정합니다. *publication_type* 는 **tinyint** 기본값인 **0**합니다. 경우 **0**, 게시는 트랜잭션 유형입니다. 경우 **1**, 게시는 스냅숏 유형입니다. 경우 **2**, 게시는 병합 유형입니다.  
  
 [ **@dts_package_name**=] **'***dts_package_name***'**  
 DTS 패키지의 이름을 지정합니다. *dts_package_name* 는 **sysname** 기본값은 NULL입니다. 예를 들어 `DTSPub_Package`의 패키지를 지정하려면 매개 변수가 `@dts_package_name = N'DTSPub_Package'`여야 합니다.  
  
 [ **@dts_package_password**=] **'***dts_package_password***'**  
 패키지의 암호를 지정합니다. *dts_package_password* 은 **sysname** 이며 기본값은 NULL 의미 하는 패키지에 암호가 없습니다.  
  
> [!NOTE]  
>  경우에 암호를 지정 해야 *dts_package_name* 지정 됩니다.  
  
 [ **@dts_package_location**=] **'***dts_package_location***'**  
 패키지 위치를 지정합니다. *dts_package_location* 는 **nvarchar (12)**, 기본값은 **구독자**합니다. 패키지의 위치 일 수 있습니다 **배포자** 또는 **구독자**합니다.  
  
 [ **@reserved**=] **'***예약***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@offloadagent**=] '*remote_agent_activation*'  
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. 설정 *remote_agent_activation* 이외의 다른 값으로 **false** 오류가 생성 됩니다.  
  
 [ **@offloadserver**=] '*remote_agent_server_name*'  
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. 설정 *remote_agent_server_name* NULL이 아닌 값으로 오류가 생성 됩니다.  
  
 [ **@job_name**=] '*job_name*'  
 기존 에이전트 작업의 이름입니다. *job_name* 은 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 구독이 동기화될 경우에만 지정됩니다. 구성원이 아닌 경우는 **sysadmin** 고정 서버 역할을 지정 해야 *job_login* 및 *job_password* 지정 하는 경우 *job_name*.  
  
 [ **@job_login**=] **'***job_login***'**  
 에이전트 실행에 사용되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)**, 기본값은 없습니다. 이 Windows 계정은 에이전트가 구독자에 연결할 때 항상 사용됩니다.  
  
 [ **@job_password**=] **'***job_password***'**  
 에이전트 실행에 사용되는 Windows 계정의 암호입니다. *job_password* 은 **sysname**, 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_addpullsubscription_agent** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_addpullsubscription_agent**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
