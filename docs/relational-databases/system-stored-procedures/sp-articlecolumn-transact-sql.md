---
title: sp_articlecolumn (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72d9238e5b0f8ad5480e05ded3a0154eb5510904
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640721"
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
 이 아티클을 포함하는 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@article=**] **'***문서***'**  
 아티클의 이름입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@column=**] **'***열***'**  
 추가하거나 삭제할 열의 이름입니다. *열* 됩니다 **sysname**, 기본값은 NULL입니다. NULL인 경우 모든 열이 게시됩니다.  
  
 [  **@operation=**] **'***작업***'**  
 아티클에서 열의 추가 또는 삭제 여부를 지정합니다. *작업이* 됩니다 **nvarchar(5)**, 기본값은 add 사용 하 여 합니다. **추가** 복제에 대 한 열을 표시 합니다. **drop** 열 표시를 지웁니다.  
  
 [  **@refresh_synctran_procs=**] *refresh_synctran_procs*  
 복제한 열 수와 일치하도록 즉시 업데이트 구독을 지원하는 저장 프로시저를 다시 생성할지 여부를 지정합니다. *refresh_synctran_procs* 됩니다 **비트**, 기본값은 **1**합니다. 하는 경우 **1**, 저장된 프로시저 다시 생성 됩니다.  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 이 저장 프로시저가 배포자에 연결되지 않고 실행되는지 여부를 표시합니다. *ignore_distributor* 됩니다 **비트**, 기본값은 **0**합니다. 하는 경우 **0**, 게시 하기 위해 데이터베이스를 활성화 해야 하며 문서에서 복제 된 새 열을 반영 하도록 문서 캐시를 새로 고쳐야 합니다. 하는 경우 **1**, 아티클 열 게시 되지 않은 데이터베이스에 복구 상황 에서만에서 사용 해야 하는 문서에 대 한 삭제할 수 있습니다.  
  
 [  **@change_active =** ] *change_active*  
 구독이 있는 게시에서 열을 수정할 수 있도록 허용합니다. *change_active* 되는 **int** 이며 기본값은 **0**합니다. 하는 경우 **0**, 열은 수정 되지 않습니다. 하는 경우 **1**, 열을 추가 하거나 구독이 있는 활성 아티클에서 삭제할 수 있습니다.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 으로 인해이 저장된 프로시저가 수행한 동작 기존 스냅숏을 무효화 될 수 있습니다. *force_invalidate_snapshot* 되는 **비트**, 기본값은 **0**합니다.  
  
 **0** 는 아티클에 대 한 변경 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅숏을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클의 변경이 잘못 스냅숏이 무효화 될 수 있습니다 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 되지 않음으로 표시 하 고 새 스냅숏을 생성할 권한을 부여 되도록 지정 합니다.  
  
 [ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화해야 할 수도 있습니다. *force_reinit_subscription* 되는 **비트**, 기본값은 **0**합니다.  
  
 **0** 문서를 변경으로 인해 구독이 다시 초기화 되지 않습니다 지정 합니다. 저장 프로시저가 구독의 다시 초기화를 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다. **1** 문서 변경으로 인해 기존 구독이 다시 초기화 되도록 지정 하며 구독을 다시 초기화할 수에 대 한 사용 권한을 부여 합니다.  
  
 [  **@publisher=** ] **'***게시자***'**  
 이외[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 사용 하 여 사용할 수 없습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
 [  **@internal=** ] **'***내부***'**  
 내부적으로만 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_articlecolumn** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 사용 하 여 아티클만 필터링 할 수 있습니다 **sp_articlecolumn**합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_articlecolumn**합니다.  
  
## <a name="see-also"></a>관련 항목  
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
  
  
