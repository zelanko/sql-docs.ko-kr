---
title: sp_replqueuemonitor (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replqueuemonitor
- sp_replqueuemonitor_TSQL
helpviewer_keywords:
- sp_replqueuemonitor
ms.assetid: 6909a3f1-43a2-4df5-a6a5-9e6f347ac841
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8eb21085625c7f2f0071c18da80501774088fdc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52789375"
---
# <a name="spreplqueuemonitor-transact-sql"></a>sp_replqueuemonitor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  큐 메시지를 나열 된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지정한 게시에 지연된 업데이트 구독에 대 한 메시지 큐입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐를 사용하는 경우 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다. Message Queuing을 사용하는 경우 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replqueuemonitor [ @publisher = ] 'publisher'  
    [ , [ @publisherdb = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @tranid = ] 'tranid' ]  
    [ , [ @queuetype = ] 'queuetype' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publisher** = ] **'***publisher***'**  
 게시자의 이름입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다. 해당 서버는 반드시 게시용으로 구성되어야 합니다. 모든 게시자에 대해 NULL입니다.  
  
 [ **@publisherdb** =] **'***publisher_db***'** ]  
 게시 데이터베이스의 이름입니다. *publisher_db* 됩니다 **sysname**, 기본값은 NULL입니다. 모든 게시 데이터베이스에 대해 NULL입니다.  
  
 [ **@publication** =] **'***게시***'** ]  
 게시의 이름입니다. *게시*됩니다 **sysname**, 기본값은 NULL입니다. 모든 게시에 대해 NULL입니다.  
  
 [ **@tranid** =] **'***tranid***'** ]  
 트랜잭션 ID입니다. *tranid*됩니다 **sysname**, 기본값은 NULL입니다. 모든 트랜잭션에 대해 NULL입니다.  
  
 [**@queuetype=** ] **'***queuetype***'** ]  
 트랜잭션을 저장하는 큐의 유형입니다. *queuetype* 됩니다 **tinyint** 이며 기본값은 **0**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|모든 유형의 큐입니다.|  
|**1**|메시지 큐|  
|**2**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_replqueuemonitor** 지연된 업데이트 구독이 있는 트랜잭션 복제 또는 스냅숏 복제에 사용 됩니다. SQL 명령을 포함하지 않거나 영향을 미치는 SQL 명령의 일부인 큐 메시지는 표시되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_replqueuemonitor**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
