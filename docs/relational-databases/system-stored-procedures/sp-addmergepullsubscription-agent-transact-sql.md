---
title: sp_addmergepullsubscription_agent (거래 -SQL) | 마이크로 소프트 문서
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 07cc514d615c86a90dcf37fbd4748c3ab1776f06
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528977"
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
`[ @name = ] 'name'`에이전트의 이름입니다. *이름은* **sysname**, NULL의 기본값입니다.  
  
`[ @publisher = ] 'publisher'`게시자 서버의 이름입니다. *게시자는* **sysname입니다.**  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db* **sysname이며**기본값은 없습니다.  
  
`[ @publication = ] 'publication'`발행물의 이름입니다. *발행물은* **sysname이며**기본값은 없습니다.  
  
`[ @publisher_security_mode = ] publisher_security_mode`동기화할 때 게시자에 연결할 때 사용할 보안 모드입니다. *publisher_security_mode* 기본값은 1인 **int입니다.** 경우 **0은**인증을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정합니다. 경우 **1은**Windows 인증을 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`동기화할 때 게시자에 연결할 때 사용할 로그인입니다. *publisher_login* **sysname이며**기본값은 NULL입니다.  
  
`[ @publisher_password = ] 'publisher_password'`게시자에 연결할 때 사용되는 암호입니다. *publisher_password* **sysname이며**기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @publisher_encrypted_password = ]publisher_encrypted_password`*publisher_encrypted_password* 설정은 더 이상 지원되지 않습니다. 이 **비트** 매개 변수를 **1로** 설정하면 오류가 발생합니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자는* **sysname**, NULL의 기본값입니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* **sysname이며**기본값은 NULL입니다.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`동기화 할 때 가입자에 연결할 때 사용할 보안 모드입니다. *subscriber_security_mode* **기본값은**1입니다. 경우 **0은**인증을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정합니다. 경우 **1은**Windows 인증을 지정합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 병합 에이전트는 항상 Windows 인증을 사용해 로컬 구독자로 연결됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
`[ @subscriber_login = ] 'subscriber_login'`동기화할 때 구독자에 연결할 때 사용할 구독자 로그인입니다. *subscriber_security_mode* **0으로**설정된 경우 *subscriber_login* 필요합니다. *subscriber_login* **sysname이며**기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
`[ @subscriber_password = ] 'subscriber_password'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증의 구독자 암호입니다. *subscriber_security_mode* **0으로**설정된 경우 *subscriber_password* 필요합니다. *subscriber_password* **sysname이며**기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 이 매개 변수의 값을 지정하면 경고 메시지가 반환되고 값은 무시됩니다.  
  
`[ @distributor = ] 'distributor'`배포자의 이름입니다. *배포자는* **sysname입니다.** *publisher* 즉, 게시자는 배포자이기도 합니다.  
  
`[ @distributor_security_mode = ] distributor_security_mode`동기화 할 때 배포자에 연결할 때 사용할 보안 모드입니다. *distributor_security_mode* **int**기본값은 0입니다. **0은** 인증을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정합니다. **1은** Windows 인증을 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`동기화할 때 배포자에 연결할 때 사용할 배포자 로그인입니다. *distributor_security_mode* **0으로**설정된 경우 *distributor_login* 필요합니다. *distributor_login* **sysname이며**기본값은 NULL입니다.  
  
`[ @distributor_password = ] 'distributor_password'`배포자 암호입니다. *distributor_security_mode* **0으로**설정된 경우 *distributor_password* 필요합니다. *distributor_password* **sysname이며**기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @encrypted_password = ] encrypted_password`*encrypted_password* 설정은 더 이상 지원되지 않습니다. 이 **비트** 매개 변수를 **1로** 설정하면 오류가 발생합니다.  
  
`[ @frequency_type = ] frequency_type`병합 에이전트를 예약할 빈도입니다. *frequency_type* **int이며**다음 값 중 하나가 될 수 있습니다.  
  
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
|NULL(기본값)||  
  
> [!NOTE]  
>  **값을 64로** 지정하면 병합 에이전트가 연속 모드에서 실행됩니다. 이는 에이전트에 대한 **-Continuous** 매개 변수 설정에 해당합니다. 자세한 내용은 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)을(를) 참조하세요.  
  
`[ @frequency_interval = ] frequency_interval`병합 에이전트가 실행되는 일 또는 일입니다. *frequency_interval* **int이며**이러한 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|일요일|  
|**2**|월요일|  
|**3**|화요일|  
|**4**|수요일|  
|**5**|목요일|  
|**6**|금요일|  
|**7**|토요일|  
|**8**|일|  
|**9**|평일|  
|**10**|주말|  
|NULL(기본값)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`병합 에이전트의 날짜입니다. 이 매개 변수는 *frequency_type* **32(월별** 상대)로 설정될 때 사용됩니다. *frequency_relative_interval* **int이며**이러한 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|처음|  
|**2**|초|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
|NULL(기본값)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*frequency_type*사용하는 재발 인자입니다. *frequency_recurrence_factor* NULL의 기본값으로 **int입니다.**  
  
`[ @frequency_subday = ] frequency_subday`정의된 기간 동안 일정을 조정하는 빈도입니다. *frequency_subday* **int이며**이러한 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|초|  
|**4**|Minute|  
|**8**|Hour|  
|NULL(기본값)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*frequency_subday*간격입니다. *frequency_subday_interval* **INT이며**기본값은 NULL입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`병합 에이전트가 먼저 예약되고 HHMMSS로 포맷되는 시간입니다. *active_start_time_of_day* **INT이며**기본값은 NULL입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`병합 에이전트가 예약되는 중지되는 시간입니다. *active_end_time_of_day* **INT이며**기본값은 NULL입니다.  
  
`[ @active_start_date = ] active_start_date`병합 에이전트가 YYYMMDD로 서식이 지정된 첫 번째 예약 날짜입니다. *active_start_date* **INT이며**기본값은 NULL입니다.  
  
`[ @active_end_date = ] active_end_date`병합 에이전트가 예약되는 중지되는 날짜입니다. *active_end_date* NULL의 기본값으로 **int입니다.**  
  
`[ @optional_command_line = ] 'optional_command_line'`병합 에이전트에 제공되는 선택적 명령 프롬프트입니다. *optional_command_line* **nvarchar (255)이며**기본값은 '입니다. 병합 에이전트에 추가 매개 변수를 제공하는 데 사용할 수 있으며 다음 예에서는 기본 쿼리 제한 시간을 `600`초로 늘립니다.  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
`[ @merge_jobid = ] merge_jobid`작업 ID의 출력 매개 변수입니다. *merge_jobid* **이진(16)이며**기본값은 NULL입니다.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`구독을 Windows 동기화 관리자를 통해 동기화할 수 있는지 지정합니다. *enabled_for_syncmgr* **nvarchar(5)이며**기본값은 FALSE입니다. **false이면**구독이 동기화 관리자에 등록되지 않습니다. **true이면**구독이 동기화 관리자에 등록되어 있으며 을 시작하지 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]않고 동기화할 수 있습니다.  
  
`[ @ftp_address = ] 'ftp_address'`이전 버전과의 호환성에만 적합합니다.  
  
`[ @ftp_port = ] ftp_port`이전 버전과의 호환성에만 적합합니다.  
  
`[ @ftp_login = ] 'ftp_login'`이전 버전과의 호환성에만 적합합니다.  
  
`[ @ftp_password = ] 'ftp_password'`이전 버전과의 호환성에만 적합합니다.  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`스냅숏 파일을 선택할 위치를 지정합니다. *alternate_snapshot_folder* **nvarchar (255)이며,** NULL의 기본값입니다. NULL인 경우 게시자가 지정한 기본 위치에 스냅샷이 선택됩니다.  
  
`[ @working_directory = ] 'working_directory'`FTP가 스냅샷 파일을 전송하는 데 사용될 때 게시에 대한 데이터와 스키마 파일을 일시적으로 저장하는 데 사용되는 작업 디렉토리의 이름입니다. *working_directory* **nvarchar (255)이며**NULL의 기본값입니다.  
  
`[ @use_ftp = ] 'use_ftp'`스냅숏을 검색하는 일반적인 프로토콜 대신 FTP 사용을 지정합니다. *use_ftp* **nvarchar(5)이며**기본값은 FALSE입니다.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver' ]`대화형 해결 프로그램을 사용하여 대화형 해결을 허용하는 모든 아티클의 충돌을 해결합니다. *use_interactive_resolver* **nvarchar(5)이며**기본값은 FALSE입니다.  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. **false** 가 아닌 값으로 *remote_agent_activation* 설정하면 오류가 발생합니다.  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. *null이* 아닌 값으로 remote_agent_server_name 설정하면 오류가 발생합니다.  
  
`[ @job_name = ] 'job_name' ]`기존 에이전트 작업의 이름입니다. *job_name* **sysname이며**기본값은 NULL입니다. 이 매개 변수는 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 구독이 동기화될 경우에만 지정됩니다. **sysadmin** 고정 서버 역할의 구성원이 아닌 경우 *job_name*지정할 때 *job_login* *및 job_password* 지정해야 합니다.  
  
`[ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]`필터링된 데이터 스냅숏을 사용할 경우 스냅숏 파일을 읽을 폴더에 대한 경로입니다. *dynamic_snapshot_location* **nvarchar (260)이며,** NULL의 기본값입니다. 자세한 내용은 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
`[ @use_web_sync = ] use_web_sync`웹 동기화가 활성화되어 있음을 나타냅니다. *use_web_sync* **비트이며**기본값은 0입니다. **1은** 끌어오기 구독이 HTTP를 사용하여 인터넷을 통해 동기화될 수 있음을 지정합니다.  
  
`[ @internet_url = ] 'internet_url'`복제 리스너(REPLISAPI)의 위치입니다. 웹 동기화에 대한 DLL)을 사용합니다. *internet_url* **nvarchar (260)이며,** NULL의 기본값입니다. *internet_url* 형식의 `http://server.domain.com/directory/replisapi.dll`정규화된 URL입니다. 서버가 포트 80 이외의 다른 포트에서 수신하도록 구성된 경우 포트 번호도 `http://server.domain.com:portnumber/directory/replisapi.dll` 형식으로 제공되어야 합니다. 여기서 `portnumber`는 포트를 나타냅니다.  
  
`[ @internet_login = ] 'internet_login'`HTTP 기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 로그인입니다. *internet_login* **sysname이며**기본값은 NULL입니다.  
  
`[ @internet_password = ] 'internet_password'`HTTP 기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 암호입니다. *internet_password* **nvarchar(524)이며**기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
`[ @internet_security_mode = ] internet_security_mode`HTTPS를 사용하여 웹 동기화 중에 웹 서버에 연결할 때 병합 에이전트에서 사용하는 인증 방법입니다. *internet_security_mode* **int이며** 이러한 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|기본 인증이 사용됩니다.|  
|**1** (기본값)|Windows 통합 인증이 사용됩니다.|  
  
> [!NOTE]  
>  웹 동기화에는 기본 인증을 사용하는 것이 좋습니다. 웹 동기화를 사용하려면 웹 서버에 TLS 연결을 만들어야 합니다. 자세한 내용은 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)을 참조하세요.  
  
`[ @internet_timeout = ] internet_timeout`웹 동기화 요청이 만료되기 전의 시간(초)입니다. *internet_timeout* **기본값인** **300초입니다.**  
  
`[ @hostname = ] 'hostname'`이 함수가 매개 변수화된 필터의 WHERE 절에서 사용되는 경우 HOST_NAME() 값을 재정의합니다. *호스트 이름은* **sysname이며**기본값은 NULL입니다.  
  
`[ @job_login = ] 'job_login'`에이전트가 실행되는 Windows 계정에 대한 로그인입니다. *job_login* **nvarchar (257)이며**기본값은 없습니다. 이 Windows 계정은 Windows 통합 인증을 사용하는 경우 에이전트를 구독자에 연결하고 배포자 및 게시자에 연결할 때 항상 사용됩니다.  
  
`[ @job_password = ] 'job_password'`에이전트가 실행되는 Windows 계정의 암호입니다. *job_password* **sysname이며**기본값은 없습니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 최상의 보안을 위해 런타임에 로그인 이름과 암호를 제공해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergepullsubscription_agent** 병합 복제에 사용되며 [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)유사한 기능을 사용합니다.  
  
 **sp_addmergepullsubscription_agent**실행 시 보안 설정을 올바르게 지정하는 방법의 예는 [[구독자 수 만들기]](../../relational-databases/replication/create-a-pull-subscription.md)  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **시스템 관리자** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 구성원만 **sp_addmergepullsubscription_agent**실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)   
 [간행물 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
