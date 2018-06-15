---
title: sp_dropmergefilter (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_dropmergefilter_TSQL
- sp_dropmergefilter
helpviewer_keywords:
- sp_dropmergefilter
ms.assetid: 798586d7-05f3-4a5e-bea8-a34b7b52d0fd
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e44ef9e0fe6dec28143a1d017da37732491d4441
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32990068"
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
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@article=**] **'***문서***'**  
 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@filtername=**] **'***filtername***'**  
 삭제할 필터의 이름입니다. *filtername* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 스냅숏 무효화 기능을 설정하거나 해제합니다. *force_invalidate_snapshot* 는 **비트**, 기본값 **0**합니다.  
  
 **0** 병합 아티클의 변경이 스냅숏을 무효화 인해 되지 않도록 지정 합니다.  
  
 **1** 병합 아티클에 대 한 변경을 의미 올바르지 않게 스냅숏을 무효화 합니다. 해당 되는 값의 경우 **1** 새 스냅숏 발생에 대 한 사용 권한을 부여 합니다.  
  
 [ **@force_reinit_subscription**=] *force_reinit_subscription*  
 구독을 무효로 표시하는 기능을 설정하거나 해제합니다. *force_reinit_subscription* 는 **비트**, 기본값 **0**합니다.  
  
 **0** 변경 내용을 병합 아티클 필터에 잘못 된 것에 대 한 구독 인해 되지 않도록 지정 합니다.  
  
 **1** 병합 아티클 필터를 변경 하는 수단으로 인해 구독이 유효 하지 않은 것입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_dropmergefilter** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_dropmergefilter**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
