---
title: sp_dropmergesubscription (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 34ba40387c246fe5f7f2de8dd74197b7cd43c0f5
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130743"
---
# <a name="spdropmergesubscription-transact-sql"></a>sp_dropmergesubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시에 대한 구독 및 연결된 병합 에이전트를 삭제합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=** ] **'**_게시_**'**  
 게시 이름입니다. *게시* 됩니다 **sysname**, 기본값은 NULL입니다. 게시는 이미 존재하고 있어야 하며 식별자에 적용되는 규칙을 준수해야 합니다.  
  
 [  **@subscriber=**] **'**_구독자_**'**  
 구독자의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscriber_db=** ] **'**_subscriber_db_**'**  
 구독 데이터베이스의 이름입니다. *subscription_database*됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscription_type=** ] **'**_subscription_type_**'**  
 구독 유형입니다. *subscription_type*됩니다 **nvarchar(15)**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**모든**|밀어넣기, 끌어오기 및 익명 구독|  
|**익명**|익명 구독입니다.|  
|**푸시**|밀어넣기 구독입니다.|  
|**끌어오기**|끌어오기 구독입니다.|  
|**둘 다** (기본값)|밀어넣기 및 끌어오기 구독 모두입니다.|  
  
 [  **@ignore_distributor =** ] *ignore_distributor*  
 이 저장 프로시저가 배포자에 연결되지 않고 실행되는지 여부를 표시합니다. *ignore_distributor* 됩니다 **비트**, 기본값은 **0**합니다. 이 매개 변수는 배포자에서 정리 태스크를 수행하지 않고 게시를 삭제하는 데 사용할 수 있습니다. 또한 배포자를 다시 설치해야 하는 경우에도 유용합니다.  
  
 [  **@reserved=** ] *예약*  
 나중에 사용하도록 예약되었습니다. *예약* 됩니다 **비트**, 기본값은 **0**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropmergesubscription** 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergesubscription_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_dropmergesubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [밀어넣기 구독 삭제](../../relational-databases/replication/delete-a-push-subscription.md)   
 [끌어오기 구독 삭제](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
