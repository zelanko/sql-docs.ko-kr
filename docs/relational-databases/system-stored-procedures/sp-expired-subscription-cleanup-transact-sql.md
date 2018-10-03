---
title: sp_expired_subscription_cleanup (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_expired_subscription_cleanup
- SP_EXPIRED_SUBSCRIPTION_CLEANUP_TSQL
helpviewer_keywords:
- sp_expired_subscription_cleanup
ms.assetid: 6abc29fe-d77a-4673-9d99-ae31c688012c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6bff1330bcd0b3db77060274529c55c6baf58d05
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733947"
---
# <a name="spexpiredsubscriptioncleanup-transact-sql"></a>sp_expired_subscription_cleanup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 게시의 모든 구독 상태를 확인하고 만료된 구독을 삭제합니다. 모든 데이터베이스의 게시자 또는 배포자의 배포 데이터베이스에 대 한 비-이 저장된 프로시저 실행 됩니다[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>인수  
 [  **@publisher=** ] **'***게시자***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 게시자의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 NULL입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 이 매개 변수를 지정하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_expired_subscription_cleanup** 모든 유형의 복제에 사용 됩니다.  
  
 **sp_expired_subscription_cleanup** 만료 된 구독 정리 작업을 검색 하 고 24 시간 마다 게시 데이터베이스에서 만료 된 구독을 제거 하 여 실행 됩니다. 구독이 최신이 아닌 경우 즉, 보존 기간 동안 게시자와 동기화하지 않은 경우 게시가 만료된 것으로 선언되며 게시자에서 구독의 추적이 정리됩니다. 자세한 내용은 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)을(를) 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_expired_subscription_cleanup**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_mergesubscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
