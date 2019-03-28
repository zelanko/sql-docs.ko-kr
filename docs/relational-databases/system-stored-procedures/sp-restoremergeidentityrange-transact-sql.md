---
title: sp_restoremergeidentityrange (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_restoremergeidentityrange_TSQL
- sp_restoremergeidentityrange
helpviewer_keywords:
- sp_restoremergeidentityrange
ms.assetid: 7923e422-2748-40c0-b5a8-6410c48d5b70
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0576f180809a4432af022d278867d847c8087dd4
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526215"
---
# <a name="sprestoremergeidentityrange-transact-sql"></a>sp_restoremergeidentityrange(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 ID 범위 할당을 업데이트하는 데 사용되며 백업에서 게시자를 복원한 후 자동 ID 범위 관리가 제대로 작동하도록 해 줍니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_restoremergeidentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 **모든**합니다. 지정한 경우 해당 게시에 대한 ID 범위만 복원됩니다.  
  
`[ @article = ] 'article'` 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 **모든**합니다. 지정한 경우 해당 아티클에 대한 ID 범위만 복원됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_restoremergeidentityrange** 병합 복제에 사용 됩니다.  
  
 **sp_restoremergeidentityrange** 배포자 로부터 최대 id 범위 할당 정보를 가져오고 값을 업데이트 합니다 **max_used** 열의 [MSmerge_identity_range_allocations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-identity-range-allocations-transact-sql.md) 자동 id 범위 관리를 사용 하는 아티클에 대해 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_restoremergeidentityrange**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
