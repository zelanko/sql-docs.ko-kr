---
title: sp_setreplfailovermode (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_setreplfailovermode
- sp_setreplfailovermode_TSQL
helpviewer_keywords:
- sp_setreplfailovermode
ms.assetid: ca98a4c3-bea4-4130-88d7-79e0fd1e85f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 97254571aaa19acb71928424a20ec9ffb741ee02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772941"
---
# <a name="spsetreplfailovermode-transact-sql"></a>sp_setreplfailovermode(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지연 업데이트를 장애 조치(Failover)로 사용하고 즉시 업데이트를 기본 사용하도록 설정된 구독에 대한 장애 조치 실행 모드를 설정할 수 있도록 합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다. 장애 조치 모드에 대 한 자세한 내용은 참조 하세요. [업데이트할 수 있는 Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_setreplfailovermode [ @publisher= ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication= ] 'publication' ]  
    [ , [ @failover_mode= ] 'failover_mode' ]  
    [ , [ @override = ] override ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publisher=**] **'***publisher***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다. 반드시 게시가 이미 존재해야 합니다.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 게시 데이터베이스의 이름입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시*됩니다 **sysname**, 기본값은 없습니다.  
  
 [**@failover_mode=**] **'***failover_mode***'**  
 구독의 장애 조치(failover) 모드입니다. *failover_mode* 됩니다 **nvarchar(10)** 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**즉시** 또는 **동기화**|구독자에서 수행된 데이터 변경 내용을 즉시 게시자로 대량 복사합니다.|  
|**큐에 대기**|데이터 수정에 저장 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐입니다.|  
  
> [!NOTE]  
>  MSMQ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing)는 더 이상 사용되지 않으며 지원되지 않습니다.  
  
 [ **@override**=] *재정의*  
 내부적으로만 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_setreplfailovermode** 사용할지 트랜잭션 복제 또는 스냅숏 복제에는 구독을 사용 하거나 즉시 업데이트로 장애 조치를 사용 하 여 업데이트를 지연 하는 것에 대 한 장애 조치를 사용 하 여 즉시 업데이트를 큐에 대기 업데이트 중입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_setreplfailovermode**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Switch Between Update Modes for an Updatable Transactional Subscription](../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
