---
title: sp_dropmergefilter (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergefilter_TSQL
- sp_dropmergefilter
helpviewer_keywords:
- sp_dropmergefilter
ms.assetid: 798586d7-05f3-4a5e-bea8-a34b7b52d0fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c4e95865ea3c3b56c4d48036715b05a306f8b0a2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830100"
---
# <a name="sp_dropmergefilter-transact-sql"></a>sp_dropmergefilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 필터를 삭제합니다. 삭제할 병합 필터에 정의 된 모든 병합 필터 열을 삭제 **sp_dropmergefilter** 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergefilter [ @publication= ] 'publication', [ @article= ] 'article'     , [ @filtername= ] 'filtername'  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @filtername = ] 'filtername'`삭제할 필터의 이름입니다. *filtername* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`스냅숏이 무효화 되는 기능을 사용 하거나 사용 하지 않도록 설정 합니다. *force_invalidate_snapshot* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 병합 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되지 않도록 지정 합니다.  
  
 **1** 은 병합 아티클에 대 한 변경으로 인해 스냅숏이 무효화 될 수 있음을 의미 합니다. 해당 하는 경우 값 **1** 은 새 스냅숏이 발생할 수 있는 권한을 부여 합니다.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`구독을 유효 하지 않은 것으로 표시 하는 기능을 사용 하거나 사용 하지 않도록 설정 합니다. *force_reinit_subscription* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 병합 아티클 필터에 대 한 변경으로 인해 구독이 무효화 되지 않도록 지정 합니다.  
  
 **1** 은 병합 아티클 필터에 대 한 변경으로 인해 구독이 무효화 되는 것을 의미 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropmergefilter** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_dropmergefilter**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Transact-sql&#41;sp_addmergefilter &#40;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [Transact-sql&#41;sp_changemergefilter &#40;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergefilter &#40;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
