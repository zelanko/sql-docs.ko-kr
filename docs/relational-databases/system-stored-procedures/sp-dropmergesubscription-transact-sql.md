---
title: sp_dropmergesubscription (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergesubscription_TSQL
- sp_dropmergesubscription
helpviewer_keywords:
- sp_dropmergesubscription
ms.assetid: 34244ae6-bd98-4a6a-bbd3-85f50edfcdc0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8bf38ef67089c65d53bedcb56afd81de3e21a413
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933878"
---
# <a name="sp_dropmergesubscription-transact-sql"></a>sp_dropmergesubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시에 대한 구독 및 연결된 병합 에이전트를 삭제합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergesubscription [ [ @publication= ] 'publication' ]   
    [ , [ @subscriber= ] 'subscriber'    
    [ , [ @subscriber_db= ] 'subscriber_db' ]   
    [ , [ @subscription_type= ] 'subscription_type' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시 이름입니다. *게시* 는 **sysname**이며 기본값은 NULL입니다. 게시는 이미 존재하고 있어야 하며 식별자에 적용되는 규칙을 준수해야 합니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscription_database*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscription_type = ] 'subscription_type'`구독의 유형입니다. *subscription_type*은 **nvarchar (15)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**모두가**|밀어넣기, 끌어오기 및 익명 구독|  
|**익명**|익명 구독입니다.|  
|**누르기**|밀어넣기 구독입니다.|  
|**서브스크립션을**|끌어오기 구독입니다.|  
|**모두** (기본값)|밀어넣기 및 끌어오기 구독 모두입니다.|  
  
`[ @ignore_distributor = ] ignore_distributor`이 저장 프로시저가 배포자에 연결 되지 않고 실행 되는지 여부를 나타냅니다. *ignore_distributor* 은 **bit**이며 기본값은 **0**입니다. 이 매개 변수는 배포자에서 정리 태스크를 수행하지 않고 게시를 삭제하는 데 사용할 수 있습니다. 또한 배포자를 다시 설치해야 하는 경우에도 유용합니다.  
  
`[ @reserved = ] reserved`는 나중에 사용 하도록 예약 되어 있습니다. *reserved* 는 **bit**이며 기본값은 **0**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropmergesubscription** 는 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergesubscription_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_dropmergesubscription**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [밀어넣기 구독 삭제](../../relational-databases/replication/delete-a-push-subscription.md)   
 [끌어오기 구독 삭제](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [Transact-sql&#41;sp_addmergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [Transact-sql&#41;sp_changemergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
