---
title: sp_articlefilter (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 11d00c389f815117f624ea0a8099a49e7db28fdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129749"
---
# <a name="sparticlefilter-transact-sql"></a>sp_articlefilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  테이블 아티클을 기준으로 게시할 데이터를 필터링합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'` 아티클이 속한 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @article = ] 'article'` 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @filter_name = ] 'filter_name'` 만들 필터 저장 프로시저의 이름은 합니다 *filter_name*합니다. *filter_name* 됩니다 **nvarchar(386)** , 기본값은 NULL입니다. 고유한 아티클 필터의 이름을 지정해야 합니다.  
  
`[ @filter_clause = ] 'filter_clause'` 제한은 행 필터를 정의 하는 (WHERE) 절입니다. 제약 조건 절을 입력할 때는 키워드인 WHERE를 생략합니다. *filter_clause* 됩니다 **ntext**, 기본값은 NULL입니다.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 으로 인해이 저장된 프로시저가 수행한 동작 기존 스냅숏을 무효화 될 수 있습니다. *force_invalidate_snapshot* 되는 **비트**, 기본값은 **0**합니다.  
  
 **0** 는 아티클에 대 한 변경 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅숏을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클의 변경이 잘못 스냅숏이 무효화 될 수 있습니다 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 되지 않음으로 표시 하 고 새 스냅숏을 생성할 권한을 부여 되도록 지정 합니다.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 이 저장된 프로시저가 수행한 동작 기존 구독을 다시 초기화에 필요할 수 있음을 승인 합니다. *force_reinit_subscription* 되는 **비트**, 기본값은 **0**합니다.  
  
 **0** 아티클의 아티클의 변경이 수행 하지 않는 구독을 다시 초기화 해야 합니다. 저장 프로시저가 구독의 다시 초기화를 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 문서 변경으로 인해 기존 구독이 다시 초기화 되도록 지정 하며 구독을 다시 초기화할 수에 대 한 사용 권한을 부여 합니다.  
  
`[ @publisher = ] 'publisher'` 이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 사용 하 여 사용할 수 없습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_articlefilter** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 실행 **sp_articlefilter** 하려면 기존 구독을 사용 하 여 문서에 대 한 해당 구독을 다시 초기화 합니다.  
  
 **sp_articlefilter** 필터를 만들고 필터 저장 프로시저의 ID를 삽입 합니다 **필터** 열의 합니다 [sysarticles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블 차례로 제한 절의 텍스트를 삽입 합니다 **filter_clause** 열입니다.  
  
 아티클을 행 필터링을 사용 하 여 만들려는 실행 [sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 없이 *필터* 매개 변수입니다. 실행 **sp_articlefilter**를 비롯 한 모든 매개 변수를 제공 *filter_clause*, 및 실행 한 다음 [sp_articleview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md), 동일한 포함 하는 모든 매개 변수를 제공 *filter_clause*합니다. 필터가 이미 존재 하는 경우는 **형식** 에 **sysarticles** 됩니다 **1** (로그 기반 아티클) 이면 이전 필터가 삭제 되 고 새 필터가 작성 됩니다.  
  
 하는 경우 *filter_name* 하 고 *filter_clause* 를 제공 하지 않은 이전 필터가 삭제 되 고 필터 ID로 설정 됩니다 **0**합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_articlefilter**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [정적 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
