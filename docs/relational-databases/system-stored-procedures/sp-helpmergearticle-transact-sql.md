---
title: sp_helpmergearticle (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticle
- sp_helpmergearticle_TSQL
helpviewer_keywords:
- sp_helpmergearticle
ms.assetid: 0fb9986a-3c33-46ef-87bb-297396ea5a6a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 04d1397494aec0d35e0ecfa9debcb6f844e6ebc2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733131"
---
# <a name="sp_helpmergearticle-transact-sql"></a>sp_helpmergearticle(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  아티클에 대한 정보를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자 또는 구독 데이터베이스의 재게시 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergearticle [ [ @publication = ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`정보를 검색할 게시의 이름입니다. *게시*는 **sysname**이며 기본값은 **%** 현재 데이터베이스의 모든 게시에 포함 된 모든 병합 아티클에 대 한 정보를 반환 하는입니다.  
  
`[ @article = ] 'article'`정보를 반환할 아티클의 이름입니다. *article*은 **sysname**이며 기본값은 지정 된 **%** 게시의 모든 병합 아티클에 대 한 정보를 반환 하는입니다.  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|아티클 식별자입니다.|  
|**name**|**sysname**|아티클의 이름입니다.|  
|**source_owner**|**sysname**|원본 개체의 소유자 이름입니다.|  
|**source_object**|**sysname**|아티클을 추가할 출처가 되는 원본 개체의 이름입니다.|  
|**sync_object_owner**|**sysname**|게시된 아티클을 정의하는 뷰의 소유자 이름입니다.|  
|**sync_object**|**sysname**|파티션에 대한 초기 데이터를 설정하는 데 사용하는 사용자 지정 개체의 이름입니다.|  
|**한**|**nvarchar(255)**|아티클에 대한 설명입니다.|  
|**status**|**tinyint**|아티클의 상태이며 다음 중 하나일 수 있습니다.<br /><br /> **1** = 비활성<br /><br /> **2** = 활성<br /><br /> **5** = DDL (데이터 정의 언어) 작업 보류 중<br /><br /> **6** = 새로 생성 된 스냅숏을 사용 하는 DDL 작업<br /><br /> 참고: 아티클이 다시 초기화 되 면 **5** 와 **6** 의 값이 **2**로 변경 됩니다.|  
|**creation_script**|**nvarchar(255)**|구독 데이터베이스에서 아티클을 만드는 데 사용된 선택적 아티클 스키마 스크립트의 경로 및 이름입니다.|  
|**conflict_table**|**nvarchar (270)**|삽입 또는 업데이트 충돌을 저장하고 있는 테이블의 이름입니다.|  
|**article_resolver**|**nvarchar(255)**|아티클에 대한 사용자 지정 해결 프로그램입니다.|  
|**subset_filterclause**|**nvarchar(1000)**|행 필터링을 지정하는 WHERE 절입니다.|  
|**pre_creation_command**|**tinyint**|사전 생성 방법이며 다음 중 하나일 수 있습니다.<br /><br /> **0** = 없음<br /><br /> **1** = 삭제<br /><br /> **2** = 삭제<br /><br /> **3** = 자름|  
|**schema_option**|**binary (8)**|아티클에 대한 스키마 생성 옵션의 비트맵입니다. 이 비트맵 옵션에 대 한 자세한 내용은 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 또는 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)를 참조 하세요.|  
|**type**|**smallint**|아티클의 유형으로 다음 중 하나일 수 있습니다.<br /><br /> **10** = 테이블<br /><br /> **32** = 저장 프로시저<br /><br /> **64** = 뷰 또는 인덱싱된 뷰<br /><br /> **128** = 사용자 정의 함수<br /><br /> **160** = 동의어 스키마만|  
|**column_tracking**|**int**|열 수준 추적에 대 한 설정 여기서 **1** 은 열 수준 추적이 설정 되어 있음을 의미 하 고 **0** 은 열 수준 추적이 해제 됨을 의미 합니다.|  
|**resolver_info**|**nvarchar(255)**|아티클 해결 프로그램의 이름입니다.|  
|**vertical_partition**|**bit**|아티클이 수직 분할 된 경우 여기서 **1** 은 아티클이 수직 분할 되었음을 의미 하 고 **0** 은 그렇지 않음을 의미 합니다.|  
|**destination_owner**|**sysname**|대상 개체의 소유자입니다. 저장 프로시저, 뷰 및 UDF(사용자 정의 함수) 스키마 아티클 병합에만 적용할 수 있습니다.|  
|**identity_support**|**int**|자동 id 범위 처리를 사용할 수 있으면이 고, 그렇지 않으면입니다. 여기서 **1** 은 사용 하도록 설정 되 고 **0** 은 사용 하지 않도록 설정 됩니다.|  
|**pub_identity_range**|**bigint**|새 ID 값 할당 시 사용할 범위 크기입니다. 자세한 내용은 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)의 "병합 복제" 섹션을 참조 하세요.|  
|**identity_range**|**bigint**|새 ID 값 할당 시 사용할 범위 크기입니다. 자세한 내용은 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)의 "병합 복제" 섹션을 참조 하세요.|  
|**threshold**|**int**|또는 이전 버전의를 실행 하는 구독자에 사용 되는 백분율 값입니다 [!INCLUDE[ssEW](../../includes/ssew-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **임계값** 병합 에이전트 새 id 범위를 할당 하는 시기를 제어 합니다. 임계값에 지정된 백분율 값을 사용하는 경우 해당 병합 에이전트가 새 ID 범위를 만듭니다. 자세한 내용은 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)의 "병합 복제" 섹션을 참조 하세요.|  
|**verify_resolver_signature**|**int**|병합 복제에서 해결 프로그램을 사용 하기 전에 디지털 서명을 확인 하면이 고, 그렇지 않으면입니다. 여기서 **0** 은 서명이 확인 되지 않음을 의미 하 고, **1** 은 서명이 신뢰할 수 있는 소스에서 온 것인지를 확인 하는 것을 의미 합니다.|  
|**destination_object**|**sysname**|대상 개체의 이름입니다. 저장 프로시저, 뷰 및 UDF 스키마 아티클 병합에만 적용할 수 있습니다.|  
|**allow_interactive_resolver**|**int**|아티클에서 대화형 해결 프로그램을 사용 하는 경우 여기서 **1** 은이 해결 프로그램이 사용 됨을 의미 하 고 **0** 은 사용 되지 않음을 의미 합니다.|  
|**fast_multicol_updateproc**|**int**|한 UPDATE 문에서 동일한 행의 여러 열에 변경 내용을 적용 하기 위해 병합 에이전트를 사용 하거나 사용 하지 않도록 설정 합니다. 여기서 **1** 은 한 문에서 여러 열이 업데이트 됨을 의미 하 고 **0** 은 업데이트 된 각 열에 대해 별도의 UPDATE 문이 문제 임을 의미 합니다.|  
|**check_permissions**|**int**|확인된 테이블 수준 권한의 비트맵을 나타내는 정수 값입니다. 가능한 값 목록은 [sp_addmergearticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)를 참조 하세요.|  
|**processing_order**|**int**|게시 내에서 아티클에 데이터 변경 사항을 적용하는 순서입니다.|  
|**upload_options**|**tinyint**|클라이언트 구독이 있는 구독자에서 수행되는 업데이트에 대한 제한을 정의하며 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **0** = 클라이언트 구독이 있는 구독자에서 수행 되는 업데이트에 대 한 제한은 없습니다. 모든 변경 내용이 게시자로 업로드 됩니다.<br /><br /> **1** = 클라이언트 구독이 있는 구독자에서 변경이 허용 되지만 게시자로 업로드 되지 않습니다.<br /><br /> **2** = 클라이언트 구독이 있는 구독자에서 변경이 허용 되지 않습니다.<br /><br /> 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.|  
|**identityrangemanagementoption**|**int**|자동 id 범위 처리를 사용할 수 있으면이 고, 그렇지 않으면입니다. 여기서 **1** 은 사용 하도록 설정 되 고 **0** 은 사용 하지 않도록 설정 됩니다.|  
|**delete_tracking**|**bit**|삭제가 복제 되 면이 고, 여기서 **1** 은 삭제가 복제 됨을 의미 하 고 **0** 은 그렇지 않음을 의미 합니다.|  
|**compensate_for_errors**|**bit**|동기화 중에 오류가 발생할 경우 보정 동작을 수행 하는지 여부를 나타냅니다. 여기서 **1** 은 보정 작업이 수행 됨을 나타내고 **0** 은 보정 작업이 수행 되지 않음을 의미 합니다.|  
|**partition_options**|**tinyint**|아티클의 데이터 분할 방식을 정의합니다. 데이터를 분할하면 모든 행이 하나의 파티션 또는 하나의 구독에만 속한 경우 성능을 최적화할 수 있습니다. *partition_options* 는 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 아티클의 필터링이 정적 이거나 각 파티션에 대 한 고유한 데이터 하위 집합을 생성 하지 않습니다. 즉, "겹치는" 파티션입니다.<br /><br /> **1** = 파티션이 겹칩니다. 구독자에서 DML (데이터 조작 언어) 업데이트를 수행 하면 행이 속한 파티션이 변경 되지 않습니다.<br /><br /> **2** = 아티클을 필터링 하면 겹치지 않는 파티션이 생성 되지만 여러 구독자가 동일한 파티션을 받을 수 있습니다.<br /><br /> **3** = 아티클에 대 한 필터링은 각 구독에 고유한 겹치지 않는 파티션을 생성 합니다.|  
|**artid**|**uniqueidentifier**|아티클을 고유하게 식별하는 식별자입니다.|  
|**pubid**|**uniqueidentifier**|아티클이 게시되는 게시를 고유하게 식별하는 식별자입니다.|  
|**stream_blob_columns**|**bit**|BLOB(Binary Large Object) 열을 복제할 때 데이터 스트림 최적화를 사용할지 여부입니다. **1** 은 최적화가 사용 됨을 의미 하 고 **0** 은 최적화가 사용 되지 않음을 의미 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpmergearticle** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 게시 데이터베이스의 **db_owner** 고정 데이터베이스 역할, 배포 데이터베이스의 **replmonitor** 역할 또는 게시에 대 한 게시 액세스 목록의 멤버만 **sp_helpmergearticle**을 실행할 수 있습니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_helpmergearticle](../../relational-databases/replication/codesnippet/tsql/sp-helpmergearticle-tran_1.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [아티클 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Transact-sql&#41;sp_addmergearticle &#40;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [Transact-sql&#41;sp_changemergearticle &#40;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergearticle &#40;](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
