---
title: sp_articleview (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articleview
- sp_articleview_TSQL
helpviewer_keywords:
- sp_articleview
ms.assetid: a3d63fd6-f360-4a2f-8a82-a0dc15f650b3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7cc40187ccafebee672214a0926a3ca0d0bc4176
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768989"
---
# <a name="sp_articleview-transact-sql"></a>sp_articleview(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  테이블을 수직 또는 수평으로 필터링할 때 게시된 아티클을 정의하는 뷰를 만듭니다. 이 뷰는 대상 테이블에 대한 스키마 및 데이터의 필터링된 원본으로 사용됩니다. 이 저장 프로시저로는 구독되지 않은 아티클만 수정할 수 있습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_articleview [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @view_name = ] 'view_name']  
    [ , [ @filter_clause = ] 'filter_clause']  
    [ , [ @change_active = ] change_active ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @refreshsynctranprocs = ] refreshsynctranprocs ]  
    [ , [ @internal = ] internal ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`아티클이 포함 된 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @view_name = ] 'view_name'`게시 된 아티클을 정의 하는 뷰의 이름입니다. *view_name* 은 **nvarchar (386)** 이며 기본값은 NULL입니다.  
  
`[ @filter_clause = ] 'filter_clause'`는 가로 필터를 정의 하는 제한 (WHERE) 절입니다. 제약 조건 절을 입력할 때는 WHERE 키워드를 생략합니다. *filter_clause* 는 **ntext**이며 기본값은 NULL입니다.  
  
`[ @change_active = ] change_active`구독이 있는 게시에서 열을 수정할 수 있습니다. *change_active* 은 **int**이며 기본값은 **0**입니다. **0**인 경우 열은 변경 되지 않습니다. **1**인 경우 구독이 있는 활성 아티클에서 뷰를 만들거나 다시 만들 수 있습니다.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`이 저장 프로시저가 수행한 동작으로 인해 기존 스냅숏이 무효화 될 수 있음을 승인 합니다. *force_invalidate_snapshot* 는 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅샷을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 될 수 있음을 지정 합니다. 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 사용 되지 않는 것으로 표시 되 고 새 스냅숏으로 생성 될 수 있는 권한을 부여 합니다.  
  
`[ @force_reinit_subscription = ] _force_reinit_subscription_`이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화 해야 할 수도 있습니다. *force_reinit_subscription* 는 **bit** 이며 기본값은 **0**입니다.  
  
 **0** 은 아티클에 대 한 변경으로 인해 구독이 다시 초기화 되지 않도록 지정 합니다. 저장 프로시저가 구독의 다시 초기화를 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클에 대 한 변경으로 인해 기존 구독이 다시 초기화 되도록 지정 하며 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
`[ @publisher = ] 'publisher'`[!INCLUDE[msCoName](../../includes/msconame-md.md)] 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정 합니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시할 때는 게시자를 사용 하면 안 됩니다.  
  
`[ @refreshsynctranprocs = ] refreshsynctranprocs`복제를 동기화 하는 데 사용 되는 저장 프로시저가 자동으로 다시 생성 되는지 여부입니다. *refreshsynctranprocs* 는 **bit**이며 기본값은 1입니다.  
  
 **1** 은 저장 프로시저가 다시 생성 됨을 의미 합니다.  
  
 **0** 은 저장 프로시저가 다시 생성 되지 않음을 의미 합니다.  
  
`[ @internal = ] internal` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_articleview** 는 게시 된 아티클을 정의 하는 뷰를 만들고 [sysarticles &#40;transact-sql&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블의 **sync_objid** 열에이 뷰의 ID를 삽입 한 다음에 restriction 절의 텍스트를 삽입 합니다. **filter_clause** 열입니다. 모든 열이 복제 되 고 **filter_clause**없으면 [sysarticles &#40;&#41; transact-sql](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블의 **sync_objid** 는 기본 테이블의 ID로 설정 되 고 **sp_articleview** 사용은 필요 하지 않습니다.  
  
 세로로 필터링 된 테이블을 게시 하려면 (즉, 열을 필터링 하려면) 먼저 *sync_object* 매개 변수 없이 **sp_addarticle** 를 실행 하 고, 복제할 각 열에 대해 [sp_articlecolumn &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 을 한 번씩 실행 합니다. 세로 필터)를 클릭 한 다음 **sp_articleview** 를 실행 하 여 게시 된 아티클을 정의 하는 뷰를 만듭니다.  
  
 행을 필터링 하기 위해 행 필터링 된 테이블을 게시 하려면 *필터* 매개 변수 없이 [sp_addarticle &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 을 실행 합니다. *Filter_clause*를 포함 한 모든 매개 변수를 제공 하 여 [sp_articlefilter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)을 실행 합니다. 그런 다음 **sp_articleview**를 실행 하 여 동일한 *filter_clause*를 포함 하는 모든 매개 변수를 제공 합니다.  
  
 수직 및 수평 필터링 된 테이블을 게시 하려면 *sync_object* 또는 *필터* 매개 변수 없이 [sp_addarticle &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 을 실행 합니다. 복제할 각 열에 대해 [sp_articlecolumn &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 을 한 번 실행 한 다음 [ &#40;sp_articlefilter transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 및 **sp_articleview**를 실행 합니다.  
  
 아티클이 이미 게시 된 아티클을 정의 하는 뷰를 포함 하는 경우 **sp_articleview** 는 기존 뷰를 삭제 하 고 새 뷰를 자동으로 만듭니다. 뷰가 수동으로 만들어진 경우 ( [sysarticles &#40;transact-sql&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) 이 **5**인 경우) 기존 보기는 삭제 되지 않습니다.  
  
 사용자 지정 필터 저장 프로시저 및 게시 된 아티클을 수동으로 정의 하는 뷰를 만드는 경우 **sp_articleview**를 실행 하지 마십시오. 대신, 적절 한 *형식* 값과 함께 [sp_addarticle &#40;&#41;transact-sql](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)에 *filter* 및 *sync_object* 매개 변수로 제공 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만이 **sp_articleview**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [정적 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
