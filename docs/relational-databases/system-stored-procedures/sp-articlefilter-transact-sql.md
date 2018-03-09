---
title: sp_articlefilter (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de8979cdc3cb382aa290148e560d8eb72db94b1b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
 [  **@publication=**] **'***게시***'**  
 아티클을 포함하는 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@article=**] **'***문서***'**  
 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@filter_name=**] **'***filter_name***'**  
 만들 필터 저장 프로시저의 이름인는 *filter_name*합니다. *filter_name* 은 **nvarchar (386)**, 기본값은 NULL입니다. 고유한 아티클 필터의 이름을 지정해야 합니다.  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 행 필터를 정의하는 제한(WHERE) 절입니다. 제약 조건 절을 입력할 때는 키워드인 WHERE를 생략합니다. *filter_clause* 은 **ntext**, 기본값은 NULL입니다.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 으로 인해이 저장된 프로시저가 수행한 동작 기존 스냅숏을 무효화 될 수 있습니다. *force_invalidate_snapshot* 는 **비트**, 기본값은 **0**합니다.  
  
 **0** 은 아티클의 변경이 스냅숏을 무효화 인해 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅숏을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 는 아티클에 대 한 변경 유효 하려면 스냅숏을 무효화를 의미 하며 새 스냅숏이 필요한 기존 구독이 있는 경우에 사용 되지 않는 것으로 표시 될 기존 스냅숏과 새 스냅숏을 생성할 권한을 부여 하도록 지정 합니다.  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화해야 할 수도 있습니다. *force_reinit_subscription* 는 **비트**, 기본값은 **0**합니다.  
  
 **0** 변경이 구독이 다시 초기화에 대 한 요구가 인해 되지 않도록 지정 합니다. 저장 프로시저가 구독의 다시 초기화를 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 를 문서에 대 한 변경 하면 기존 구독이 다시 초기화 되도록 지정 하며 구독을 다시 초기화할 수에 대 한 사용 권한을 부여 합니다.  
  
 [  **@publisher=** ] **'***게시자***'**  
 지정 된 비-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 으로 쓰일 수 없습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_articlefilter** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 실행 **sp_articlefilter** 을 사용 하려면 기존 구독이 있는 아티클에 대 한 구독 다시 초기화 해야 합니다.  
  
 **sp_articlefilter** 는 필터를 만들고 삽입 하는 필터 저장 프로시저의 ID는 **필터** 의 열은 [sysarticles &#40; Transact SQL &#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블을 선택한 다음에 제한 절의 텍스트를 삽입는 **filter_clause** 열입니다.  
  
 행 필터를 사용 하 여 문서를 만들려면 실행 [sp_addarticle &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 없이 *필터* 매개 변수입니다. 실행 **sp_articlefilter**를 비롯 한 모든 매개 변수 *filter_clause*, 다음 실행 [sp_articleview &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md), 모든 매개 변수를 포함 하 여 동일한 *filter_clause*합니다. 필터가 이미 존재 하는 경우는 **형식** 에 **sysarticles** 은 **1** (로그 기반 아티클) 이면 이전 필터가 삭제 되 고 새 필터가 작성 됩니다.  
  
 경우 *filter_name* 및 *filter_clause* 를 제공 하지 않은 이전 필터가 삭제 되 고 필터 ID로 설정 되어 **0**합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_articlefilter**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [정적 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
