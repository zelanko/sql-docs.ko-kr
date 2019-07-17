---
title: sp_helppullsubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppullsubscription_TSQL
- sp_helppullsubscription
helpviewer_keywords:
- sp_helppullsubscription
ms.assetid: a0d9c3f1-1fe9-497c-8e2f-5b74f47a7346
author: stevestein
ms.author: sstein
ms.openlocfilehash: 777e9b2afceb3e9a58030a225a0cbff34375165b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914959"
---
# <a name="sphelppullsubscription-transact-sql"></a>sp_helppullsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  구독자에서 하나 이상의 구독에 관한 정보를 표시합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helppullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @show_push = ] 'show_push' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 원격 서버의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 **%** , 모든 게시자에 대 한 정보를 반환 하는 합니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시자 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 **%** , 모든 게시자 데이터베이스를 반환 하는 합니다.  
  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 **%** , 모든 게시를 반환 하는 합니다. 독립 에이전트를 사용 하 여 모든 전용 끌어오기 구독에이 매개 변수가 같으면 = **0** 반환 됩니다.  
  
`[ @show_push = ] 'show_push'` 반환할 모든 밀어넣기 구독 인지 됩니다. *show_push*됩니다 **nvarchar(5)** , 이며 기본값은 FALSE 반환 하지 않는 밀어넣기 구독입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**게시자 데이터베이스**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**publication**|**sysname**|게시의 이름입니다.|  
|**independent_agent**|**bit**|이 게시에 대한 독립 실행형 배포 에이전트가 있는지 여부를 나타냅니다.|  
|**구독 유형**|**int**|게시에 대한 구독 유형입니다.|  
|**배포 에이전트**|**nvarchar(100)**|구독을 처리하는 배포 에이전트입니다.|  
|**게시 설명**|**nvarchar(255)**|게시에 대한 설명입니다.|  
|**마지막 업데이트 시간**|**date**|구독 정보가 업데이트된 시각입니다. 이는 ISO 날짜(114) + ODBC 시간(121)의 유니코드 문자열입니다. 형식은 yyyymmdd hh:mi:sss.mmm이며 여기서 'yyyy'는 연도, 'mm'은 월, 'dd'는 날짜, 'hh'는 시간, 'mi'는 분, 'sss'는 초, 'mmm'은 밀리초에 해당합니다.|  
|**구독 이름**|**varchar(386)**|구독의 이름입니다.|  
|**마지막 트랜잭션 타임 스탬프**|**varbinary(16)**|마지막으로 복제된 트랜잭션의 타임스탬프입니다.|  
|**업데이트 모드**|**tinyint**|허용되는 업데이트 유형입니다.|  
|**배포 에이전트 job_id**|**int**|배포 에이전트의 작업 ID입니다.|  
|**enabled_for_synmgr**|**int**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 동기화 관리자를 통해 구독을 동기화할 수 있는지 여부입니다.|  
|**구독 guid**|**binary(16)**|게시에 대한 구독 버전의 전역 식별자입니다.|  
|**subid**|**binary(16)**|익명 구독의 전역 식별자입니다.|  
|**immediate_sync**|**bit**|스냅샷 에이전트가 실행될 때마다 동기화 파일이 생성 또는 다시 생성되는지 여부를 나타냅니다.|  
|**게시자 로그인**|**sysname**|게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 로그인 ID입니다.|  
|**게시자 암호**|**nvarchar(524)**|게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 암호입니다.|  
|**게시자 security_mode**|**int**|게시자에서 구현된 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1** = Windows 인증<br /><br /> **2** = 동기화 트리거를 사용 하는 정적 **sysservers** 항목을 원격 프로시저 호출 (RPC), 및 *게시자* 정의 해야 합니다는 **sysservers**테이블에서 원격 서버 또는 연결 된 서버입니다.|  
|**distributor**|**sysname**|배포자의 이름입니다.|  
|**distributor_login**|**sysname**|배포자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 로그인 ID입니다.|  
|**distributor_password**|**nvarchar(524)**|배포자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 암호입니다.|  
|**distributor_security_mode**|**int**|배포자에서 구현된 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1** = Windows 인증|  
|**ftp_address**|**sysname**|이전 버전과의 호환성을 위해서만 지원됩니다.|  
|**ftp_port**|**int**|이전 버전과의 호환성을 위해서만 지원됩니다.|  
|**ftp_login**|**sysname**|이전 버전과의 호환성을 위해서만 지원됩니다.|  
|**ftp_password**|**nvarchar(524)**|이전 버전과의 호환성을 위해서만 지원됩니다.|  
|**alt_snapshot_folder**|**nvarchar(255)**|기본 위치가 아니거나 기본 위치에 추가된 위치일 경우, 스냅샷 폴더가 저장되는 위치입니다.|  
|**working_directory**|**nvarchar(255)**|해당 옵션이 지정된 경우에 스냅샷 파일이 FTP(파일 전송 프로토콜)를 사용하여 전송되는 디렉터리의 정규화된 경로입니다.|  
|**use_ftp**|**bit**|구독이 인터넷을 통해 게시를 구독하고 있으며 FTP 주소 속성이 구성되었습니다. 하는 경우 **0**, 구독은 FTP를 사용 하지 않습니다. 하는 경우 **1**, 구독은 FTP를 사용 합니다.|  
|**publication_type**|**int**|다음과 같은 게시의 복제 유형을 지정합니다.<br /><br /> **0** = 트랜잭션 복제<br /><br /> **1** = 스냅숏 복제<br /><br /> **2** = 병합 복제|  
|**dts_package_name**|**sysname**|DTS(데이터 변환 서비스) 패키지의 이름을 지정합니다.|  
|**dts_package_location**|**int**|DTS 패키지가 저장된 위치입니다.<br /><br /> **0** = 배포자<br /><br /> **1** = 구독자|  
|**offload_agent**|**bit**|에이전트를 원격으로 활성화할 수 있는지 지정합니다. 하는 경우 **0**, 에이전트를 원격으로 활성화할 수 없습니다.|  
|**offload_server**|**sysname**|원격 활성화에 사용하는 서버의 네트워크 이름을 지정합니다.|  
|**last_sync_status**|**int**|구독 상태입니다.<br /><br /> **0** = 모든 작업이 시작 되기를 기다리고 있습니다<br /><br /> **1** = 하나 이상의 작업이 시작 됩니다<br /><br /> **2** = 모든 작업이 성공적으로 실행<br /><br /> **3** = 하나 이상의 작업이 실행 중입니다<br /><br /> **4** = 모든 작업이 예약 되었으며 유휴 상태<br /><br /> **5** = 하나 이상의 작업 이전에 실패 한 후 실행 하려고 합니다.<br /><br /> **6** = 하나 이상의 작업이 성공적으로 실행에 실패 했습니다|  
|**last_sync_summary**|**sysname**|마지막 동기화 결과에 관한 설명입니다.|  
|**last_sync_time**|**datetime**|구독 정보가 업데이트된 시각입니다. 이는 ISO 날짜(114) + ODBC 시간(121)의 유니코드 문자열입니다. 형식은 yyyymmdd hh:mi:sss.mmm이며 여기서 'yyyy'는 연도, 'mm'은 월, 'dd'는 날짜, 'hh'는 시간, 'mi'는 분, 'sss'는 초, 'mmm'은 밀리초에 해당합니다.|  
|**job_login**|**nvarchar(512)**|배포 에이전트를 실행 하는 형식으로 반환 되는 Windows 계정입니다 *도메인*\\*username*합니다.|  
|**job_password**|**sysname**|보안상의 이유로 값 " **\*\*\*\*\*\*\*\*\*\*** "는 항상 반환 됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helppullsubscription** 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_helppullsubscription** 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_addpullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_droppullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
