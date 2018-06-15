---
title: sp_addmergearticle (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_addmergearticle
- sp_addmergearticle_TSQL
helpviewer_keywords:
- sp_addmergearticle
ms.assetid: 0df654ea-24e2-4c61-a75a-ecaa7a140a6c
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d60ceb96dfaf5f690a8485c74648707da0ae59ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993660"
---
# <a name="spaddmergearticle-transact-sql"></a>sp_add_targetservergroup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 병합 게시에 아티클을 추가합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergearticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @source_object = ] 'source_object'   
    [ , [ @type = ] 'type' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @column_tracking = ] 'column_tracking' ]   
    [ , [ @status = ] 'status' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @subset_filterclause = ] 'subset_filterclause' ]   
    [ , [ @article_resolver = ] 'article_resolver' ]   
    [ , [ @resolver_info = ] 'resolver_info' ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @verify_resolver_signature = ] verify_resolver_signature ]   
    [ , [ @destination_object = ] 'destination_object' ]   
    [ , [ @allow_interactive_resolver = ] 'allow_interactive_resolver' ]   
    [ , [ @fast_multicol_updateproc = ] 'fast_multicol_updateproc' ]   
    [ , [ @check_permissions = ] check_permissions ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @published_in_tran_pub = ] 'published_in_tran_pub' ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @logical_record_level_conflict_detection = ] 'logical_record_level_conflict_detection' ]  
    [ , [ @logical_record_level_conflict_resolution = ] 'logical_record_level_conflict_resolution' ]  
    [ , [ @partition_options = ] partition_options ]  
    [ , [ @processing_order = ] processing_order ]  
    [ , [ @subscriber_upload_options = ] subscriber_upload_options ]  
    [ , [ @identityrangemanagementoption = ] 'identityrangemanagementoption' ]  
    [ , [ @delete_tracking = ] delete_tracking ]  
    [ , [ @compensate_for_errors = ] 'compensate_for_errors' ]   
    [ , [ @stream_blob_columns = ] 'stream_blob_columns' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=** ] **'***게시***'**  
 아티클을 포함하는 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@article=** ] **'***문서***'**  
 아티클의 이름입니다. 이름은 반드시 게시 내에서 고유해야 합니다. *문서* 은 **sysname**, 기본값은 없습니다. *문서* 실행 하는 로컬 컴퓨터에 있어야 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 고 식별자 규칙을 따라야 합니다.  
  
 [  **@source_object=** ] **'***source_object***'**  
 게시할 데이터베이스 개체입니다. *source_object* 은 **sysname**, 기본값은 없습니다. 병합 복제를 사용 하 여 게시할 수 있는 개체의 형식에 대 한 자세한 내용은 참조 [게시 데이터 및 데이터베이스 개체](../../relational-databases/replication/publish/publish-data-and-database-objects.md)합니다.  
  
 [ **@type=** ] **'***type***'**  
 아티클의 유형입니다. *형식* 은 **sysname**, 기본값은 **테이블**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**테이블** (기본값)|스키마와 데이터가 있는 테이블입니다. 복제는 테이블을 모니터링하여 복제할 데이터를 결정합니다.|  
|**func 스키마 전용**|스키마가 있는 함수 전용입니다.|  
|**인덱싱된 뷰** **스키마 전용**|스키마가 있는 인덱싱된 뷰 전용입니다.|  
|**프로시저 스키마 전용**|스키마가 있는 저장 프로시저 전용입니다.|  
|**동의어 스키마 전용**|스키마가 있는 동의어 전용입니다.|  
|**뷰 스키마 전용**|스키마가 있는 뷰 전용입니다.|  
  
 [  **@description=** ] **'***설명***'**  
 아티클에 대한 설명입니다. *설명* 은 **nvarchar (255)**, 기본값은 NULL입니다.  
  
 [  **@column_tracking=** ] **'***column_tracking***'**  
 열 수준 추적에 대한 설정입니다. *column_tracking* 은 **nvarchar (10)**, 기본값은 FALSE입니다. **true**열 추적을 설정 합니다. **false** 열 추적을 해제 하 고 행 수준에서 충돌 감지를 유지 합니다. 해당 테이블이 이미 다른 병합 게시에 게시된 경우 이 테이블을 기반으로 하는 기존 아티클이 사용하는 열 추적 값과 동일한 값을 사용해야 합니다. 이 매개 변수는 테이블 아티클에만 해당합니다.  
  
> [!NOTE]  
>  충돌 감지에 행 추적을 사용하는 경우(기본값) 기본 테이블에 최대 1,024개의 열을 포함할 수 있지만 아티클에서 열을 필터링해야 하므로 최대 246개의 열이 게시됩니다. 열 추적을 사용하면 기본 테이블은 최대 246개의 열을 포함할 수 있습니다.  
  
 [  **@status=** ] **'***상태***'**  
 아티클의 상태입니다. *상태* 은 **nvarchar (10)**, 기본값은 **unsynced**합니다. 경우 **활성**, 테이블을 게시 하는 초기 처리 스크립트가 실행 됩니다. 경우 **unsynced**, 스냅숏 에이전트가 실행 될 다음 시간에 테이블을 게시할 때는 초기 처리 스크립트가 실행 됩니다.  
  
 [  **@pre_creation_cmd=** ] **'***pre_creation_cmd***'**  
 스냅숏 적용 시 구독자에 테이블이 있는 경우 시스템이 수행할 작업을 지정합니다. *pre_creation_cmd* 은 **nvarchar (10)**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**없음**|구독자에 이미 테이블이 존재하는 경우 아무런 동작이 발생하지 않습니다.|  
|**delete**|하위 집합 필터의 WHERE 절을 기반으로 하여 삭제를 실행합니다.|  
|**drop** (기본값)|테이블을 다시 만들기 전에 삭제합니다. 지 원하는 데 필요한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자입니다.|  
|**truncate**|대상 테이블을 자릅니다.|  
  
 [  **@creation_script=** ] **'***creation_script***'**  
 구독 데이터베이스에서 아티클을 만드는 데 사용된 선택적 아티클 스키마 스크립트의 경로 및 이름입니다. *creation_script* 은 **nvarchar (255)**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  생성 스크립트는 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자에서 실행되지 않습니다.  
  
 [  **@schema_option=** ] *schema_option*  
 지정한 아티클에 대한 스키마 생성 옵션의 비트맵입니다. *schema_option* 은 **binary (8)**, 수 및는 [| (비트 OR) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) 다음이 값 중 하나 이상의 제품입니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**0x00**|스냅숏 에이전트의 스크립팅을 사용 하지 않도록 설정 하 고에 정의 된 제공 된 스키마 사전 작성 스크립트를 사용 하 여 *creation_script*합니다.|  
|**0x01**|개체를 만듭니다(CREATE TABLE, CREATE PROCEDURE 등). 이는 저장 프로시저 아티클에 대한 기본값입니다.|  
|**0x10**|해당 클러스터형 인덱스를 생성합니다. 이 옵션을 설정하지 않아도 게시된 테이블에 이미 정의되어 있으면 기본 키 및 UNIQUE 제약 조건과 관련된 인덱스가 생성됩니다.|  
|**0x20**|사용자 정의 데이터 형식(UDT)을 구독자에서의 기본 데이터 형식으로 변환합니다. UDT 열에 CHECK 또는 DEFAULT 제약 조건이 있거나 UDT 열이 기본 키의 일부이거나 계산 열이 UDT 열을 참조하는 경우 이 옵션을 사용할 수 없습니다.|  
|**0x40**|해당 비클러스터형 인덱스를 생성합니다. 이 옵션을 설정하지 않아도 게시된 테이블에 이미 정의되어 있으면 기본 키 및 UNIQUE 제약 조건과 관련된 인덱스가 생성됩니다.|  
|**0x80**|PRIMARY KEY 제약 조건을 복제합니다. 제약 조건에 연결 된 인덱스가 모두 복제 됩니다 경우에 옵션 **0x10** 및 **0x40** 을 사용할 수 없습니다.|  
|**0x100**|정의된 경우 테이블 아티클에 사용자 트리거를 복제합니다.|  
|**0x200**|FOREIGN KEY 제약 조건을 복제합니다. 참조되는 테이블이 게시의 일부가 아닌 경우 게시된 테이블의 모든 FOREIGN KEY 제약 조건은 복제되지 않습니다.|  
|**0x400**|CHECK 제약 조건을 복제합니다.|  
|**0 x 800**|기본값을 복제합니다.|  
|**0x1000**|열 수준 데이터 정렬을 복제합니다.|  
|**0x2000**|게시된 아티클 원본 개체와 연관된 확장 속성을 복제합니다.|  
|**0x4000**|UNIQUE 제약 조건을 복제합니다. 제약 조건에 연결 된 인덱스가 모두 복제 됩니다 경우에 옵션 **0x10** 및 **0x40** 을 사용할 수 없습니다.|  
|**0x8000**|이 옵션은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 실행하는 게시자에 대해 유효하지 않습니다.|  
|**0x10000**|동기화하는 동안 CHECK 조건이 강제 적용되지 않도록 해당 제약 조건을 NOT FOR REPLICATION으로 복제합니다.|  
|**0 x 20000**|동기화하는 동안 FOREIGN KEY 제약 조건이 강제 적용되지 않도록 해당 제약 조건을 NOT FOR REPLICATION으로 복제합니다.|  
|**0x40000**|분할된 테이블이나 인덱스와 연결된 파일 그룹을 복제합니다.|  
|**0x80000**|분할된 테이블에 대한 파티션 구성표를 복제합니다.|  
|**0x100000**|분할된 인덱스에 대한 파티션 구성표를 복제합니다.|  
|**0x200000**|테이블 통계를 복제합니다.|  
|**0x400000**|기본 바인딩을 복제합니다.|  
|**0x800000**|규칙 바인딩을 복제합니다.|  
|**0x1000000**|전체 텍스트 인덱스를 복제합니다.|  
|**0x2000000**|XML 스키마 컬렉션에 바인딩된 **xml** 열이 복제 되지 않습니다.|  
|**0x4000000**|인덱스를 복제 **xml** 열입니다.|  
|**0x8000000**|구독자에 없는 스키마를 만듭니다.|  
|**0x10000000**|변환 **xml** 열을 **ntext** 구독자에 있습니다.|  
|**0x20000000**|변환 큰 개체 데이터 형식 (**nvarchar (max)**, **varchar (max)**, 및 **varbinary (max)**)에 도입 된 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서지원되는데이터형식[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0x40000000**|사용 권한을 복제합니다.|  
|**0 x 80000000**|게시의 일부가 아닌 개체에 대한 종속성을 삭제합니다.|  
|**0x100000000**|로 지정 될 경우 FILESTREAM 특성을 복제 하려면이 옵션을 사용 하 여 **varbinary (max)** 열입니다. 테이블을 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 구독자에 복제할 경우에는 이 옵션을 지정하지 마십시오. 테이블에 FILESTREAM 열이 있는 복제 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 이 스키마 옵션이 어떻게 설정 되었는지에 관계 없이 구독자가 지원 되지 않습니다. 관련된 옵션 참조 **0x800000000**합니다.|  
|**0x200000000**|날짜 및 시간 데이터 형식으로 변환 (**날짜**, **시간**, **datetimeoffset**, 및 **datetime2**)에 도입 된 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 데이터 이전 버전에서 지원 되는 형식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|**0x400000000**|데이터 및 인덱스에 대한 압축 옵션을 복제합니다. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요.|  
|**0x800000000**|FILESTREAM 데이터를 구독자에서 고유한 파일 그룹에 저장하려면 이 옵션을 설정합니다. 이 옵션을 설정하지 않으면 FILESTREAM 데이터는 기본 파일 그룹에 저장됩니다. 복제 기능에서는 파일 그룹을 만들지 않으므로 이 옵션을 설정할 경우 구독자에서 스냅숏을 적용하기 전에 파일 그룹을 만들어야 합니다. 스냅숏을 적용 하기 전에 개체를 만드는 방법에 대 한 자세한 내용은 참조 [실행 스크립트 전과 후의 스냅숏 적용](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)합니다.<br /><br /> 관련된 옵션 참조 **0x100000000**합니다.|  
|**0x1000000000**|공용 언어 런타임 (CLR) 사용자 정의 형식 (Udt) 변환 **varbinary (max)** 형식의 열을 실행 하는 구독자에 복제할 수 있도록 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다.|  
|**0 x 2000000000**|변환는 **hierarchyid** 데이터 형식을 **varbinary (max)** 있도록 형식의 열 **hierarchyid** 실행 하는 구독자에 복제할 수 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다. 사용 하는 방법에 대 한 자세한 내용은 **hierarchyid** 복제 된 테이블의 열 참조 [hierarchyid &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)합니다.|  
|**0x4000000000**|테이블의 필터링된 인덱스를 복제합니다. 필터링 된 인덱스에 대 한 자세한 내용은 참조 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)합니다.|  
|**0x8000000000**|변환 된 **geography** 및 **기 하 도형** 데이터 형식을 **varbinary (max)** 를실행하는구독자에이러한형식의열을복제할수있도록[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|형식의 열에 인덱스를 복제 **geography** 및 **geometry**합니다.|  
  
 이 값이 NULL인 경우 시스템은 아티클에 대해 유효한 스키마 옵션을 자동으로 생성합니다. **기본 스키마 옵션** 주의 섹션의 표에서 아티클 유형에 따라 선택할 수 있는 값입니다. 또한 일부 *schema_option* 모든 복제 유형 및 아티클 유형에 대해 값이 유효 합니다. **유효한 스키마 옵션** 설명에는 테이블에 지정 된 아티클 유형에 대해 지정할 수 있는 옵션을 보여 줍니다.  
  
> [!NOTE]  
>  *schema_option* 매개 변수는 초기 스냅숏에 대 한 복제 옵션에만 영향을 줍니다. 초기 스키마 스냅숏 에이전트에 의해 생성 되었으며 구독자에 적용 되 면 게시 스키마 변경 내용이 구독자에 복제할 스키마 변경 복제 규칙에 따라 및 *replicate_ddl* 에 지정 된 매개 변수 설정을 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다. 자세한 내용은 [게시 데이터베이스의 스키마 변경](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
 [  **@subset_filterclause=** ] **'***subset_filterclause***'**  
 WHERE 단어를 포함하지 않고 테이블 아티클의 행 필터링을 지정하는 WHERE 절입니다. *subset_filterclause* 의 **nvarchar (1000)**, 기본값은 빈 문자열입니다.  
  
> [!IMPORTANT]  
>  성능상의 이유로 `LEFT([MyColumn]) = SUSER_SNAME()`과 같은 매개 변수가 있는 행 필터 절의 열 이름에는 함수를 적용하지 않는 것이 좋습니다. 사용 하는 경우 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 필터 절에 HOST_NAME 값 재정의 사용 하 여 데이터 형식을 변환 해야 할 수 있습니다 [변환](../../t-sql/functions/cast-and-convert-transact-sql.md)합니다. 이 경우에 대 한 모범 사례에 대 한 자세한 내용은 "host_name () 값 재정의" 섹션을 참조 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)합니다.  
  
 [  **@article_resolver=** ] **'***article_resolver***'**  
 테이블 아티클에서 사용자 지정 비즈니스 논리를 실행하기 위해 호출된 .NET Framework 어셈블리 또는 테이블 아티클 자체의 충돌을 해결하는 데 사용하는 COM 기반 해결 프로그램입니다. *article_resolver* 은 **varchar (255)**, 기본값은 NULL입니다. 이 매개 변수에 사용할 수 있는 값은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 사용자 지정 해결 프로그램에 나열되어 있습니다. 제공된 값이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 해결 프로그램 중 하나가 아닌 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 시스템이 제공하는 해결 프로그램 대신 지정된 해결 프로그램을 사용합니다. 사용 하 여 **sp_enumcustomresolvers** 를 사용할 수 있는 사용자 지정 해결 프로그램 목록을 열거 합니다. 자세한 내용은 참조 [병합 동기화 중 비즈니스 논리 실행](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md) 및 [고급 병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)합니다.  
  
 [  **@resolver_info=** ] **'***resolver_info***'**  
 사용자 지정 해결 프로그램에 필요한 추가 정보를 지정하는 데 사용합니다. 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 해결 프로그램에는 입력으로 제공되는 열이 필요합니다. *resolver_info* 은 **nvarchar (255)**, 기본값은 NULL입니다. 자세한 내용은 [Microsoft COM 기반 해결 프로그램](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)을(를) 참조하세요.  
  
 [  **@source_owner=** ] **'***source_owner***'**  
 소유자의 이름인는 *source_object*합니다. *source_owner* 은 **sysname**, 기본값은 NULL입니다. NULL인 경우 현재 사용자가 소유자로 간주됩니다.  
  
 [  **@destination_owner=** ] **'***destination_owner***'**  
 'dbo'가 아닌 경우 구독 데이터베이스 내 개체의 소유자입니다. *destination_owner* 은 **sysname**, 기본값은 NULL입니다. NULL인 경우 'dbo'가 소유자로 간주됩니다.  
  
 [  **@vertical_partition=** ] **'***column_filter***'**  
 테이블 아티클에 열 필터링을 사용하거나 사용하지 않도록 합니다. *vertical_partition* 은 **nvarchar (5)** 기본값은 FALSE입니다.  
  
 **false** 는 열 필터링을 나타내는 모든 열을 게시 합니다.  
  
 **true** 선언 된 기본 키를 제외한 모든 열과 ROWGUID 열을 지웁니다. 사용 하 여 열이 추가 됩니다 **sp_mergearticlecolumn**합니다.  
  
 [  **@auto_identity_range=** ] **'***automatic_identity_range***'**  
 게시가 생성될 때 게시에서 테이블 아티클에 대한 자동 ID 범위 처리를 사용하거나 사용하지 않도록 합니다. *auto_identity_range* 은 **nvarchar (5)**, 기본값은 FALSE입니다. **true** 자동 id 범위를 사용 하도록 설정 하는 동안 처리, **false** 사용 되지 않습니다.  
  
> [!NOTE]  
>  *auto_identity_range* 사용 되지 않으며 이전 버전과 호환성을 위해 제공 됩니다. 사용 해야 *identityrangemanagementoption* id 범위 관리 옵션을 지정 하는 데 있습니다. 자세한 내용은 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
 [  **@pub_identity_range=** ] *pub_identity_range*  
 자동 ID 범위 관리가 사용될 때 구독 유형이 서버 구독인 구독자에 할당되는 ID 범위 크기를 제어합니다. 이 ID 범위는 재게시 구독자가 해당 구독자에게 할당하도록 예약됩니다. *pub_identity_range* 은 **bigint**, 기본값은 NULL입니다. 경우에이 매개 변수를 지정 해야 *identityrangemanagementoption* 은 **자동** 경우 *auto_identity_range* 은 **true**합니다.  
  
 [  **@identity_range=** ] *identity_range*  
 자동 ID 범위 관리가 사용될 때 게시자와 구독자 모두에게 할당되는 ID 범위 크기를 제어합니다. *identity_range* 은 **bigint**, 기본값은 NULL입니다. 경우에이 매개 변수를 지정 해야 *identityrangemanagementoption* 은 **자동** 경우 *auto_identity_range* 은 **true**합니다.  
  
> [!NOTE]  
>  *identity_range* 재게시 구독자의 이전 버전을 사용 하 여 id 범위 크기를 제어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 [  **@threshold=** ] *임계값*  
 병합 에이전트가 새 ID 범위를 할당할 때 사용되는 범위의 백분율 값입니다. 에 지정 된 값의 백분율 *임계값* 는 사용 하는 병합 에이전트가 새 id 범위를 만듭니다. *임계값* 은 **int**, 기본값은 NULL입니다. 경우에이 매개 변수를 지정 해야 *identityrangemanagementoption* 은 **자동** 경우 *auto_identity_range* 은 **true**합니다.  
  
 [  **@verify_resolver_signature=** ] *verify_resolver_signature*  
 해결 프로그램을 병합 복제에 사용하기 전에 디지털 서명을 확인할 것인지 여부를 지정합니다. *verify_resolver_signature* 은 **int**, 기본값은 1입니다.  
  
 **0** 지정는 서명을 확인 하지 것입니다.  
  
 **1** 지정 하는 시그니처를 확인 하 출처를 신뢰할 수 있는지 확인 하십시오.  
  
 [  **@destination_object=** ] **'***destination_object***'**  
 구독 데이터베이스에 있는 개체의 이름입니다. *destination_object* 은 **sysname**, 기본 값에 포함 된 내용으로 **@source_object**합니다. 이 매개 변수는 아티클이 저장 프로시저, 뷰 및 UDF와 같은 스키마 전용 아티클일 경우에만 지정할 수 있습니다. 지정 된 값의 테이블 아티클에 경우 *@source_object* 의 값을 재정의 *destination_object*합니다.  
  
 [  **@allow_interactive_resolver=** ] **'***allow_interactive_resolver***'**  
 아티클에서 대화형 해결 프로그램을 사용하거나 사용하지 않도록 합니다. *allow_interactive_resolver* 은 **nvarchar (5)**, 기본값은 FALSE입니다. **true** ; 아티클에서 대화형 해결 프로그램을 사용 하도록 설정 **false** 사용 되지 않습니다.  
  
> [!NOTE]  
>  대화형 해결 프로그램은 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자에서 지원되지 않습니다.  
  
 [  **@fast_multicol_updateproc=** ] **'***fast_multicol_updateproc***'**  
 이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다.  
  
 [  **@check_permissions=** ] *check_permissions*  
 병합 에이전트가 변경 사항을 게시자에 적용할 때 확인할 테이블 수준 권한의 비트맵입니다. 병합 프로세스가 사용하는 게시자 로그인/사용자 계정에 올바른 테이블 사용 권한이 없는 경우 잘못된 변경은 충돌로 기록됩니다. *check_permissions* 은 **int**, 수 및는 [| (비트 OR) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) 다음 값 중 하나 이상의 제품입니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**0x00** (기본값)|사용 권한을 확인하지 않습니다.|  
|**0x10**|구독자에서 실행한 삽입 작업이 업로드되기 전에 게시자에서 사용 권한을 확인합니다.|  
|**0x20**|구독자에서 실행한 업데이트 작업이 업로드되기 전에 게시자에서 사용 권한을 확인합니다.|  
|**0x40**|구독자에서 실행한 삭제 작업이 업로드되기 전에 게시자에서 사용 권한을 확인합니다.|  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 으로 인해이 저장된 프로시저가 수행한 동작 기존 스냅숏을 무효화 될 수 있습니다. *force_invalidate_snapshot* 는 **비트**, 기본값은 0입니다.  
  
 **0** 를 아티클을 추가 해도 발생 하지 스냅숏이 무효화 되도록 지정 합니다. 저장 프로시저가 새 스냅숏을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 유효 하려면 스냅숏을 무효화 아티클을 추가할를 새 스냅숏이 필요한 기존 구독이 있는 경우에 사용 되지 않는 것으로 표시 될 기존 스냅숏과 새 스냅숏을 생성할 권한을 부여 하도록 지정 합니다. *force_invalidate_snapshot* 로 설정 된 **1** 기존 스냅숏이 있는 게시에 아티클을 추가할 때.  
  
 [  **@published_in_tran_pub=** ] **'***published_in_tran_pub***'**  
 병합 게시의 아티클이 트랜잭션 게시에도 게시됨을 나타냅니다. *published_in_tran_pub* 은 **nvarchar (5)**, 기본값은 FALSE입니다. **true** 아티클이 트랜잭션 게시에도 게시를 지정 합니다.  
  
 [  **@force_reinit_subscription=** ] *force_reinit_subscription*  
 이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화해야 할 수도 있습니다. *force_reinit_subscription* 는 **비트**, 기본값은 0입니다.  
  
 **0** 를 아티클을 추가 해도 발생 하지 구독이 다시 초기화 되도록 지정 합니다. 저장 프로시저가 기존 구독을 다시 초기화해야 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 병합 아티클에 대 한 변경을 의미 인해 기존 구독이 다시 초기화 해야 할 구독을 다시 초기화할 수 있는 권한을 부여 합니다. *force_reinit_subscription* 로 설정 된 **1** 때 *subset_filterclause* 매개 변수가 있는 행 필터를 지정 합니다.  
  
 [  **@logical_record_level_conflict_detection=** ] **'***logical_record_level_conflict_detection***'**  
 논리적 레코드의 멤버인 아티클에 대한 충돌 감지 수준을 지정합니다. *logical_record_level_conflict_detection* 은 **nvarchar (5)**, 기본값은 FALSE입니다.  
  
 **true** 변경 사항이 논리적 레코드의 경우 충돌을 검색할 수 있도록 지정 합니다.  
  
 **false** 기본 충돌 감지 사용 되도록 지정 하 여 지정 된 대로 *column_tracking*합니다. 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
> [!NOTE]  
>  논리적 레코드에서 지원 되지 않으므로 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자의 값을 지정 해야 **false** 에 대 한 *logical_record_level_conflict_detection* 이러한 구독자를 지원 하도록 합니다.  
  
 [  **@logical_record_level_conflict_resolution=** ] **'***logical_record_level_conflict_resolution***'**  
 논리적 레코드의 멤버인 아티클에 대한 충돌 해결 수준을 지정합니다. *logical_record_level_conflict_resolution* 은 **nvarchar (5)**, 기본값은 FALSE입니다.  
  
 **true** 전체 우위 논리적 레코드가 무시 되를 덮어쓰도록 지정 합니다.  
  
 **false** 지정 적용 되는 행은 논리적 레코드로 제한 되지 않습니다. 경우 *logical_record_level_conflict_detection* 은 **true**, 다음 *logical_record_level_conflict_resolution* 로 설정 해야 **true**. 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
> [!NOTE]  
>  논리적 레코드에서 지원 되지 않으므로 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자의 값을 지정 해야 **false** 에 대 한 *logical_record_level_conflict_resolution* 이러한 구독자를 지원 하도록 합니다.  
  
 [  **@partition_options=** ] *partition_options*  
 아티클의 데이터 분할 방식을 정의합니다. 데이터를 분할하면 모든 행이 하나의 파티션 또는 하나의 구독에만 속한 경우 성능을 최적화할 수 있습니다. *partition_options* 은 **tinyint**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**0** (기본값)|아티클에 대한 필터링이 정적이거나, 각 파티션에 대해 고유한 데이터 하위 집합을 생성하지 않습니다. 즉, "겹치는" 파티션입니다.|  
|**1**|파티션이 겹치며 구독자에서 DML(데이터 조작 언어) 업데이트를 수행해도 행이 속한 파티션이 변경되지 않습니다.|  
|**2**|아티클을 필터링하면 겹치지 않는 파티션이 생성되지만 여러 구독자가 동일한 파티션을 받을 수 있습니다.|  
|**3**|아티클을 필터링하면 각 구독에 고유한 겹치지 않는 파티션이 생성됩니다.|  
  
> [!NOTE]  
>  아티클의 원본 테이블이 이미 다른 게시 한 후의 값에 게시 된 경우 *partition_options* 두 아티클에 대해 동일 해야 합니다.  
  
 [  **@processing_order=** ] *processing_order*  
 병합 게시에서 아티클의 처리 순서를 나타냅니다. *processing_order* 은 **int**, 기본값은 0입니다. **0** 지정은 아티클이 정렬 되지 및 다른 모든 값이 아티클의 처리 순서의 서 수 값을 나타냅니다. 아티클은 최하위에서 최상위의 순서로 처리됩니다. 처리 순서에서의 아티클 애칭 순서에 따라 결정은 두 개의 아티클을 동일한 값이 있으면는 [sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 시스템 테이블입니다. 자세한 내용은 [병합 아티클의 처리 순서 지정](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)을 참조하세요.  
  
 [  **@subscriber_upload_options=** ] *subscriber_upload_options*  
 구독 유형이 클라이언트 구독인 구독자에서 수행되는 업데이트에 대한 제한을 정의합니다. 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요. *subscriber_upload_options* 은 **tinyint**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**0** (기본값)|제한이 없습니다. 구독자의 변경 내용이 게시자에 업로드됩니다.|  
|**1**|구독자에서 변경이 허용되지만 변경 내용이 게시자에 업로드되지 않습니다.|  
|**2**|구독자에서 변경이 허용되지 않습니다.|  
  
 변경 *subscriber_upload_options* 호출 하 여 다시 초기화 하려면 구독 [sp_reinitmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md)합니다.  
  
> [!NOTE]  
>  아티클의 원본 테이블이 이미 다른 게시의 값에 게시 된 경우 *subscriber_upload_options* 두 아티클에 대해 동일 해야 합니다.  
  
 [  **@identityrangemanagementoption=** ] *identityrangemanagementoption*  
 아티클에 대해 ID 범위 관리를 처리하는 방법을 지정합니다. *identityrangemanagementoption* 은 **nvarchar (10)**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**없음**|ID 범위 관리를 사용하지 않습니다.|  
|**수동**|수동 ID 범위 처리를 사용하려면 NOT FOR REPLICATION을 사용하여 ID 열을 표시합니다.|  
|**자동**|ID 범위의 자동 관리를 지정합니다.|  
|NULL(default)|기본적으로 **none**때의 값 *auto_identity_range* 않습니다 **true**합니다.|  
  
 이전 버전과 호환성에 대 한 경우의 값 *identityrangemanagementoption* 가 NULL 인 값 *auto_identity_range* 을 선택 합니다. 그러나 때의 값 *identityrangemanagementoption* 가 NULL이 아니면 값 *auto_identity_range* 는 무시 됩니다. 자세한 내용은 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
 [  **@delete_tracking=** ] **'***delete_tracking***'**  
 삭제 내용을 복제하는지 여부를 나타냅니다. *delete_tracking* 은 **nvarchar (5)**, 기본값은 TRUE입니다. **false** 삭제 복제 하지는 및 **true** 이것이 병합 복제에 대 한 일반적인 동작 삭제 내용을 복제지 않습니다 나타냅니다. 때 *delete_tracking* 로 설정 된 **false**구독자에서 삭제 된 행은 게시자에서 수동으로 제거 하 고 게시자에서 삭제 된 행은 구독자에서 수동으로 제거 해야 합니다.  
  
> [!IMPORTANT]  
>  설정 *delete_tracking* 를 **false** 불일치가 발생 합니다. 아티클의 원본 테이블이 이미 다른 게시 한 후의 값에 게시 된 경우 *delete_tracking* 두 아티클에 대해 동일 해야 합니다.  
  
> [!NOTE]  
>  *delete_tracking* 옵션을 사용 하 여 설정할 수 없습니다는 **새 게시 마법사** 또는 **게시 속성** 대화 상자.  
  
 [  **@compensate_for_errors=** ] **'***compensate_for_errors***'**  
 동기화 중에 오류가 발생할 경우 보정 동작이 수행될지 여부를 나타냅니다. *compensate_for_errors i*s **nvarchar (5)**, 기본값은 FALSE입니다. 로 설정 하면 **true**, 변경 내용이 항상 동기화 중 게시자에서 변경 내용을 취소 하려면 보정 동작을 발생할; 하지만 하나 잘못 구성 된 오류 수를 생성 하는 구독자 또는 구독자에서 적용할 수 없습니다 변경 내용을 취소할 수 있도록 다른 구독자와 게시자에서 발생 합니다. **하지만 false** 이러한 보정 작업을 오류는 계속 기록 되며 보정 및 후속 병합 성공할 때까지 변경 내용을 적용 하려고 계속 사용 하지 않도록 설정 합니다.  
  
> [!IMPORTANT]  
>  영향을 받는 행의 데이터가 일치하지 않은 것으로 나타날 수 있지만 오류를 처리하면 바로 변경 내용을 적용할 수 있어서 데이터가 일치하게 됩니다. 아티클의 원본 테이블이 이미 다른 게시 한 후의 값에 게시 된 경우 *compensate_for_errors* 두 아티클에 대해 동일 해야 합니다.  
  
 [  **@stream_blob_columns=** ] **'***stream_blob_columns***'**  
 BLOB(Binary Large Object) 열을 복제할 때 데이터 스트림 최적화를 사용하도록 지정합니다. *stream_blob_columns* 은 **nvarchar (5)**, 기본값은 FALSE입니다. **true** 의미 하는 최적화를 시도 합니다. *stream_blob_columns* 활성화 되어 있는 경우 true로 설정 됩니다. 그러면 FILESTREAM 데이터 복제가 최적의 방식으로 수행되고 메모리 활용률이 낮아집니다. Blob 스트리밍을 사용 하지 않도록 FILESTREAM 테이블 아티클에서 사용 하 여 **sp_changemergearticle** 설정 하려면 *stream_blob_columns* 를 false입니다.  
  
> [!IMPORTANT]  
>  이 메모리 최적화를 설정하면 동기화 중에 병합 에이전트의 성능이 저하될 수 있습니다. MB 단위의 데이터가 포함된 열을 복제할 때만 이 옵션을 사용해야 합니다.  
  
> [!NOTE]  
>  논리적 레코드와 같은 특정 병합 복제 기능은 스트림 최적화를 사용 하더라도 이진 대형 개체를 복제할 때 사용 되 고 없도록 수 *stream_blob_columns* 로 설정 **true**.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 **sp_addmergearticle** 병합 복제에 사용 됩니다.  
  
 개체를 게시하면 해당 정의가 구독자로 복사됩니다. 하나 이상의 다른 개체에 종속된 데이터베이스 개체를 게시하는 경우 참조되는 개체를 모두 게시해야 합니다. 예를 들어 테이블에 종속된 뷰를 게시하는 경우 테이블도 게시해야 합니다.  
  
 값을 지정 하면 **3** 에 대 한 *partition_options*, 구독이 하나만 각 파티션에 대 한 해당 문서의 데이터의 있을 수 있습니다. 새 구독의 필터링 조건이 기존 구독과 동일한 파티션을 사용하도록 하여 두 번째 구독이 생성될 경우 기존 구독이 삭제됩니다.  
  
 에 대 한 3의 값을 지정 하는 경우 *partition_options*, 메타 데이터 정리 되어 병합 에이전트가 실행 되 고 분할 된 스냅숏은 더 빨리 만료 될 때마다 합니다. 이 옵션을 사용할 때는 구독자가 요청한 분할된 스냅숏을 활성화해야 합니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)을 참조하세요.  
  
 정적 행 필터와 아티클을 추가, 사용 하 여 *subset_filterclause*에 매개 변수가 있는 필터 하는 아티클 기존 게시의 구독을 다시 초기화 해야 합니다.  
  
 지정 하는 경우 *processing_order*, 권장 아티클 순서 값 간에 간격을 두 쉽게 나중에 새 값을 설정할 수 있습니다. 예를 들어 Article1, Article2 및 Article3 세 개의 문서를 설정한 경우 설정 *processing_order* 10, 20, 및 30 일 보다는 1, 2 및 3에 있습니다. 자세한 내용은 [병합 아티클의 처리 순서 지정](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)을 참조하세요.  
  
## <a name="default-schema-option-table"></a>기본 스키마 옵션 표  
 이 표에서 NULL 값을 지정 하는 경우 저장된 프로시저에 의해 설정 된 기본값 *schema_option*, 아티클 유형에 따라입니다.  
  
|아티클 유형|스키마 옵션 값|  
|------------------|-------------------------|  
|**func 스키마 전용**|**0x01**|  
|**인덱싱된 뷰 스키마 전용**|**0x01**|  
|**프로시저 스키마 전용**|**0x01**|  
|**table**|**0x0C034FD1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 기본 모드 스냅숏 사용 하 여 이상 호환 게시입니다.<br /><br /> **0x08034FF1**  -  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 문자 모드 스냅숏 사용 하 여 이상 호환 게시입니다.|  
|**뷰 스키마 전용**|**0x01**|  
  
> [!NOTE]  
>  게시의 이전 버전에서 지 원하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 기본 스키마 옵션에 대 한 **테이블** 은 **0x30034FF1**합니다.  
  
## <a name="valid-schema-option-table"></a>유효한 스키마 옵션 표  
 다음 표에서 허용 되는 값 설명 *schema_option* 아티클 유형에 따라 합니다.  
  
|아티클 유형|스키마 옵션 값|  
|------------------|--------------------------|  
|**func 스키마 전용**|**0x01** 및 **0x2000**|  
|**인덱싱된 뷰 스키마 전용**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**, 및 **0x200000**|  
|**프로시저 스키마 전용**|**0x01** 및 **0x2000**|  
|**table**|모든 옵션|  
|**뷰 스키마 전용**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**, 및 **0x200000**|  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-addmergearticle-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [sp_changemergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
