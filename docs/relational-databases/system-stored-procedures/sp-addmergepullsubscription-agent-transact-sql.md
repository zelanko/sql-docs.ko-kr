---
title: sp_addmergepullsubscription_agent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 69b751dc93ad4512498530ddd99cf4fc8edee62a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826305"
---
# <a name="sp_addmergepullsubscription_agent-transact-sql"></a>sp_addmergepullsubscription_agent(Transact-SQL)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  끌어오기 구독의 동기화를 예약하는 데 사용되는 새 에이전트 작업을 병합 게시에 추가합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @name = ] 'name'`에이전트의 이름입니다. *name* 은 **sysname**이며 기본값은 NULL입니다.  
  
`[ @publisher = ] 'publisher'`게시자 서버의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_security_mode = ] publisher_security_mode`동기화 시 게시자에 연결할 때 사용 하는 보안 모드입니다. *publisher_security_mode* 은 **int**이며 기본값은 1입니다. **0**인 경우 인증을 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **1**인 경우 Windows 인증을 지정 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`동기화 시 게시자에 연결할 때 사용 하는 로그인입니다. *publisher_login* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @publisher_password = ] 'publisher_password'`게시자에 연결할 때 사용 되는 암호입니다. *publisher_password* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @publisher_encrypted_password = ]publisher_encrypted_password`*Publisher_encrypted_password* 설정은 더 이상 지원 되지 않습니다. 이 **비트** 매개 변수를 **1** 로 설정 하려고 하면 오류가 발생 합니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`동기화 시 구독자에 연결할 때 사용 하는 보안 모드입니다. *subscriber_security_mode* 은 **int**이며 기본값은 1입니다. **0**인 경우 인증을 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **1**인 경우 Windows 인증을 지정 합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 병합 에이전트는 항상 Windows 인증을 사용해 로컬 구독자로 연결됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
`[ @subscriber_login = ] 'subscriber_login'`동기화 할 때 구독자에 연결 하는 데 사용할 구독자 로그인입니다. *subscriber_security_mode* 가 **0**으로 설정 된 경우 *subscriber_login* 필요 합니다. *subscriber_login* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
`[ @subscriber_password = ] 'subscriber_password'`인증에 대 한 구독자 암호입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *subscriber_security_mode* 가 **0**으로 설정 된 경우 *subscriber_password* 필요 합니다. *subscriber_password* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
`[ @distributor = ] 'distributor'`배포자의 이름입니다. *배포자* 는 **sysname**이며 기본값은 *게시자*입니다. 즉, 게시자도 배포자입니다.  
  
`[ @distributor_security_mode = ] distributor_security_mode`동기화 할 때 배포자에 연결할 때 사용 하는 보안 모드입니다. *distributor_security_mode* 은 **int**이며 기본값은 0입니다. **0** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지정 합니다. **1** 은 Windows 인증을 지정 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`동기화 할 때 배포자에 연결 하는 데 사용 하는 배포자 로그인입니다. *distributor_security_mode* 가 **0**으로 설정 된 경우 *distributor_login* 필요 합니다. *distributor_login* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @distributor_password = ] 'distributor_password'`배포자 암호입니다. *distributor_security_mode* 가 **0**으로 설정 된 경우 *distributor_password* 필요 합니다. *distributor_password* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @encrypted_password = ] encrypted_password`*Encrypted_password* 설정은 더 이상 지원 되지 않습니다. 이 **비트** 매개 변수를 **1** 로 설정 하려고 하면 오류가 발생 합니다.  
  
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
|**128**|되풀이|  
|NULL(기본값)||  
  
> [!NOTE]  
>  **64** 값을 지정 하면 병합 에이전트 연속 모드로 실행 됩니다. 이는 에이전트에 대 한 **-연속** 매개 변수 설정에 해당 합니다. 자세한 내용은 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)을(를) 참조하세요.  
  
`[ @frequency_interval = ] frequency_interval`병합 에이전트 실행 되는 일 또는 날짜입니다. *frequency_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|일요일|  
|**2**|월요일|  
|**3**|화요일|  
|**4**|수요일|  
|**5**|목요일|  
|**6**|금요일|  
|**7**|토요일|  
|**20cm(8**|일|  
|**9**|평일|  
|**10**|주말|  
|NULL(기본값)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`병합 에이전트 날짜입니다. 이 매개 변수는 *frequency_type* 이 **32** (매월 상대적)로 설정 된 경우에 사용 됩니다. *frequency_relative_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|처음|  
|**2**|초|  
|**4**|셋째|  
|**20cm(8**|넷째|  
|**x**|마지막|  
|NULL(기본값)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @frequency_subday = ] frequency_subday`정의 된 기간 동안 다시 예약 하는 빈도입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|초|  
|**4**|Minute|  
|**20cm(8**|시간|  
|NULL(기본값)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*에 대 한 간격입니다. *frequency_subday_interval* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중 병합 에이전트 처음으로 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중 병합 에이전트이 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_date = ] active_start_date`병합 에이전트 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_date = ] active_end_date`병합 에이전트가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @optional_command_line = ] 'optional_command_line'`는 병합 에이전트에 제공 되는 선택적 명령 프롬프트입니다. *optional_command_line* 은 **nvarchar (255)** 이며 기본값은 ' '입니다. 병합 에이전트에 추가 매개 변수를 제공하는 데 사용할 수 있으며 다음 예에서는 기본 쿼리 제한 시간을 `600`초로 늘립니다.  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
`[ @merge_jobid = ] merge_jobid`작업 ID의 출력 매개 변수입니다. *merge_jobid* 는 **binary (16)** 이며 기본값은 NULL입니다.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`Windows 동기화 관리자를 통해 구독을 동기화 할 수 있는지 여부를 지정 합니다. *enabled_for_syncmgr* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **False**이면 구독이 동기화 관리자에 등록 되지 않습니다. **True**이면 구독이 동기화 관리자에 등록 되며를 시작 하지 않고 동기화 할 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
`[ @ftp_address = ] 'ftp_address'`이전 버전과의 호환성을 위한 것입니다.  
  
`[ @ftp_port = ] ftp_port`이전 버전과의 호환성을 위한 것입니다.  
  
`[ @ftp_login = ] 'ftp_login'`이전 버전과의 호환성을 위한 것입니다.  
  
`[ @ftp_password = ] 'ftp_password'`이전 버전과의 호환성을 위한 것입니다.  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`스냅숏 파일을 선택할 위치를 지정 합니다. *alternate_snapshot_folder* 는 **nvarchar (255)** 이며 기본값은 NULL입니다. NULL인 경우 게시자가 지정한 기본 위치에 스냅샷이 선택됩니다.  
  
`[ @working_directory = ] 'working_directory'`FTP를 사용 하 여 스냅숏 파일을 전송 하는 경우 게시에 대 한 데이터 및 스키마 파일을 임시로 저장 하는 데 사용 되는 작업 디렉터리의 이름입니다. *working_directory* 는 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @use_ftp = ] 'use_ftp'`일반 프로토콜 대신 FTP를 사용 하 여 스냅숏을 검색 하도록 지정 합니다. *use_ftp* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver' ]`대화형 해결 프로그램을 사용 하 여 대화형 해결을 허용 하는 모든 아티클의 충돌을 해결 합니다. *use_interactive_resolver* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다.  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. *Remote_agent_activation* 를 **false** 이외의 값으로 설정 하면 오류가 발생 합니다.  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. *Remote_agent_server_name* 를 NULL이 아닌 값으로 설정 하면 오류가 발생 합니다.  
  
`[ @job_name = ] 'job_name' ]`기존 에이전트 작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 구독이 동기화될 경우에만 지정됩니다. **Sysadmin** 고정 서버 역할의 멤버가 아닌 경우 *job_name*을 지정할 때 *job_login* 및 *job_password* 를 지정 해야 합니다.  
  
`[ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]`필터링 된 데이터 스냅숏을 사용 하는 경우 스냅숏 파일을 읽을 폴더의 경로입니다. *dynamic_snapshot_location* 은 **nvarchar (260)** 이며 기본값은 NULL입니다. 자세한 내용은 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
`[ @use_web_sync = ] use_web_sync`웹 동기화가 사용 하도록 설정 되어 있음을 나타냅니다. *use_web_sync* 은 **bit**이며 기본값은 0입니다. **1** 은 HTTP를 사용 하 여 끌어오기 구독을 인터넷을 통해 동기화 할 수 있도록 지정 합니다.  
  
`[ @internet_url = ] 'internet_url'`복제 수신기 (REPLISAPI)의 위치입니다. DLL)을 동기화 합니다. *internet_url* 은 **nvarchar (260)** 이며 기본값은 NULL입니다. *internet_url* 은 형식의 정규화 된 url입니다 `http://server.domain.com/directory/replisapi.dll` . 서버가 포트 80 이외의 다른 포트에서 수신하도록 구성된 경우 포트 번호도 `http://server.domain.com:portnumber/directory/replisapi.dll` 형식으로 제공되어야 합니다. 여기서 `portnumber`는 포트를 나타냅니다.  
  
`[ @internet_login = ] 'internet_login'`는 HTTP 기본 인증을 사용 하 여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트에서 사용 하는 로그인입니다. *internet_login* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @internet_password = ] 'internet_password'`는 HTTP 기본 인증을 사용 하 여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트 사용 하는 암호입니다. *internet_password* 은 **nvarchar (524)** 이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
`[ @internet_security_mode = ] internet_security_mode`HTTPS를 사용 하 여 웹 동기화 중에 웹 서버에 연결할 때 병합 에이전트에서 사용 하는 인증 방법입니다. *internet_security_mode* 은 **int** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|기본 인증이 사용됩니다.|  
|**1** (기본값)|Windows 통합 인증이 사용됩니다.|  
  
> [!NOTE]  
>  웹 동기화에는 기본 인증을 사용하는 것이 좋습니다. 웹 동기화를 사용 하려면 웹 서버에 대 한 TLS 연결을 설정 해야 합니다. 자세한 내용은 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)을 참조하세요.  
  
`[ @internet_timeout = ] internet_timeout`웹 동기화 요청이 만료 되기 전 까지의 시간 (초)입니다. *internet_timeout* 는 **int**이며 기본값은 **300** 초입니다.  
  
`[ @hostname = ] 'hostname'`매개 변수가 있는 필터의 WHERE 절에서이 함수를 사용 하는 경우 HOST_NAME () 값을 재정의 합니다. *호스트 이름은* **sysname**이며 기본값은 NULL입니다.  
  
`[ @job_login = ] 'job_login'`에이전트가 실행 되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)** 이며 기본값은 없습니다. 이 Windows 계정은 Windows 통합 인증을 사용하는 경우 에이전트를 구독자에 연결하고 배포자 및 게시자에 연결할 때 항상 사용됩니다.  
  
`[ @job_password = ] 'job_password'`에이전트를 실행 하는 Windows 계정의 암호입니다. *job_password* 는 **sysname**이며 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 최상의 보안을 위해 런타임에 로그인 이름과 암호를 제공해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergepullsubscription_agent** 는 병합 복제에 사용 되며 [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)와 유사한 기능을 사용 합니다.  
  
 **Sp_addmergepullsubscription_agent**를 실행할 때 보안 설정을 올바르게 지정 하는 방법에 대 한 예는 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)를 참조 하세요.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addmergepullsubscription_agent**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Transact-sql&#41;sp_addmergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_changemergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
