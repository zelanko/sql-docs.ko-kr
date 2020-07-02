---
title: sp_setreplfailovermode (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setreplfailovermode
- sp_setreplfailovermode_TSQL
helpviewer_keywords:
- sp_setreplfailovermode
ms.assetid: ca98a4c3-bea4-4130-88d7-79e0fd1e85f6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fc6851a9467f0d3f9e3a9becb2f3e3aa6fdb88c3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85645290"
---
# <a name="sp_setreplfailovermode-transact-sql"></a>sp_setreplfailovermode(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  지연 업데이트를 장애 조치(Failover)로 사용하고 즉시 업데이트를 기본 사용하도록 설정된 구독에 대한 장애 조치 실행 모드를 설정할 수 있도록 합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다. 장애 조치 (failover) 모드에 대 한 자세한 내용은 [트랜잭션 복제를 위한 업데이트할](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)수 있는 구독을 참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_setreplfailovermode [ @publisher= ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication= ] 'publication' ]  
    [ , [ @failover_mode= ] 'failover_mode' ]  
    [ , [ @override = ] override ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다. 반드시 게시가 이미 존재해야 합니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @failover_mode = ] 'failover_mode'`구독에 대 한 장애 조치 (failover) 모드입니다. *failover_mode* 은 **nvarchar (10)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**즉시** 또는 **동기화**|구독자에서 수행된 데이터 변경 내용을 즉시 게시자로 대량 복사합니다.|  
|**넣었습니다**|데이터 수정 내용은 큐에 저장 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
> [!NOTE]  
>  MSMQ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing)는 더 이상 사용되지 않으며 지원되지 않습니다.  
  
`[ @override = ] override`내부용 으로만 사용 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 즉시 업데이트에 대 한 장애 조치 (failover)가 포함 된 지연 업데이트 또는 지연 업데이트에 대 한 장애 조치 (failover)를 사용 하는 즉시 업데이트의 경우 구독이 사용 하도록 설정 된 스냅숏 복제 또는 트랜잭션 복제에 사용 됩니다. **sp_setreplfailovermode**  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_setreplfailovermode**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [업데이트 가능한 트랜잭션 구독에 대 한 업데이트 모드 전환](../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
