---
title: sp_dropmergefilter (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7de6c03b133746156f414687fd661f70b40e842e
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54128120"
---
# <a name="spdropmergefilter-transact-sql"></a>sp_dropmergefilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 필터를 삭제합니다. **sp_dropmergefilter** 삭제 될 병합 필터에서 정의 된 모든 병합 필터 열을 삭제 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergefilter [ @publication= ] 'publication', [ @article= ] 'article'     , [ @filtername= ] 'filtername'  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=**] **'**_게시_**'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@article=**] **'**_문서_**'**  
 아티클의 이름입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@filtername=**] **'**_filtername_**'**  
 삭제할 필터의 이름입니다. *filtername* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 스냅숏 무효화 기능을 설정하거나 해제합니다. *force_invalidate_snapshot* 되는 **비트**, 기본값 **0**합니다.  
  
 **0** 병합 아티클에 대 한 변경 인해 스냅숏이 무효화 되지 않도록 지정 합니다.  
  
 **1** 병합 아티클을 변경 하는 수단을 유효 하지 않게 스냅숏을 무효화 합니다. 하는 경우, 값이 **1** 새 스냅숏 발생에 대 한 사용 권한을 부여 합니다.  
  
 [ **@force_reinit_subscription**=] *force_reinit_subscription*  
 구독을 무효로 표시하는 기능을 설정하거나 해제합니다. *force_reinit_subscription* 되는 **비트**, 기본값 **0**합니다.  
  
 **0** 병합 아티클 필터 변경 내용을 잘못 된 것에 대 한 구독으로 인해 되지 않도록 지정 합니다.  
  
 **1** 병합 아티클 필터를 변경 하는 방법으로 인해 구독이 무효화 되도록 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropmergefilter** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_dropmergefilter**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
