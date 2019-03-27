---
title: sp_articleview (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 10c46ac2ff35d73453976a91276246d3e810e425
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492835"
---
# <a name="sparticleview-transact-sql"></a>sp_articleview(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'` 아티클이 속한 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @article = ] 'article'` 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @view_name = ] 'view_name'` 게시 된 아티클을 정의 하는 뷰의 이름이입니다. *view_name* 됩니다 **nvarchar(386)**, 기본값은 NULL입니다.  
  
`[ @filter_clause = ] 'filter_clause'` 제한은 행 필터를 정의 하는 (WHERE) 절입니다. 제약 조건 절을 입력할 때는 WHERE 키워드를 생략합니다. *filter_clause* 됩니다 **ntext**, 기본값은 NULL입니다.  
  
`[ @change_active = ] change_active` 구독이 있는 게시에서 열을 수정할 수 있습니다. *change_active* 되는 **int**, 기본값은 **0**합니다. 하는 경우 **0**, 열은 변경 되지 않습니다. 하는 경우 **1**, 뷰를 생성 또는 구독이 있는 활성 아티클에서 다시 만들 수 있습니다.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 으로 인해이 저장된 프로시저가 수행한 동작 기존 스냅숏을 무효화 될 수 있습니다. *force_invalidate_snapshot* 되는 **비트**, 기본값은 **0**합니다.  
  
 **0** 는 아티클에 대 한 변경 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅숏을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클의 변경이 잘못 스냅숏이 무효화 될 수 있습니다 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 되지 않음으로 표시 하 고 새 스냅숏을 생성할 권한을 부여 되도록 지정 합니다.  
  
`[ @force_reinit_subscription = ] _force_reinit_subscription_` 이 저장된 프로시저가 수행한 동작 기존 구독을 다시 초기화에 필요할 수 있음을 승인 합니다. *force_reinit_subscription* 되는 **비트** 이며 기본값은 **0**합니다.  
  
 **0** 문서를 변경으로 인해 구독이 다시 초기화 되지 않습니다 지정 합니다. 저장 프로시저가 구독의 다시 초기화를 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 문서 변경으로 인해 기존 구독이 다시 초기화 되도록 지정 하며 구독을 다시 초기화할 수에 대 한 사용 권한을 부여 합니다.  
  
`[ @publisher = ] 'publisher'` 이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에서 게시 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
`[ @refreshsynctranprocs = ] refreshsynctranprocs` 복제를 동기화 하는 데 저장된 프로시저는 자동으로 다시 생성 하는 경우입니다. *refreshsynctranprocs* 됩니다 **비트**, 기본값은 1입니다.  
  
 **1** 저장된 프로시저 다시 생성 됨을 의미 합니다.  
  
 **0** 저장된 프로시저 다시 생성 됨을 의미 합니다.  
  
`[ @internal = ] internal` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_articleview** 게시 된 아티클을 정의 하 고이 뷰의 ID를 삽입 하는 뷰를 만들고는 **sync_objid** 열의 합니다 [sysarticles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블을 마우스에 제한 절의 텍스트를 삽입 합니다 **filter_clause** 열입니다. 모든 열이 복제 되 고 없는 경우 없습니다 **filter_clause**의 **sync_objid** 에 [sysarticles &#40;Transact SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블의 ID로 설정 되어를 사용 하 여 기본 테이블 **sp_articleview** 필요 하지 않습니다.  
  
 열 필터링 된 테이블을 게시 하려면 (즉, 필터 열에) 처음 실행할 **sp_addarticle** 없이 *sync_object* 매개 변수를 실행 [sp_articlecolumn &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) (열 필터 정의)에 복제 하 고 실행 하려면 각 열에 한 번씩 **sp_articleview** 게시 된 아티클을 정의 하는 보기를 만듭니다.  
  
 필터링 된 테이블을 게시 하려면 (즉, 행 필터링) 실행 [sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 없이 *필터* 매개 변수입니다. 실행 [sp_articlefilter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)를 비롯 한 모든 매개 변수 *filter_clause*. 그런 다음 **sp_articleview**, 동일한을 비롯 한 모든 매개 변수 *filter_clause*합니다.  
  
 세로 및 가로로 필터링된 된 테이블을 게시 하려면 [sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 없이 *sync_object* 하거나 *필터* 매개 변수. 실행 [sp_articlecolumn &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 복제할 각 열에 한 번씩 및 실행 [sp_articlefilter &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 고 **sp_ articleview**합니다.  
  
 문서 게시 된 아티클을 정의 하는 보기를 이미 있으면 **sp_articleview** 기존 뷰를 삭제 하 고 새 브러시를 자동으로 만듭니다. 뷰가 수동으로 생성 된 경우 (**형식** 에 [sysarticles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) 됩니다 **5**), 기존 뷰는 삭제 되지 않습니다.  
  
 사용자 지정 필터 저장 프로시저와 게시 아티클을 수동으로 정의 하는 보기를 만드는 경우 실행 되지 않습니다 **sp_articleview**합니다. 대신 이러한를 제공 합니다 *필터* 및 *sync_object* 매개 변수를 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)를 함께 적절 한 *형식* 값입니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_articleview**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [정적 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
