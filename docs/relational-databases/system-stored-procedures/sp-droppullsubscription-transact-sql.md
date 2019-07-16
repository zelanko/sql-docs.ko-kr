---
title: sp_droppullsubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords:
- sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
author: stevestein
ms.author: sstein
ms.openlocfilehash: 706f76f0b12ad6ce9077a36115bba4634cd94642
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933840"
---
# <a name="spdroppullsubscription-transact-sql"></a>sp_droppullsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  구독자의 현재 데이터베이스에서 구독을 삭제합니다. 이 저장 프로시저는 끌어오기 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 원격 서버 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다. 하는 경우 **모든**, 구독이 전혀 게시자 삭제 됩니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시자 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다. **모든** 은 모든 게시자 데이터베이스를 의미 합니다.  
  
`[ @publication = ] 'publication'` 게시 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다. 하는 경우 **모든**, 모든 게시에 대 한 구독이 삭제 됩니다.  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_droppullsubscription** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_droppullsubscription** 에서 해당 행을 삭제 합니다 [MSreplication_subscriptions &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) 테이블 및 구독자에서 해당 배포자 에이전트입니다. 남아 있는 행이 없는 경우 [MSreplication_subscriptions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md), 테이블을 삭제 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 끌어오기 구독을 만든 사용자를 실행할 수 있습니다 **sp_droppullsubscription**합니다. 합니다 **db_owner** 고정된 데이터베이스 역할은 실행할 수만 **sp_droppullsubscription** 끌어오기 구독을 만든 사용자가이 역할에 속한 경우.  
  
## <a name="see-also"></a>관련 항목  
 [끌어오기 구독 삭제](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
