---
title: sp_setreplfailovermode (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_setreplfailovermode
- sp_setreplfailovermode_TSQL
helpviewer_keywords:
- sp_setreplfailovermode
ms.assetid: ca98a4c3-bea4-4130-88d7-79e0fd1e85f6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 68851fb6ad9a242536cc81c6688b7caed1067a2c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spsetreplfailovermode-transact-sql"></a>sp_setreplfailovermode(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지연 업데이트를 장애 조치(Failover)로 사용하고 즉시 업데이트를 기본 사용하도록 설정된 구독에 대한 장애 조치 실행 모드를 설정할 수 있도록 합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다. 장애 조치 모드에 대 한 자세한 내용은 참조 [업데이트할 수 있는 Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)합니다.  
  
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
 [  **@publisher=**] **'***게시자***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다. 반드시 게시가 이미 존재해야 합니다.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 게시 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publication=**] **'***게시***'**  
 게시의 이름입니다. *게시*은 **sysname**, 기본값은 없습니다.  
  
 [**@failover_mode=**] **'***failover_mode***'**  
 구독의 장애 조치(failover) 모드입니다. *failover_mode* 은 **nvarchar (10)** 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**즉시** 또는 **동기화**|구독자에서 수행된 데이터 변경 내용을 즉시 게시자로 대량 복사합니다.|  
|**큐에 대기**|데이터 수정에 저장 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐입니다.|  
  
> [!NOTE]  
>  MSMQ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing)는 더 이상 사용되지 않으며 지원되지 않습니다.  
  
 [  **@override** =] *재정의*  
 내부적으로만 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_setreplfailovermode** 하는 데 스냅숏 복제 또는 트랜잭션 복제에서 즉시 업데이트를 장애 조치 또는 구독을 사용 하거나 지연 장애 조치를 즉시 업데이트와 업데이트에 대 한 큐에 대기 업데이트 중입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_setreplfailovermode**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [업데이트 가능한 트랜잭션 구독에 대 한 업데이트 모드 전환](../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
