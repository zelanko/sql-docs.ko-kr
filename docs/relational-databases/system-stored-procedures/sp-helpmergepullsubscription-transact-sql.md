---
title: sp_helpmergepullsubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepullsubscription
- sp_helpmergepullsubscription_TSQL
helpviewer_keywords:
- sp_helpmergepullsubscription
ms.assetid: 6f3125f3-0dfa-40bd-b725-8aa1591234f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: adbb39c32f09898e6d521b0ecff3c06c1a6494f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639981"
---
# <a name="sphelpmergepullsubscription-transact-sql"></a>sp_helpmergepullsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  구독자에 있는 끌어오기 구독에 대한 정보를 반환합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergepullsubscription [ [ @publication=] 'publication']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
```  
  
## <a name="argument"></a>인수  
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 **%** 합니다. 하는 경우 *게시* 됩니다 **%**, 현재 데이터베이스의 모든 구독과 병합 게시에 대 한 정보가 반환 됩니다.  
  
 [ **@publisher=**] **'***publisher***'**  
 게시자의 이름입니다. *게시자*됩니다 **sysname**, 기본값은 **%** 합니다.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 게시자 데이터베이스의 이름입니다. *publisher_db*됩니다 **sysname**, 기본값은 **%** 합니다.  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 끌어오기 구독을 표시할지 여부입니다. *subscription_type*됩니다 **nvarchar(10)**, 기본값은 **'pull'** 합니다. 유효한 값은 **'push'** 를 **'pull'**, 또는 **'both'** 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**nvarchar(1000)**|구독의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**subscriber**|**sysname**|구독자의 이름입니다.|  
|**subscription_db**|**sysname**|구독 데이터베이스의 이름입니다.|  
|**상태**|**int**|구독 상태입니다.<br /><br /> **0** = 비활성 구독<br /><br /> **1** = 활성 구독<br /><br /> **2** = 삭제 된 구독<br /><br /> **3** = 분리 된 구독<br /><br /> **4** = 연결 된 구독<br /><br /> **5** = 구독이 업로드를 사용 하 여 다시 초기화 하도록 표시 되었으며<br /><br /> **6** = 구독 연결 실패<br /><br /> **7** = 백업에서 복원 하는 구독|  
|**subscriber_type**|**int**|구독자의 유형입니다.<br /><br /> **1** = 전역<br /><br /> **2** = 로컬<br /><br /> **3** = 익명|  
|**subscription_type**|**int**|구독 유형:<br /><br /> **0** = 밀어넣기<br /><br /> **1** = 끌어오기<br /><br /> **2** = 익명|  
|**priority**|**float(8)**|구독 우선 순위입니다. 값은 여야 미만 **100.00**합니다.|  
|**sync_type**|**tinyint**|구독 동기화 유형입니다.<br /><br /> **1** = 자동<br /><br /> **2** = 스냅숏이 사용 되지 않습니다.|  
|**description**|**nvarchar(255)**|해당 끌어오기 구독에 관한 간략한 설명입니다.|  
|**merge_jobid**|**binary(16)**|병합 에이전트의 작업 ID입니다.|  
|**enabled_for_syncmgr**|**int**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 동기화 관리자를 통해 구독을 동기화할 수 있는지 여부입니다.|  
|**last_updated**|**nvarchar(26)**|병합 에이전트가 구독의 동기화를 마지막으로 성공한 시각입니다.|  
|**publisher_login**|**sysname**|게시자 로그인 이름입니다.|  
|**publisher_password**|**sysname**|게시자 암호입니다.|  
|**publisher_security_mode**|**int**|게시자의 보안 모드를 지정합니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1** = Windows 인증|  
|**배포자**|**sysname**|배포자의 이름입니다.|  
|**distributor_login**|**sysname**|배포자의 로그인 이름입니다.|  
|**distributor_password**|**sysname**|배포자 암호입니다.|  
|**distributor_security_mode**|**int**|배포자의 보안 모드를 지정합니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1** = Windows 인증|  
|**ftp_address**|**sysname**|이전 버전과의 호환성을 위해서만 사용 가능합니다. 배포자용 FTP(파일 전송 프로토콜) 서비스의 네트워크 주소입니다.|  
|**ftp_port**|**int**|이전 버전과의 호환성을 위해서만 사용 가능합니다. 배포자용 FTP 서비스의 포트 번호입니다.|  
|**ftp_login**|**sysname**|이전 버전과의 호환성을 위해서만 사용 가능합니다. FTP 서비스 연결에 사용되는 사용자 이름입니다.|  
|**ftp_password**|**sysname**|이전 버전과의 호환성을 위해서만 사용 가능합니다. FTP 서비스에 연결할 때 사용되는 사용자 암호입니다.|  
|**alt_snapshot_folder**|**nvarchar(255)**|기본 위치가 아니거나 기본 위치에 추가된 위치일 경우, 스냅숏 폴더가 저장되는 위치입니다.|  
|**working_directory**|**nvarchar(255)**|해당 옵션이 지정된 경우 FTP를 사용하여 스냅숏 파일이 전송될 디렉터리의 정규화된 경로입니다.|  
|**use_ftp**|**bit**|구독이 인터넷을 통해 게시를 구독하고 있으며 FTP 주소 속성이 구성되었습니다. 하는 경우 **0**, 구독은 FTP를 사용 하지 않습니다. 하는 경우 **1**, 구독은 FTP를 사용 합니다.|  
|**offload_agent**|**bit**|에이전트가 활성화되어 원격으로 실행될 수 있는지 여부를 지정합니다. 하는 경우 **0**, 에이전트를 원격으로 활성화할 수 없습니다.|  
|**offload_server**|**sysname**|원격 활성화에 필요한 서버의 이름입니다.|  
|**use_interactive_resolver**|**int**|조정 상태 동안 대화형 해결 프로그램의 사용 여부를 반환합니다. 하는 경우 **0**, 대화형 해결 프로그램 사용 되지 않습니다.|  
|**subid**|**uniqueidentifier**|구독자의 ID입니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|스냅숏 파일을 저장한 폴더의 경로입니다.|  
|**last_sync_status**|**int**|동기화 상태입니다.<br /><br /> **1** = 시작<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태<br /><br /> **5** = 이전의 실패 후 다시 시도 중<br /><br /> **6** = 실패<br /><br /> **7** = 유효성 검사 실패<br /><br /> **8** = 유효성 검사 통과<br /><br /> **9** = 종료 요청|  
|**last_sync_summary**|**sysname**|마지막 동기화 결과에 관한 설명입니다.|  
|**use_web_sync**|**bit**|여기서 값 HTTPS를 통해 구독을 동기화 할 경우를 지정 **1** 이 기능을 사용 하는 것을 의미 합니다.|  
|**internet_url**|**nvarchar(260)**|웹 동기화를 위한 복제 수신기의 위치를 나타내는 URL입니다.|  
|**internet_login**|**nvarchar(128)**|기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 로그인입니다.|  
|**internet_password**|**nvarchar(524)**|기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 로그인 암호입니다.|  
|**internet_security_mode**|**int**|웹 동기화를 호스팅하는 웹 서버에 연결할 때 사용하는 인증 모드입니다. 값이 **1** Windows 인증 및 값 의미 **0** 의미 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.|  
|**internet_timeout**|**int**|웹 동기화 요청이 만료되기 전까지의 시간(초)입니다.|  
|**호스트 이름**|**nvarchar(128)**|에 대 한 오버 로드 된 값을 지정 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 매개 변수가 있는 행 필터의 WHERE 절에이 함수는 사용 하는 경우.|  
|**job_login**|**nvarchar(512)**|병합 에이전트가 실행 하는 형식으로 반환 되는 Windows 계정입니다 *도메인*\\*username*합니다.|  
|**job_password**|**sysname**|보안상의 이유로 값 "**\*\*\*\*\*\*\*\*\*\***"는 항상 반환 됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpmergepullsubscription** 병합 복제에 사용 됩니다. 결과 집합에 반환 된 날짜 **last_updated** 서식이 *YYYYMMDD hh:mm:ss.fff*합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 및 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_helpmergepullsubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_addmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
