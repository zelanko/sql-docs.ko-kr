---
title: sp_addpublication (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
author: stevestein
ms.author: sstein
ms.openlocfilehash: f676acf9b3ee91bb5a1fb46cae2f7c693dc66983
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061819"
---
# <a name="spaddpublication-transact-sql"></a>sp_addpublication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  스냅샷 또는 트랜잭션 게시를 만듭니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addpublication [ @publication = ] 'publication'  
    [ , [ @taskid = ] tasked ]  
    [ , [ @restricted = ] 'restricted' ]  
    [ , [ @sync_method = ] 'sync_method' ]  
    [ , [ @repl_freq = ] 'repl_freq' ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @status = ] 'status' ]  
    [ , [ @independent_agent = ] 'independent_agent' ]  
    [ , [ @immediate_sync = ] 'immediate_sync' ]  
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]  
    [ , [ @allow_push = ] 'allow_push'  
    [ , [ @allow_pull = ] 'allow_pull' ]  
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]  
    [ , [ @allow_sync_tran = ] 'allow_sync_tran' ]  
    [ , [ @autogen_sync_procs = ] 'autogen_sync_procs' ]  
    [ , [ @retention = ] retention ]  
    [ , [ @allow_queued_tran= ] 'allow_queued_updating' ]  
    [ , [ @snapshot_in_defaultfolder= ] 'snapshot_in_default_folder' ]  
    [ , [ @alt_snapshot_folder= ] 'alternate_snapshot_folder' ]  
    [ , [ @pre_snapshot_script= ] 'pre_snapshot_script' ]  
    [ , [ @post_snapshot_script= ] 'post_snapshot_script' ]  
    [ , [ @compress_snapshot= ] 'compress_snapshot' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port= ] ftp_port ]  
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @allow_dts = ] 'allow_dts' ]  
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]  
    [ , [ @conflict_policy = ] 'conflict_policy' ]  
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @queue_type = ] 'queue_type' ]  
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]  
    [ , [ @logreader_job_name = ] 'logreader_agent_name' ]  
    [ , [ @qreader_job_name = ] 'queue_reader_agent_name' ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @allow_initialize_from_backup = ] 'allow_initialize_from_backup' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @enabled_for_p2p = ] 'enabled_for_p2p' ]  
    [ , [ @publish_local_changes_only = ] 'publish_local_changes_only' ]  
    [ , [ @enabled_for_het_sub = ] 'enabled_for_het_sub' ]  
    [ , [ @p2p_conflictdetection = ] 'p2p_conflictdetection' ]  
    [ , [ @p2p_originator_id = ] p2p_originator_id  
    [ , [ @p2p_continue_onconflict = ] 'p2p_continue_onconflict'  
    [ , [ @allow_partition_switch = ] 'allow_partition_switch'  
    [ , [ @replicate_partition_switch = ]'replicate_partition_switch'  
```  
  
## <a name="arguments"></a>인수  
`[ \@publication = ] 'publication'` 만들 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다. 이름은 반드시 데이터베이스 내에서 고유해야 합니다.  
  
`[ \@taskid = ] taskid` 이전 버전과 호환 되지 않습니다. 사용 하 여 [sp_addpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)합니다.  
  
`[ \@restricted = ] 'restricted'` 이전 버전과 호환 되지 않습니다. 사용 하 여 *default_access*합니다.  
  
`[ \@sync_method = ] _'sync_method'` 동기화 모드가입니다. *sync_method* 됩니다 **nvarchar(13)** , 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**native**|모든 테이블의 기본 모드 대량 복사 프로그램 출력을 생성합니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*합니다.|  
|**character**|모든 테이블의 문자 모드 대량 복사 프로그램 출력을 생성합니다. _Oracle 게시자에 대 한_ **문자** _스냅숏 복제에 대해서만 유효_합니다.|  
|**concurrent**|모든 테이블의 기본 모드 대량 복사 프로그램 출력을 생성하지만 스냅샷을 실행하는 동안 테이블을 잠그지 않습니다. 트랜잭션 게시에 대해서만 지원됩니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*합니다.|  
|**concurrent_c**|모든 테이블의 문자 모드 대량 복사 프로그램 출력을 생성하지만 스냅샷을 실행하는 동안 테이블을 잠그지 않습니다. 트랜잭션 게시에 대해서만 지원됩니다.|  
|**데이터베이스 스냅숏**|데이터베이스 스냅샷에서 모든 테이블의 기본 모드 대량 복사 프로그램 출력을 생성합니다. 데이터베이스 스냅숏은의 모든 버전에서 사용할 수 없습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.|  
|**데이터베이스 스냅숏 문자**|데이터베이스 스냅샷에서 모든 테이블의 문자 모드 대량 복사 프로그램 출력을 생성합니다. 데이터베이스 스냅숏은의 모든 버전에서 사용할 수 없습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.|  
|NULL(기본값)|기본값으로 **네이티브** 에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. 에 대 한 비[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 경우 기본값은 **문자** 때의 값 *repl_freq* 됩니다 **스냅숏** 하 고 **concurrent_c** 다른 모든 경우.|  
  
`[ \@repl_freq = ] 'repl_freq'` 복제 빈도의 형식인 *repl_freq* 됩니다 **nvarchar(10)** , 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**연속** (기본값)|게시자가 모든 로그 기반 트랜잭션의 출력을 제공합니다. 에 대 한 비[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는이 게시자 *sync_method* 로 설정 **concurrent_c**합니다.|  
|**snapshot**|게시자가 예약된 동기화 이벤트만 생성합니다. 에 대 한 비[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는이 게시자 *sync_method* 로 설정 **문자**합니다.|  
  
`[ \@description = ] 'description'` 게시에 대 한 선택적 설명이입니다. *설명* 됩니다 **nvarchar(255)** , 기본값은 NULL입니다.  
  
`[ \@status = ] 'status'` 게시 데이터를 사용할 수 있는지를 지정 합니다. *상태* 됩니다 **nvarchar(8)** , 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**active**|구독자가 게시 데이터를 즉시 사용할 수 있습니다.|  
|**비활성** (기본값)|게시가 처음 작성될 때 구독자가 게시 데이터를 사용할 수 없습니다. 구독할 수는 있으나 구독이 처리되지 않습니다.|  
  
 *Oracle 게시자에 대해서는 지원 되지 않습니다*합니다.  
  
`[ \@independent_agent = ] 'independent_agent'` 이 게시에 대 한 독립 실행형 배포 에이전트가 있는지를 지정 합니다. *independent_agent* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. 하는 경우 **true**,이 게시에 대 한 독립 실행형 배포 에이전트가 있습니다. 하는 경우 **false**게시는 공유 배포 에이전트를 사용 하 고 각 게시자 데이터베이스/구독자 데이터베이스 쌍에는 하나의 공유 에이전트가 있습니다.  
  
`[ \@immediate_sync = ] 'immediate_synchronization'` 게시용 동기화 파일이 경우 스냅숏 에이전트가 실행 될 때마다 생성 됩니다 지정 합니다. *immediate_synchronization* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. 하는 경우 **true**, 동기화 파일이 만들어지거나 스냅숏 에이전트가 실행 될 때마다 다시 생성 합니다. 구독을 만들기 전에 스냅샷 에이전트가 완료되면 구독자가 즉시 동기화 파일을 얻을 수 있습니다. 새 구독은 스냅샷 에이전트를 가장 최근에 실행하여 생성된 최신 동기화 파일을 가져옵니다. *independent_agent* 있어야 **true** 에 대 한 *immediate_synchronization* 되도록 **true**합니다. 하는 경우 **false**, 새 구독이 있는 경우에 동기화 파일이 생성 됩니다. 호출 해야 합니다 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 기존 게시에 새 아티클을 증분 방식으로 추가 하면 각 구독에 대 한 합니다. 구독자는 스냅샷 에이전트가 시작되어 완료될 때까지는 구독 이후에 동기화 파일을 받을 수 없습니다.  
  
`[ \@enabled_for_internet = ] 'enabled_for_internet'` 게시 인터넷을 사용 하도록 설정 되 고 구독자에 스냅숏 파일을 전송할 파일 전송 프로토콜 (FTP)를 사용할 수 있는 경우 결정을 지정 합니다. *enabled_for_internet* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. 하는 경우 **true**, 게시용 동기화 파일은 C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 디렉터리에 저장 합니다. 사용자는 반드시 Ftp 디렉터리를 만들어야 합니다.  
  
`[ \@allow_push = ] 'allow_push'` 지정된 된 게시에 대 한 밀어넣기 구독을 만들 수 있습니다 하는 경우를 지정 합니다. *allow_push* 됩니다 **nvarchar(5)** , 기본값은 TRUE 허용 하는 밀어넣기 구독에 게시 합니다.  
  
`[ \@allow_pull = ] 'allow_pull'` 지정된 된 게시에 대 한 끌어오기 구독을 만들 수 있는지를 지정 합니다. *allow_pull* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. 하는 경우 **false**, 게시에 끌어오기 구독이 허용 되지 않습니다.  
  
`[ \@allow_anonymous = ] 'allow_anonymous'` 지정된 된 게시에 대 한 익명 구독을 만들 수 있는지를 지정 합니다. *allow_anonymous* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. 하는 경우 **true**를 *immediate_synchronization* 로 설정 해야 **true**합니다. 하는 경우 **false**, 게시에서 익명 구독이 허용 되지 않습니다.  
  
`[ \@allow_sync_tran = ] 'allow_sync_tran'` 게시에서 즉시 업데이트 구독이 허용 되는지 여부를 지정 합니다. *allow_sync_tran* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. **true 이면** 됩니다 *Oracle 게시자에 대 한 지원 되지 않습니다*합니다.  
  
`[ \@autogen_sync_procs = ] 'autogen_sync_procs'` 구독 업데이트에 대 한 동기화 저장된 프로시저가 게시자에서 생성 된 경우를 지정 합니다. *autogen_sync_procs* 됩니다 **nvarchar(5)** , 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**true**|업데이트 구독이 사용될 때 자동으로 설정됩니다.|  
|**false**|업데이트 구독이 사용되지 않을 때나 Oracle 게시자에 대해서 자동으로 설정됩니다.|  
|NULL(기본값)|기본값으로 **true** 업데이트 구독을 사용 하는 경우 하 **false** 등록을 업데이트 하는 사용 되지 않는 경우.|  
  
> [!NOTE]  
>  사용자에 대 한 값을 제공한 *autogen_sync_procs*지정 된 값에 따라 재정의 됩니다 *allow_queued_tran* 하 고 *allow_sync_tran*합니다.  
  
`[ \@retention = ] retention` 구독 작업에 대 한 시간 보존 기간이입니다. *보존* 됩니다 **int**, 기본값: 336 시간입니다. 구독이 보존 기간 내에 활성화되지 않으면 만료되어 제거됩니다. 해당 값은 게시자가 사용하는 배포 데이터베이스의 최대 보존 기간보다 길 수 있습니다. 하는 경우 **0**, 게시에 대 한 잘 알려진 구독 만료 되지 않으며 만료 된 구독 정리 에이전트에서 제거 합니다.  
  
`[ \@allow_queued_tran = ] 'allow_queued_updating'` 사용 하거나 게시자에서 적용할 수 있을 때까지 구독자에서 변경 내용의 지연을 사용 하지 않도록 설정 합니다. *allow_queued_updating* 됩니다 **nvarchar(5)** 이며 기본값은 FALSE입니다. 하는 경우 **false**, 구독자의 변경 내용이 지연 되지 않습니다. **true 이면** 됩니다 *Oracle 게시자에 대 한 지원 되지 않습니다*합니다.  
  
`[ \@snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'` 경우에 스냅숏 파일이 기본 폴더에 저장 됩니다 지정 합니다. *snapshot_in_default_folder* 됩니다 **nvarchar(5)** 이며 기본값은 TRUE입니다. 하는 경우 **true**, 스냅숏 파일이 기본 폴더에서 찾을 수 있습니다. 하는 경우 **false**, 지정 된 대체 위치에 저장 된 스냅숏 파일 *alternate_snapshot_folder*합니다. 대체 위치는 다른 서버, 네트워크 드라이브 또는 이동식 미디어(CD-ROM 또는 이동식 디스크 등)가 될 수 있습니다. 구독자가 나중에 검색할 수 있도록 스냅샷 파일을 FTP 사이트에 저장할 수도 있습니다. 이 매개 변수 true 될 수 있고의 위치를 아직 합니다  **\@alt_snapshot_folder** 매개 변수입니다. 이 조합은 스냅샷 파일이 기본 위치 및 대체 위치 양쪽 모두에 저장되도록 지정합니다.  
  
`[ \@alt_snapshot_folder = ] 'alternate_snapshot_folder'` 스냅숏의 대체 폴더의 위치를 지정 합니다. *alternate_snapshot_folder* 됩니다 **nvarchar(255)** 이며 기본값은 NULL입니다.  
  
`[ \@pre_snapshot_script = ] 'pre_snapshot_script'` 에 대 한 포인터를 지정 된 **.sql** 파일 위치입니다. *pre_snapshot_script* 됩니다 **nvarchar(255),** 이며 기본값은 NULL입니다. 배포 에이전트는 구독자에서 스냅샷을 적용할 때 복제된 개체 스크립트를 실행하기 전에 프리 스냅샷 스크립트를 실행합니다. 구독 데이터베이스에 연결할 때 배포 에이전트에서 사용되는 보안 컨텍스트에서 스크립트가 실행됩니다.  
  
`[ \@post_snapshot_script = ] 'post_snapshot_script'` 에 대 한 포인터를 지정 된 **.sql** 파일 위치입니다. *post_snapshot_script* 됩니다 **nvarchar(255)** , 기본값은 NULL입니다. 배포 에이전트는 초기 동기화 중 복제된 다른 모든 개체 스크립트 및 데이터가 적용된 후 포스트 스냅샷 스크립트를 실행합니다. 구독 데이터베이스에 연결할 때 배포 에이전트에서 사용되는 보안 컨텍스트에서 스크립트가 실행됩니다.  
  
`[ \@compress_snapshot = ] 'compress_snapshot'` 지정에 기록 되는 스냅숏 합니다  **\@alt_snapshot_folder** 위치가로 압축할 수는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 형식으로 합니다. *compress_snapshot* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. **false** 는 스냅숏이 압축 되지 않으면 지정 **true** 는 스냅숏이 압축 됩니다 지정 합니다. 2GB(기가바이트)를 넘는 스냅샷 파일은 압축할 수 없습니다. 압축된 스냅샷 파일은 배포 에이전트가 실행되는 위치에 풀립니다. 압축 파일이 구독자에 풀리도록 압축 스냅샷에는 일반적으로 끌어오기 구독이 사용됩니다. 기본 폴더에 있는 스냅샷은 압축할 수 없습니다.  
  
`[ \@ftp_address = ] 'ftp_address'` 배포자 용 FTP 서비스의 네트워크 주소가입니다. *ftp_address* 됩니다 **sysname**, 기본값은 NULL입니다. 선택할 구독자의 배포 에이전트 또는 병합 에이전트에 대한 게시 스냅샷 파일의 위치를 지정합니다. 이 속성은 각 게시에 저장 되므로 각 게시에는 서로 다른 *ftp_address*합니다. 게시는 FTP를 사용하여 스냅샷 전파를 지원해야 합니다.  
  
`[ \@ftp_port = ] ftp_port` 배포자 용 FTP 서비스의 포트 번호가입니다. *ftp_port* 됩니다 **int**, 기본값은 21입니다. 선택할 구독자의 배포 에이전트 또는 병합 에이전트에 대한 게시 스냅샷 파일의 위치를 지정합니다. 이 속성은 각 게시에 저장 되므로 각 게시는 고유한 *ftp_port*합니다.  
  
`[ \@ftp_subdirectory = ] 'ftp_subdirectory'` 배포 에이전트 또는 게시에서 FTP를 사용 하 여 스냅숏 전파를 지 원하는 경우 선택할 구독자의 병합 에이전트에 사용할 수 있는 스냅숏 파일 위치를 지정 합니다. *ftp_subdirectory* 됩니다 **nvarchar(255)** , 기본값은 NULL입니다. 이 속성은 각 게시에 저장 되므로 각 게시는 고유한 *ftp_subdirctory* 또는 NULL 값으로 표시 된 하위 디렉터리를 선택 합니다.  
  
`[ \@ftp_login = ] 'ftp_login'` FTP 서비스에 연결할 사용자 이름을 사용 됩니다. *ftp_login* 됩니다 **sysname**, 기본값은 ANONYMOUS입니다.  
  
`[ \@ftp_password = ] 'ftp_password'` FTP 서비스에 연결할 사용자 암호가 사용 됩니다. *ftp_password* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ \@allow_dts = ] 'allow_dts'` 게시에서 데이터 변환을 허용을 지정 합니다. 구독을 만들 때 DTS 패키지를 지정할 수 있습니다. *allow_transformable_subscriptions* 됩니다 **nvarchar(5)** 이며 기본값은 FALSE는 허용 하지 않는 DTS 변환 합니다. 때 *allow_dts* 가 true 이면 *sync_method* 설정 해야 중 하나로 **문자** 또는 **concurrent_c**합니다.  
  
 **true 이면** 됩니다 *Oracle 게시자에 대 한 지원 되지 않습니다*합니다.  
  
`[ \@allow_subscription_copy = ] 'allow_subscription_copy'` 사용 하거나이 게시를 구독 하는 구독 데이터베이스를 복사 하는 기능을 사용 하지 않도록 설정 합니다. *allow_subscription_copy* 됩니다**nvarchar(5)** , 기본값은 FALSE입니다.  
  
`[ \@conflict_policy = ] 'conflict_policy'` 지연된 업데이트 구독자 옵션을 사용 하는 경우 뒤에 충돌 해결 정책을 지정 합니다. *conflict_policy* 됩니다 **nvarchar(100)** 이며 기본값은 NULL 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**pub wins**|충돌 시 게시자 내용을 적용합니다.|  
|**sub reinit**|구독을 다시 초기화합니다.|  
|**sub wins**|충돌 시 구독자 내용을 적용합니다.|  
|NULL(기본값)|NULL이 고 게시가 스냅숏 게시 인 경우 기본 정책이 됩니다 **sub reinit**합니다. 없으면 NULL이 고 게시가 스냅숏 게시, 기본 정책이 됩니다 **pub wins**합니다.|  
  
 *Oracle 게시자에 대해서는 지원 되지 않습니다*합니다.  
  
`[ \@centralized_conflicts = ] 'centralized_conflicts'` 충돌 레코드가 게시자에 저장 된 경우를 지정 합니다. *centralized_conflicts* 됩니다 **nvarchar(5)** , 기본값은 TRUE입니다. 하는 경우 **true**에 충돌 레코드가 게시자에 저장 됩니다. 하는 경우 **false**에 충돌 레코드가 충돌을 일으킨 구독자 및 게시자 양쪽 모두에서 저장 됩니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*합니다.  
  
`[ \@conflict_retention = ] conflict_retention` 충돌 보존 기간을 일 단위로 지정 합니다. 피어 투 피어 트랜잭션 복제 및 지연 업데이트 구독에 대해 충돌 메타데이터가 저장되는 기간입니다. *conflict_retention* 됩니다 **int**, 기본값은 14입니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*합니다.  
  
`[ \@queue_type = ] 'queue_type'` 사용할 큐의 유형을 지정 합니다. *queue_type* 됩니다 **nvarchar(10)** , 기본값은 NULL 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**sql**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 트랜잭션을 저장합니다.|  
|NULL(기본값)|기본값으로 **sql**를 사용 하도록 지정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 트랜잭션을 저장 합니다.|  
  
> [!NOTE]  
>  MSMQ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing) 사용이 더 이상 지원되지 않습니다. 값을 지정 **msmq** 경고를 발생 하 고 복제 값이 자동으로 설정 됩니다 **sql**합니다.  
  
 *Oracle 게시자에 대해서는 지원 되지 않습니다*합니다.  
  
`[ \@add_to_active_directory = ] 'add\to_active_directory'` 이 매개 변수는 않으며 스크립트와의 이전 버전과 호환성에 대해서만 지원 됩니다. 더 이상 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory에 게시 정보를 추가할 수 없습니다.  
  
`[ \@logreader_job_name = ] 'logreader_agent_name'` 기존 에이전트 작업의 이름이입니다. *logreader_agent_name* 됩니다 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 로그 판독기 에이전트가 새로 만든 작업 대신 기존 작업을 사용하는 경우에만 지정됩니다.  
  
`[ \@qreader_job_name = ] 'queue_reader_agent_name'` 기존 에이전트 작업의 이름이입니다. *queue_reader_agent_name* 됩니다 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 큐 판독기 에이전트가 새로 만든 작업 대신 기존 작업을 사용하는 경우에만 지정됩니다.  
  
`[ \@publisher = ] 'publisher'` 지정 된 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에 게시를 추가 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
`[ \@allow_initialize_from_backup = ] 'allow_initialize_from_backup'` 경우 구독자가 구독을 초기화할 수이 게시에는 초기 스냅숏이 아닌 백업 으로부터 나타냅니다. *allow_initialize_from_backup* 됩니다 **nvarchar(5)** , 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**true**|백업으로부터 초기화할 수 있습니다.|  
|**false**|백업으로부터 초기화할 수 없습니다.|  
|NULL(기본값)|기본값으로 **true** 피어 투 피어 복제 토폴로지에서 게시에 대 한 및 **false** 다른 모든 게시에 대 한 합니다.|  
  
 자세한 내용은 [스냅샷 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.  
  
> [!WARNING]  
>  구독자 데이터가 누락되는 것을 방지하려면 **에서** sp_addpublication `@allow_initialize_from_backup = N'true'`을 사용할 때 항상 `@immediate_sync = N'true'`를 사용하십시오.  
  
`[ \@replicate_ddl = ] replicate_ddl` 게시에 대해 스키마 복제가 지원 되는지 여부를 나타냅니다. *replicate_ddl* 됩니다 **int**, 기본값은 **1** 에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자 및 **0** 에 대 한 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. **1** 게시자에서 실행 하는 데이터 정의 언어 (DDL) 문이 복제 됩니다 및 **0** DDL 문이 복제 되지 않음을 나타냅니다. *Oracle 게시자에 대해 스키마 복제가 지원 되지 않습니다.* 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
 합니다  *\@replicate_ddl* 매개 변수는 DDL 문이 열을 추가 하는 경우에 적용 됩니다. 합니다  *\@replicate_ddl* DDL 문은 변경 하거나 다음과 같은 이유로 열을 삭제 하는 경우 매개 변수가 무시 됩니다.  
  
-   열을 삭제 하는 경우 새 DML 문에 삭제 된 배포 에이전트 실패를 유발 하는 열을 포함 하지 않으려면 sysarticlecolumns 업데이트 되어야 합니다. 합니다  *\@replicate_ddl* 복제 스키마 변경 복제 항상 해야 하기 때문에 매개 변수가 무시 됩니다.  
  
-   열이 변경될 경우 원본 데이터 형식 또는 Null 허용 여부가 변경되었을 수 있으므로 DML 문에 구독자에 있는 테이블과 호환되지 않는 값이 포함될 수 있습니다. 이러한 DML 문으로 인해 배포 에이전트가 실패할 수 있습니다. 합니다  *\@replicate_ddl* 복제 스키마 변경 복제 항상 해야 하기 때문에 매개 변수가 무시 됩니다.  
  
-   DDL 문이 새 열을 추가 하면 sysarticlecolumns 새 열을 포함 하지 않습니다. DML 문은 새 열에 대해 데이터 복제를 시도하지 않습니다. DDL을 복제하거나 복제하지 않는 경우가 모두 허용되므로 매개 변수가 인식됩니다.  
  
`[ \@enabled_for_p2p = ] 'enabled_for_p2p'` 게시를에 피어 투 피어 복제 토폴로지에서 사용할 수 있습니다. *enabled_for_p2p* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. **true** 게시에서 피어 투 피어 복제를 지원함을 나타냅니다. 설정 하는 경우 *enabled_for_p2p* 에 **true**, 다음 제한 사항이 적용 됩니다.  
  
-   *allow_anonymous* 있어야 **false**합니다.  
  
-   *allow_dts* 있어야 **false**합니다.  
  
-   *allow_initialize_from_backup* 있어야 **true**합니다.  
  
-   *allow_queued_tran* 있어야 **false**합니다.  
  
-   *allow_sync_tran* 있어야 **false**합니다.  
  
-   *conflict_policy* 있어야 **false**합니다.  
  
-   *independent_agent* 있어야 **true**합니다.  
  
-   *repl_freq* 있어야 **연속**합니다.  
  
-   *replicate_ddl* 있어야 **1**합니다.  
  
 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
`[ \@publish_local_changes_only = ] 'publish_local_changes_only'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ \@enabled_for_het_sub = ] 'enabled_for_het_sub'` 비-지원 하도록 게시를 설정[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다. *enabled_for_het_sub* 됩니다 **nvarchar(5)** 이며 기본값은 FALSE입니다. 값이 **true** 지원 이외 게시 한다는 의미[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다. 때 *enabled_for_het_sub* 은 **true**, 다음과 같은 제한 사항이 적용 됩니다.  
  
-   *allow_initialize_from_backup* 있어야 **false**합니다.  
  
-   *allow_push* 있어야 **true**합니다.  
  
-   *allow_queued_tran* 있어야 **false**합니다.  
  
-   *allow_subscription_copy* 있어야 **false**합니다.  
  
-   *allow_sync_tran* 있어야 **false**합니다.  
  
-   *autogen_sync_procs* 있어야 **false**합니다.  
  
-   *conflict_policy* NULL 이어야 합니다.  
  
-   *enabled_for_internet* 있어야 **false**합니다.  
  
-   *enabled_for_p2p* 있어야 **false**합니다.  
  
-   *ftp_address* NULL 이어야 합니다.  
  
-   *ftp_subdirectory* NULL 이어야 합니다.  
  
-   *ftp_password* NULL 이어야 합니다.  
  
-   *pre_snapshot_script* NULL 이어야 합니다.  
  
-   *post_snapshot_script* NULL 이어야 합니다.  
  
-   *replicate_ddl* 0 이어야 합니다.  
  
-   *qreader_job_name* NULL 이어야 합니다.  
  
-   *queue_type* NULL 이어야 합니다.  
  
-   *sync_method* 일 수 없습니다 **네이티브** 하거나 **동시**합니다.  
  
 자세한 내용은 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)을(를) 참조하세요.  
  
`[ \@p2p_conflictdetection = ] 'p2p_conflictdetection'` 배포 에이전트가 게시는 피어 투 피어 복제용으로 활성화 하는 경우 충돌을 검색할 수 있습니다. *p2p_conflictdetection* 됩니다 **nvarchar(5)** 이며 기본값은 TRUE입니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을(를) 참조하세요.  
  
`[ \@p2p_originator_id = ] p2p_originator_id` 피어 투 피어 토폴로지의 노드에 대 한 ID를 지정합니다. *p2p_originator_id* 됩니다 **int**, 기본값은 NULL입니다. 이 ID 경우 충돌 검색에 사용 됩니다 *p2p_conflictdetection* 가 TRUE로 설정 합니다. 토폴로지에 사용되지 않은 0이 아닌 양수 ID를 지정합니다. 이미 사용 하는 Id의 목록에서 실행할 [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md)합니다.  
  
`[ \@p2p_continue_onconflict = ] 'p2p_continue_onconflict'` 배포 에이전트가 계속 충돌이 검색 된 후 변경 내용을 처리할 수 있는지 여부를 결정 합니다. *p2p_continue_onconflict* 됩니다 **nvarchar(5)** 이며 기본값은 FALSE입니다.  
  
> [!CAUTION]  
>  기본값인 FALSE를 사용하는 것이 좋습니다. 이 옵션이 TRUE로 설정된 경우 배포 에이전트는 송신자 ID가 가장 높은 노드에서 충돌 행을 적용하여 토폴로지의 데이터를 일치시킵니다. 이 방법으로 데이터가 일치하게 되지 않는 경우도 있습니다. 충돌이 검색된 후 토폴로지의 일관성을 확인해야 합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)의 "충돌 처리"를 참조하십시오.  
  
  
`[ \@allow_partition_switch = ] 'allow_partition_switch'` 지정 여부를 ALTER TABLE... SWITCH 문은 게시 된 데이터베이스에 대해 실행할 수 있습니다. *allow_partition_switch* 됩니다 **nvarchar(5)** 이며 기본값은 FALSE입니다. 자세한 내용은 [분할 테이블 및 인덱스 복제](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)를 참조하세요.  
  
`[ \@replicate_partition_switch = ] 'replicate_partition_switch'` 지정 여부를 ALTER TABLE... 게시 데이터베이스에 대해 실행 되는 스위치 문은 구독자에 복제 되어야 합니다. *replicate_partition_switch* 됩니다 **nvarchar(5)** 이며 기본값은 FALSE입니다. 이 옵션을 사용할 경우에만 *allow_partition_switch* 가 TRUE로 설정 합니다.  

## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addpublication** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 같은 데이터베이스 개체를 사용 하는 게시에 게시 하는 게시가 여러 개 있으면 한 *replicate_ddl* 의 값 **1** ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION 복제 및 ALTER TRIGGER DDL 문입니다. 그러나 ALTER TABLE DROP COLUMN DDL 문은 삭제된 열을 게시하는 모든 게시에 의해 복제됩니다.  
  
 DDL 복제를 사용 하도록 설정 (*replicate_ddl* = **1**) 게시의 경우 복제 하지 않을 DDL 변경 내용을 적용 하려면 해당 게시를 [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 설정 하려면 먼저 실행 해야 합니다 *replicate_ddl* 하려면 **0**합니다. 복제 하지 않을 DDL 문을 발급 한 후 [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) DDL 복제를 다시 설정 하려면 다시 실행할 수 있습니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_addpublication**합니다. Windows 인증 로그인에는 Windows 사용자 계정을 나타내는 데이터베이스의 사용자 계정이 있어야 합니다. Windows 그룹을 나타내는 사용자 계정은 충분하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_addlogreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
