---
title: sp_changemergearticle (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergearticle_TSQL
- sp_changemergearticle
helpviewer_keywords:
- sp_changemergearticle
ms.assetid: 0dc3da5c-4af6-45be-b5f0-074da182def2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 97c6a7d309578ebe0cc6e93b5408ad6d9fad6296
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771508"
---
# <a name="sp_changemergearticle-transact-sql"></a>sp_changemergearticle(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  병합 아티클의 속성을 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changemergearticle [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`아티클이 있는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`변경할 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @property = ] 'property'`지정 된 아티클 및 게시에 대해 변경할 속성입니다. *속성* 은 **nvarchar (30)** 이며 표에 나열 된 값 중 하나일 수 있습니다.  
  
`[ @value = ] 'value'`지정 된 속성의 새 값입니다. *value* 는 **nvarchar (1000)** 이며 표에 나열 된 값 중 하나일 수 있습니다.  
  
 다음 표에서는 아티클의 속성 및 해당 속성의 값을 설명합니다.  
  
|속성|값|설명|  
|--------------|------------|-----------------|  
|**allow_interactive_resolver**|**true**|아티클에 대해 대화형 해결 프로그램을 사용합니다.|  
||**false**|아티클에 대해 대화형 해결 프로그램을 사용하지 않습니다.|  
|**article_resolver**||아티클에 대한 사용자 지정 해결 프로그램입니다. 테이블 아티클에만 적용됩니다.|  
|**check_permissions** (비트맵)|**0x00**|테이블 수준 권한을 확인하지 않습니다.|  
||**10**|구독자에서 작성된 INSERT 문이 게시자에 적용되기 전에 게시자에서 테이블 수준 권한을 확인합니다.|  
||**0x20**|구독자에서 작성된 UPDATE 문이 게시자에 적용되기 전에 게시자에서 테이블 수준 권한을 확인합니다.|  
||**0x40**|구독자에서 작성된 DELETE 문이 게시자에 적용되기 전에 게시자에서 테이블 수준 권한을 확인합니다.|  
|**column_tracking**|**true**|열 수준 추적을 설정합니다. 테이블 아티클에만 적용됩니다.<br /><br /> 참고: 246 개 이상의 열이 있는 테이블을 게시 하는 경우 열 수준 추적을 사용할 수 없습니다.|  
||**false**|열 수준 추적을 해제하고 행 수준에서 충돌 감지를 유지합니다. 테이블 아티클에만 적용됩니다.|  
|**compensate_for_errors**|**true**|동기화 중 오류가 발생하면 보정 동작을 수행합니다. 자세한 내용은 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)를 참조 하세요.|  
||**false**|보정 동작을 수행하지 않습니다(기본 동작). 자세한 내용은 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)를 참조 하세요.<br /><br /> 중요 영향을 받는 행의 데이터는 오류를 해결 하는 즉시 적용 되지 않는 것 처럼 보일 수 있지만 변경 내용을 적용 하 고 데이터를 수렴 합니다. ** \* \* \* \* ** 아티클의 원본 테이블이 이미 다른 게시에 게시 된 경우 *compensate_for_errors* 의 값은 두 아티클에 대해 동일 해야 합니다.|  
|**creation_script**||구독 데이터베이스에서 아티클을 만드는 데 사용된 선택적 아티클 스키마 스크립트의 경로 및 이름입니다.|  
|**delete_tracking**|**true**|DELETE 문을 복제합니다(기본 동작).|  
||**false**|DELETE 문을 복제하지 않습니다.<br /><br /> ** \* \* 중요 \* 한 \* ** 설정 **delete_tracking** **false** 이면 일치 하지 않으므로 삭제 된 행을 수동으로 제거 해야 합니다.|  
|**한**||아티클에 대한 설명 항목입니다.|  
|**destination_owner**||**Dbo**가 아닌 경우 구독 데이터베이스에 있는 개체 소유자의 이름입니다.|  
|**identity_range**||아티클에 **identityrangemanagementoption** 가 **auto** 로 설정 되어 있거나 **auto_identity_range** **true**로 설정 된 경우 새 id 값을 할당할 때 사용할 범위 크기를 지정 하는 **bigint** 입니다. 테이블 아티클에만 적용됩니다. 자세한 내용은 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)의 "병합 복제" 섹션을 참조 하세요.|  
|**identityrangemanagementoption**|**수동**|자동 ID 범위 관리를 사용하지 않습니다. 수동 ID 범위 처리를 사용하려면 NOT FOR REPLICATION을 사용하여 ID 열을 표시합니다. 자세한 내용은 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.|  
||**없음**|모든 ID 범위 관리를 사용하지 않습니다.|  
|**logical_record_level_conflict_detection**|**true**|논리적 레코드에 변경 사항이 발생하면 충돌이 감지됩니다. **Logical_record_level_conflict_resolution** **true**로 설정 해야 합니다.|  
||**false**|기본 충돌 검색은 **column_tracking**에 지정 된 대로 사용 됩니다.|  
|**logical_record_level_conflict_resolution**|**true**|전체 적용되는 논리적 레코드가 무시되는 논리적 레코드를 덮어씁니다.|  
||**false**|적용되는 행은 논리적 레코드로 제한되지 않습니다.|  
|**partition_options**|**0**|아티클에 대한 필터링이 정적이거나 각 파티션에 대한 고유한 데이터 하위 집합을 생성하지 않습니다. 즉, "겹치는" 파티션입니다.|  
||**1**|파티션이 겹치며 구독자에서 DML 업데이트를 수행해도 행이 속한 파티션이 변경되지 않습니다.|  
||**2**|아티클을 필터링하면 겹치지 않는 파티션이 생성되지만 여러 구독자가 동일한 파티션을 받을 수 있습니다.|  
||**3**|아티클을 필터링하면 각 구독에 고유한 겹치지 않는 파티션이 생성됩니다.<br /><br /> 참고: **partition_options**에 값 **3** 을 지정 하면 해당 아티클의 각 데이터 파티션에 대해 구독이 하나만 있을 수 있습니다. 새 구독의 필터링 조건이 기존 구독과 동일한 파티션을 사용하도록 하여 두 번째 구독이 생성될 경우 기존 구독이 삭제됩니다.|  
|**pre_creation_command**|**없음**|구독자에 이미 테이블이 존재하는 경우 아무런 동작이 발생하지 않습니다.|  
||**delete**|하위 집합 필터의 WHERE 절을 기반으로 하여 삭제를 실행합니다.|  
||**그림자**|테이블을 다시 만들기 전에 삭제합니다.|  
||**잘라내야**|대상 테이블을 자릅니다.|  
|**processing_order**||병합 게시에서 아티클의 처리 순서를 나타내는 **int** 입니다.|  
|**pub_identity_range**||아티클의 **identityrangemanagementoption** 가 **auto** 로 설정 되거나 **auto_identity_range** **true**로 설정 된 경우 서버 구독이 있는 구독자에 할당 된 범위 크기를 지정 하는 **bigint** 입니다. 이 ID 범위는 재게시 구독자가 해당 구독자에게 할당하도록 예약됩니다. 테이블 아티클에만 적용됩니다. 자세한 내용은 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)의 "병합 복제" 섹션을 참조 하세요.|  
|**published_in_tran_pub**|**true**|아티클을 트랜잭션 게시에도 게시합니다.|  
||**false**|아티클을 트랜잭션 게시에 게시하지 않습니다.|  
|**resolver_info**||사용자 지정 해결 프로그램에 필요한 추가 정보를 지정하는 데 사용합니다. 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 해결 프로그램에는 입력으로 제공되는 열이 필요합니다. **resolver_info** 는 **nvarchar (255)** 이며 기본값은 NULL입니다. 자세한 내용은 [Microsoft COM 기반 해결 프로그램](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)을(를) 참조하세요.|  
|**schema_option** (비트맵)||자세한 내용은 이 항목의 뒷부분에 나오는 주의 섹션을 참조하십시오.|  
||**0x00**|스냅숏 에이전트에서 스크립팅을 사용 하지 않도록 설정 하 고 **creation_script**에 제공 된 스크립트를 사용 합니다.|  
||**0x01**|개체 만들기 스크립트(CREATE TABLE, CREATE PROCEDURE 등)를 생성합니다.|  
||**10**|해당 클러스터형 인덱스를 생성합니다.|  
||**0x20**|사용자 정의 데이터 형식을 구독자에서의 기본 데이터 형식으로 변환합니다. UDT 열에 CHECK 또는 DEFAULT 제약 조건이 있거나 UDT(사용자 정의 형식) 열이 기본 키의 일부이거나 계산 열이 UDT 열을 참조하는 경우 이 옵션을 사용할 수 없습니다.|  
||**0x40**|해당 비클러스터형 인덱스를 생성합니다.|  
||**0x80**|기본 키에 대해 선언된 참조 무결성을 포함합니다.|  
||**0x100**|정의된 경우 테이블 아티클에 사용자 트리거를 복제합니다.|  
||**0x200**|FOREIGN KEY 제약 조건을 복제합니다. 참조되는 테이블이 게시의 일부가 아닌 경우 게시된 테이블의 모든 FOREIGN KEY 제약 조건은 복제되지 않습니다.|  
||**0x400**|CHECK 제약 조건을 복제합니다.|  
||**0x800**|기본값을 복제합니다.|  
||**0x1000**|열 수준 데이터 정렬을 복제합니다.|  
||**0x2000**|게시된 아티클 원본 개체와 연관된 확장 속성을 복제합니다.|  
||**0x4000**|테이블 아티클에 정의된 경우 고유 키를 복제합니다.|  
||**0x8000**|제약 조건을 스크립팅할 때 ALTER TABLE 문을 생성합니다.|  
||**0x10000**|동기화하는 동안 CHECK 조건이 강제 적용되지 않도록 해당 제약 조건을 NOT FOR REPLICATION으로 복제합니다.|  
||**0x20000**|동기화하는 동안 FOREIGN KEY 제약 조건이 강제 적용되지 않도록 해당 제약 조건을 NOT FOR REPLICATION으로 복제합니다.|  
||**0x40000**|분할된 테이블이나 인덱스와 연결된 파일 그룹을 복제합니다.|  
||**0x80000**|분할된 테이블에 대한 파티션 구성표를 복제합니다.|  
||**0x100000**|분할된 인덱스에 대한 파티션 구성표를 복제합니다.|  
||**0x200000**|테이블 통계를 복제합니다.|  
||**0x400000**|기본 바인딩을 복제합니다.|  
||**0x800000**|규칙 바인딩을 복제합니다.|  
||**0x1000000**|전체 텍스트 인덱스를 복제합니다.|  
||**0x2000000**|**Xml** 열에 바인딩된 xml 스키마 컬렉션은 복제 되지 않습니다.|  
||**0x4000000**|**Xml** 열에 인덱스를 복제 합니다.|  
||**0x8000000**|구독자에 없는 스키마를 만듭니다.|  
||**0x10000000**|구독자에서 **xml** 열을 **ntext** 로 변환 합니다.|  
||**0x20000000**|에 도입 된 large object 데이터 형식 (**nvarchar (max)**, **varchar (max)** 및 **varbinary (max)**) [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 을에서 지원 되는 데이터 형식으로 변환 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 합니다.|  
||**0x40000000**|사용 권한을 복제합니다.|  
||**0x80000000**|게시의 일부가 아닌 개체에 대한 종속성을 삭제합니다.|  
||**0x100000000**|**Varbinary (max)** 열에 지정 된 경우이 옵션을 사용 하 여 FILESTREAM 특성을 복제 합니다. 테이블을 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 구독자에 복제할 경우에는 이 옵션을 지정하지 마십시오. FILESTREAM 열이 있는 테이블 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 은이 스키마 옵션이 설정 된 방법에 관계 없이 구독자에 복제할 수 없습니다. 관련 옵션 **0x800000000**을 참조 하십시오.|  
||**0x200000000**|에서 도입 된 날짜 및 시간 데이터 형식 (**date**, **time**, **datetimeoffset**및 **datetime2**) [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 을 이전 버전의에서 지원 되는 데이터 형식으로 변환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
||**0x400000000**|데이터 및 인덱스에 대한 압축 옵션을 복제합니다. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요.|  
||**0x800000000**|FILESTREAM 데이터를 구독자에서 고유한 파일 그룹에 저장하려면 이 옵션을 설정합니다. 이 옵션을 설정하지 않으면 FILESTREAM 데이터는 기본 파일 그룹에 저장됩니다. 복제 기능에서는 파일 그룹을 만들지 않으므로 이 옵션을 설정할 경우 구독자에서 스냅샷을 적용하기 전에 파일 그룹을 만들어야 합니다. 스냅숏을 적용 하기 전에 개체를 만드는 방법에 대 한 자세한 내용은 [스냅숏 적용 전후에 스크립트 실행](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)을 참조 하세요.<br /><br /> 관련 옵션인 **0x100000000**을 참조 하십시오.|  
||**0x1000000000**|UDT 형식의 열을를 실행 하는 구독자로 복제할 수 있도록 CLR (공용 언어 런타임) Udt (사용자 정의 형식)를 **varbinary (max)** 로 변환 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 합니다.|  
||**0x2000000000**|**Hierarchyid 데이터 형식을** **varbinary (max)** 로 변환 하 여 **hierarchyid** 형식의 열을를 실행 하는 구독자로 복제할 수 있습니다 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . 복제 된 테이블에서 **hierarchyid** 열을 사용 하는 방법에 대 한 자세한 내용은 [hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)를 참조 하세요.|  
||**0x4000000000**|테이블의 필터링된 인덱스를 복제합니다. 필터링 된 인덱스에 대 한 자세한 내용은 [필터링 된 인덱스 만들기](../../relational-databases/indexes/create-filtered-indexes.md)를 참조 하세요.|  
||**0x8000000000**|**Geography** 및 **geometry** 데이터 형식을 **varbinary (max)** 로 변환 하 여 이러한 형식의 열을를 실행 하는 구독자로 복제할 수 있습니다 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .|  
||**0x10000000000**|**Geography** 및 **geometry**형식의 열에 대 한 인덱스를 복제 합니다.|  
||NULL|시스템에서 아티클에 대해 유효한 스키마 옵션을 자동으로 생성합니다.|  
|**status**|**active**|테이블 게시를 위한 초기 처리 스크립트가 실행됩니다.|  
||**unsynced**|스냅샷 에이전트가 다음에 실행될 때 테이블 게시를 위한 초기 처리 스크립트가 실행됩니다.|  
|**stream_blob_columns**|**true**|BLOB(Binary Large Object) 열을 복제할 때 데이터 스트림 최적화를 사용합니다. 그러나 논리적 레코드와 같은 특정 병합 복제 기능은 스트림 최적화를 사용할 수 없도록 합니다. FILESTREAM을 사용 하는 경우 *stream_blob_columns* true로 설정 됩니다. 그러면 FILESTREAM 데이터 복제가 최적의 방식으로 수행되고 메모리 활용률이 낮아집니다. FILESTREAM 테이블 아티클에서 blob 스트리밍을 사용 하지 않도록 하려면 *stream_blob_columns* 을 false로 설정 합니다.<br /><br /> 중요이 메모리 최적화를 사용 하도록 설정 하면 동기화 하는 동안 병합 에이전트의 성능이 저하 될 수 있습니다. ** \* \* \* \* ** MB 단위의 데이터가 포함된 열을 복제할 때만 이 옵션을 사용해야 합니다.|  
||**false**|BLOB 열을 복제할 때 최적화를 사용하지 않습니다.|  
|**subscriber_upload_options**|**0**|클라이언트 구독이 있는 구독자에서 수행되는 업데이트에 제한이 없으며 변경 내용이 게시자로 업로드됩니다. 이 속성을 변경하려면 기존 구독자를 다시 초기화해야 합니다.|  
||**1**|클라이언트 구독이 있는 구독자에서 변경이 허용되지만 변경 내용이 게시자로 업로드되지 않습니다.|  
||**2**|클라이언트 구독이 있는 구독자에서 변경이 허용되지 않습니다.|  
|**subset_filterclause**||행 필터링을 지정하는 WHERE 절입니다. 테이블 아티클에만 적용됩니다.<br /><br /> 중요 성능상의 이유로과 같은 매개 변수가 있는 행 필터 절의 열 이름에는 함수를 적용 하지 않는 것이 좋습니다. ** \* \* \* \* ** `LEFT([MyColumn]) = SUSER_SNAME()` 필터 절에 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 를 사용 하 고 HOST_NAME 값을 재정의 하는 경우 [convert](../../t-sql/functions/cast-and-convert-transact-sql.md)를 사용 하 여 데이터 형식을 변환 해야 할 수 있습니다. 이 경우 모범 사례에 대 한 자세한 내용은 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)의 "HOST_NAME () 값 재정의" 섹션을 참조 하세요.|  
|**threshold**||이전 버전의를 실행 하는 구독자에 사용 되는 백분율 값입니다 [!INCLUDE[ssEW](../../includes/ssew-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **임계값** 병합 에이전트 새 id 범위를 할당 하는 시기를 제어 합니다. 임계값에 지정된 백분율 값을 사용하는 경우 해당 병합 에이전트가 새 ID 범위를 만듭니다. **Identityrangemanagementoption** 가 **auto** 로 설정 되거나 **auto_identity_range** 이 **true**로 설정 된 경우 사용 됩니다. 테이블 아티클에만 적용됩니다. 자세한 내용은 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)의 "병합 복제" 섹션을 참조 하세요.|  
|**verify_resolver_signature**|**1**|트러스트된 원본에서 제공된 것인지 판단하기 위해 사용자 지정 해결 프로그램의 디지털 서명을 확인합니다|  
||**0**|트러스트된 원본에서 제공된 것인지 판단하기 위해 사용자 지정 해결 프로그램의 디지털 서명을 확인을 하지 않습니다.|  
|NULL(기본값)||*속성*에 대해 지원 되는 값 목록을 반환 합니다.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`이 저장 프로시저가 수행한 동작으로 인해 기존 스냅숏이 무효화 될 수 있음을 승인 합니다. *force_invalidate_snapshot* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 병합 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅샷을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 병합 아티클에 대 한 변경으로 인해 스냅숏이 무효화 될 수 있음을 의미 하며, 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 사용 되지 않는 것으로 표시 되 고 새 스냅숏으로 생성 될 수 있는 권한을 부여 합니다.  
  
 변경 시 새 스냅샷의 생성을 필요로 하는 속성에 대해서는 주의 섹션을 참조하십시오.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화 해야 할 수도 있습니다. *force_reinit_subscription* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 병합 아티클에 대 한 변경으로 인해 구독이 다시 초기화 되지 않도록 지정 합니다. 저장 프로시저가 기존 구독을 다시 초기화해야 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 병합 아티클에 대 한 변경으로 인해 기존 구독이 다시 초기화 됨을 의미 하며 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
 변경 시 기존의 모든 구독을 다시 초기화해야 하는 속성에 대해서는 주의 섹션을 참조하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changemergearticle** 는 병합 복제에 사용 됩니다.  
  
 **Sp_changemergearticle** 은 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)를 사용 하 여 처음에 지정 된 아티클 속성을 변경 하는 데 사용 되므로 이러한 속성에 대 한 자세한 내용은 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 을 참조 하십시오.  
  
 다음 속성을 변경 하려면 새 스냅숏을 생성 해야 하며 *force_invalidate_snapshot* 매개 변수에 **1** 값을 지정 해야 합니다.  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **schema_options**  
  
-   **subset_filterclause**  
  
 다음 속성을 변경 하려면 기존 구독을 다시 초기화 해야 하며 *force_reinit_subscription* 매개 변수에 **1** 값을 지정 해야 합니다.  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **identityrangemanagementoption**  
  
-   **subscriber_upload_options**  
  
-   **subset_filterclause**  
  
-   **creation_script**  
  
-   **schema_option**  
  
-   **logical_record_level_conflict_detection**  
  
-   **logical_record_level_conflict_resolution**  
  
 **Partition_options**에 값 3을 지정 하는 경우 병합 에이전트 실행 될 때마다 메타 데이터가 정리 되 고 분할 된 스냅숏은 더 빨리 만료 됩니다. 이 옵션을 사용할 때는 구독자가 요청한 분할된 스냅샷을 활성화해야 합니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을(를) 참조하세요.  
  
 **Column_tracking** 속성을 설정할 때 테이블이 이미 다른 병합 게시에 게시 된 경우 열 추적은이 테이블을 기반으로 하는 기존 아티클에서 사용 하는 값과 동일 해야 합니다. 이 매개 변수는 테이블 아티클에만 해당합니다.  
  
 여러 게시에서 동일한 기본 테이블을 기반으로 아티클을 게시 하는 경우 한 아티클의 **delete_tracking** 속성이 나 **compensate_for_errors** 속성을 변경 하면 같은 테이블을 기반으로 하는 다른 아티클의 변경 내용이 동일 하 게 적용 됩니다.  
  
 병합 프로세스가 사용하는 게시자 로그인/사용자 계정에 올바른 테이블 사용 권한이 없는 경우 잘못된 변경은 충돌로 기록됩니다.  
  
 **Schema_option**값을 변경 하는 경우 시스템은 비트 업데이트를 수행 하지 않습니다. 즉, **sp_changemergearticle**를 사용 하 여 **schema_option** 를 설정 하면 기존 비트 설정이 해제 될 수 있습니다. 기존 설정을 유지 하려면 설정 하는 값과 *schema_option*의 현재 값 사이에 [& (비트 and)](../../t-sql/language-elements/bitwise-and-transact-sql.md) 를 수행 해야 합니다 .이 값은 [sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)를 실행 하 여 확인할 수 있습니다.  
  
> [!CAUTION]  
>  게시에 수백 개의 아티클이 있고 문서 중 하나에 대해 **sp_changemergearticle** 를 실행 하는 경우 실행을 완료 하는 데 시간이 오래 걸릴 수 있습니다.  
  
## <a name="valid-schema-option-table"></a>유효한 스키마 옵션 표  
 다음 표에서는 아티클 유형에 따라 허용 되는 *schema_option*값에 대해 설명 합니다.  
  
|아티클 유형|스키마 옵션 값|  
|------------------|--------------------------|  
|**func schema only**|**0x01** 및 **0x2000**|  
|**indexed view schema only**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**및 **0x200000**|  
|**proc schema only**|**0x01** 및 **0x2000**|  
|**table**|모든 옵션|  
|**view schema only**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**및 **0x200000**|  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_changemergearticle](../../relational-databases/replication/codesnippet/tsql/sp-changemergearticle-tr_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_changemergearticle**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [아티클 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Transact-sql&#41;sp_addmergearticle &#40;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergearticle &#40;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergearticle &#40;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
