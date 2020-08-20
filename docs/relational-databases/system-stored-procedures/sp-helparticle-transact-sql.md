---
description: sp_helparticle(Transact-SQL)
title: sp_helparticle (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ca400eb6fc015acff452ca4ae6a7658a05145f8a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474165"
---
# <a name="sp_helparticle-transact-sql"></a>sp_helparticle(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  아티클에 대한 정보를 표시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. Oracle 게시자의 경우 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'` 게시에 있는 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 **%** 입니다. *문서* 를 제공 하지 않으면 지정 된 게시에 대 한 모든 아티클에 대 한 정보가 반환 됩니다.  
  
`[ @returnfilter = ] returnfilter` 필터 절을 반환할지 여부를 지정 합니다. *returnfilter* 는 **bit**이며 기본값은 필터 절을 반환 하는 **1**입니다.  
  
`[ @publisher = ] 'publisher'` 이외 게시자를 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자가 게시 한 아티클에 대 한 정보를 요청할 때 *게시자* 를 지정 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
`[ @found = ] found OUTPUT` 내부용 으로만 사용 됩니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**문서 id**|**int**|아티클의 ID입니다.|  
|**article name**|**sysname**|아티클의 이름입니다.|  
|**base object**|**nvarchar (257)**|아티클 또는 저장 프로시저가 나타내는 기본 테이블의 이름입니다.|  
|**대상 개체**|**sysname**|대상(구독) 테이블의 이름입니다.|  
|**synchronization object**|**nvarchar (257)**|게시된 아티클을 정의하는 뷰의 이름입니다.|  
|**type**|**smallint**|아티클의 유형입니다.<br /><br /> **1** = 로그를 기반으로 합니다.<br /><br /> **3** = 수동 필터를 사용 하 여 로그 기반<br /><br /> **5** = 수동 뷰를 사용 하 여 로그를 기반으로 합니다.<br /><br /> **7** = 수동 필터 및 수동 보기를 사용 하 여 로그를 기반으로 합니다.<br /><br /> **8** = 저장 프로시저 실행<br /><br /> **24** = serialize 할 수 있는 저장 프로시저 실행<br /><br /> **32** = 저장 프로시저 (스키마 전용)입니다.<br /><br /> **64** = 뷰 (스키마 전용)입니다.<br /><br /> **96** = 집계 함수 (스키마 전용)입니다.<br /><br /> **128** = 함수 (스키마 전용)입니다.<br /><br /> **257** = 로그 기반 인덱싱된 뷰입니다.<br /><br /> **259** = 수동 필터가 있는 로그 기반 인덱싱된 뷰입니다.<br /><br /> **261** = 수동 뷰가 있는 로그 기반 인덱싱된 뷰입니다.<br /><br /> **263** = 수동 필터 및 수동 뷰가 있는 로그 기반의 인덱싱된 뷰입니다.<br /><br /> **320** = 인덱싱된 뷰 (스키마 전용)입니다.<br /><br />|  
|**status**|**tinyint**|하나 이상의 아티클 속성의 [& (비트 and)](../../t-sql/language-elements/bitwise-and-transact-sql.md) 일 수 있습니다.<br /><br /> **0x00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0x01** = 아티클이 활성 상태입니다.<br /><br /> **0x08** = insert 문에 열 이름을 포함 합니다.<br /><br /> **0x16** = 매개 변수가 있는 문을 사용 합니다.<br /><br /> **0x32** = 매개 변수가 있는 문을 사용 하 고 insert 문에 열 이름을 포함 합니다.|  
|**필터가**|**nvarchar (257)**|테이블을 행 필터링하는 데 사용하는 저장 프로시저입니다. 이 저장 프로시저는 FOR REPLICATION 절을 사용하여 만들어야 합니다.|  
|**description**|**nvarchar(255)**|아티클에 대한 설명 항목입니다.|  
|**insert_command**|**nvarchar(255)**|삽입을 복제할 때 테이블 아티클에서 사용되는 복제 명령 유형입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.|  
|**update_command**|**nvarchar(255)**|업데이트를 복제할 때 테이블 아티클에서 사용되는 복제 명령 유형입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.|  
|**delete_command**|**nvarchar(255)**|삭제를 복제할 때 테이블 아티클에서 사용되는 복제 명령 유형입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.|  
|**creation script path**|**nvarchar(255)**|대상 테이블을 만드는 데 사용하는 아티클 스키마 스크립트의 경로 및 이름입니다.|  
|**vertical partition**|**bit**|아티클에 대해 수직 분할을 사용할 수 있는지 여부입니다. 값이 **1** 이면 수직 분할을 사용할 수 있음을 의미 합니다.|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE, DELETE TABLE 또는 TRUNCATE TABLE에 대한 사전 생성 명령입니다.|  
|**filter_clause**|**ntext**|행 필터링을 지정하는 WHERE 절입니다.|  
|**schema_option**|**binary (8)**|지정한 아티클에 대한 스키마 생성 옵션의 비트맵입니다. **Schema_option** 값의 전체 목록은 [transact-sql&#41;sp_addarticle &#40;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)를 참조 하세요.|  
|**dest_owner**|**sysname**|대상 개체 소유자의 이름입니다.|  
|**source_owner**|**sysname**|원본 개체 소유자의 이름입니다.|  
|**unqua_source_object**|**sysname**|소유자 이름을 제외한 원본 개체의 이름입니다.|  
|**sync_object_owner**|**sysname**|게시된 아티클을 정의하는 뷰의 소유자입니다. .|  
|**unqualified_sync_object**|**sysname**|게시된 아티클을 정의하는 뷰의 소유자 이름을 제외한 이름입니다.|  
|**filter_owner**|**sysname**|필터의 소유자입니다.|  
|**unqua_filter**|**sysname**|소유자 이름을 제외한 필터의 이름입니다.|  
|**@auto_identity_range**|**int**|자동 ID 범위 처리가 게시에서 생성될 때 활성화 여부를 나타내는 플래그입니다. **1** 은 자동 id 범위를 사용할 수 있음을 의미 합니다. **0** 은 사용할 수 없음을 의미 합니다.|  
|**publisher_identity_range**|**int**|아티클의 *identityrangemanagementoption* 이 **auto** 로 설정 되어 있거나 **auto_identity_range** **true**로 설정 된 경우 게시자에 있는 id 범위의 범위 크기입니다.|  
|**identity_range**|**bigint**|아티클의 *identityrangemanagementoption* 이 **auto** 로 설정 되어 있거나 **auto_identity_range** **true**로 설정 된 경우 구독자에서 id 범위의 범위 크기입니다.|  
|**threshold**|**bigint**|배포 에이전트가 새로운 ID범위를 할당하는 시기를 나타내는 백분율 값입니다.|  
|**identityrangemanagementoption**|**int**|아티클에 대해 처리되는 ID 범위 관리를 나타냅니다.|  
|**fire_triggers_on_snapshot**|**bit**|복제된 사용자 트리거를 초기 스냅샷이 적용될 때 실행할지 여부입니다.<br /><br /> **1** = 사용자 트리거가 실행 됩니다.<br /><br /> **0** = 사용자 트리거가 실행 되지 않습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helparticle** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버, **db_owner** 고정 데이터베이스 역할 또는 현재 게시에 대 한 게시 액세스 목록의 멤버만 **sp_helparticle**을 실행할 수 있습니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [아티클 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Transact-sql&#41;sp_addarticle &#40;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [Transact-sql&#41;sp_articlecolumn &#40;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [Transact-sql&#41;sp_changearticle &#40;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [Transact-sql&#41;sp_droparticle &#40;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
