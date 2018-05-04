---
title: sp_articlecolumn (Transact SQL) | Microsoft Docs
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
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 407c4470ae7dad6a871736df822cb00a22882122
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sparticlecolumn-transact-sql"></a>sp_articlecolumn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시된 테이블의 데이터를 열 필터링하기 위해 아티클에 포함된 열을 지정하는 데 사용합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_articlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column' ]  
    [ , [ @operation = ] 'operation' ]  
    [ , [ @refresh_synctran_procs = ] refresh_synctran_procs ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @change_active = ] change_actve ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @internal = ] 'internal' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 이 아티클을 포함하는 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@article=**] **'***문서***'**  
 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@column=**] **'***열***'**  
 추가하거나 삭제할 열의 이름입니다. *열* 은 **sysname**, 기본값은 NULL입니다. NULL인 경우 모든 열이 게시됩니다.  
  
 [  **@operation=**] **'***작업***'**  
 아티클에서 열의 추가 또는 삭제 여부를 지정합니다. *작업* 은 **nvarchar (5)**, 기본값은 add입니다. **추가** 복제에 대 한 열을 표시 합니다. **drop** 열 표시를 해제 합니다.  
  
 [  **@refresh_synctran_procs=**] *refresh_synctran_procs*  
 복제한 열 수와 일치하도록 즉시 업데이트 구독을 지원하는 저장 프로시저를 다시 생성할지 여부를 지정합니다. *refresh_synctran_procs* 은 **비트**, 기본값은 **1**합니다. 경우 **1**, 저장된 프로시저 다시 생성 됩니다.  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 이 저장 프로시저가 배포자에 연결되지 않고 실행되는지 여부를 표시합니다. *ignore_distributor* 은 **비트**, 기본값은 **0**합니다. 경우 **0**, 데이터베이스, 게시에 설정 해야 하 고 문서에서 복제 된 새 열을 반영 하기 위해 아티클 캐시 새로 고쳐야 합니다. 경우 **1**, 아티클 열을 게시 되지 않은 데이터베이스에 있는; 복구 상황 에서만에서 사용 해야 하는 문서에 대 한 삭제할 수 있습니다.  
  
 [  **@change_active =** ] *change_active*  
 구독이 있는 게시에서 열을 수정할 수 있도록 허용합니다. *change_active* 는 **int** 기본값인 **0**합니다. 경우 **0**, 열 수정 되지 않습니다. 경우 **1**, 열 추가 또는 구독이 있는 활성 아티클에서 삭제 될 수 있습니다.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 으로 인해이 저장된 프로시저가 수행한 동작 기존 스냅숏을 무효화 될 수 있습니다. *force_invalidate_snapshot* 는 **비트**, 기본값은 **0**합니다.  
  
 **0** 은 아티클의 변경이 스냅숏을 무효화 인해 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅숏을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 는 아티클에 대 한 변경 유효 하려면 스냅숏을 무효화를 의미 하며 새 스냅숏이 필요한 기존 구독이 있는 경우에 사용 되지 않는 것으로 표시 될 기존 스냅숏과 새 스냅숏을 생성할 권한을 부여 하도록 지정 합니다.  
  
 [ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화해야 할 수도 있습니다. *force_reinit_subscription* 는 **비트**, 기본값은 **0**합니다.  
  
 **0** 문서에 대 한 변경으로 인해 구독이 다시 초기화 해야 하지 않도록 지정 합니다. 저장 프로시저가 구독의 다시 초기화를 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다. **1** 아티클의 변경이 아티클에 기존 구독이 다시 초기화 해야 할 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
 [  **@publisher=** ] **'***게시자***'**  
 지정 된 비-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 으로 쓰일 수 없습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
 [  **@internal=** ] **'***내부***'**  
 내부적으로만 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_articlecolumn** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 등록 취소할된 아티클을만 사용 하 여 필터링 할 수 있습니다 **sp_articlecolumn**합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_articlecolumn**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [열 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
