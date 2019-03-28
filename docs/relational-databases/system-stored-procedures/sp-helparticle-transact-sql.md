---
title: sp_helparticle (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticle_TSQL
- sp_helparticle
helpviewer_keywords:
- sp_helparticle
ms.assetid: 9c4a1a88-56f1-45a0-890c-941b8e0f0799
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43eada100fb1de531c0d16082bdf0977e479ccfb
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536154"
---
# <a name="sphelparticle-transact-sql"></a>sp_helparticle(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  아티클에 대한 정보를 표시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. Oracle 게시자의 경우 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @article = ] 'article'` 게시에서 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 **%** 합니다. 하는 경우 *문서* 는 제공 되지 않으면 지정된 된 게시에 대 한 모든 문서에 대 한 정보 반환 됩니다.  
  
`[ @returnfilter = ] returnfilter` 필터 절을 반환할지 여부를 지정 합니다. *returnfilter* 됩니다 **비트**, 기본값은 **1**, 필터 절을 반환 하는 합니다.  
  
`[ @publisher = ] 'publisher'` 이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 에서 게시 아티클에 대 한 정보를 요청할 때 지정할 수 없습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
`[ @found = ] found OUTPUT` 내부 전용입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**문서 id**|**int**|아티클의 ID입니다.|  
|**문서 이름**|**sysname**|아티클의 이름입니다.|  
|**기본 개체**|**nvarchar(257)**|아티클 또는 저장 프로시저가 나타내는 기본 테이블의 이름입니다.|  
|**대상 개체**|**sysname**|대상(구독) 테이블의 이름입니다.|  
|**동기화 개체**|**nvarchar(257)**|게시된 아티클을 정의하는 뷰의 이름입니다.|  
|**type**|**smallint**|아티클의 유형입니다.<br /><br /> **1** = 로그 기반 합니다.<br /><br /> **3** 수동 필터가 있는 로그 기반 =.<br /><br /> **5** = 수동 뷰가 있는 로그 기반 합니다.<br /><br /> **7** = 수동 필터 및 수동 뷰가 있는 로그 기반 합니다.<br /><br /> **8** = 저장 프로시저 실행 합니다.<br /><br /> **24** = 직렬화 가능 프로시저 실행 합니다.<br /><br /> **32** = 저장 프로시저 (스키마 전용).<br /><br /> **64** = 뷰 (스키마 전용).<br /><br /> **96** = 집계 함수 (스키마 전용).<br /><br /> **128** = 함수 (스키마 전용).<br /><br /> **257** = 로그 기반 인덱싱된 뷰.<br /><br /> **259** 수동 필터가 있는 로그 기반의 인덱싱된 뷰를 =.<br /><br /> **261** = 수동 뷰가 있는 로그 기반의 인덱싱된 뷰.<br /><br /> **-263** = 수동 필터가 있는 로그 기반의 인덱싱된 뷰 및 수동 뷰가 있습니다.<br /><br /> **320** = 인덱싱된 뷰 (스키마 전용).<br /><br />|  
|**상태**|**tinyint**|수는 [& (비트 AND)](../../t-sql/language-elements/bitwise-and-transact-sql.md) 결과 중 하나 이상 이러한 문서 속성:<br /><br /> **0x00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0x01** = 아티클이 활성 상태입니다.<br /><br /> **0x08** = insert 문에 열 이름을 포함 합니다.<br /><br /> **0x16** = 문을 매개 변수화 사용 합니다.<br /><br /> **0x32** = 문을 매개 변수화 사용 및 insert 문에 열 이름을 포함 합니다.|  
|**filter**|**nvarchar(257)**|테이블을 행 필터링하는 데 사용하는 저장 프로시저입니다. 이 저장 프로시저는 FOR REPLICATION 절을 사용하여 만들어야 합니다.|  
|**description**|**nvarchar(255)**|아티클에 대한 설명 항목입니다.|  
|**insert_command**|**nvarchar(255)**|삽입을 복제할 때 테이블 아티클에서 사용되는 복제 명령 유형입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.|  
|**update_command**|**nvarchar(255)**|업데이트를 복제할 때 테이블 아티클에서 사용되는 복제 명령 유형입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.|  
|**delete_command**|**nvarchar(255)**|삭제를 복제할 때 테이블 아티클에서 사용되는 복제 명령 유형입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.|  
|**생성 스크립트 경로**|**nvarchar(255)**|대상 테이블을 만드는 데 사용하는 아티클 스키마 스크립트의 경로 및 이름입니다.|  
|**수직 분할**|**bit**|아티클에 수직 분할 사용 여부는 여기서 값 **1** 수직 분할은 사용할 수 있음을 의미 합니다.|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE, DELETE TABLE 또는 TRUNCATE TABLE에 대한 사전 생성 명령입니다.|  
|**filter_clause**|**ntext**|행 필터링을 지정하는 WHERE 절입니다.|  
|**schema_option**|**binary(8)**|지정한 아티클에 대한 스키마 생성 옵션의 비트맵입니다. 전체 목록은 **schema_option** 값을 참조 하십시오 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|대상 개체 소유자의 이름입니다.|  
|**source_owner**|**sysname**|원본 개체 소유자의 이름입니다.|  
|**unqua_source_object**|**sysname**|소유자 이름을 제외한 원본 개체의 이름입니다.|  
|**sync_object_owner**|**sysname**|게시된 아티클을 정의하는 뷰의 소유자입니다. .|  
|**unqualified_sync_object**|**sysname**|게시된 아티클을 정의하는 뷰의 소유자 이름을 제외한 이름입니다.|  
|**filter_owner**|**sysname**|필터의 소유자입니다.|  
|**unqua_filter**|**sysname**|소유자 이름을 제외한 필터의 이름입니다.|  
|**auto_identity_range**|**int**|자동 ID 범위 처리가 게시에서 생성될 때 활성화 여부를 나타내는 플래그입니다. **1** 자동 id 범위는 사용할 수 있음을 의미 합니다. **0** 비활성화 된 것을 의미 합니다.|  
|**publisher_identity_range**|**int**|기술 자료 문서에 하는 경우 게시자에서 id 범위 크기 범위 *identityrangemanagementoption* 로 설정 **자동** 하거나 **auto_identity_range** 로  **true**합니다.|  
|**identity_range**|**bigint**|문서에 있는 경우 구독자에서 id 범위 크기 범위 *identityrangemanagementoption* 로 설정 **자동** 하거나 **auto_identity_range** 로  **true**합니다.|  
|**threshold**|**bigint**|배포 에이전트가 새로운 ID범위를 할당하는 시기를 나타내는 백분율 값입니다.|  
|**identityrangemanagementoption**|**int**|아티클에 대해 처리되는 ID 범위 관리를 나타냅니다.|  
|**fire_triggers_on_snapshot**|**bit**|복제된 사용자 트리거를 초기 스냅숏이 적용될 때 실행할지 여부입니다.<br /><br /> **1** = 사용자 트리거가 실행 됩니다.<br /><br /> **0** = 사용자 트리거가 실행 되지 않습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_helparticle** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버만 합니다 **sysadmin** 고정 서버 역할을 합니다 **db_owner** 고정된 데이터베이스 역할 또는 현재 게시에 대 한 게시 액세스 목록에서 실행할 수 있습니다 **sp_helparticle**.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>관련 항목  
 [문서 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
