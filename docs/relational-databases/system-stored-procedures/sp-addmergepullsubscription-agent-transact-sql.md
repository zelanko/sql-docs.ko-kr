---
title: sp_addmergepullsubscription_agent (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_agent
- sp_addmergepullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addmergepullsubscription_agent
ms.assetid: a2f4b086-078d-49b5-8971-8a1e3f6a6feb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ba75dc83e8fb4ce5a9ad31876b2b2592b22b7197
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791785"
---
# <a name="spaddmergepullsubscriptionagent-transact-sql"></a>sp_addmergepullsubscription_agent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  끌어오기 구독의 동기화를 예약하는 데 사용되는 새 에이전트 작업을 병합 게시에 추가합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergepullsubscription_agent [ [ @name = ] 'name' ]   
        , [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication =] 'publication'   
    [ , [ @publisher_security_mod e= ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher_encrypted_password = ] publisher_encrypted_password ]   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password= ] 'subscriber_password' ]   
    [ , [ @distributor = ] 'distributor' ]   
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @encrypted_password = ] encrypted_password ]   
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
    [ , [ @optional_command_line = ] 'optional_command_line' ]   
    [ , [ @merge_jobid = ] merge_jobid ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]    
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @working_directory = ] 'working_directory' ]   
    [ , [ @use_ftp = ] 'use_ftp' ]   
    [ , [ @reserved = ] 'reserved' ]   
    [ , [ @use_interactive_resolver = ] 'use_interactive_resolver' ]   
    [ , [ @offloadagent = ] 'remote_agent_activation' ]   
    [ , [ @offloadserver = ] 'remote_agent_server_name']   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]  
    [ , [ @use_web_sync = ] use_web_sync ]  
        [ , [ @internet_url = ] 'internet_url' ]  
    [ , [ @internet_login = ] 'internet_login' ]  
        [ , [ @internet_password = ] 'internet_password' ]  
    [ , [ @internet_security_mode = ] internet_security_mode ]  
        [ , [ @internet_timeout = ] internet_timeout ]  
    [ , [ @hostname = ] 'hostname' ]  
        [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>인수  
 [ **@name =** ] **'***name***'**  
 에이전트의 이름입니다. *이름* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@publisher =** ] **'***게시자***'**  
 게시자 서버의 이름입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher_db =** ] **'***publisher_db***'**  
 게시자 데이터베이스의 이름입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@publication =** ] **'***게시***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 동기화 시 게시자에 연결하는 데 사용할 보안 모드입니다. *publisher_security_mode* 됩니다 **int**, 기본값은 1입니다. 하는 경우 **0**, 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. 하는 경우 **1**, Windows 인증을 지정 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login =** ] **'***publisher_login***'**  
 동기화 시 게시자에 연결하는 데 사용할 로그인입니다. *publisher_login* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@publisher_password =** ] **'***publisher_password***'**  
 게시자에 연결할 때 사용하는 암호입니다. *publisher_password* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
 [  **@publisher_encrypted_password =** ]*publisher_encrypted_password*  
 설정 *publisher_encrypted_password* 는 지원 되지 않습니다. 이 설정 하려고 **비트** 매개 변수를 **1** 오류가 발생 합니다.  
  
 [  **@subscriber =** ] **'***구독자***'**  
 구독자의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 구독 데이터베이스의 이름입니다. *subscriber_db* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscriber_security_mode =** ] *subscriber_security_mode*  
 동기화 시 구독자에 연결하는 데 사용할 보안 모드입니다. *subscriber_security_mode* 됩니다 **int**, 기본값은 1입니다. 하는 경우 **0**, 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. 하는 경우 **1**, Windows 인증을 지정 합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 병합 에이전트는 항상 Windows 인증을 사용해 로컬 구독자로 연결됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
 [  **@subscriber_login =** ] **'***subscriber_login***'**  
 동기화 시 구독자에 연결하는 데 사용할 구독자 로그인입니다. *subscriber_login* 필요한 경우 *subscriber_security_mode* 로 설정 되어 **0**합니다. *subscriber_login* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
 [  **@subscriber_password =** ] **'***subscriber_password***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위한 구독자 암호입니다. *subscriber_password* 필요한 경우 *subscriber_security_mode* 로 설정 되어 **0**합니다. *subscriber_password* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
 [  **@distributor =** ] **'***배포자***'**  
 배포자의 이름입니다. *배포자* 됩니다 **sysname**, 기본값은 *게시자*; 즉, 게시자가 배포자 역할도 합니다.  
  
 [  **@distributor_security_mode =** ] *distributor_security_mode*  
 동기화 시 배포자에 연결하는 데 사용할 보안 모드입니다. *distributor_security_mode* 됩니다 **int**, 기본값은 0입니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. **1** Windows 인증을 지정 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login =** ] **'***distributor_login***'**  
 동기화 시 배포자에 연결하는 데 사용할 배포자 로그인입니다. *distributor_login* 필요한 경우 *distributor_security_mode* 로 설정 되어 **0**합니다. *distributor_login* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@distributor_password =** ] **'***distributor_password***'**  
 배포자 암호입니다. *distributor_password* 필요한 경우 *distributor_security_mode* 로 설정 되어 **0**합니다. *distributor_password* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
 [  **@encrypted_password =** ] *encrypted_password*  
 설정 *encrypted_password* 는 지원 되지 않습니다. 이 설정 하려고 **비트** 매개 변수를 **1** 오류가 발생 합니다.  
  
 [  **@frequency_type =** ] *frequency_type*  
 병합 에이전트를 예약하는 빈도입니다. *frequency_type* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
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
|NULL(기본값)||  
  
> [!NOTE]  
>  값을 지정 **64** 하면 병합 에이전트가 연속 모드로 실행 합니다. 이 설정에 해당 하는 **-연속** 에이전트에 대 한 매개 변수입니다. 자세한 내용은 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)을 참조하세요.  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 병합 에이전트가 실행되는 요일입니다. *frequency_interval* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
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
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 병합 에이전트의 날짜입니다. 이 매개 변수를 사용 하면 *frequency_type* 로 설정 된 **32** (매월 상대적)입니다. *frequency_relative_interval* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|첫째|  
|**2**|Second|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
|NULL(기본값)||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 정의된 기간 동안 다시 예약하는 빈도입니다. *frequency_subday* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL(기본값)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 에 대 한 간격인 *frequency_subday*합니다. *frequency_subday_interval* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 하루 중에서 병합 에이전트가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 하루 중에서 병합 에이전트가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [ **@active_start_date =** ] *active_start_date*  
 병합 에이전트가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [ **@active_end_date =** ] *active_end_date*  
 병합 에이전트가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@optional_command_line =** ] **'***optional_command_line***'**  
 병합 에이전트에 제공되는 선택적 명령 프롬프트입니다. *optional_command_line* 됩니다 **nvarchar(255)**, 기본값은 ' '입니다. 병합 에이전트에 추가 매개 변수를 제공하는 데 사용할 수 있으며 다음 예에서는 기본 쿼리 제한 시간을 `600`초로 늘립니다.  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
 [  **@merge_jobid =** ] *merge_jobid*  
 작업 ID의 출력 매개 변수입니다. *merge_jobid* 됩니다 **binary(16)**, 기본값은 NULL입니다.  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 Windows 동기화 관리자를 통해 구독을 동기화할 수 있는지 여부를 지정합니다. *enabled_for_syncmgr* 됩니다 **nvarchar(5)**, 기본값은 FALSE입니다. 하는 경우 **false**의 구독이 동기화 관리자에 등록 되지 않았습니다. 하는 경우 **true**, 구독이 동기화 관리자에 등록 및 시작 하지 않고 동기화 할 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@ftp_port =** ] *ftp_port*  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@alt_snapshot_folder =** ] **'***alternate_snapshot_folder***'**  
 선택할 스냅숏 파일의 위치를 지정합니다. *alternate_snapshot_folder* 됩니다 **nvarchar(255)**, 기본값은 NULL입니다. NULL인 경우 게시자가 지정한 기본 위치에 스냅숏이 선택됩니다.  
  
 [  **@working_directory =** ] **'***working_directory***'**  
 FTP를 사용하여 스냅숏 파일을 전송할 때 게시에 있는 스키마 파일 및 데이터를 임시로 저장하는 데 사용하는 작업 디렉터리의 이름입니다. *working_directory* 됩니다 **nvarchar(255)**, 기본값은 NULL입니다.  
  
 [  **@use_ftp =** ] **'***use_ftp***'**  
 일반 프로토콜 대신 FTP를 사용하여 스냅숏을 검색하도록 지정합니다. *use_ftp* 됩니다 **nvarchar(5)**, 기본값은 FALSE입니다.  
  
 [  **@reserved =** ] **'***예약 된***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@use_interactive_resolver =** ] **'***use_interactive_resolver***'** ]  
 대화형 해결을 허용하는 모든 아티클의 충돌을 해결하기 위해 대화형 해결 프로그램을 사용합니다. *use_interactive_resolver* 됩니다 **nvarchar(5)**, 기본값은 FALSE입니다.  
  
 [  **@offloadagent =** ] **'***remote_agent_activation***'**  
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. 설정 *remote_agent_activation* 이외의 값으로 **false** 오류가 생성 됩니다.  
  
 [  **@offloadserver =** ] **'***remote_agent_server_name***'**  
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. 설정 *remote_agent_server_name* NULL이 아닌 값으로 오류가 생성 됩니다.  
  
 [  **@job_name =** ] **'***job_name***'** ]  
 기존 에이전트 작업의 이름입니다. *job_name* 됩니다 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 구독이 동기화될 경우에만 지정됩니다. 구성원이 아닌 경우는 **sysadmin** 고정 서버 역할을 지정 해야 *job_login* 하 고 *job_password* 지정 하는 경우 *job_name*.  
  
 [  **@dynamic_snapshot_location =** ] **'***dynamic_snapshot_location***'** ]  
 필터링된 데이터 스냅숏을 사용하는 경우에 스냅숏 파일을 읽을 대상 폴더 경로입니다. *dynamic_snapshot_location* 됩니다 **nvarchar(260)**, 기본값은 NULL입니다. 자세한 내용은 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
 [  **@use_web_sync =** ] *use_web_sync*  
 웹 동기화를 사용할 수 있음을 나타냅니다. *use_web_sync* 됩니다 **비트**, 기본값은 0입니다. **1** HTTP를 사용해 인터넷으로 끌어오기 구독을 동기화 할 수 있음을 지정 합니다.  
  
 [  **@internet_url =** ] **'***internet_url***'**  
 웹 동기화용 복제 수신기(REPLISAPI.DLL)의 위치입니다. *internet_url* 됩니다 **nvarchar(260)**, 기본값은 NULL입니다. *internet_url* 형식으로 정규화 된 URL은 `https://server.domain.com/directory/replisapi.dll`합니다. 서버가 포트 80 이외의 다른 포트에서 수신하도록 구성된 경우 포트 번호도 `https://server.domain.com:portnumber/directory/replisapi.dll` 형식으로 제공되어야 합니다. 여기서 `portnumber`는 포트를 나타냅니다.  
  
 [  **@internet_login =** ] **'***internet_login***'**  
 병합 에이전트가 HTTP 기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 사용하는 로그인입니다. *internet_login* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@internet_password =** ] **'***internet_password***'**  
 병합 에이전트가 HTTP 기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 사용하는 암호입니다. *internet_password* 됩니다 **nvarchar(524)**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [  **@internet_security_mode =** ] *internet_security_mode*  
 HTTPS를 사용하여 웹 동기화 동안 웹 서버에 연결할 때 병합 에이전트에서 사용하는 인증 방법입니다. *internet_security_mode* 됩니다 **int** 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|기본 인증이 사용됩니다.|  
|**1** (기본값)|Windows 통합 인증이 사용됩니다.|  
  
> [!NOTE]  
>  웹 동기화에는 기본 인증을 사용하는 것이 좋습니다. 웹 동기화를 사용하려면 웹 서버에 SSL 연결을 해야 합니다. 자세한 내용은 [웹 동기화 구성](../../relational-databases/replication/configure-web-synchronization.md)을 참조하세요.  
  
 [  **@internet_timeout =** ] *internet_timeout*  
 웹 동기화 요청이 만료되기 전까지의 시간(초)입니다. *internet_timeout* 됩니다 **int**, 기본값은 **300** 시간 (초)입니다.  
  
 [  **@hostname =** ] **'***hostname***'**  
 이 함수가 매개 변수가 있는 필터의 WHERE 절에 사용되는 경우 HOST_NAME()의 값보다 우선합니다. *호스트 이름* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@job_login =** ] **'***job_login***'**  
 에이전트 실행에 사용되는 Windows 계정의 로그인입니다. *job_login* 됩니다 **nvarchar(257)**, 기본값은 없습니다. 이 Windows 계정은 Windows 통합 인증을 사용하는 경우 에이전트를 구독자에 연결하고 배포자 및 게시자에 연결할 때 항상 사용됩니다.  
  
 [  **@job_password =** ] **'***job_password***'**  
 에이전트 실행에 사용되는 Windows 계정의 암호입니다. *job_password* 됩니다 **sysname**, 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 최상의 보안을 위해 런타임에 로그인 이름과 암호를 제공해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergepullsubscription_agent** 병합 복제에 사용 되 고와 유사한 기능을 사용 하 여 [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)합니다.  
  
 실행할 때 보안 설정이 올바르게 지정 하는 방법의 예 **sp_addmergepullsubscription_agent**를 참조 하십시오 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_addmergepullsubscription_agent**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
