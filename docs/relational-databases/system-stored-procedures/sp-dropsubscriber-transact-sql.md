---
title: sp_dropsubscriber (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropsubscriber_TSQL
- sp_dropsubscriber
helpviewer_keywords:
- sp_dropsubscriber
ms.assetid: 8c6eb282-81b5-4ec4-b691-aa061d9267dc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9bef68803beedbfdb0d6034b2a92665f033d9641
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768294"
---
# <a name="spdropsubscriber-transact-sql"></a>sp_dropsubscriber(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  등록된 서버에서 구독자 지정을 제거합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  이 저장 프로시저는 더 이상 사용되지 않습니다. 더 이상 게시자에서 구독자를 명시적으로 등록할 필요가 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropsubscriber [ @subscriber= ] 'subscriber'   
    [ , [ @reserved= ] 'reserved' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>인수  
`[ @subscriber = ] 'subscriber'`삭제할 구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropsubscriber** 은 모든 유형의 복제에 사용 됩니다.  
  
 이 저장 프로시저는 서버 **하위** 옵션을 제거 하 고 **repl_subscriber**에 대 한 시스템 관리자의 원격 로그인 매핑을 제거 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_dropsubscriber**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [밀어넣기 구독 삭제](../../relational-databases/replication/delete-a-push-subscription.md)   
 [끌어오기 구독 삭제](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addsubscriber &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_helpdistributor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
