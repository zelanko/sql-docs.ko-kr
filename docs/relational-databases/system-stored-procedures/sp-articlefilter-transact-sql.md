---
title: sp_articlefilter (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 037812be8b38c9be107197a72bd7a161e56904c9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716229"
---
# <a name="sp_articlefilter-transact-sql"></a>sp_articlefilter(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  테이블 아티클을 기준으로 게시할 데이터를 필터링합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_articlefilter [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @filter_name = ] 'filter_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`아티클이 포함 된 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @filter_name = ] 'filter_name'`*Filter_name*에서 만들 필터 저장 프로시저의 이름입니다. *filter_name* 은 **nvarchar (386)** 이며 기본값은 NULL입니다. 고유한 아티클 필터의 이름을 지정해야 합니다.  
  
`[ @filter_clause = ] 'filter_clause'`는 가로 필터를 정의 하는 제한 (WHERE) 절입니다. 제약 조건 절을 입력할 때는 키워드인 WHERE를 생략합니다. *filter_clause* 는 **ntext**이며 기본값은 NULL입니다.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`이 저장 프로시저가 수행한 동작으로 인해 기존 스냅숏이 무효화 될 수 있음을 승인 합니다. *force_invalidate_snapshot* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅샷을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 될 수 있음을 지정 합니다. 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 사용 되지 않는 것으로 표시 되 고 새 스냅숏으로 생성 될 수 있는 권한을 부여 합니다.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화 해야 할 수도 있습니다. *force_reinit_subscription* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 아티클에 대 한 변경으로 인해 구독을 다시 초기화할 필요가 없도록 지정 합니다. 저장 프로시저가 구독의 다시 초기화를 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클에 대 한 변경으로 인해 기존 구독이 다시 초기화 되도록 지정 하며 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
`[ @publisher = ] 'publisher'`이외 게시자를 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에는 *게시자* 를 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_articlefilter** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 기존 구독이 있는 아티클에 대해 **sp_articlefilter** 를 실행 하려면 해당 구독을 다시 초기화 해야 합니다.  
  
 **sp_articlefilter** 필터를 만들고 [sysarticles &#40;transact-sql&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블의 **필터** 열에 필터 저장 프로시저의 ID를 삽입 한 다음 제한 절의 텍스트를 **filter_clause** 열에 삽입 합니다.  
  
 행 필터를 사용 하 여 아티클을 만들려면 *필터* 매개 변수 없이 [transact-sql&#41;&#40;sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 를 실행 합니다. **Sp_articlefilter**를 실행 하 여 *filter_clause*를 비롯 한 모든 매개 변수를 제공한 다음 [transact-sql&#41;sp_articleview &#40;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)실행 하 여 동일한 *filter_clause*를 포함 하는 모든 매개 변수를 제공 합니다. 필터가 이미 존재 하 고 **sysarticles** 의 **유형이** **1** (로그 기반 아티클) 인 경우에는 이전 필터가 삭제 되 고 새 필터가 생성 됩니다.  
  
 *Filter_name* 및 *filter_clause* 를 제공 하지 않으면 이전 필터가 삭제 되 고 필터 ID가 **0**으로 설정 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_articlefilter**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [아티클 정의](../../relational-databases/replication/publish/define-an-article.md)   
 [정적 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [Transact-sql&#41;sp_addarticle &#40;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [Transact-sql&#41;sp_articleview &#40;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [Transact-sql&#41;sp_changearticle &#40;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [Transact-sql&#41;sp_droparticle &#40;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [Transact-sql&#41;sp_helparticle &#40;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
