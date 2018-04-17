---
title: sp_helpmergepublication (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helpmergepublication
- sp_helpmergepublication_TSQL
helpviewer_keywords:
- sp_helpmergepublication
ms.assetid: dfe1e1e1-9a65-406a-aced-6385a078e135
caps.latest.revision: 55
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d5005db95a4153259dd000cda87823368255a722
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpmergepublication-transact-sql"></a>sp_helpmergepublication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시에 대한 정보를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergepublication [ [ @publication = ] 'publication' ]  
    [ , [ @found = ] 'found' OUTPUT ]  
    [ , [ @publication_id = ] 'publication_id' OUTPUT ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @publication **=** ] **'***게시***'**  
 게시의 이름입니다. *게시*은 **sysname**, 기본값은 **%**, 현재 데이터베이스의 모든 병합 게시에 대 한 정보를 반환 하는 합니다.  
  
 [ @found **=** ] **'***발견***'** 출력  
 행을 반환하는지 여부를 나타내는 플래그입니다. *찾을*은 **int** 및 출력 매개 변수, 기본값은 NULL입니다. **1** 은 게시를 찾았음을 나타냅니다. **0** 게시를 찾지 못했음을 나타냅니다.  
  
 [ @publication_id **=**] **'***publication_id***'** 출력  
 게시 ID 번호입니다. *publication_id* 은 **uniqueidentifier** 및 출력 매개 변수, 기본값은 NULL입니다.  
  
 [ @reserved **=**] **'***예약***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *예약 된* 은 **nvarchar (20)**, 기본값은 NULL입니다.  
  
 [ @publisher **=** ] **'***게시자***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
 [@publisher_db **=** ] **'***publisher_db***'**  
 게시 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|결과 집합 목록 내 게시의 순차적 순서입니다.|  
|name|**sysname**|게시의 이름입니다.|  
|description|**nvarchar(255)**|게시에 대한 설명입니다.|  
|상태|**tinyint**|게시 데이터를 언제 사용할 수 있는지 나타냅니다.|  
|retention|**int**|게시에 있는 아티클의 변경 내용에 대한 메타데이터를 저장하는 데 걸린 시간입니다. 이 기간의 단위는 일, 주, 월 또는 년으로 지정할 수 있습니다. 단위에 대한 자세한 내용은 retention_period_unit 열을 참조하십시오.|  
|sync_mode|**tinyint**|해당 게시의 동기화 모드입니다.<br /><br /> **0** = 네이티브 대량 복사 프로그램 (**bcp** 유틸리티)<br /><br /> **1** = 문자 대량 복사|  
|allow_push|**int**|지정된 게시에 대해 밀어넣기 구독을 만들 수 있는지 여부를 나타냅니다. **0** 은 밀어넣기 구독을 허용 하지 않음을 의미 합니다.|  
|allow_pull|**int**|지정된 게시에 대해 끌어오기 구독을 만들 수 있는지 여부를 나타냅니다. **0** 끌어오기 구독이 허용 되지 않음을 의미 합니다.|  
|allow_anonymous|**int**|지정된 게시에 대해 익명 구독을 만들 수 있는지 여부를 나타냅니다. **0** 익명 구독이 허용 되지 않음을 의미 합니다.|  
|centralized_conflicts|**int**|지정한 게시자에 충돌 레코드가 저장되는지 여부를 나타냅니다.<br /><br /> **0** = 충돌 레코드가 충돌을 일으킨 구독자 및 게시자 양쪽 모두에서 저장 됩니다.<br /><br /> **1** = 모든 충돌 레코드가 게시자에 저장 됩니다.|  
|priority|**float(8)**|루프 백 구독의 우선 순위입니다.|  
|snapshot_ready|**tinyint**|해당 게시의 스냅숏이 준비되었는지 여부를 나타냅니다.<br /><br /> **0** = 스냅숏을 사용할 준비가 되었습니다.<br /><br /> **1** = 스냅숏을 사용할 준비가 되었습니다.|  
|publication_type|**int**|게시 유형입니다.<br /><br /> **0** = 스냅숏 합니다.<br /><br /> **1** = 트랜잭션.<br /><br /> **2** = 병합 합니다.|  
|pubid|**uniqueidentifier**|해당 게시의 고유 식별자입니다.|  
|snapshot_jobid|**binary(16)**|스냅숏 에이전트의 작업 ID입니다. 스냅숏 작업에 대 한 항목을 가져오려면는 [sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md) 시스템 테이블에이 16 진수 값을 변환 해야 **uniqueidentifier**합니다.|  
|enabled_for_internet|**int**|인터넷에서 게시를 사용할 수 있는지 여부를 나타냅니다. 경우 **1**, 게시용 동기화 파일에 저장 되는 `C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\Ftp` 디렉터리입니다. 사용자가 FTP(파일 전송 프로토콜) 디렉터리를 만들어야 합니다. 경우 **0**를 인터넷 액세스용는 게시가 활성화 되지 않았습니다.|  
|dynamic_filter|**int**|매개 변수가 있는 행 필터가 사용되는지 여부를 나타냅니다. **0** 매개 변수가 있는 행 필터가 사용 되지 않음을 의미 합니다.|  
|has_subscription|**bit**|게시에 구독이 있는지 여부를 나타냅니다. **0** 은 현재이 게시에 구독이 없음을 의미 합니다.|  
|snapshot_in_default_folder|**bit**|스냅숏 파일을 기본 폴더에 저장하는지 여부를 지정합니다.<br /><br /> 경우 **1**, 스냅숏 파일이 기본 폴더에 있습니다.<br /><br /> 경우 **0**, 스냅숏 파일으로 지정한 대체 위치에 저장 됩니다 **alt_snapshot_folder**합니다. 대체 위치는 다른 서버, 네트워크 드라이브 또는 이동식 미디어(예, CD-ROM 또는 이동식 디스크)가 될 수 있습니다. 또한 구독자가 나중에 검색할 수 있도록 FTP 사이트에 스냅숏 파일을 저장할 수도 있습니다.<br /><br /> 참고:이 매개 변수 수 true 있고의 위치를 아직 있어서는 **alt_snapshot_folder** 매개 변수입니다. 이 경우 스냅숏 파일은 기본 위치와 대체 위치에 모두 저장됩니다.|  
|alt_snapshot_folder|**nvarchar(255)**|스냅숏의 대체 폴더 위치를 지정합니다.|  
|pre_snapshot_script|**nvarchar(255)**|에 대 한 포인터를 지정 된 **.sql** 이전 복제 된 개체에 병합 에이전트가 실행 되는 파일 스크립트는 구독자에서 스냅숏을 적용할 때.|  
|post_snapshot_script|**nvarchar(255)**|에 대 한 포인터를 지정 된 **.sql** 병합 에이전트가 실행 결국 다른 파일 복제 된 개체 스크립트 및 데이터는 초기 동기화 동안 적용 된 합니다.|  
|compress_snapshot|**bit**|지정 하는 스냅숏에 기록 되는 **alt_snapshot_folder** 위치에 압축는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 형식.|  
|ftp_address|**sysname**|배포자용 FTP 서비스의 네트워크 주소입니다. 병합 에이전트가 선택할 게시 스냅숏 파일의 위치를 지정합니다.|  
|ftp_port|**int**|배포자용 FTP 서비스의 포트 번호입니다. **ftp_port** 는 기본값으로 **21**합니다. 병합 에이전트가 선택할 게시 스냅숏 파일의 위치를 지정합니다.|  
|ftp_subdirectory|**nvarchar(255)**|FTP를 사용하여 스냅숏을 배달할 때 배포 에이전트에서 스냅숏 파일을 선택할 수 있는 위치를 지정합니다.|  
|ftp_login|**sysname**|FTP 서비스 연결에 사용되는 사용자 이름입니다.|  
|conflict_retention|**int**|충돌을 보존할 보존 기간을 일 수로 지정합니다. 지정한 일 수가 지나면 충돌 행은 충돌 테이블에서 제거됩니다.|  
|keep_partition_changes|**int**|해당 게시에 대해 동기화가 최적화되는지 여부를 지정합니다. **keep_partition_changes** 는 기본값으로 **0**합니다. 값이 **0** 동기화가 최적화 되지 않으며 모든 구독자에 게 보낸 파티션은 파티션에서 데이터가 변경 될 때 확인 됩니다.<br /><br /> **1** 동기화가 최적화 되 고 변경된 된 파티션에 행을 가진 구독자만 영향을 받습니다.<br /><br /> 참고: 기본적으로 병합 게시의이 옵션 보다 높은 수준의 최적화를 제공 하는 사전 계산된 파티션을 사용 합니다. 자세한 내용은 참조 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) 및 [Optimize Parameterized Filter Performance with Precomputed](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)합니다.|  
|allow_subscription_copy|**int**|해당 게시를 구독하는 구독 데이터베이스를 복사하는 기능이 활성화되었는지 여부를 지정합니다. 값이 **0** 복사가 허용 되지 않음을 의미 합니다.|  
|allow_synctoalternate|**int**|대체 동기화 파트너가 해당 게시자와 동기화될 수 있는지 여부를 지정합니다. 값이 **0** 동기화 파트너가 허용 되지 않음을 의미 합니다.|  
|validate_subscriber_info|**nvarchar(500)**|구독자 정보를 검색하고 구독자에서 매개 변수가 있는 행 필터링 조건의 유효성을 검사하는 데 사용하는 함수를 나열합니다. 정보가 각 병합으로 일관성 있게 분할되는지 확인하는 데 유용합니다.|  
|backward_comp_level|**int**|데이터베이스 호환성 수준으로서 다음 값 중 하나일 수 있습니다.<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_activedirectory|**bit**|게시 정보가 Active Directory에 게시되는지 여부를 지정합니다. 값이 **0** 게시 정보를 Active Directory에서 사용할 수 없는 것을 의미 합니다.<br /><br /> 이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해서만 지원됩니다. 더 이상 Active Directory에 게시 정보를 추가할 수 없습니다.|  
|max_concurrent_merge|**int**|동시 병합 프로세스의 수입니다. 경우 **0**, 지정된 된 시간에 실행 중인 동시 병합 프로세스 수에 대 한 제한은 없습니다.|  
|max_concurrent_dynamic_snapshots|**int**|병합 게시에 대해 실행할 수 있는 필터링된 동시 데이터 스냅숏 세션의 최대 수입니다. 경우 **0**, 지정된 된 시간에 게시에 대해 동시에 실행할 수 있는 필터링 된 동시 데이터 스냅숏 세션의 최대 수에 대 한 제한은 없습니다.|  
|use_partition_groups|**int**|사전 계산 파티션이 사용되는지 여부를 나타냅니다. 값이 **1** 즉 사전 계산 파티션이 사용 됩니다.|  
|num_of_articles|**int**|게시의 아티클 수입니다.|  
|replicate_ddl|**int**|게시된 테이블의 스키마 변경을 복제하는지 여부를 지정합니다. 값이 **1** 스키마 변경 복제를 의미 합니다.|  
|publication_number|**smallint**|해당 게시에 할당된 번호입니다.|  
|allow_subscriber_initiated_snapshot|**bit**|구독자가 필터링된 데이터 스냅숏 생성 프로세스를 시작할 수 있는지 여부를 나타냅니다. 값이 **1** 구독자가 스냅숏 프로세스를 시작할 수 있음을 의미 합니다.|  
|allow_web_synchronization|**bit**|웹 동기화에 게시를 사용할 수 있는지 여부를 나타냅니다. 값이 **1** 웹 동기화를 사용할 수 있음을 의미 합니다.|  
|web_synchronization_url|**nvarchar(500)**|웹 동기화에 사용되는 인터넷 URL입니다.|  
|allow_partition_realignment|**bit**|게시자에서 행을 수정하여 파티션이 변경되는 경우 구독자에 삭제 내용을 보낼지 여부를 나타냅니다. 값이 **1** 삭제가 구독자에 전송 됩니다.  자세한 내용은 참조 [sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다.|  
|retention_period_unit|**tinyint**|보존 기간을 정할 때 사용할 단위를 정의합니다. 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 일<br /><br /> **1** = 주<br /><br /> **2** = 개월<br /><br /> **3** = 년|  
|has_downloadonly_articles|**bit**|게시에 속한 아티클이 다운로드 전용 아티클인지 여부를 나타냅니다. 값이 **1** 다운로드 전용 아티클이 있음을 나타냅니다.|  
|decentralized_conflicts|**int**|충돌을 일으킨 구독자에 충돌 레코드가 저장되는지 여부를 나타냅니다. 값이 **0** 충돌 레코드가 구독자에서 저장 되지 않습니다 나타냅니다. 값이 1이면 충돌 레코드가 구독자에 저장됩니다.|  
|generation_leveling_threshold|**int**|하나의 생성에 포함되는 변경 내용 수를 지정합니다. 생성은 게시자 또는 구독자에 배달되는 변경 내용 모음입니다.|  
|automatic_reinitialization_policy|**bit**|자동 다시 초기화가 발생하기 전에 구독자에서 변경 사항을 업로드할지 여부를 나타냅니다. 값이 **1** 자동 다시 초기화가 발생 하기 전에 구독자에서 변경 내용이 업로드 됨을 나타냅니다. 값이 0이면 자동 다시 초기화가 발생하기 전에 변경 내용이 업로드되지 않습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_helpmergepublication은 병합 복제에 사용됩니다.  
  
## <a name="permissions"></a>Permissions  
 게시에 대한 게시 액세스 목록의 멤버는 해당 게시에 대해 sp_helpmergepublication을 실행할 수 있습니다. 게시 데이터베이스에서 db_owner 고정 데이터베이스 역할의 멤버는 모든 게시의 정보에 대해 sp_helpmergepublication을 실행할 수 있습니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_helpmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-helpmergepublication-_1.sql)]  
  
## <a name="see-also"></a>관련 항목:  
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
