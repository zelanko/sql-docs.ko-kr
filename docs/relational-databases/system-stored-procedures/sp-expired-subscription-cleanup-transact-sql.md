---
title: sp_expired_subscription_cleanup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_expired_subscription_cleanup
- SP_EXPIRED_SUBSCRIPTION_CLEANUP_TSQL
helpviewer_keywords:
- sp_expired_subscription_cleanup
ms.assetid: 6abc29fe-d77a-4673-9d99-ae31c688012c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f739a51e57337628c666ac8e5ccee253785a1df6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820511"
---
# <a name="sp_expired_subscription_cleanup-transact-sql"></a>sp_expired_subscription_cleanup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 게시의 모든 구독 상태를 확인하고 만료된 구독을 삭제합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 또는 이외 게시자에 대 한 배포 데이터베이스의 배포자에서 실행 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`이외 게시자의 이름입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *게시* 는 **sysname**이며 기본값은 NULL입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 이 매개 변수를 지정하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_expired_subscription_cleanup** 은 모든 유형의 복제에 사용 됩니다.  
  
 만료 된 구독 정리 작업에 의해 실행 되는 **sp_expired_subscription_cleanup** 는 24 시간 마다 게시 데이터베이스에서 만료 된 구독을 검색 하 고 제거 합니다. 구독이 최신이 아닌 경우 즉, 보존 기간 동안 게시자와 동기화하지 않은 경우 게시가 만료된 것으로 선언되며 게시자에서 구독의 추적이 정리됩니다. 자세한 내용은 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)을(를) 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_expired_subscription_cleanup**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_mergesubscription_cleanup &#40;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [Transact-sql&#41;sp_subscription_cleanup &#40;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
