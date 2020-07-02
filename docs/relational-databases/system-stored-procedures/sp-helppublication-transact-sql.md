---
title: sp_helppublication (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b4c5d3157c6683a793f30eccd878aa9e691c7023
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729217"
---
# <a name="sp_helppublication-transact-sql"></a>sp_helppublication(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  게시에 관한 정보를 반환합니다. 게시의 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행 됩니다. Oracle 게시의 경우 이 저장 프로시저는 배포자에서 모든 데이터베이스에 대해 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`보려는 게시의 이름입니다. *게시* 는 sysname 이며 기본값은 **%** 모든 게시에 대 한 정보를 반환 하는입니다.  
  
`[ @found = ] 'found' OUTPUT`반환 하는 행을 나타내는 플래그입니다. *검색*된 **int** 및 OUTPUT 매개 변수 이며 기본값은 **23456**입니다. **1** 은 게시가 발견 되었음을 나타냅니다. **0** 은 게시를 찾을 수 없음을 나타냅니다.  
  
`[ @publisher = ] 'publisher'`이외 게시자를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 sysname 이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에서 게시 정보를 요청할 때 *게시자* 를 지정 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|pubid|**int**|게시에 대한 ID입니다.|  
|name|**sysname**|게시의 이름입니다.|  
|restricted|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|상태|**tinyint**|게시의 현재 상태입니다.<br /><br /> **0** = 비활성<br /><br /> **1** = 활성|  
|task||이전 버전과의 호환성을 위해서 사용됩니다.|  
|replication frequency|**tinyint**|복제 빈도의 유형입니다.<br /><br /> **0** = 트랜잭션<br /><br /> **1** = 스냅숏|  
|synchronization method|**tinyint**|동기화 모드입니다.<br /><br /> **0** = 네이티브 대량 복사 프로그램 (**bcp** 유틸리티)<br /><br /> **1** = 문자 대량 복사<br /><br /> **3** = 동시, 네이티브 대량 복사 (**bcp**유틸리티)를 사용 하지만 스냅숏 동안 테이블이 잠기지 않음을 의미 합니다.<br /><br /> **4** = Concurrent_c. 문자 대량 복사를 사용 하지만 스냅숏 동안 테이블이 잠기지 않음을 의미 합니다.|  
|description|**nvarchar(255)**|게시에 관한 선택적인 설명입니다.|  
|immediate_sync|**bit**|스냅샷 에이전트가 실행될 때마다 동기화 파일이 생성 또는 다시 생성되는지 여부를 나타냅니다.|  
|enabled_for_internet|**bit**|게시에 관한 동기화 파일이 FTP(파일 전송 프로토콜) 및 기타 서비스를 통해 인터넷에 노출되는지 여부를 나타냅니다.|  
|allow_push|**bit**|게시에서 밀어넣기 구독이 허용되는지 여부를 나타냅니다.|  
|allow_pull|**bit**|게시에서 끌어오기 구독이 허용되는지 여부를 나타냅니다.|  
|allow_anonymous|**bit**|게시에서 익명 구독이 허용되는지 여부를 나타냅니다.|  
|independent_agent|**bit**|해당 게시에 대한 독립 실행형 배포 에이전트가 있는지 여부를 나타냅니다.|  
|immediate_sync_ready|**bit**|스냅샷 에이전트가 새 구독에서 사용할 수 있는 스냅샷을 생성했는지 여부를 나타냅니다. 이 매개 변수는 게시가 새 구독이나 다시 초기화된 구독에 대해 항상 스냅샷을 사용할 수 있도록 설정된 경우에만 정의됩니다.|  
|allow_sync_tran|**bit**|게시에서 즉시 업데이트 구독이 허용되는지 여부를 나타냅니다.|  
|autogen_sync_procs|**bit**|즉시 업데이트 구독을 지원하는 저장 프로시저를 자동으로 생성하는지 여부를 나타냅니다.|  
|snapshot_jobid|**binary(16)**|예약된 태스크 ID입니다.|  
|retention|**int**|지정한 게시에 대해 저장할 변경 내용의 양을 시간으로 나타낸 것입니다.|  
|has subscription|**bit**|게시에 활성 구독이 있는지 여부를 나타냅니다. **1** 은 게시에 활성 구독이 있음을 의미 하 고 **0** 은 게시에 구독이 없음을 의미 합니다.|  
|allow_queued_tran|**bit**|활성화된 게시자에 변경 내용을 적용할 수 있을 때까지 구독자에서 변경 내용 지연을 비활성화할지 여부를 지정합니다. **0**인 경우 구독자의 변경 내용이 큐에 저장 되지 않습니다.|  
|snapshot_in_defaultfolder|**bit**|스냅샷 파일을 기본 폴더에 저장할지 여부를 지정합니다. **0**인 경우 스냅숏 파일이 *alternate_snapshot_folder*에 지정 된 대체 위치에 저장 됩니다. **1**인 경우 기본 폴더에서 스냅숏 파일을 찾을 수 있습니다.|  
|alt_snapshot_folder|**nvarchar(255)**|스냅샷의 대체 폴더 위치를 지정합니다.|  
|pre_snapshot_script|**nvarchar(255)**|**.Sql** 파일 위치에 대 한 포인터를 지정 합니다. 배포 에이전트는 구독자에서 스냅샷을 적용할 때 복제된 개체 스크립트를 실행하기 전에 프리 스냅샷 스크립트를 실행합니다.|  
|post_snapshot_script|**nvarchar(255)**|**.Sql** 파일 위치에 대 한 포인터를 지정 합니다. 배포 에이전트는 초기 동기화 중 복제된 다른 모든 개체 스크립트 및 데이터가 적용된 후 포스트 스냅샷 스크립트를 실행합니다.|  
|compress_snapshot|**bit**|*Alt_snapshot_folder* 위치에 기록 되는 스냅숏이 CAB 형식으로 압축 되도록 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] . **0** 은 스냅숏이 압축 되지 않도록 지정 합니다.|  
|ftp_address|**sysname**|배포자용 FTP 서비스의 네트워크 주소입니다. 선택할 구독자의 배포 에이전트 또는 병합 에이전트에 대한 게시 스냅샷 파일의 위치를 지정합니다.|  
|ftp_port|**int**|배포자용 FTP 서비스의 포트 번호입니다.|  
|ftp_subdirectory|**nvarchar(255)**|게시에서 FTP를 사용하는 스냅샷 전파를 지원하는 경우 선택할 구독자의 배포 에이전트 또는 병합 에이전트에 사용 가능한 스냅샷 파일의 위치를 지정합니다.|  
|ftp_login|**sysname**|FTP 서비스에 연결하는 데 사용되는 사용자 이름입니다.|  
|allow_dts|**bit**|게시에서 데이터 변환을 허용하도록 지정합니다. **0** 은 DTS 변환이 허용 되지 않도록 지정 합니다.|  
|allow_subscription_copy|**bit**|해당 게시를 구독하는 구독 데이터베이스를 복사하는 기능이 활성화되었는지 여부를 지정합니다. **0** 은 복사가 허용 되지 않음을 의미 합니다.|  
|centralized_conflicts|**bit**|게시자에 충돌 레코드를 저장하는지 여부를 지정합니다.<br /><br /> **0** = 충돌을 일으킨 게시자와 구독자 모두에 충돌 레코드가 저장 됩니다.<br /><br /> **1** = 충돌 레코드가 게시자에 저장 됩니다.|  
|conflict_retention|**int**|충돌 보존 기간(일)을 지정합니다.|  
|conflict_policy|**int**|지연 업데이트 구독자 옵션을 사용할 때 수행하는 충돌 해결 정책을 지정합니다. 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **1** = 게시자가 충돌을 적용 합니다.<br /><br /> **2** = 구독자가 충돌을 적용 합니다.<br /><br /> **3** = 구독이 다시 초기화 됩니다.|  
|queue_type||사용할 큐의 유형을 지정합니다. 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **msmq** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] 메시지 큐를 사용 하 여 트랜잭션을 저장 합니다.<br /><br /> **sql** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션을 저장 하는 데 사용 합니다.<br /><br /> 참고: 메시지 큐에 대 한 지원이 중단 되었습니다.|  
|backward_comp_level||데이터베이스 호환성 수준으로서 다음 값 중 하나일 수 있습니다.<br /><br /> **90**  =  90 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100**  =  100 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|게시를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory에 게시할지 여부를 지정합니다. 값 **1** 은 게시 됨을 나타내고 값 **0** 은 게시 되지 않았음을 나타냅니다.|  
|allow_initialize_from_backup|**bit**|구독자가 초기 스냅샷 대신 백업으로부터 이 게시에 대한 구독을 초기화할 수 있는지 여부를 나타냅니다. **1** 은 백업에서 구독을 초기화할 수 있음을 의미 하 고 **0** 은 사용할 수 없음을 의미 합니다. 자세한 내용은 스냅숏 없이 트랜잭션 구독자를 스냅숏 없이 트랜잭션 [구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) 를 참조 하세요.|  
|replicate_ddl|**int**|게시에 대해 스키마 복제가 지원되는지 여부를 나타냅니다. **1** 은 게시자에서 실행 된 ddl (데이터 정의 언어) 문이 복제 됨을 나타내고 **0** 은 ddl 문이 복제 되지 않음을 나타냅니다. 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.|  
|enabled_for_p2p|**int**|피어 투 피어 복제 토폴로지에서 게시가 사용될 수 있는지 여부를 나타냅니다. **1** 은 게시에서 피어 투 피어 복제를 지원함을 나타냅니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.|  
|publish_local_changes_only|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**int**|게시에서 비[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자를 지원하는지 여부를 지정합니다. 값 **1** 은 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자가 지원 됨을 의미 합니다. 값이 **0** 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자만 지원 됩니다. 자세한 내용은 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)을(를) 참조하세요.|  
|enabled_for_p2p_conflictdetection|**int**|피어 투 피어 복제에 게시가 사용되도록 설정된 경우 배포 에이전트에서 충돌을 검색할지 여부를 지정합니다. 값 **1** 은 충돌이 검색 됨을 의미 합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을 참조하세요.|  
|originator_id|**int**|피어 투 피어 토폴로지에 있는 노드의 ID를 지정합니다. 이 ID는 **enabled_for_p2p_conflictdetection** **1**로 설정 된 경우 충돌 검색에 사용 됩니다. 이미 사용된 ID 목록을 보려면 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 시스템 테이블을 쿼리하십시오.|  
|p2p_continue_onconflict|**int**|충돌이 검색되면 배포 에이전트에서 변경 내용을 계속 처리할지 여부를 지정합니다. 값이 **1** 이면 에이전트에서 변경 내용을 계속 처리 합니다.<br /><br /> ** \* \* 주의 \* 기본값 \* ** **0**을 사용 하는 것이 좋습니다. 이 옵션을 **1**로 설정 하면 배포 에이전트는 송신자 ID가 가장 높은 노드에서 충돌 하는 행을 적용 하 여 토폴로지의 데이터를 수렴 하려고 시도 합니다. 이 방법으로 데이터가 일치하게 되지 않는 경우도 있습니다. 충돌이 검색된 후 토폴로지의 일관성을 확인해야 합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)의 "충돌 처리"를 참조하십시오.|  
|allow_partition_switch|**int**|ALTER TABLE ... SWITCH 문은 게시 된 데이터베이스에 대해 실행할 수 있습니다. 자세한 내용은 [분할 테이블 및 인덱스 복제](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)를 참조하세요.|  
|replicate_partition_switch|**int**|ALTER TABLE ... 게시 된 데이터베이스에 대해 실행 되는 SWITCH 문을 구독자에 복제 해야 합니다. 이 옵션은 *allow_partition_switch* **1**로 설정 된 경우에만 유효 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_helppublication은 스냅샷 및 트랜잭션 복제에 사용됩니다.  
  
 sp_helppublication은 이 프로시저를 실행하는 사용자가 소유하는 모든 게시에 대한 정보를 반환합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 게시자에서 sysadmin 고정 서버 역할의 멤버 또는 게시 데이터베이스에 대한 db_owner 고정 데이터베이스 역할의 멤버 또는 PAL(게시 액세스 목록)의 사용자만 sp_helppublication을 실행할 수 있습니다.  
  
 이외 게시자의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에서 sysadmin 고정 서버 역할의 멤버 또는 배포 데이터베이스에 대 한 db_owner 고정 데이터베이스 역할의 멤버 또는 PAL의 사용자만 sp_helppublication를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Transact-sql&#41;sp_addpublication &#40;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [Transact-sql&#41;sp_changepublication &#40;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [Transact-sql&#41;sp_droppublication &#40;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
