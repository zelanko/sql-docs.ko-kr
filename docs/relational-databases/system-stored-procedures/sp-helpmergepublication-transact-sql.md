---
description: sp_helpmergepublication(Transact-SQL)
title: sp_helpmergepublication (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepublication
- sp_helpmergepublication_TSQL
helpviewer_keywords:
- sp_helpmergepublication
ms.assetid: dfe1e1e1-9a65-406a-aced-6385a078e135
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1042543ba82dcbd4bc7376acf6943a838506b6fa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549606"
---
# <a name="sp_helpmergepublication-transact-sql"></a>sp_helpmergepublication(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  병합 게시에 대한 정보를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @publication **=** ] **'**_게시_**'**  
 게시의 이름입니다. *게시*는 **sysname**이며 기본값은 **%** 현재 데이터베이스의 모든 병합 게시에 대 한 정보를 반환 하는입니다.  
  
 [ @found **=** ] **'***found***'** 출력  
 행을 반환하는지 여부를 나타내는 플래그입니다. *검색*된 **int** 및 OUTPUT 매개 변수 이며 기본값은 NULL입니다. **1** 은 게시가 발견 되었음을 나타냅니다. **0** 은 게시를 찾을 수 없음을 나타냅니다.  
  
 [ @publication_id **=** ] **'***publication_id***'** 출력  
 게시 ID 번호입니다. *publication_id* 은 **uniqueidentifier** 및 OUTPUT 매개 변수 이며 기본값은 NULL입니다.  
  
 [ @reserved **=** ] **'***예약 됨***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]*reserved* 는 **nvarchar (20)** 이며 기본값은 NULL입니다.  
  
 [ @publisher **=** ] **'***게시자***'**  
 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
 [ @publisher_db **=** ] **'***publisher_db***'**  
 게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|결과 집합 목록 내 게시의 순차적 순서입니다.|  
|name|**sysname**|게시의 이름입니다.|  
|description|**nvarchar(255)**|게시에 대한 설명입니다.|  
|상태|**tinyint**|게시 데이터를 언제 사용할 수 있는지 나타냅니다.|  
|retention|**int**|게시에 있는 아티클의 변경 내용에 대한 메타데이터를 저장하는 데 걸린 시간입니다. 이 기간의 단위는 일, 주, 월 또는 년으로 지정할 수 있습니다. 단위에 대한 자세한 내용은 retention_period_unit 열을 참조하십시오.|  
|sync_mode|**tinyint**|해당 게시의 동기화 모드입니다.<br /><br /> **0** = 네이티브 대량 복사 프로그램 (**bcp** 유틸리티)<br /><br /> **1** = 문자 대량 복사|  
|allow_push|**int**|지정된 게시에 대해 밀어넣기 구독을 만들 수 있는지 여부를 나타냅니다. **0** 은 밀어넣기 구독이 허용 되지 않음을 의미 합니다.|  
|allow_pull|**int**|지정된 게시에 대해 끌어오기 구독을 만들 수 있는지 여부를 나타냅니다. **0** 은 끌어오기 구독이 허용 되지 않음을 의미 합니다.|  
|allow_anonymous|**int**|지정된 게시에 대해 익명 구독을 만들 수 있는지 여부를 나타냅니다. **0** 은 익명 구독이 허용 되지 않음을 의미 합니다.|  
|centralized_conflicts|**int**|지정한 게시자에 충돌 레코드가 저장되는지 여부를 나타냅니다.<br /><br /> **0** = 충돌을 일으킨 게시자와 구독자 모두에 충돌 레코드가 저장 됩니다.<br /><br /> **1** = 모든 충돌 레코드가 게시자에 저장 됩니다.|  
|priority|**float (8)**|루프 백 구독의 우선 순위입니다.|  
|snapshot_ready|**tinyint**|해당 게시의 스냅샷이 준비되었는지 여부를 나타냅니다.<br /><br /> **0** = 스냅숏을 사용할 준비가 되었습니다.<br /><br /> **1** = 스냅숏을 사용할 준비가 되지 않았습니다.|  
|publication_type|**int**|게시 유형입니다.<br /><br /> **0** = 스냅숏<br /><br /> **1** = 트랜잭션.<br /><br /> **2** = 병합.|  
|pubid|**uniqueidentifier**|해당 게시의 고유 식별자입니다.|  
|snapshot_jobid|**binary(16)**|스냅샷 에이전트의 작업 ID입니다. [Sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md) 시스템 테이블에서 스냅숏 작업에 대 한 항목을 가져오려면이 16 진수 값을 **uniqueidentifier**로 변환 해야 합니다.|  
|enabled_for_internet|**int**|인터넷에서 게시를 사용할 수 있는지 여부를 나타냅니다. **1**인 경우 게시에 대 한 동기화 파일이 디렉터리에 배치 됩니다 `C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\Ftp` . 사용자가 FTP(파일 전송 프로토콜) 디렉터리를 만들어야 합니다. **0**인 경우 게시는 인터넷에 액세스할 수 없습니다.|  
|dynamic_filter|**int**|매개 변수가 있는 행 필터가 사용되는지 여부를 나타냅니다. **0** 은 매개 변수가 있는 행 필터가 사용 되지 않음을 의미 합니다.|  
|has_subscription|**bit**|게시에 구독이 있는지 여부를 나타냅니다. **0** 은 현재이 게시에 대 한 구독이 없음을 의미 합니다.|  
|snapshot_in_default_folder|**bit**|스냅샷 파일을 기본 폴더에 저장하는지 여부를 지정합니다.<br /><br /> **1**인 경우 기본 폴더에서 스냅숏 파일을 찾을 수 있습니다.<br /><br /> **0**인 경우 스냅숏 파일이 **alt_snapshot_folder**에 지정 된 대체 위치에 저장 됩니다. 대체 위치는 다른 서버, 네트워크 드라이브 또는 이동식 미디어(예, CD-ROM 또는 이동식 디스크)가 될 수 있습니다. 또한 구독자가 나중에 검색할 수 있도록 FTP 사이트에 스냅샷 파일을 저장할 수도 있습니다.<br /><br /> 참고:이 매개 변수는 true 일 수 있으며 여전히 **alt_snapshot_folder** 매개 변수에 위치를 포함 합니다. 이 경우 스냅샷 파일은 기본 위치와 대체 위치에 모두 저장됩니다.|  
|alt_snapshot_folder|**nvarchar(255)**|스냅샷의 대체 폴더 위치를 지정합니다.|  
|pre_snapshot_script|**nvarchar(255)**|구독자에서 스냅숏을 적용할 때 병합 에이전트 복제 된 개체 스크립트 보다 먼저 실행 되는 **.sql** 파일에 대 한 포인터를 지정 합니다.|  
|post_snapshot_script|**nvarchar(255)**|초기 동기화 중에 다른 모든 복제 된 개체 스크립트 및 데이터를 적용 한 후 병합 에이전트 실행 되는 **.sql** 파일에 대 한 포인터를 지정 합니다.|  
|compress_snapshot|**bit**|**Alt_snapshot_folder** 위치에 기록 되는 스냅숏이 CAB 형식으로 압축 되도록 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|  
|ftp_address|**sysname**|배포자용 FTP 서비스의 네트워크 주소입니다. 병합 에이전트가 선택할 게시 스냅샷 파일의 위치를 지정합니다.|  
|ftp_port|**int**|배포자용 FTP 서비스의 포트 번호입니다. **ftp_port** 기본값은 **21**입니다. 병합 에이전트가 선택할 게시 스냅샷 파일의 위치를 지정합니다.|  
|ftp_subdirectory|**nvarchar(255)**|FTP를 사용하여 스냅샷을 배달할 때 배포 에이전트에서 스냅샷 파일을 선택할 수 있는 위치를 지정합니다.|  
|ftp_login|**sysname**|FTP 서비스 연결에 사용되는 사용자 이름입니다.|  
|conflict_retention|**int**|충돌을 보존할 보존 기간을 일 수로 지정합니다. 지정한 일 수가 지나면 충돌 행은 충돌 테이블에서 제거됩니다.|  
|keep_partition_changes|**int**|해당 게시에 대해 동기화가 최적화되는지 여부를 지정합니다. **keep_partition_changes** 기본값은 **0**입니다. 값이 **0** 이면 동기화가 최적화 되지 않으며 파티션에서 데이터가 변경 될 때 모든 구독자에 게 전송 된 파티션이 확인 됩니다.<br /><br /> **1** 은 동기화가 최적화 되었음을 의미 하며 변경 된 파티션에 행이 있는 구독자만 영향을 받습니다.<br /><br /> 참고: 기본적으로 병합 게시는이 옵션 보다 높은 수준의 최적화를 제공 하는 사전 계산 파티션을 사용 합니다. 자세한 내용은 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) 및 [사전 계산 파티션을 사용 하 여 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조 하세요.|  
|allow_subscription_copy|**int**|해당 게시를 구독하는 구독 데이터베이스를 복사하는 기능이 활성화되었는지 여부를 지정합니다. 값 **0** 은 복사가 허용 되지 않음을 의미 합니다.|  
|allow_synctoalternate|**int**|대체 동기화 파트너가 해당 게시자와 동기화될 수 있는지 여부를 지정합니다. **0** 값은 동기화 파트너가 허용 되지 않음을 의미 합니다.|  
|validate_subscriber_info|**nvarchar (500)**|구독자 정보를 검색하고 구독자에서 매개 변수가 있는 행 필터링 조건의 유효성을 검사하는 데 사용하는 함수를 나열합니다. 정보가 각 병합으로 일관성 있게 분할되는지 확인하는 데 유용합니다.|  
|backward_comp_level|**int**|데이터베이스 호환성 수준으로서 다음 값 중 하나일 수 있습니다.<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_activedirectory|**bit**|게시 정보가 Active Directory에 게시되는지 여부를 지정합니다. 값 **0** 은 Active Directory에서 게시 정보를 사용할 수 없음을 의미 합니다.<br /><br /> 이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해서만 지원됩니다. 더 이상 Active Directory에 게시 정보를 추가할 수 없습니다.|  
|max_concurrent_merge|**int**|동시 병합 프로세스의 수입니다. **0**인 경우에는 지정 된 시간에 실행 중인 동시 병합 프로세스 수에 제한이 없습니다.|  
|max_concurrent_dynamic_snapshots|**int**|병합 게시에 대해 실행할 수 있는 필터링된 동시 데이터 스냅샷 세션의 최대 수입니다. **0**인 경우 지정 된 시간에 게시에 대해 동시에 실행할 수 있는 필터링 된 동시 데이터 스냅숏 세션의 최대 수에 제한이 없습니다.|  
|use_partition_groups|**int**|사전 계산 파티션이 사용되는지 여부를 나타냅니다. 값 **1** 은 사전 계산 파티션이 사용 됨을 의미 합니다.|  
|num_of_articles|**int**|게시의 아티클 수입니다.|  
|replicate_ddl|**int**|게시된 테이블의 스키마 변경을 복제하는지 여부를 지정합니다. 값 **1** 은 스키마 변경이 복제 됨을 의미 합니다.|  
|publication_number|**smallint**|해당 게시에 할당된 번호입니다.|  
|allow_subscriber_initiated_snapshot|**bit**|구독자가 필터링된 데이터 스냅샷 생성 프로세스를 시작할 수 있는지 여부를 나타냅니다. 값 **1** 은 구독자가 스냅숏 프로세스를 시작할 수 있음을 의미 합니다.|  
|allow_web_synchronization|**bit**|웹 동기화에 게시를 사용할 수 있는지 여부를 나타냅니다. 값 **1** 은 웹 동기화가 사용 됨을 의미 합니다.|  
|web_synchronization_url|**nvarchar (500)**|웹 동기화에 사용되는 인터넷 URL입니다.|  
|allow_partition_realignment|**bit**|게시자에서 행을 수정하여 파티션이 변경되는 경우 구독자에 삭제 내용을 보낼지 여부를 나타냅니다. 값 **1** 은 삭제가 구독자에 전송 됨을 의미 합니다.  자세한 내용은 [sp_addmergepublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)를 참조 하세요.|  
|retention_period_unit|**tinyint**|보존 기간을 정할 때 사용할 단위를 정의합니다. 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 일<br /><br /> **1** = 주<br /><br /> **2** = 개월<br /><br /> **3** = 년|  
|has_downloadonly_articles|**bit**|게시에 속한 아티클이 다운로드 전용 아티클인지 여부를 나타냅니다. 값 **1** 은 다운로드 전용 아티클이 있음을 나타냅니다.|  
|decentralized_conflicts|**int**|충돌을 일으킨 구독자에 충돌 레코드가 저장되는지 여부를 나타냅니다. 값이 **0** 이면 충돌 레코드가 구독자에 저장 되지 않습니다. 값이 1이면 충돌 레코드가 구독자에 저장됩니다.|  
|generation_leveling_threshold|**int**|하나의 생성에 포함되는 변경 내용 수를 지정합니다. 생성은 게시자 또는 구독자에 배달되는 변경 내용 모음입니다.|  
|automatic_reinitialization_policy|**bit**|자동 다시 초기화가 발생하기 전에 구독자에서 변경 사항을 업로드할지 여부를 나타냅니다. 값 **1** 은 자동 다시 초기화가 발생 하기 전에 구독자에서 변경 내용이 업로드 됨을 나타냅니다. 값이 0이면 자동 다시 초기화가 발생하기 전에 변경 내용이 업로드되지 않습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_helpmergepublication은 병합 복제에 사용됩니다.  
  
## <a name="permissions"></a>사용 권한  
 게시에 대한 게시 액세스 목록의 멤버는 해당 게시에 대해 sp_helpmergepublication을 실행할 수 있습니다. 게시 데이터베이스에서 db_owner 고정 데이터베이스 역할의 멤버는 모든 게시의 정보에 대해 sp_helpmergepublication을 실행할 수 있습니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_helpmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-helpmergepublication-_1.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Transact-sql&#41;sp_addmergepublication &#40;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergepublication &#40;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
