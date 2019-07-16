---
title: sp_droparticle (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 050de12a1dc1ff91071ae3c81d3b30425f1a590e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912887"
---
# <a name="spdroparticle-transact-sql"></a>sp_droparticle(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  스냅숏 또는 트랜잭션 게시에서 아티클을 삭제합니다. 아티클에 한 개 이상의 구독이 있는 경우에는 아티클을 제거할 수 없습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'` 삭제할 아티클이 속한 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @article = ] 'article'` 삭제할 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 으로 인해이 저장된 프로시저가 수행한 동작 기존 스냅숏을 무효화 될 수 있습니다. *force_invalidate_snapshot* 되는 **비트**, 기본값은 **0**합니다.  
  
 **0** 는 아티클에 대 한 변경 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅숏을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 아티클의 변경이 잘못 스냅숏이 무효화 될 수 있습니다 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 되지 않음으로 표시 하 고 새 스냅숏을 생성할 권한을 부여 되도록 지정 합니다.  
  
`[ @publisher = ] 'publisher'` 이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에서 아티클 속성을 변경 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
`[ @from_drop_publication = ] from_drop_publication` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_droparticle** 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 행 필터링 된 아티클에 대 한 **sp_droparticle** 확인 합니다 **형식** 에서 아티클 열을 [sysarticles &#40;Transact SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블 삭제할지 여부를 뷰 또는 필터도 결정 합니다. 뷰 또는 필터가 자동으로 생성된 경우에는 아티클과 함께 삭제됩니다. 수동으로 만든 경우에는 삭제되지 않습니다.  
  
 실행 **sp_droparticle** 게시에서 아티클을 삭제 하려면에서 제거 되지는 않습니다 개체 게시 데이터베이스나 구독 데이터베이스에서 해당 하는 개체입니다. 필요한 경우 `DROP <object>`를 사용하여 이러한 개체를 수동으로 제거합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_droparticle](../../relational-databases/replication/codesnippet/tsql/sp-droparticle-transact-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_droparticle**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [아티클 삭제](../../relational-databases/replication/publish/delete-an-article.md)   
 [기존 게시에 대한 아티클 추가 및 삭제](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
