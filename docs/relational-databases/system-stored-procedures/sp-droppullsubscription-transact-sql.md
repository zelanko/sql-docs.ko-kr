---
title: sp_droppullsubscription (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 12215e39e90586bf8346c96cde3f0f3f5f386e6a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783801"
---
# <a name="sp_droppullsubscription-transact-sql"></a>sp_droppullsubscription(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  구독자의 현재 데이터베이스에서 구독을 삭제합니다. 이 저장 프로시저는 끌어오기 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`원격 서버 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다. **All**인 경우 모든 게시자에서 구독이 삭제 됩니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다. **all** 은 모든 게시자 데이터베이스를 의미 합니다.  
  
`[ @publication = ] 'publication'`게시 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다. **All**인 경우 모든 게시에 대 한 구독이 삭제 됩니다.  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_droppullsubscription** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_droppullsubscription** [MSreplication_subscriptions &#40;Transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) 테이블과 구독자의 해당 배포자 에이전트에서 해당 행을 삭제 합니다. [Transact-sql&#41;MSreplication_subscriptions &#40;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)행이 남아 있지 않으면 해당 테이블을 삭제 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버 또는 끌어오기 구독을 만든 사용자만 **sp_droppullsubscription**을 실행할 수 있습니다. **Db_owner** 고정 데이터베이스 역할은 끌어오기 구독을 만든 사용자가이 역할에 속하는 경우에만 **sp_droppullsubscription** 을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [끌어오기 구독 삭제](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [Transact-sql&#41;sp_addpullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_change_subscription_properties &#40;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [Transact-sql&#41;sp_helppullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_dropsubscription &#40;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
