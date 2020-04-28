---
title: sp_addpullsubscription (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpullsubscription
- sp_addpullsubscription_TSQL
helpviewer_keywords:
- sp_addpullsubscription
ms.assetid: 0f4bbedc-0c1c-414a-b82a-6fd47f0a6a7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7f65d868f7560f1e413b8c28308afac495233102
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68769077"
---
# <a name="sp_addpullsubscription-transact-sql"></a>sp_addpullsubscription(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  스냅샷 또는 트랜잭션 게시에 끌어오기 구독을 추가합니다. 이 저장 프로시저는 끌어오기 구독을 만들 구독자의 데이터베이스에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addpullsubscription [ @publisher= ] 'publisher'  
    [ , [ @publisher_db= ] 'publisher_db' ]  
        , [ @publication= ] 'publication'  
    [ , [ @independent_agent= ] 'independent_agent' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @update_mode= ] 'update_mode' ]  
    [ , [ @immediate_sync = ] immediate_sync ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 NULL입니다. Oracle 게시자는 *publisher_db* 무시 됩니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @independent_agent = ] 'independent_agent'`이 게시에 대 한 독립 실행형 배포 에이전트 있는지 여부를 지정 합니다. *independent_agent* 은 **nvarchar (5)** 이며 기본값은 TRUE입니다. **True**이면이 게시에 대 한 독립 실행형 배포 에이전트 있습니다. **False**이면 각 게시자 데이터베이스/구독자 데이터베이스 쌍에 대해 하나의 배포 에이전트 있습니다. *independent_agent* 는 게시의 속성 이며 게시자와 같은 값을 가져야 합니다.  
  
`[ @subscription_type = ] 'subscription_type'`구독의 유형입니다. *subscription_type* 은 **nvarchar (9)** 이며 기본값은 **anonymous**입니다. 게시자에서 구독을 등록 하지 않고 구독을 만들려는 경우를 제외 하 고는 *subscription_type*에 대 한 **pull** 값을 지정 해야 합니다. 이 경우에는 **익명**값을 지정 해야 합니다. 구독 구성 중에 게시자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 설정할 수 없는 경우 이 작업을 수행해야 합니다.  
  
`[ @description = ] 'description'`게시에 대 한 설명입니다. *description* 은 **nvarchar (100)** 이며 기본값은 NULL입니다.  
  
`[ @update_mode = ] 'update_mode'`업데이트의 유형입니다. *update_mode* 은 **nvarchar (30)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**읽기 전용** (기본값)|구독이 읽기 전용입니다. 구독자에서의 변경 내용이 게시자로 다시 전달되지 않습니다. 구독자에서 업데이트가 수행되지 않을 때 사용해야 합니다.|  
|**synctran**|즉시 업데이트 구독에 대한 지원을 설정합니다.|  
|**queued tran**|지연 업데이트 구독을 설정합니다. 구독자에서 데이터를 수정하고 큐에 저장한 후 게시자에 전파할 수 있습니다.|  
|**조치가**|즉시 업데이트를 기본으로 사용하고 장애 조치(Failover)로 지연 업데이트를 사용합니다. 구독자에서 데이터를 수정하고 게시자에 즉시 전파할 수 있습니다. 게시자와 구독자가 연결되지 않은 경우 구독자에서의 데이터 수정 내용은 구독자와 게시자가 다시 연결될 때까지 큐에 저장됩니다.|  
|**queued failover**|구독을 지연 업데이트 구독으로 설정하며 즉시 업데이트 모드로 변경할 수 있는 기능을 포함합니다. 구독자에서 데이터를 수정한 후 구독자와 게시자가 연결될 때까지 수정 내용을 큐에 저장할 수 있습니다. 지속적 연결이 설정되는 경우 업데이트 모드를 즉시 업데이트로 변경할 수 있습니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.|  
  
`[ @immediate_sync = ] immediate_sync`스냅숏 에이전트 실행 될 때마다 동기화 파일을 만들지 아니면 다시 만들지를 나타냅니다. *immediate_sync* 은 **bit** 이며 기본값은 1 이며 **sp_addpublication**의 *immediate_sync* 와 동일한 값으로 설정 해야 합니다. *immediate_sync* 는 게시의 속성 이며 게시자와 같은 값을 가져야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addpullsubscription** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
> [!IMPORTANT]  
>  지연 업데이트 구독의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 구독자에 연결하고 각 구독자로의 연결에는 다른 계정을 지정합니다. 지연 업데이트를 지원하는 끌어오기 구독을 만드는 경우 복제는 항상 Windows 인증을 사용하도록 연결을 설정합니다. 끌어오기 구독에서 복제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 데 필요한 메타데이터를 구독자에서 액세스할 수 없습니다. 이 경우 구독을 구성한 후에 [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) 인증을 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하도록 연결을 변경 하려면 sp_changesubscription를 실행 해야 합니다.  
  
 [MSreplication_subscriptions &#40;transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) 테이블이 구독자에 없는 경우 **sp_addpullsubscription** 만듭니다. 또한 [MSreplication_subscriptions &#40;transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) 테이블에 행을 추가 합니다. 끌어오기 구독의 경우 [sp_addsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 먼저 게시자에서 호출 해야 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-t_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addpullsubscription**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [게시를 구독](../../relational-databases/replication/subscribe-to-publications.md) 하 [는 트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Transact-sql&#41;sp_addpullsubscription_agent &#40;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [Transact-sql&#41;sp_change_subscription_properties &#40;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [Transact-sql&#41;sp_droppullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helppullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helpsubscription_properties &#40;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
