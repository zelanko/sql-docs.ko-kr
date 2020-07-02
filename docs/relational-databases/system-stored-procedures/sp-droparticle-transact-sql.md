---
title: sp_droparticle (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droparticle_TSQL
- sp_droparticle
helpviewer_keywords:
- sp_droparticle
ms.assetid: 09fec594-53f4-48a5-8edb-c50731c7adb2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1b150636804bc4d312f6f6bfbe046ef7e9612207
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717294"
---
# <a name="sp_droparticle-transact-sql"></a>sp_droparticle(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  스냅샷 또는 트랜잭션 게시에서 아티클을 삭제합니다. 아티클에 한 개 이상의 구독이 있는 경우에는 아티클을 제거할 수 없습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droparticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @from_drop_publication = ] from_drop_publication ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`삭제할 아티클을 포함 하는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`삭제할 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`이 저장 프로시저가 수행한 동작으로 인해 기존 스냅숏이 무효화 될 수 있음을 승인 합니다. *force_invalidate_snapshot* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅샷을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 될 수 있음을 지정 합니다. 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 사용 되지 않는 것으로 표시 되 고 새 스냅숏으로 생성 될 수 있는 권한을 부여 합니다.  
  
`[ @publisher = ] 'publisher'`이외 게시자를 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에 대 한 아티클 속성을 변경할 때는 *게시자* 를 사용 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
`[ @from_drop_publication = ] from_drop_publication` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_droparticle** 는 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 행 필터링 된 **sp_droparticle** 아티클의 경우 [sysarticles &#40;transact-sql&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블에서 아티클의 **유형** 열을 확인 하 여 뷰나 필터도 삭제할지 여부를 결정할 수 있습니다. 뷰 또는 필터가 자동으로 생성된 경우에는 아티클과 함께 삭제됩니다. 수동으로 만든 경우에는 삭제되지 않습니다.  
  
 게시에서 아티클을 삭제 하기 위해 **sp_droparticle** 를 실행 해도 게시 데이터베이스에서 개체가 제거 되거나 구독 데이터베이스에서 해당 개체가 제거 되지 않습니다. 필요한 경우 `DROP <object>`를 사용하여 이러한 개체를 수동으로 제거합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_droparticle](../../relational-databases/replication/codesnippet/tsql/sp-droparticle-transact-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_droparticle**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [아티클 삭제](../../relational-databases/replication/publish/delete-an-article.md)   
 [기존 게시에 대 한 아티클 추가 및 삭제](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Transact-sql&#41;sp_addarticle &#40;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [Transact-sql&#41;sp_changearticle &#40;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [Transact-sql&#41;sp_helparticle &#40;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Transact-sql&#41;sp_helparticlecolumns &#40;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
