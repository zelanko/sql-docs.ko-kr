---
title: sp_addmergepullsubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 247d32980a54656c0baa7e2869d6218a2e85946a
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032180"
---
# <a name="spaddmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시에 끌어오기 구독을 추가합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher=**] **'***publisher***'**  
 게시자의 이름입니다. *게시자* 됩니다 **sysname**, 로컬 서버 이름의 기본값입니다. 게시자는 유효한 서버여야 합니다.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 게시자 데이터베이스의 이름입니다. *publisher_db* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscriber_type=**] **'***subscriber_type***'**  
 구독자의 유형입니다. *subscriber_type* 됩니다 **nvarchar(15)**, 수 및 **전역**를 **로컬** 또는 **익명**합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 로컬 구독은 클라이언트 구독이라고 하며 전역 구독은 서버 구독이라고 합니다.  
  
 [  **@subscription_priority=**] *subscription_priority*  
 구독 우선 순위입니다. *subscription_priority*됩니다 **실제**, 기본값은 NULL입니다. 우선 순위는 로컬 및 익명 구독의 **0.0**합니다. 우선 순위는 기본 해결 프로그램이 충돌을 감지했을 때 먼저 적용할 항목을 선택하는 데 사용합니다. 전역 구독자인 경우 구독 우선 순위는 100 미만이어야 합니다. 100은 게시자의 우선 순위입니다.  
  
 [  **@sync_type=**] **'***sync_type***'**  
 구독 동기화 유형입니다. *sync_type*됩니다 **nvarchar(15)**, 기본값은 **자동**합니다. 일 수 있습니다 **자동** 하거나 **none**합니다. 하는 경우 **자동**, 스키마 및 게시 된 테이블의 초기 데이터가 먼저 구독자에 전송 됩니다. 하는 경우 **none**를 구독자에 이미 게시 된 테이블에 대 한 초기 데이터 및 스키마를 가정 합니다. 시스템 테이블 및 데이터는 항상 전송됩니다.  
  
> [!NOTE]  
>  값을 지정 하지 않는 것이 좋습니다 **none**합니다.  
  
 [  **@description=**] **'***설명***'**  
 해당 끌어오기 구독에 대한 간단한 설명입니다. *설명*됩니다 **nvarchar(255)**, 기본값은 NULL입니다. 이 값의 복제 모니터에 의해 표시 됩니다는 **이름을** 모니터링 되는 게시에 대 한 구독을 정렬 하는 열입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergepullsubscription** 병합 복제에 사용 됩니다.  
  
 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독을 동기화 하는 에이전트는 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) 에이전트 및 게시와 동기화 하는 작업을 만들려면 구독자의 저장된 프로시저를 실행 해야 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_addmergepullsubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
