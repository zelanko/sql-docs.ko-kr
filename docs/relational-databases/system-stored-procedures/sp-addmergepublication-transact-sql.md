---
title: sp_addmergepublication (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords:
- sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c6571ce334c1534dd6fe869f37f007da793469d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118045"
---
# <a name="spaddmergepublication-transact-sql"></a>sp_addmergepublication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 병합 게시를 만듭니다. 이 저장 프로시저는 게시되는 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergepublication [ @publication = ] 'publication'   
    [ , [ @description = ] 'description'   
    [ , [ @retention = ] retention ]   
    [ , [ @sync_mode = ] 'sync_mode' ]   
    [ , [ @allow_push = ] 'allow_push' ]   
    [ , [ @allow_pull = ] 'allow_pull' ]   
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]   
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]   
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @dynamic_filters = ] 'dynamic_filters' ]   
    [ , [ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder' ]   
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @pre_snapshot_script = ] 'pre_snapshot_script' ]   
    [ , [ @post_snapshot_script = ] 'post_snapshot_script' ]   
    [ , [ @compress_snapshot = ] 'compress_snapshot' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]   
    [ , [ @conflict_retention = ] conflict_retention ]   
    [ , [ @keep_partition_changes = ] 'keep_partition_changes' ]   
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]   
    [ , [ @allow_synctoalternate = ] 'allow_synctoalternate' ]   
    [ , [ @validate_subscriber_info = ] 'validate_subscriber_info' ]   
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]   
    [ , [ @max_concurrent_merge = ] maximum_concurrent_merge ]   
    [ , [ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots ]  
    [ , [ @use_partition_groups = ] 'use_partition_groups' ]  
    [ , [ @publication_compatibility_level = ] 'backward_comp_level' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot' ]   
    [ , [ @allow_web_synchronization = ] 'allow_web_synchronization' ]   
    [ , [ @web_synchronization_url = ] 'web_synchronization_url' ]  
    [ , [ @allow_partition_realignment = ] 'allow_partition_realignment' ]  
    [ , [ @retention_period_unit = ] 'retention_period_unit' ]  
    [ , [ @generation_leveling_threshold = ] generation_leveling_threshold ]  
    [ , [ @automatic_reinitialization_policy = ] automatic_reinitialization_policy ]  
    [ , [ @conflict_logging = ] 'conflict_logging' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 만들 병합 게시의 이름이입니다. *게시* 됩니다 **sysname**없습니다 기본적 이며 반드시 키워드가 모든 합니다. 게시의 이름은 데이터베이스 내에서 고유해야 합니다.  
  
`[ @description = ] 'description'` 게시 설명이입니다. *설명* 됩니다 **nvarchar(255)** , 기본값은 NULL입니다.  
  
`[ @retention = ] retention` 보존에서 기간에 대 한 변경 내용을 저장 하려는 기간 단위는 주어진 *게시*합니다. *보존* 됩니다 **int**, 기본값은 14 단위입니다. 보존 기간 단위는 정의한 *retention_period_unit*합니다. 보존 기간 내에 구독이 동기화되지 않고 구독이 받은 보류 중인 변경 내용이 배포자에서 정리 작업에 의해 제거되었으면 구독은 만료되며 다시 초기화해야 합니다. 최대 허용 보존 기간은 9999년 12월 31일과 현재 날짜 사이의 일수입니다.  
  
> [!NOTE]  
>  병합 게시의 보존 기간은 다양한 표준 시간대의 구독자를 수용하기 위해 24시간의 유예 기간을 갖습니다. 예를 들어 보존 기간을 하루로 설정한 경우 실제 보존 기간은 48시간이 됩니다.  
  
`[ @sync_mode = ] 'sync_mode'` 게시에 대 한 구독자의 초기 동기화 모드가입니다. *sync_mode* 됩니다 **nvarchar(10)** , 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**네이티브** (기본값)|모든 테이블의 기본 모드 대량 복사 프로그램 출력을 생성합니다.|  
|**character**|모든 테이블의 문자 모드 대량 복사 프로그램 출력을 생성합니다. 지 원하는 데 필요한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] 및 비-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.|  
  
`[ @allow_push = ] 'allow_push'` 지정된 된 게시에 대 한 밀어넣기 구독을 만들 수 있습니다 하는 경우를 지정 합니다. *allow_push* 됩니다 **nvarchar(5)** , 기본값은 TRUE 허용 하는 밀어넣기 구독에 게시 합니다.  
  
`[ @allow_pull = ] 'allow_pull'` 지정된 된 게시에 대 한 끌어오기 구독을 만들 수 있는지를 지정 합니다. *allow_pull* 됩니다 **nvarchar(5)** , 기본값은 TRUE 허용 하는 끌어오기 구독에 게시 합니다. 지원 하려면 true를 지정 해야 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자입니다.  
  
`[ @allow_anonymous = ] 'allow_anonymous'` 지정된 된 게시에 대 한 익명 구독을 만들 수 있는지를 지정 합니다. *allow_anonymous* 됩니다 **nvarchar(5)** , 기본값은 TRUE 허용 하는 익명 구독에 게시 합니다. 지원 하기 위해 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 를 지정 해야 구독자 **true**합니다.  
  
`[ @enabled_for_internet = ] 'enabled_for_internet'` 게시 인터넷을 사용 하도록 설정 되 고 구독자에 스냅숏 파일을 전송할 파일 전송 프로토콜 (FTP)를 사용할 수 있는 경우 결정을 지정 합니다. *enabled_for_internet* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. 하는 경우 **true**, 게시용 동기화 파일은 C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 디렉터리에 저장 합니다. 사용자는 반드시 Ftp 디렉터리를 만들어야 합니다. 하는 경우 **false**를 인터넷 액세스용는 게시가 활성화 되지 않았습니다.  
  
`[ @centralized_conflicts = ] 'centralized_conflicts'` 이 매개 변수는 않으며 스크립트와의 이전 버전과 호환성에 대해서만 지원 됩니다. 사용 하 여 *conflict_logging* 충돌 레코드가 저장 된 위치를 지정 합니다.  
  
`[ @dynamic_filters = ] 'dynamic_filters'` 매개 변수가 있는 행 필터를 사용 하도록 병합 게시를 설정 합니다. *dynamic_filters* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다.  
  
> [!NOTE]  
>  이 매개 변수를 직접 지정하기보다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 매개 변수가 있는 행 필터를 사용할지 여부를 자동으로 결정할 수 있도록 허용해야 합니다. 값을 지정 하는 경우 **true** 에 대 한 *dynamic_filters*, 문서에 대 한 매개 변수가 있는 행 필터를 정의 해야 합니다. 자세한 내용은 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
`[ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'` 경우에 스냅숏 파일이 기본 폴더에 저장 됩니다 지정 합니다. *snapshot_in_default_folder* 됩니다 **nvarchar(5)** , 기본값은 TRUE입니다. 하는 경우 **true**, 스냅숏 파일이 기본 폴더에서 찾을 수 있습니다. 하는 경우 **false**, 스냅숏 파일에서 지정한 대체 위치에 저장 됩니다 *alternate_snapshot_folder*합니다. 대체 위치는 다른 서버, 네트워크 드라이브 또는 이동식 미디어(예, CD-ROM 또는 이동식 디스크)가 될 수 있습니다. 또한 구독자가 나중에 검색할 수 있도록 FTP(파일 전송 프로토콜) 사이트에 스냅숏 파일을 저장할 수도 있습니다. 이 매개 변수 수 true 일을 하 여 지정 된 위치에 아직 *alt_snapshot_folder*합니다. 이 조합은 스냅숏 파일이 기본 위치 및 대체 위치 양쪽 모두에 저장되도록 지정합니다.  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'` 스냅숏의 대체 폴더의 위치를 지정 합니다. *alternate_snapshot_folder* 됩니다 **nvarchar(255)** , 기본값은 NULL입니다.  
  
`[ @pre_snapshot_script = ] 'pre_snapshot_script'` 에 대 한 포인터를 지정 된 **.sql** 파일 위치입니다. *pre_snapshot_script* 됩니다 **nvarchar(255)** , 기본값은 NULL입니다. 병합 에이전트는 스냅숏을 구독자에 적용할 때 복제된 임의의 개체 스크립트를 실행하기 전에 프리 스냅숏 스크립트를 실행합니다. 구독 데이터베이스에 연결할 때 병합 에이전트에 사용되는 보안 컨텍스트에서 스크립트가 실행됩니다. 프리 스냅숏 스크립트에서 실행 되지 않으므로 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자입니다.  
  
`[ @post_snapshot_script = ] 'post_snapshot_script'` 에 대 한 포인터를 지정 된 **.sql** 파일 위치입니다. *post_snapshot_script* 됩니다 **nvarchar(255)** , 기본값은 NULL입니다. 병합 에이전트는 초기 동기화 동안 복제된 다른 모든 개체 스크립트와 데이터를 적용한 후에 포스트 스냅숏 스크립트를 실행합니다. 구독 데이터베이스에 연결할 때 병합 에이전트에 사용되는 보안 컨텍스트에서 스크립트가 실행됩니다. 포스트 스냅숏 스크립트에서 실행 되지 않으므로 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자입니다.  
  
`[ @compress_snapshot = ] 'compress_snapshot'` 에 작성 한 스냅숏을 지정 합니다 **@alt_snapshot_folder** 위치가로 압축할 수는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 형식으로 합니다. *compress_snapshot* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. **false** 는 스냅숏이 압축 되지 않으면 지정 **true** 는 스냅숏이 압축 되도록 지정 합니다. 2GB 이상의 스냅숏 파일은 압축할 수 없습니다. 압축된 스냅숏 파일은 병합 에이전트가 실행되는 위치에 풀립니다. 압축 스냅숏은 구독자에서 압축 파일을 풀 수 있도록 일반적으로 끌어오기 구독과 함께 사용됩니다. 기본 폴더에 있는 스냅숏은 압축할 수 없습니다. 지원 하기 위해 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 를 지정 해야 구독자 **false**합니다.  
  
`[ @ftp_address = ] 'ftp_address'` 배포자 용 FTP 서비스의 네트워크 주소가입니다. *ftp_address* 됩니다 **sysname**, 기본값은 NULL입니다. 구독자의 병합 에이전트가 선택할 게시 스냅숏 파일의 위치를 지정합니다. 이 속성은 각 게시에 저장 되므로 각 게시에는 서로 다른 *ftp_address*합니다. 게시는 FTP를 사용하여 스냅숏 전파를 지원해야 합니다.  
  
`[ @ftp_port = ] ftp_port` 배포자 용 FTP 서비스의 포트 번호가입니다. *ftp_port* 됩니다 **int**, 기본값은 21입니다. 구독자의 병합 에이전트가 선택할 게시 스냅숏 파일의 위치를 지정합니다. 이 속성은 각 게시에 저장 되므로 각 게시는 고유한 *ftp_port*합니다.  
  
`[ @ftp_subdirectory = ] 'ftp_subdirectory'` 게시에서 FTP를 사용 하 여 스냅숏 전파를 지 원하는 경우 선택할 구독자의 병합 에이전트에 사용할 수 있는 스냅숏 파일 위치를 지정 합니다. *ftp_subdirectory* 됩니다 **nvarchar(255)** , 기본값은 NULL입니다. 이 속성은 각 게시에 저장 되므로 각 게시는 고유한 *ftp_subdirctory* 또는 NULL 값으로 표시 된 하위 디렉터리를 선택 합니다.  
  
 매개 변수가 있는 필터를 이용해 게시에 대한 스냅숏을 미리 생성할 때 각 구독자 파티션에 대한 데이터 스냅숏은 자체 폴더 내에 있어야 합니다. FTP를 사용하여 미리 생성된 스냅숏에 대한 디렉터리 구조는 다음 구조를 따라야 합니다.  
  
 *alternate_snapshot_folder*\ftp\\*publisher_publicationDB_publication*\\*partitionID*.  
  
> [!NOTE]  
>  위에서 기울임꼴로 표시한 값은 게시와 구독자 파티션의 지정 사항에 따라 달라집니다.  
  
`[ @ftp_login = ] 'ftp_login'` FTP 서비스에 연결할 사용자 이름을 사용 됩니다. *ftp_login* 됩니다 **sysname**, 기본값은 '익명'.  
  
`[ @ftp_password = ] 'ftp_password'` FTP 서비스에 연결할 사용자 암호가 사용 됩니다. *ftp_password* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요.  
  
`[ @conflict_retention = ] conflict_retention` 충돌은 보존할 일의 보존 기간을 지정 합니다. *conflict_retention* 됩니다 **int**, 충돌 전까지 14 일의 기본값을 사용 하 여 행은 충돌 테이블에서 제거 됩니다.  
  
`[ @keep_partition_changes = ] 'keep_partition_changes'` 사전 계산된 파티션을 사용할 수 없는 때 파티션 변경 최적화를 사용할지를 지정 합니다. *keep_partition_changes* 됩니다 **nvarchar(5)** , 기본값은 TRUE입니다. **false** 즉 파티션 변경 최적화 되지 및 모든 구독자에 게 보낸 파티션은 파티션에서 데이터가 변경 될 때 확인 됩니다 사전 계산된 파티션을 사용 되지 않는 경우. **true** 즉 파티션 변경 최적화 및 변경된 된 파티션에 행을 가진 구독자만 영향을 받습니다. 사전 계산된 파티션을 사용할 때 설정 *use_partition_groups* 하 **true** 설정 *keep_partition_changes* 하 **false**합니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
> [!NOTE]  
>  값을 지정 하는 경우 **true** 에 대 한 *keep_partition_changes*에 값을 지정 **1** 스냅숏 에이전트 매개 변수에 대해 **-MaxNetworkOptimization** . 이 매개 변수에 대 한 자세한 내용은 참조 하세요. [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)합니다. 에이전트 매개 변수를 지정 하는 방법에 대 한 정보를 참조 하세요 [복제 에이전트 관리](../../relational-databases/replication/agents/replication-agent-administration.md)합니다.  
  
 사용 하 여 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자 *keep_partition_changes* 삭제가 올바르게 전파 되도록 보장 하려면 true로 설정 해야 합니다. false로 설정한 경우 구독자에 예상한 것보다 많은 행이 포함될 수 있습니다.  
  
`[ @allow_subscription_copy = ] 'allow_subscription_copy'` 사용 하거나이 게시를 구독 하는 구독 데이터베이스를 복사 하는 기능을 사용 하지 않도록 설정 합니다. *allow_subscription_copy* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. 복사할 구독 데이터베이스의 크기는 2GB 미만이어야 합니다.  
  
`[ @allow_synctoalternate = ] 'allow_synctoalternate'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @validate_subscriber_info = ] 'validate_subscriber_info'` 매개 변수가 있는 행 필터를 사용할 때 게시 된 데이터의 구독자 파티션을 정의 하는 데 사용 되는 함수를 나열 합니다. *validate_subscriber_info* 됩니다 **nvarchar(500)** , 기본값은 NULL입니다. 병합 에이전트는 이 정보를 사용하여 구독자의 파티션에 대한 유효성을 검사합니다. 예를 들어 있으면 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 는 매개 변수가 있는 행 필터에서 매개 변수 여야 합니다 `@validate_subscriber_info=N'SUSER_SNAME()'`합니다.  
  
> [!NOTE]  
>  이 매개 변수를 직접 지정하기보다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 필터링 조건을 자동으로 결정할 수 있도록 허용해야 합니다.  
  
`[ @add_to_active_directory = ] 'add_to_active_directory'` 이 매개 변수는 않으며 스크립트와의 이전 버전과 호환성에 대해서만 지원 됩니다. 더 이상 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory에 게시 정보를 추가할 수 없습니다.  
  
`[ @max_concurrent_merge = ] maximum_concurrent_merge` 동시 병합 프로세스의 최대 수입니다. *maximum_concurrent_merge* 됩니다 **int** 이며 기본값은 0입니다. 값이 **0** 에이 속성의 지정된 된 시간에 실행 중인 동시 병합 프로세스 수 제한이 있다는 것을 의미 합니다. 이 속성은 병합 게시에 대해 한 시점에 실행할 수 있는 동시 병합 프로세스의 수 제한을 설정합니다. 실행 허용된 값보다 많은 병합 프로세스가 동시에 계획되면 초과 작업은 큐로 이동하여 현재 실행 중인 병합 프로세스가 끝날 때까지 대기합니다.  
  
`[ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots` 구독자 파티션 위한 필터링 된 데이터 스냅숏을 생성 하기 위해 동시에 실행할 수 있는 스냅숏 에이전트 세션의 최대 수입니다. *maximum_concurrent_dynamic_snapshots* 됩니다 **int** 이며 기본값은 0입니다. 하는 경우 **0**, 스냅숏 세션의 수에 대 한 제한은 없습니다. 실행하도록 허용된 값보다 많은 스냅숏 프로세스를 동시에 실행하도록 예약할 경우 초과 작업은 큐에 두고 현재 실행 중인 스냅숏 프로세스가 완료될 때까지 기다립니다.  
  
`[ @use_partition_groups = ] 'use_partition_groups'` 지정 하는 사전 계산 파티션을 동기화 프로세스를 최적화 하기 위해 사용 해야 합니다. *use_partition_groups* 됩니다 **nvarchar(5)** , 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**true**|게시에서 사전 계산 파티션을 사용합니다.|  
|**false**|게시에서 사전 계산 파티션을 사용하지 않습니다.|  
|NULL(default)|시스템이 분할 전략을 결정합니다.|  
  
 기본적으로 사전 계산 파티션이 사용됩니다. 사전 계산된 파티션을 사용 하지 않으려면 *use_partition_groups* 으로 설정 되어 있어야 **false**합니다. NULL인 경우 사전 계산 파티션을 사용할지 여부를 시스템이 결정합니다. 파티션을 사용할 수 없는, 그런 다음이 값은 효과적으로 사전 계산 하는 경우 **false** 오류를 생성 하지 않고 있습니다. 이러한 경우 *keep_partition_changes* 로 설정할 수 있습니다 **true** 일부 최적화를 제공 합니다. 자세한 내용은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) 하 고 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)합니다.  
  
`[ @publication_compatibility_level = ] backward_comp_level` 게시의 이전 버전과 호환성을 나타냅니다. *backward_comp_level* 됩니다 **nvarchar(6)** , 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|버전|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
`[ @replicate_ddl = ] replicate_ddl` 게시에 대해 스키마 복제가 지원 되는지 여부를 나타냅니다. *replicate_ddl* 됩니다 **int**, 기본값은 1입니다. **1** 게시자에서 실행 하는 데이터 정의 언어 (DDL) 문이 복제 됩니다 및 **0** DDL 문이 복제 되지 않음을 나타냅니다. 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
 합니다 *@replicate_ddl* 매개 변수는 DDL 문이 열을 추가 하는 경우에 적용 됩니다. 합니다 *@replicate_ddl* DDL 문은 변경 하거나 다음과 같은 이유로 열을 삭제 하는 경우 매개 변수가 무시 됩니다.  
  
-   열을 삭제 하는 경우 새 DML 문에 삭제 된 배포 에이전트 실패를 유발 하는 열을 포함 하지 않으려면 sysarticlecolumns 업데이트 되어야 합니다. 합니다 *@replicate_ddl* 복제 스키마 변경 복제 항상 해야 하기 때문에 매개 변수가 무시 됩니다.  
  
-   열이 변경될 경우 원본 데이터 형식 또는 Null 허용 여부가 변경되었을 수 있으므로 DML 문에 구독자에 있는 테이블과 호환되지 않는 값이 포함될 수 있습니다. 이러한 DML 문으로 인해 배포 에이전트가 실패할 수 있습니다. 합니다 *@replicate_ddl* 복제 스키마 변경 복제 항상 해야 하기 때문에 매개 변수가 무시 됩니다.  
  
-   DDL 문이 새 열을 추가 하면 sysarticlecolumns 새 열을 포함 하지 않습니다. DML 문은 새 열에 대해 데이터 복제를 시도하지 않습니다. DDL을 복제하거나 복제하지 않는 경우가 모두 허용되므로 매개 변수가 인식됩니다.  
  
`[ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot'` 이 게시에 구독자가 자신의 데이터 파티션 위한 필터링된 된 스냅숏을 생성 하는 스냅숏 프로세스를 시작할 수 하는 경우를 나타냅니다. *allow_subscriber_initiated_snapshot* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. **true** 구독자가 스냅숏 프로세스를 시작할 수 있음을 나타냅니다.  
  
`[ @allow_web_synchronization = ] 'allow_web_synchronization'` 웹 동기화에 게시 하도록 설정할지 여부를 지정 합니다. *allow_web_synchronization* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. **true** HTTPS를 통해이 게시에 대 한 구독을 동기화 할 수 있음을 지정 합니다. 자세한 내용은 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)를 참조하세요. 지원 하기 위해 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 를 지정 해야 구독자 **true**합니다.  
  
`[ @web_synchronization_url = ] 'web_synchronization_url'` 웹 동기화에 사용 되는 인터넷 URL의 기본값을 지정 합니다. *web_synchronization_url 있습니까*s **nvarchar(500)** , 기본값은 NULL입니다. 하나가 설정 되어 있지 않으면 명시적으로 때 기본 인터넷 URL을 정의 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) 실행 됩니다.  
  
`[ @allow_partition_realignment = ] 'allow_partition_realignment'` 게시자에서 행을 수정 하면 해당 파티션이 변경 하는 경우 삭제가 구독자에 보낼지 여부를 결정 합니다. *allow_partition_realignment* 됩니다 **nvarchar(5)** , 기본값은 TRUE입니다. **true** 삭제는 더 이상 구독자의 파티션에 속하지 않는 데이터를 제거 하 여 파티션 변경 결과 반영 하도록 구독자에 게 보냅니다. **false** 여기서 게시자에서이 데이터 변경 내용이 구독자로 복제 되지 것입니다 하지만 구독자에서 변경 내용을 게시자로 복제는 구독자에서 이전 파티션에서 받은 데이터를 유지 합니다. 설정 *allow_partition_realignment* 하 **false** 데이터 기록 목적으로 액세스할 수 있어야 하는 경우 이전 파티션에서 받은 구독에서 데이터를 유지 하는 데 사용 됩니다.  
  
> [!NOTE]  
>  구독자에 남은 데이터는 *allow_partition_realignment* 하 **false** 읽기 전용인 것 처럼 처리 됩니다; 그러나이에서 적용 하는 복제 시스템입니다.  
  
`[ @retention_period_unit = ] 'retention_period_unit'` 기간으로 설정한 보존에 대 한 단위를 지정 *보존*합니다. *retention_period_unit* 됩니다 **nvarchar(10)** , 이며 다음 값 중 하나일 수 있습니다.  
  
|값|버전|  
|-----------|-------------|  
|**일** (기본값)|보존 기간(일)을 지정합니다.|  
|**week**|보존 기간(주)을 지정합니다.|  
|**month**|보존 기간(월)을 지정합니다.|  
|**year**|보존 기간(년)을 지정합니다.|  
  
`[ @generation_leveling_threshold = ] generation_leveling_threshold` 하나의 생성에 포함 된 변경 횟수를 지정 합니다. 생성은 게시자 또는 구독자에 배달되는 변경 내용 모음입니다. *generation_leveling_threshold* 됩니다 **int**를 기본값인 1000입니다.  
  
`[ @automatic_reinitialization_policy = ] automatic_reinitialization_policy` 값의 게시 변경에 따라 요구 되는 자동 다시 초기화 하기 전에 구독자에서 변경 내용을 업로드할지 여부를 지정 **1** 에 대해 지정 된 **@force_reinit_subscription** 합니다. *automatic_reinitialization_policy* 는 bit 이며 기본값은 0입니다. **1** 자동 다시 초기화가 발생 하기 전에 구독자에서 변경 내용이 업로드를 의미 합니다.  
  
> [!IMPORTANT]  
>  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
`[ @conflict_logging = ] 'conflict_logging'` 충돌 레코드가 저장 되는 위치를 지정 합니다. *conflict_logging* 됩니다 **nvarchar(15)** , 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**publisher**|충돌 레코드가 게시자에 저장됩니다.|  
|**subscriber**|충돌 레코드가 충돌을 발생시킨 구독자에 저장됩니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자에 대해서는 지원되지 않습니다.|  
|**both**|충돌 레코드가 게시자와 구독자 둘 다에 저장됩니다.|  
|NULL(기본값)|복제를 자동으로 설정 *conflict_logging* 하 **둘 다** 때 값 *backward_comp_level* 는 **90RTM** 하 **게시자** 다른 모든 경우에 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergepublication** 병합 복제에 사용 됩니다.  
  
 사용 하 여 Active Directory에 게시 개체를 나열 합니다 **@add_to_active_directory** 매개 변수를는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체는 Active Directory에서 이미 만들어져 있어야 합니다.  
  
 같은 데이터베이스 개체를 사용 하는 게시에 게시 하는 게시가 여러 개 있으면 한 *replicate_ddl* 의 값 **1** ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION 복제 및 ALTER TRIGGER DDL 문입니다. 그러나 ALTER TABLE DROP COLUMN DDL 문은 삭제된 열을 게시하는 모든 게시에 의해 복제됩니다.  
  
 에 대 한 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자의 경우 값 *alternate_snapshot_folder* 은 경우에 사용 값 *snapshot_in_default_folder* 됩니다 **false**합니다.  
  
 DDL 복제를 사용 하도록 설정 (_replicate_ddl_ **= 1**)는 게시에 대 한 복제 하지 않을 DDL 변경 내용을 적용 하려면 게시 [sp_changemergepublication &#40; TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 설정 하려면 먼저 실행 해야 합니다 *replicate_ddl* 하 **0**. 복제 하지 않을 DDL 문을 발급 한 후 **sp_changemergepublication** DDL 복제를 다시 설정 하려면 다시 실행할 수 있습니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_addmergepublication**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [sp_changemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
