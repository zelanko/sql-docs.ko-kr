---
description: sp_addmergepullsubscription(Transact-SQL)
title: sp_addmergepullsubscription (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 13e89d2dfe90789071821f7ad6714361f1954a8d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89529707"
---
# <a name="sp_addmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  병합 게시에 끌어오기 구독을 추가합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergepullsubscription [ @publication= ] 'publication'   
    [ , [ @publisher= ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @subscriber_type= ] 'subscriber_type' ]   
    [ , [ @subscription_priority= ] subscription_priority ]   
    [ , [ @sync_type= ] 'sync_type' ]   
    [ , [ @description= ] 'description' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher = ] 'publisher'` 게시자의 이름입니다. *Publisher* 는 **sysname**이며 기본값은 로컬 서버 이름입니다. 게시자는 유효한 서버여야 합니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_type = ] 'subscriber_type'` 구독자의 유형입니다. *subscriber_type* 은 **nvarchar (15)** 이며 **전역**, **로컬** 또는 **익명**일 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 로컬 구독은 클라이언트 구독이라고 하며 전역 구독은 서버 구독이라고 합니다.  
  
`[ @subscription_priority = ] subscription_priority` 구독 우선 순위입니다. *subscription_priority*은 **실제**이며 기본값은 NULL입니다. 로컬 및 익명 구독의 경우 우선 순위는 **0.0**입니다. 우선 순위는 기본 해결 프로그램이 충돌을 감지했을 때 먼저 적용할 항목을 선택하는 데 사용합니다. 전역 구독자인 경우 구독 우선 순위는 100 미만이어야 합니다. 100은 게시자의 우선 순위입니다.  
  
`[ @sync_type = ] 'sync_type'` 구독 동기화 유형입니다. *sync_type*은 **nvarchar (15)** 이며 기본값은 **automatic**입니다. **자동** 또는 **없음**일 수 있습니다. **Automatic**인 경우 게시 된 테이블의 스키마 및 초기 데이터가 먼저 구독자로 전송 됩니다. 없으면 **구독자**에 게시 된 테이블에 대 한 스키마 및 초기 데이터가 이미 있다고 가정 합니다. 시스템 테이블 및 데이터는 항상 전송됩니다.  
  
> [!NOTE]  
>  **None**값을 지정 하지 않는 것이 좋습니다.  
  
`[ @description = ] 'description'` 이 끌어오기 구독에 대 한 간단한 설명입니다. *description*은 **nvarchar (255)** 이며 기본값은 NULL입니다. 이 값은 모니터링 되는 게시에 대 한 구독을 정렬 하는 데 사용할 수 있는 **이름** 열의 복제 모니터에 의해 표시 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergepullsubscription** 는 병합 복제에 사용 됩니다.  
  
 에이전트를 사용 하 여 구독을 동기화 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시와 동기화 할 에이전트 및 작업을 만들려면 구독자에서 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) 저장 프로시저를 실행 해야 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addmergepullsubscription**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Transact-sql&#41;sp_addmergepullsubscription_agent &#40;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [Transact-sql&#41;sp_changemergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
