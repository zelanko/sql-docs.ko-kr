---
title: sp_restoremergeidentityrange (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a41b725d46c96f1ab79444246ab538b0c3f539f0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82816963"
---
# <a name="sp_restoremergeidentityrange-transact-sql"></a>sp_restoremergeidentityrange(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 ID 범위 할당을 업데이트하는 데 사용되며 백업에서 게시자를 복원한 후 자동 ID 범위 관리가 제대로 작동하도록 해 줍니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_restoremergeidentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 **all**입니다. 지정한 경우 해당 게시에 대한 ID 범위만 복원됩니다.  
  
`[ @article = ] 'article'`아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 **all**입니다. 지정한 경우 해당 아티클에 대한 ID 범위만 복원됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_restoremergeidentityrange** 는 병합 복제에 사용 됩니다.  
  
 자동 id 범위 관리를 사용 하는 아티클에 대해 [MSmerge_identity_range_allocations &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-identity-range-allocations-transact-sql.md) 의 **max_used** 열에서 값을 업데이트 하는 **sp_restoremergeidentityrange** 배포자에서 최대 id 범위 할당 정보를 가져옵니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_restoremergeidentityrange**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addmergearticle &#40;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [Transact-sql&#41;sp_changemergearticle &#40;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
