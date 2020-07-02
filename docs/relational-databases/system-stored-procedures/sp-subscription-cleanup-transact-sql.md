---
title: sp_subscription_cleanup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_subscription_cleanup_TSQL
- sp_subscription_cleanup
helpviewer_keywords:
- sp_subscription_cleanup
ms.assetid: bdc8aaa0-ff2d-40c2-84b2-4ba513ced279
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1b16ddb35ed3d8ec64eb783e904f3c9b6120cfbd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725633"
---
# <a name="sp_subscription_cleanup-transact-sql"></a>sp_subscription_cleanup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  구독자에서 구독이 삭제될 때 메타데이터를 삭제합니다. 동기화 트랜잭션 구독의 경우 즉시 업데이트 트리거도 포함됩니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_subscription_cleanup [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
    [ , [ @publication = ] 'publication']  
    [ , [ @reserved = ] 'reserved']  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 NULL입니다. NULL인 경우 게시 데이터베이스에서 공유 에이전트 게시를 사용하는 구독이 삭제됩니다.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_subscription_cleanup** 는 트랜잭션 및 스냅숏 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_subscription_cleanup**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_expired_subscription_cleanup &#40;](../../relational-databases/system-stored-procedures/sp-expired-subscription-cleanup-transact-sql.md)   
 [Transact-sql&#41;sp_mergesubscription_cleanup &#40;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
