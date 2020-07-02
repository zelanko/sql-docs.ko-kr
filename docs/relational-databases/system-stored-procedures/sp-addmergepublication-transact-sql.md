---
title: sp_addmergepublication (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 09e3c873ecdab8f967fb454854ae66b3a367ab87
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786246"
---
# <a name="sp_addmergepublication-transact-sql"></a>sp_addmergepublication(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  새 병합 게시를 만듭니다. 이 저장 프로시저는 게시되는 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'`만들 병합 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다. ALL 키워드는 아니어야 합니다. 게시의 이름은 데이터베이스 내에서 고유해야 합니다.  
  
`[ @description = ] 'description'`게시 설명입니다. *description* 은 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @retention = ] retention`지정 된 *게시*에 대 한 변경 내용을 저장할 보존 기간 (보존 기간 단위)입니다. *보존* 기간은 **int**이며 기본값은 14 단위입니다. 보존 기간 단위는 *retention_period_unit*에 의해 정의 됩니다. 보존 기간 내에 구독이 동기화되지 않고 구독이 받은 보류 중인 변경 내용이 배포자에서 정리 작업에 의해 제거되었으면 구독은 만료되며 다시 초기화해야 합니다. 최대 허용 보존 기간은 9999년 12월 31일과 현재 날짜 사이의 일수입니다.  
  
> [!NOTE]  
>  병합 게시의 보존 기간은 다양한 표준 시간대의 구독자를 수용하기 위해 24시간의 유예 기간을 갖습니다. 예를 들어 보존 기간을 하루로 설정한 경우 실제 보존 기간은 48시간이 됩니다.  
  
`[ @sync_mode = ] 'sync_mode'`게시에 대 한 구독자의 초기 동기화 모드입니다. *sync_mode* 은 **nvarchar (10)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**native** (기본값)|모든 테이블의 기본 모드 대량 복사 프로그램 출력을 생성합니다.|  
|**자의**|모든 테이블의 문자 모드 대량 복사 프로그램 출력을 생성합니다. 및 이외 구독자를 지 원하는 데 필요 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.|  
  
`[ @allow_push = ] 'allow_push'`지정 된 게시에 대해 밀어넣기 구독을 만들 수 있는지 여부를 지정 합니다. *allow_push* 은 **nvarchar (5)** 이며 기본값은 게시에 대 한 밀어넣기 구독을 허용 하는 TRUE입니다.  
  
`[ @allow_pull = ] 'allow_pull'`지정 된 게시에 대해 끌어오기 구독을 만들 수 있는지 여부를 지정 합니다. *allow_pull* 은 **nvarchar (5)** 이며 기본값은 게시에 대 한 끌어오기 구독을 허용 하는 TRUE입니다. 구독자를 지원 하려면 true를 지정 해야 합니다 [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
`[ @allow_anonymous = ] 'allow_anonymous'`지정 된 게시에 대해 익명 구독을 만들 수 있는지 여부를 지정 합니다. *allow_anonymous* 은 **nvarchar (5)** 이며 기본값은 게시에서 익명 구독을 허용 하는 TRUE입니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)]구독자를 지원 하려면 **true**를 지정 해야 합니다.  
  
`[ @enabled_for_internet = ] 'enabled_for_internet'`게시가 인터넷에 사용 되는지 여부를 지정 하 고 스냅숏 파일을 구독자로 전송 하는 데 FTP (파일 전송 프로토콜)를 사용할 수 있는지 여부를 결정 합니다. *enabled_for_internet* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **True**이면 게시에 대 한 동기화 파일이 C:\PROGRAM Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 디렉터리에 저장 됩니다. 사용자는 반드시 Ftp 디렉터리를 만들어야 합니다. **False**이면 게시에서 인터넷에 액세스할 수 없습니다.  
  
`[ @centralized_conflicts = ] 'centralized_conflicts'`이 매개 변수는 더 이상 사용 되지 않으며 스크립트의 이전 버전과의 호환성을 위해서만 지원 됩니다. *Conflict_logging* 를 사용 하 여 충돌 레코드가 저장 되는 위치를 지정할 수 있습니다.  
  
`[ @dynamic_filters = ] 'dynamic_filters'`병합 게시에서 매개 변수가 있는 행 필터를 사용할 수 있도록 합니다. *dynamic_filters* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다.  
  
> [!NOTE]  
>  이 매개 변수를 직접 지정하기보다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 매개 변수가 있는 행 필터를 사용할지 여부를 자동으로 결정할 수 있도록 허용해야 합니다. *Dynamic_filters*에 **true** 값을 지정 하는 경우 아티클에 대해 매개 변수가 있는 행 필터를 정의 해야 합니다. 자세한 내용은 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
`[ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'`스냅숏 파일이 기본 폴더에 저장 되는지 여부를 지정 합니다. *snapshot_in_default_folder* 은 **nvarchar (5)** 이며 기본값은 TRUE입니다. **True**인 경우 기본 폴더에서 스냅숏 파일을 찾을 수 있습니다. **False**이면 스냅숏 파일이 *alternate_snapshot_folder*에 지정 된 대체 위치에 저장 됩니다. 대체 위치는 다른 서버, 네트워크 드라이브 또는 이동식 미디어(예, CD-ROM 또는 이동식 디스크)가 될 수 있습니다. 또한 구독자가 나중에 검색할 수 있도록 FTP(파일 전송 프로토콜) 사이트에 스냅샷 파일을 저장할 수도 있습니다. 이 매개 변수는 true 일 수 있으며 *alt_snapshot_folder*로 지정 된 위치를 포함 합니다. 이 조합은 스냅샷 파일이 기본 위치 및 대체 위치 양쪽 모두에 저장되도록 지정합니다.  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`스냅숏에 대 한 대체 폴더의 위치를 지정 합니다. *alternate_snapshot_folder* 는 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @pre_snapshot_script = ] 'pre_snapshot_script'`**.Sql** 파일 위치에 대 한 포인터를 지정 합니다. *pre_snapshot_script* 는 **nvarchar (255)** 이며 기본값은 NULL입니다. 병합 에이전트는 스냅샷을 구독자에 적용할 때 복제된 임의의 개체 스크립트를 실행하기 전에 프리 스냅샷 스크립트를 실행합니다. 구독 데이터베이스에 연결할 때 병합 에이전트에 사용되는 보안 컨텍스트에서 스크립트가 실행됩니다. 프리 스냅숏 스크립트는 구독자에서 실행 되지 않습니다 [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
`[ @post_snapshot_script = ] 'post_snapshot_script'`**.Sql** 파일 위치에 대 한 포인터를 지정 합니다. *post_snapshot_script* 는 **nvarchar (255)** 이며 기본값은 NULL입니다. 병합 에이전트는 초기 동기화 동안 복제된 다른 모든 개체 스크립트와 데이터를 적용한 후에 포스트 스냅샷 스크립트를 실행합니다. 구독 데이터베이스에 연결할 때 병합 에이전트에 사용되는 보안 컨텍스트에서 스크립트가 실행됩니다. 포스트 스냅숏 스크립트는 구독자에서 실행 되지 않습니다 [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
`[ @compress_snapshot = ] 'compress_snapshot'`** \@ Alt_snapshot_folder** 위치에 작성 된 스냅숏이 CAB 형식으로 압축 되도록 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] . *compress_snapshot* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **false** 는 스냅숏이 압축 되지 않도록 지정 합니다. **true** 는 스냅숏이 압축 되도록 지정 합니다. 2GB 이상의 스냅샷 파일은 압축할 수 없습니다. 압축된 스냅샷 파일은 병합 에이전트가 실행되는 위치에 풀립니다. 압축 스냅샷은 구독자에서 압축 파일을 풀 수 있도록 일반적으로 끌어오기 구독과 함께 사용됩니다. 기본 폴더에 있는 스냅샷은 압축할 수 없습니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)]구독자를 지원 하려면 **false**를 지정 해야 합니다.  
  
`[ @ftp_address = ] 'ftp_address'`배포자에 대 한 FTP 서비스의 네트워크 주소입니다. *ftp_address* 는 **sysname**이며 기본값은 NULL입니다. 구독자의 병합 에이전트가 선택할 게시 스냅샷 파일의 위치를 지정합니다. 이 속성은 각 게시에 대해 저장 되므로 각 게시에는 다른 *ftp_address*있을 수 있습니다. 게시는 FTP를 사용하여 스냅샷 전파를 지원해야 합니다.  
  
`[ @ftp_port = ] ftp_port`배포자 용 FTP 서비스의 포트 번호입니다. *ftp_port* 은 **int**이며 기본값은 21입니다. 구독자의 병합 에이전트가 선택할 게시 스냅샷 파일의 위치를 지정합니다. 이 속성은 각 게시에 대해 저장 되므로 각 게시에는 자체 *ftp_port*있을 수 있습니다.  
  
`[ @ftp_subdirectory = ] 'ftp_subdirectory'`게시가 FTP를 사용 하 여 스냅숏 전파를 지원할 경우 구독자가 선택할 수 있는 스냅숏 병합 에이전트 파일의 위치를 지정 합니다. *ftp_subdirectory* 는 **nvarchar (255)** 이며 기본값은 NULL입니다. 이 속성은 각 게시에 대해 저장 되므로 각 게시에는 고유한 *ftp_subdirctory* 있거나 NULL 값으로 표시 된 하위 디렉터리가 없도록 선택할 수 있습니다.  
  
 매개 변수가 있는 필터를 이용해 게시에 대한 스냅샷을 미리 생성할 때 각 구독자 파티션에 대한 데이터 스냅샷은 자체 폴더 내에 있어야 합니다. FTP를 사용하여 미리 생성된 스냅샷에 대한 디렉터리 구조는 다음 구조를 따라야 합니다.  
  
 *alternate_snapshot_folder*\ftp \\ *publisher_publicationDB_publication* \\ *partitionID*.  
  
> [!NOTE]  
>  위에서 기울임꼴로 표시한 값은 게시와 구독자 파티션의 지정 사항에 따라 달라집니다.  
  
`[ @ftp_login = ] 'ftp_login'`FTP 서비스에 연결 하는 데 사용 되는 사용자 이름입니다. *ftp_login* 는 **sysname**이며 기본값은 ' anonymous '입니다.  
  
`[ @ftp_password = ] 'ftp_password'`FTP 서비스에 연결 하는 데 사용 되는 사용자 암호입니다. *ftp_password* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요.  
  
`[ @conflict_retention = ] conflict_retention`충돌을 보존할 보존 기간 (일)을 지정 합니다. *conflict_retention* 는 **int**이며 기본값은 충돌 테이블에서 충돌 행을 제거 하기 전 14 일입니다.  
  
`[ @keep_partition_changes = ] 'keep_partition_changes'`사전 계산 파티션을 사용할 수 없을 때 파티션 변경 최적화를 사용할지 여부를 지정 합니다. *keep_partition_changes* 은 **nvarchar (5)** 이며 기본값은 TRUE입니다. **false** 는 파티션 변경이 최적화 되지 않았음을 의미 하며, 사전 계산 파티션을 사용 하지 않을 경우 파티션에서 데이터가 변경 될 때 모든 구독자에 게 전송 되는 파티션이 확인 됩니다. **true로 설정** 하면 파티션 변경이 최적화 되 고 변경 된 파티션에 행이 있는 구독자만 영향을 받습니다. 사전 계산 파티션을 사용 하는 경우 *use_partition_groups* 를 **true** 로 설정 하 고 *keep_partition_changes* 을 **false**로 설정 합니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
> [!NOTE]  
>  *Keep_partition_changes*에 **true** 값을 지정 하는 경우 스냅숏 에이전트 매개 변수 **-maxnetworkoptimization**에 값 **1** 을 지정 합니다. 이 매개 변수에 대 한 자세한 내용은 [Replication 스냅숏 에이전트](../../relational-databases/replication/agents/replication-snapshot-agent.md)를 참조 하세요. 에이전트 매개 변수를 지정 하는 방법에 대 한 자세한 내용은 [복제 에이전트 관리](../../relational-databases/replication/agents/replication-agent-administration.md)를 참조 하세요.  
  
 구독자를 사용 하 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 는 경우에는 삭제가 올바르게 전파 되도록 *keep_partition_changes* true로 설정 해야 합니다. false로 설정한 경우 구독자에 예상한 것보다 많은 행이 포함될 수 있습니다.  
  
`[ @allow_subscription_copy = ] 'allow_subscription_copy'`이 게시를 구독 하는 구독 데이터베이스를 복사 하는 기능을 사용 하거나 사용 하지 않도록 설정 합니다. *allow_subscription_copy* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. 복사할 구독 데이터베이스의 크기는 2GB 미만이어야 합니다.  
  
`[ @allow_synctoalternate = ] 'allow_synctoalternate'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @validate_subscriber_info = ] 'validate_subscriber_info'`매개 변수가 있는 행 필터를 사용할 때 게시 된 데이터의 구독자 파티션을 정의 하는 데 사용 되는 함수를 나열 합니다. *validate_subscriber_info* 는 **nvarchar (500)** 이며 기본값은 NULL입니다. 병합 에이전트는 이 정보를 사용하여 구독자의 파티션에 대한 유효성을 검사합니다. 예를 들어 매개 변수가 있는 행 필터에 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 를 사용 하는 경우 매개 변수는 이어야 합니다 `@validate_subscriber_info=N'SUSER_SNAME()'` .  
  
> [!NOTE]  
>  이 매개 변수를 직접 지정하기보다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 필터링 조건을 자동으로 결정할 수 있도록 허용해야 합니다.  
  
`[ @add_to_active_directory = ] 'add_to_active_directory'`이 매개 변수는 더 이상 사용 되지 않으며 스크립트의 이전 버전과의 호환성을 위해서만 지원 됩니다. 더 이상 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory에 게시 정보를 추가할 수 없습니다.  
  
`[ @max_concurrent_merge = ] maximum_concurrent_merge`동시 병합 프로세스의 최대 수입니다. *maximum_concurrent_merge* 은 **int** 이며 기본값은 0입니다. 이 속성 값이 **0** 이면 지정 된 시간에 실행 중인 동시 병합 프로세스 수에 제한이 없음을 의미 합니다. 이 속성은 병합 게시에 대해 한 시점에 실행할 수 있는 동시 병합 프로세스의 수 제한을 설정합니다. 실행 허용된 값보다 많은 병합 프로세스가 동시에 계획되면 초과 작업은 큐로 이동하여 현재 실행 중인 병합 프로세스가 끝날 때까지 대기합니다.  
  
`[ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots`구독자 파티션에 대 한 필터링 된 데이터 스냅숏을 생성 하기 위해 동시에 실행할 수 있는 스냅숏 에이전트 세션의 최대 수입니다. *maximum_concurrent_dynamic_snapshots* 은 **int** 이며 기본값은 0입니다. **0**인 경우 스냅숏 세션의 수에 제한이 없습니다. 실행하도록 허용된 값보다 많은 스냅샷 프로세스를 동시에 실행하도록 예약할 경우 초과 작업은 큐에 두고 현재 실행 중인 스냅샷 프로세스가 완료될 때까지 기다립니다.  
  
`[ @use_partition_groups = ] 'use_partition_groups'`동기화 프로세스를 최적화 하는 데 사전 계산 파티션을 사용 하도록 지정 합니다. *use_partition_groups* 은 **nvarchar (5)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**true**|게시에서 사전 계산 파티션을 사용합니다.|  
|**false**|게시에서 사전 계산 파티션을 사용하지 않습니다.|  
|NULL (기본값)|시스템이 분할 전략을 결정합니다.|  
  
 기본적으로 사전 계산 파티션이 사용됩니다. 사전 계산 파티션을 사용 하지 않으려면 *use_partition_groups* 을 **false**로 설정 해야 합니다. NULL인 경우 사전 계산 파티션을 사용할지 여부를 시스템이 결정합니다. 사전 계산 파티션을 사용할 수 없는 경우이 값은 오류를 생성 하지 않고 사실상 **false** 가 됩니다. 이러한 경우에는 *keep_partition_changes* 를 **true** 로 설정 하 여 최적화를 제공할 수 있습니다. 자세한 내용은 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) 및 [사전 계산 파티션을 사용 하 여 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조 하세요.  
  
`[ @publication_compatibility_level = ] backward_comp_level`게시의 이전 버전과의 호환성을 나타냅니다. *backward_comp_level* 은 **nvarchar (6)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Version|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
`[ @replicate_ddl = ] replicate_ddl`게시에 대해 스키마 복제가 지원 되는지 여부를 나타냅니다. *replicate_ddl* 은 **int**이며 기본값은 1입니다. **1** 은 게시자에서 실행 된 ddl (데이터 정의 언어) 문이 복제 됨을 나타내고 **0** 은 ddl 문이 복제 되지 않음을 나타냅니다. 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
 * \@ Replicate_ddl* 매개 변수는 ddl 문이 열을 추가할 때 적용 됩니다. DDL 문이 다음과 같은 이유로 열을 변경 하거나 삭제 하는 경우 * \@ replicate_ddl* 매개 변수는 무시 됩니다.  
  
-   열이 삭제될 경우 새 DML 문에 삭제된 열이 포함되지 않도록 sysarticlecolumns를 업데이트해야 합니다. 삭제된 열이 포함되면 배포 에이전트가 실패합니다. 복제는 항상 스키마 변경 내용을 복제 해야 하므로 * \@ replicate_ddl* 매개 변수는 무시 됩니다.  
  
-   열이 변경될 경우 원본 데이터 형식 또는 Null 허용 여부가 변경되었을 수 있으므로 DML 문에 구독자에 있는 테이블과 호환되지 않는 값이 포함될 수 있습니다. 이러한 DML 문으로 인해 배포 에이전트가 실패할 수 있습니다. 복제는 항상 스키마 변경 내용을 복제 해야 하므로 * \@ replicate_ddl* 매개 변수는 무시 됩니다.  
  
-   DDL 문이 새 열을 추가하는 경우 sysarticlecolumns 에는 새 열이 포함되지 않습니다. DML 문은 새 열에 대해 데이터 복제를 시도하지 않습니다. DDL을 복제하거나 복제하지 않는 경우가 모두 허용되므로 매개 변수가 인식됩니다.  
  
`[ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot'`이 게시에 대 한 구독자가 스냅숏 프로세스를 시작 하 여 해당 데이터 파티션에 대 한 필터링 된 스냅숏을 생성할 수 있는지 여부를 나타냅니다. *allow_subscriber_initiated_snapshot* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **true** 는 구독자가 스냅숏 프로세스를 시작할 수 있음을 나타냅니다.  
  
`[ @allow_web_synchronization = ] 'allow_web_synchronization'`웹 동기화에 게시를 사용 하도록 설정할지 여부를 지정 합니다. *allow_web_synchronization* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **true** 는 HTTPS를 통해이 게시에 대 한 구독을 동기화 할 수 있도록 지정 합니다. 자세한 내용은 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)를 참조하세요. [!INCLUDE[ssEW](../../includes/ssew-md.md)]구독자를 지원 하려면 **true**를 지정 해야 합니다.  
  
`[ @web_synchronization_url = ] 'web_synchronization_url'`웹 동기화에 사용 되는 인터넷 URL의 기본값을 지정 합니다. *web_synchronization_url*s **nvarchar (500)** 이며 기본값은 NULL입니다. [Sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) 실행 될 때 명시적으로 설정 되지 않은 경우 기본 인터넷 URL을 정의 합니다.  
  
`[ @allow_partition_realignment = ] 'allow_partition_realignment'`게시자에서 행을 수정 하 여 파티션을 변경 하는 경우 삭제를 구독자로 보낼지 여부를 결정 합니다. *allow_partition_realignment* 은 **nvarchar (5)** 이며 기본값은 TRUE입니다. **true로 설정** 하면 더 이상 구독자의 파티션에 속하지 않는 데이터를 제거 하 여 파티션 변경 결과를 반영 하는 삭제 내용을 구독자에 게 보냅니다. **false로 설정** 하면 구독자의 이전 파티션에서 데이터가 남게 됩니다. 게시자에서이 데이터에 대 한 변경 내용은이 구독자에 복제 되지 않지만 구독자에서 변경한 내용은 게시자에 복제 됩니다. 기록을 위해 데이터에 액세스할 수 있어야 하는 경우 이전 파티션의 구독에 데이터를 유지 하는 데 **false** 로 *allow_partition_realignment* 를 설정 합니다.  
  
> [!NOTE]  
>  **False** 로 *allow_partition_realignment* 설정의 결과로 구독자에 남아 있는 데이터는 읽기 전용인 것 처럼 처리 되어야 합니다. 그러나이는 복제 시스템에 의해 적용 되지 않습니다.  
  
`[ @retention_period_unit = ] 'retention_period_unit'`보존 기간에 설정 된 보존 기간 단위를 지정 *합니다.* *retention_period_unit* 은 **nvarchar (10)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Version|  
|-----------|-------------|  
|**일** (기본값)|보존 기간(일)을 지정합니다.|  
|**week**|보존 기간(주)을 지정합니다.|  
|**month**|보존 기간(월)을 지정합니다.|  
|**year**|보존 기간(년)을 지정합니다.|  
  
`[ @generation_leveling_threshold = ] generation_leveling_threshold`세대에 포함 된 변경 내용의 수를 지정 합니다. 생성은 게시자 또는 구독자에 배달되는 변경 내용 모음입니다. *generation_leveling_threshold* 은 **int**이며 기본값은 1000입니다.  
  
`[ @automatic_reinitialization_policy = ] automatic_reinitialization_policy`게시 변경에 필요한 자동 다시 초기화를 수행 하기 전에 구독자에서 변경 내용을 업로드 하는지 여부를 지정 합니다. 여기서 값 **1** 은 ** \@ force_reinit_subscription**지정 되었습니다. *automatic_reinitialization_policy* 은 bit 이며 기본값은 0입니다. **1** 은 자동 다시 초기화가 수행 되기 전에 구독자에서 변경 내용이 업로드 됨을 의미 합니다.  
  
> [!IMPORTANT]  
>  매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
`[ @conflict_logging = ] 'conflict_logging'`충돌 레코드가 저장 되는 위치를 지정 합니다. *conflict_logging* 은 **nvarchar (15)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**발행자**|충돌 레코드가 게시자에 저장됩니다.|  
|**구독자**|충돌 레코드가 충돌을 발생시킨 구독자에 저장됩니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자에 대해서는 지원되지 않습니다.|  
|**양방향**|충돌 레코드가 게시자와 구독자 둘 다에 저장됩니다.|  
|NULL(기본값)|*Backward_comp_level* 값이 **90rtm** 이 고 다른 모든 경우에는 **게시자** **에 대 한** *conflict_logging* 자동으로 설정 됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergepublication** 는 병합 복제에 사용 됩니다.  
  
 ** \@ Add_to_active_directory** 매개 변수를 사용 하 여 Active Directory 게시 개체를 나열 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Active Directory에서 개체가 이미 만들어져 있어야 합니다.  
  
 동일한 데이터베이스 개체를 게시 하는 게시가 여러 개 있는 경우 *replicate_ddl* 값이 **1** 인 게시만 ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION 및 alter TRIGGER ddl 문을 복제 합니다. 그러나 ALTER TABLE DROP COLUMN DDL 문은 삭제된 열을 게시하는 모든 게시에 의해 복제됩니다.  
  
 구독자의 경우 [!INCLUDE[ssEW](../../includes/ssew-md.md)] *alternate_snapshot_folder* 값은 *snapshot_in_default_folder* 값이 **false**인 경우에만 사용 됩니다.  
  
 게시에 대해 DDL 복제를 사용 하도록 설정 하는 경우 (_replicate_ddl_**= 1**) 복제 되지 않는 ddl 변경 내용을 sp_changemergepublication 게시에 적용 하려면 먼저 [&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 를 실행 하 여 *replicate_ddl* 를 **0**으로 설정 해야 합니다. 복제 되지 않는 DDL 문을 실행 한 후에는 다시 실행 하 여 DDL 복제를 다시 설정할 수 **sp_changemergepublication** .  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addmergepublication**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Transact-sql&#41;sp_changemergepublication &#40;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergepublication &#40;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergepublication &#40;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
