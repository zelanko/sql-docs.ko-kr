---
title: sys.dm_tran_locks (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_tran_locks
- sys.dm_tran_locks
- sys.dm_tran_locks_TSQL
- dm_tran_locks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_locks dynamic management view
ms.assetid: f0d3b95a-8a00-471b-9da4-14cb8f5b045f
caps.latest.revision: 61
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b2e8adf59403318df0fc46bd817fc6ff12bcef0f
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmtranlocks-transact-sql"></a>sys.dm_tran_locks(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 현재 활성 상태인 잠금 관리자 리소스에 대한 정보를 반환합니다. 각 행에 부여 된 하거나 부여 되기를 기다리고 있는 잠금에 대 한 잠금 관리자가 현재 활성 요청을 나타냅니다.  
  
 결과 집합의 열은 리소스와 요청의 두 기본 그룹으로 나뉩니다. 리소스 그룹은 잠금이 요청된 리소스를 설명하고 요청 그룹은 잠금 요청을 설명합니다.  
  
> [!NOTE]  
> 이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_tran_locks**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**resource_type**|**nvarchar(60)**|리소스 유형을 나타냅니다. 값 중 하나일 수 있습니다: 데이터베이스, 파일, 개체, 페이지, 키, EXTENT, RID, 응용 프로그램, 메타 데이터, HOBT 또는 allocation_unit 중 하나일 수 있습니다.|  
|**resource_subtype**|**nvarchar(60)**|하위 유형을 나타냅니다 **resource_type**합니다. 부모 유형의 하위 유형이 아닌 유형을 잠그지 않고 하위 유형 잠금을 획득할 수 있습니다. 개별 하위 유형은 서로 충돌하지 않으며 하위 유형이 아닌 부모 유형과도 충돌하지 않습니다. 모든 리소스 유형에 하위 유형이 있는 것은 아닙니다.|  
|**resource_database_id**|**int**|이 리소스의 범위를 한정하는 데이터베이스의 ID입니다. 잠금 관리자로 처리되는 모든 리소스의 범위는 데이터베이스 ID로 결정됩니다.|  
|**resource_description**|**nvarchar(256)**|다른 리소스 열에서 사용할 수 없는 정보만 포함하는 리소스 설명입니다.|  
|**resource_associated_entity_id**|**bigint**|리소스가 연결된 데이터베이스 내의 엔터티 ID입니다. 리소스 유형에 따라 개체 ID, Hobt ID 또는 할당 단위 ID가 될 수 있습니다.|  
|**resource_lock_partition**|**Int**|분할된 잠금 리소스의 잠금 파티션 ID입니다. 분할되지 않은 잠금 리소스의 경우 이 값은 0입니다.|  
|**request_mode**|**nvarchar(60)**|요청 모드입니다. 허용된 요청의 경우 허용 모드이고 대기 중인 요청의 경우에는 요청 중인 모드가 됩니다.|  
|**request_type**|**nvarchar(60)**|요청 유형입니다. 값은 LOCK입니다.|  
|**request_status**|**nvarchar(60)**|이 요청의 현재 상태입니다. 가능한 값은 GRANTED, CONVERT, WAIT, LOW_PRIORITY_CONVERT, LOW_PRIORITY_WAIT 또는 ABORT_BLOCKERS입니다. 낮은 우선 순위 대기 및 중단 블 로커에 대 한 자세한 내용은 참조는 *low_priority_lock_wait* 섹션 [ALTER INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)합니다.|  
|**request_reference_count**|**smallint**|동일한 요청자가 이 리소스를 요청한 횟수의 근사 값을 반환합니다.|  
|**request_lifetime**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**request_session_id**|**int**|현재 이 요청을 소유한 세션 ID입니다. 분산 트랜잭션 및 바운드 트랜잭션의 소유 세션 ID를 변경할 수 있습니다. 값이 -2인 경우 요청이 분리된 분산 트랜잭션에 속함을 나타냅니다. 값이 -3인 경우 성공적으로 롤백할 수 없기 때문에 복구 시 롤백이 지연된 트랜잭션과 같이 지연된 복구 트랜잭션에 요청이 속함을 나타냅니다.|  
|**request_exec_context_id**|**int**|현재 이 요청을 소유하는 프로세스의 실행 컨텍스트 ID입니다.|  
|**request_request_id**|**int**|현재 이 요청을 소유하는 프로세스의 요청 ID(일괄 처리 ID)입니다. 이 값은 트랜잭션의 활성 MARS(Multiple Active Result Set) 연결이 변경될 때마다 달라집니다.|  
|**request_owner_type**|**nvarchar(60)**|요청을 소유하는 엔터티 유형입니다. 다양한 엔터티가 잠금 관리자 요청을 소유할 수 있습니다. 가능한 값은<br /><br /> TRANSACTION = 트랜잭션이 요청을 소유합니다.<br /><br /> CURSOR = 커서가 요청을 소유합니다.<br /><br /> SESSION = 사용자 세션이 요청을 소유합니다.<br /><br /> SHARED_TRANSACTION_WORKSPACE = 트랜잭션 작업 영역 중 공유 부분이 요청을 소유합니다.<br /><br /> EXCLUSIVE_TRANSACTION_WORKSPACE = 트랜잭션 작업 영역 중 배타 부분이 요청을 소유합니다.<br /><br /> NOTIFICATION_OBJECT = 내부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소가 요청을 소유합니다. 이 구성 요소는 다른 구성 요소가 잠금을 수행하기 위해 기다리고 있는 경우 잠금 관리자가 이를 알리도록 요청했습니다. FileTable 기능은 이 값을 사용하는 구성 요소입니다.<br /><br /> **참고:** 참여 한 세션에 대 한 잠금을 유지 하기 위해 작업 공간이 내부적으로 사용 됩니다.|  
|**request_owner_id**|**bigint**|이 요청의 특정 소유자 ID입니다.<br /><br /> 트랜잭션이 요청의 소유자인 경우 이 값에는 트랜잭션 ID가 포함됩니다.<br /><br /> FileTable이 요청의 소유자 경우 **request_owner_id** 다음 값 중 하나입니다.<br /><br /> <br /><br /> -4: FileTable이 데이터베이스 잠금을 수행 했습니다.<br /><br /> -3: FileTable이 테이블 잠금을 수행 했습니다.<br /><br /> 다른 값: 값은 파일 핸들을 나타냅니다. 이 값으로도 표시 **fcb_id** 동적 관리 뷰에 [sys.dm_filestream_non_transacted_handles &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)합니다.|  
|**request_owner_guid**|**uniqueidentifier**|이 요청의 특정 소유자 GUID입니다. 이 값이 트랜잭션의 MS DTC GUID와 일치하는 분산 트랜잭션에만 사용됩니다.|  
|**request_owner_lockspace_id**|**nvarchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] 이 값은 요청자의 잠금 공간 ID를 나타냅니다. 잠금 공간 ID는 두 요청자가 서로 충돌하지 않는지, 그리고 서로 충돌할 수 있는 모드의 경우 두 요청자에게 잠금을 허용할 수 있는지 여부를 결정합니다.|  
|**lock_owner_address**|**varbinary(8)**|이 요청을 추적하는 데 사용되는 내부 데이터 구조의 메모리 주소입니다. 이 열을 조인할 수는와 **resource_address** 열에 **sys.dm_os_waiting_tasks**합니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> <br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   
 
## <a name="remarks"></a>주의  
 허용된 요청 상태는 요청자에게 리소스에 대한 잠금이 허용되었음을 나타냅니다. 대기 중인 요청은 해당 요청이 아직 허용되지 않았음을 나타냅니다. 대기 중인 요청 유형은 다음과에서 반환 되는 **request_status** 열:  
  
-   변환 요청 상태는 리소스에 대한 요청이 이미 허용되었으며 초기 요청에 대한 업그레이드가 현재 허용 대기 상태에 있음을 나타냅니다.  
  
-   대기 요청 상태는 리소스에 대한 요청이 아직 허용되지 않았음을 나타냅니다.  
  
 때문에 **sys.dm_tran_locks** 은 구조에서 채워지므로 내부 잠금 관리자 데이터를 유지이 정보를 일반 오버 헤드가 추가로 발생 처리를 추가 하지 않습니다. 뷰를 구체화하려면 잠금 관리자 내부 데이터 구조에 액세스해야 하므로 서버의 정상적인 처리에 사소한 영향을 줄 수 있습니다. 그러나 그 영향은 무시할 만한 수준이며 매우 많이 사용되는 리소스에만 영향을 미칩니다. 이 뷰의 데이터는 잠금 관리자의 현재 상태에 따라 달라지기 때문에 언제든지 변경될 수 있으며 잠금을 획득하고 해제할 때마다 행이 추가되거나 제거됩니다. 이 뷰에는 기록 정보가 없습니다.  
  
 위의 두 요청은 리소스 열과 그룹 열이 모두 같은 경우에만 동일한 리소스에 대해 작동합니다.  
  
 다음 도구를 사용하여 읽기 작업의 잠금을 제어할 수 있습니다.  
  
-   SET TRANSACTION ISOLATION LEVEL을 사용하여 세션의 잠금 수준을 지정합니다. 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.  
  
-   FROM 절에서 테이블 잠금 힌트를 사용하여 테이블의 개별 참조에 대한 잠금 수준을 지정합니다. 구문 및 제한 사항에 대 한 참조 [테이블 힌트 &#40;TRANSACT-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)합니다.  
  
 한 세션 ID로 실행되는 리소스에 둘 이상의 잠금을 허용할 수 있습니다. 한 세션에서 실행 되는 서로 다른 엔터티 각각 소유할 수는 동일한 리소스에 대 한 잠금이 있으며 정보에 표시 되는 **request_owner_type** 및 **request_owner_id** 않은 열 반환 된 **sys.dm_tran_locks**합니다. 경우 같은 여러 인스턴스 **request_owner_type** 존재는 **request_owner_id** 열을 사용 하 여을 각 인스턴스를 구분 합니다. 분산 트랜잭션에서 **request_owner_type** 및 **request_owner_guid** 열에는 다양 한 엔터티 정보가 표시 됩니다.  
  
 예를 들어 세션 s 1에 한 공유 잠금을 소유 **Table1**; 트랜잭션 t 1 세션 s 1에서 실행 되는 때에에 공유 잠금을 소유 하 고 **Table1**합니다. 이 경우에 **resource_description** 에서 반환 되는 열 **sys.dm_tran_locks** 두 개의 동일한 리소스가 표시 됩니다. **request_owner_type** 세션으로 트랜잭션으로 다른 열에 표시 됩니다. 또한는 **resource_owner_id** 열 서로 다른 값이 적용 됩니다.  
  
 한 세션에서 실행되는 여러 커서는 서로 구분되지 않으므로 하나의 엔터티로 간주됩니다.  
  
 세션 ID 값과 연결되지 않은 분산 트랜잭션은 분리된 트랜잭션이며 -2의 세션 ID 값이 할당됩니다. 자세한 내용은 참조 [kill& #40; Transact SQL & #41; ](../../t-sql/language-elements/kill-transact-sql.md).  
  
## <a name="resource-details"></a>리소스 정보  
 다음 표에서에서 표현 되는 리소스를 나열는 **resource_associated_entity_id** 열입니다.  
  
|리소스 유형|리소스 설명|Resource_associated_entity_id|  
|-------------------|--------------------------|--------------------------------------|  
|DATABASE|데이터베이스를 나타냅니다.|해당 사항 없음|  
|FILE|데이터베이스 파일을 나타냅니다. 이 파일은 데이터 또는 로그 파일일 수 있습니다.|해당 사항 없음|  
|OBJECT|데이터베이스 개체를 나타냅니다. 이 개체는 데이터 테이블, 뷰, 저장 프로시저, 확장 저장 프로시저 또는 개체 ID가 있는 모든 개체일 수 있습니다.|개체 ID입니다.|  
|PAGE|데이터 파일 내의 단일 페이지를 나타냅니다.|HoBt ID입니다. 이 값에 해당 **sys.partitions.hobt_id**합니다. HoBt ID는 호출자가 제공할 수 있는 추가 정보이지만 모든 호출자가 이 정보를 제공할 수 있는 것은 아니기 때문에 PAGE 리소스에 대해 항상 HoBt ID를 사용할 수 있는 것은 아닙니다.|  
|KEY|인덱스의 행을 나타냅니다.|HoBt ID입니다. 이 값에 해당 **sys.partitions.hobt_id**합니다.|  
|EXTENT|데이터 파일 익스텐트를 나타냅니다. 익스텐트는 8개의 연속 페이지 그룹입니다.|해당 사항 없음|  
|RID|힙의 물리적 행을 나타냅니다.|HoBt ID입니다. 이 값에 해당 **sys.partitions.hobt_id**합니다. HoBt ID는 호출자가 제공할 수 있는 추가 정보이지만 모든 호출자가 이 정보를 제공할 수 있는 것은 아니기 때문에 RID 리소스에 대해 항상 HoBt ID를 사용할 수 있는 것은 아닙니다.|  
|APPLICATION|응용 프로그램이 지정한 리소스를 나타냅니다.|해당 사항 없음|  
|METADATA|메타데이터 정보를 나타냅니다.|해당 사항 없음|  
|HOBT|힙 또는 B-트리를 나타냅니다. 기본 액세스 경로 구조입니다.|HoBt ID입니다. 이 값에 해당 **sys.partitions.hobt_id**합니다.|  
|ALLOCATION_UNIT|인덱스 파티션과 같은 관련 페이지의 집합을 나타냅니다. 각 할당 단위는 단일 IAM(Index Allocation Map) 체인을 처리합니다.|할당 단위 ID입니다. 이 값에 해당 **sys.allocation_units.allocation_unit_id**합니다.|  
  
 다음 표에서는 각 리소스 유형에 연결된 하위 유형을 나열합니다.  
  
|ResourceSubType|동기화|  
|---------------------|------------------|  
|ALLOCATION_UNIT.BULK_OPERATION_PAGE|대량 작업에 사용되는 미리 할당된 페이지를 동기화합니다.|  
|ALLOCATION_UNIT.PAGE_COUNT|지연된 삭제 작업 중 할당 단위 페이지 수 통계를 동기화합니다.|  
|DATABASE.BULKOP_BACKUP_DB|데이터베이스 백업과 대량 작업을 동기화합니다.|  
|DATABASE.BULKOP_BACKUP_LOG|데이터베이스 로그 백업과 대량 작업을 동기화합니다.|  
|DATABASE.CHANGE_TRACKING_CLEANUP|변경 내용 추적 정리 태스크를 동기화합니다|  
|DATABASE.CT_DDL|데이터베이스 및 테이블 수준 변경 내용 추적 DDL 작업을 동기화합니다.|  
|DATABASE.CONVERSATION_PRIORITY|CREATE BROKER PRIORITY와 같은 Service Broker 변환 우선 순위 작업을 동기화합니다.|  
|DATABASE.DDL|DDL(데이터 정의 언어) 작업을 파일 그룹 작업(예: 삭제)과 동기화합니다.|  
|DATABASE.ENCRYPTION_SCAN|TDE 암호화 동기화를 수행합니다.|  
|DATABASE.PLANGUIDE|계획 지침 동기화를 수행합니다.|  
|DATABASE.RESOURCE_GOVERNOR_DDL|리소스 관리자 작업에 대한 DDL 작업(예: ALTER RESOURCE POOL)을 동기화합니다.|  
|DATABASE.SHRINK|데이터베이스 축소 작업을 동기화합니다.|  
|DATABASE.STARTUP|데이터베이스 시작 동기화에 사용합니다.|  
|FILE.SHRINK|파일 축소 작업을 동기화합니다.|  
|HOBT.BULK_OPERATION|힙 최적화 대량 로드 작업과 동시 검색을 동기화합니다. 이 작업은 행 버전 관리를 사용한 스냅숏, 커밋되지 않은 읽기 및 커밋된 읽기의 격리 수준에서 수행됩니다.|  
|HOBT.INDEX_REORGANIZE|힙 또는 인덱스 재구성 작업을 동기화합니다.|  
|OBJECT.COMPILE|저장 프로시저 컴파일을 동기화합니다.|  
|OBJECT.INDEX_OPERATION|인덱스 작업을 동기화합니다.|  
|OBJECT.UPDSTATS|테이블의 통계 업데이트를 동기화합니다.|  
|METADATA.ASSEMBLY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_CLR_NAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_TOKEN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASYMMETRIC_KEY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_ACTIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_SPECIFICATION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AVAILABILITY_GROUP|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CERTIFICATE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CHILD_INSTANCE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_FRAGMENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_ROWSET|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_RECV|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_SEND|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_GROUP|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_PRIORITY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CREDENTIAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CRYPTOGRAPHIC_PROVIDER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATA_SPACE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE_PRINCIPAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_SESSION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_WITNESS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_PRINCIPAL_SID|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT_WEBMETHOD|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_COLUMN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_STOPLIST|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEX_EXTENSION_SCHEME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEXSTATS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INSTANTIATED_TYPE_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.MESSAGE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.METADATA_CACHE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PARTITION_FUNCTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PASSWORD_POLICY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PERMISSIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE_SCOPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.REMOTE_SERVICE_BINDING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ROUTE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SCHEMA|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_CACHE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_DESCRIPTOR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SEQUENCE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_EVENT_SESSIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_PRINCIPAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_BROKER_GUID|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_CONTRACT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_MESSAGE_TYPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.STATS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SYMMETRIC_KEY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.USER_TYPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COLLECTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COMPONENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_INDEX_QNAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 다음 표에서 형식을 제공는 **resource_description** 각 리소스 유형에 대 한 열입니다.  
  
|리소스|형식|Description|  
|--------------|------------|-----------------|  
|DATABASE|해당 사항 없음|데이터베이스 ID가 이미에서 사용할 수는 **resource_database_id** 열입니다.|  
|FILE|<file_id>|이 리소스가 나타내는 파일의 ID입니다.|  
|OBJECT|<object_id>|이 리소스가 나타내는 개체의 ID입니다. 이 개체에 나열 된 모든 개체 일 수 **sys.objects**, 테이블 뿐만 아니라 합니다.|  
|PAGE|<file_id>:<page_in_file>|이 리소스가 나타내는 페이지의 파일 및 페이지 ID를 나타냅니다.|  
|KEY|<hash_value>|이 리소스가 나타내는 행에서 키 열의 해시를 나타냅니다.|  
|EXTENT|<file_id>:<page_in_files>|이 리소스가 나타내는 익스텐트의 파일 및 페이지 ID를 나타냅니다. 익스텐트 ID는 익스텐트에서 첫 페이지의 페이지 ID와 같습니다.|  
|RID|<file_id>:<page_in_file>:<row_on_page>|이 리소스가 나타내는 행의 페이지 ID와 행 ID를 나타냅니다. 연결된 개체 ID가 99인 경우 이 리소스는 IAM 체인의 첫 IAM 페이지에 있는 8개의 혼합 페이지 슬롯 중 하나를 나타냅니다.|  
|APPLICATION|\<DbPrincipalId >:\<자 이하로 32 >:(< hash_value >)|이 응용 프로그램 잠금 리소스의 범위를 한정하는 데 사용된 데이터베이스 보안 주체의 ID를 나타냅니다. 또한 이 응용 프로그램 잠금 리소스에 해당하는 리소스 문자열에서 최대 32자까지 포함합니다. 전체 문자열을 사용할 수 없어 두 문자만 표시되는 경우도 있습니다. 이 동작은 복구 과정에서 다시 획득한 응용 프로그램 잠금에 대한 데이터베이스 복구 시에만 수행됩니다. 해시 값은 이 응용 프로그램 잠금 리소스에 해당하는 전체 리소스 문자열의 해시를 나타냅니다.|  
|HOBT|해당 사항 없음|HoBt ID로 포함 되어는 **resource_associated_entity_id**합니다.|  
|ALLOCATION_UNIT|해당 사항 없음|할당 단위 ID로 포함 되어는 **resource_associated_entity_id**합니다.|  
|METADATA.ASSEMBLY|assembly_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_CLR_NAME|$qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_TOKEN|assembly_id = A, $token_id|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSYMMETRIC_KEY|asymmetric_key_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT|audit_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_ACTIONS|device_id = D, major_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_SPECIFICATION|audit_specification_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AVAILABILITY_GROUP|availability_group_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CERTIFICATE|certificate_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CHILD_INSTANCE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_FRAGMENT|object_id = O , compressed_fragment_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_ROW|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_RECV|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_SEND|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_GROUP|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_PRIORITY|conversation_priority_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CREDENTIAL|credential_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CRYPTOGRAPHIC_PROVIDER|provider_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATA_SPACE|data_space_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE|database_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE_PRINCIPAL|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_SESSION|database_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_WITNESS|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_PRINCIPAL_SID|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT|endpoint_id = E|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT_WEBMETHOD|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|fulltext_catalog_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_COLUMN|object_id = O, column_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_HASH|object_id = O, $hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|fulltext_catalog_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_STOPLIST|fulltext_stoplist_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEX_EXTENSION_SCHEME|index_extension_id = I|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEXSTATS|object_id = O, index_id or stats_id = I|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INSTANTIATED_TYPE_HASH|user_type_id = U, hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.MESSAGE|message_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.METADATA_CACHE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PARTITION_FUNCTION|function_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PASSWORD_POLICY|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PERMISSIONS|class = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE|plan_guide_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA. PLAN_GUIDE_HASH|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA. PLAN_GUIDE_SCOPE|scope_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME|$qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME_HASH|$qname_scope_id = Q, $qname_hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.REMOTE_SERVICE_BINDING|remote_service_binding_id = R|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ROUTE|route_id = R|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SCHEMA|schema_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_CACHE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_DESCRIPTOR|sd_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SEQUENCE|$seq_type = S, object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER|server_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_EVENT_SESSIONS|event_session_id = E|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_PRINCIPAL|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE|service_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_BROKER_GUID|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_CONTRACT|service_contract_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_MESSAGE_TYPE|message_type_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.STATS|object_id = O, stats_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SYMMETRIC_KEY|symmetric_key_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.USER_TYPE|user_type_id = U|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COLLECTION|xml_collection_id = X|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COMPONENT|xml_component_id = X|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_INDEX_QNAME|object_id = O, $qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 다음과 같은 Xevent를 파티션에 관련 된 **스위치** 및 온라인 인덱스 다시 작성 합니다. 구문에 대 한 정보를 참조 하십시오. [ALTER TABLE &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md) 및 [ALTER INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)합니다.  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 기존 XEvent **progress_report_online_index_operation** 온라인 인덱스에 대 한 작업 추가 하 여 확장 되었습니다 **partition_number** 및 **partition_id**합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-sysdmtranlocks-with-other-tools"></a>1. 다른 도구와 함께 sys.dm_tran_locks 사용  
 다음 예에는 다른 트랜잭션에 의해 업데이트 작업이 차단되는 시나리오에서 실행됩니다. 사용 하 여 **sys.dm_tran_locks** 및 기타 도구 리소스 잠금에 대 한 정보를 제공 합니다.  
  
```sql  
USE tempdb;  
GO  
  
-- Create test table and index.  
CREATE TABLE t_lock  
    (  
    c1 int, c2 int  
    );  
GO  
  
CREATE INDEX t_lock_ci on t_lock(c1);  
GO  
  
-- Insert values into test table  
INSERT INTO t_lock VALUES (1, 1);  
INSERT INTO t_lock VALUES (2,2);  
INSERT INTO t_lock VALUES (3,3);  
INSERT INTO t_lock VALUES (4,4);  
INSERT INTO t_lock VALUES (5,5);  
INSERT INTO t_lock VALUES (6,6);  
GO  
  
-- Session 1  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
  
BEGIN TRAN  
    SELECT c1  
        FROM t_lock  
        WITH(holdlock, rowlock);  
  
-- Session 2  
BEGIN TRAN  
    UPDATE t_lock SET c1 = 10  
```  
  
 다음 쿼리에서는 잠금 정보를 표시합니다. 에 대 한 값 `<dbid>` 로 대체 해야는 **database_id** 에서 **sys.databases**합니다.  
  
```sql  
SELECT resource_type, resource_associated_entity_id,  
    request_status, request_mode,request_session_id,  
    resource_description   
    FROM sys.dm_tran_locks  
    WHERE resource_database_id = <dbid>  
```  
  
 다음 쿼리에서는 위 쿼리의 `resource_associated_entity_id`를 사용하여 개체 정보를 반환합니다. 해당 개체가 포함된 데이터베이스에 연결되어 있는 동안 이 쿼리를 실행해야 합니다.  
  
```  
SELECT object_name(object_id), *  
    FROM sys.partitions  
    WHERE hobt_id=<resource_associated_entity_id>  
```  
  
 다음 쿼리에서는 차단 정보를 표시합니다.  
  
```sql  
SELECT   
        t1.resource_type,  
        t1.resource_database_id,  
        t1.resource_associated_entity_id,  
        t1.request_mode,  
        t1.request_session_id,  
        t2.blocking_session_id  
    FROM sys.dm_tran_locks as t1  
    INNER JOIN sys.dm_os_waiting_tasks as t2  
        ON t1.lock_owner_address = t2.resource_address;  
```  
  
 트랜잭션을 롤백하여 리소스를 해제합니다.  
  
```sql  
-- Session 1  
ROLLBACK;  
GO  
  
-- Session 2  
ROLLBACK;  
GO  
```  
  
### <a name="b-linking-session-information-to-operating-system-threads"></a>2. 운영 체제 스레드에 세션 정보 연결  
 다음 예에서는 Windows 스레드 ID와 세션 ID를 연결하는 정보를 반환합니다. 스레드 성능은 Windows 성능 모니터에서 모니터링할 수 있습니다. 이 쿼리는 현재 중지 중인 세션 ID를 반환하지 않습니다.  
  
```sql  
SELECT STasks.session_id, SThreads.os_thread_id  
    FROM sys.dm_os_tasks AS STasks  
    INNER JOIN sys.dm_os_threads AS SThreads  
        ON STasks.worker_address = SThreads.worker_address  
    WHERE STasks.session_id IS NOT NULL  
    ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_tran_database_transactions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
