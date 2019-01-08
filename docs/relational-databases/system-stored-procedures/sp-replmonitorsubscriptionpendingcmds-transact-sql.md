---
title: sp_replmonitorsubscriptionpendingcmds (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 175718b9d53556c5b24e65cb31e117fdf9a27418
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794885"
---
# <a name="spreplmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  트랜잭션 게시의 구독에 대해 보류 중인 명령의 수와 이러한 명령을 처리하는 데 걸리는 대략적인 예상 시간에 대한 정보를 반환합니다. 이 저장 프로시저는 반환된 각 구독에 대해 한 행을 반환합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replmonitorsubscriptionpendingcmds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @subscription_type = ] subscription_type  
```  
  
## <a name="arguments"></a>인수  
 [ **@publisher** = ] **'***publisher***'**  
 게시자의 이름입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 게시된 데이터베이스의 이름입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@publication** =] **'***게시***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@subscriber** =] **'***구독자***'**  
 구독자의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@subscriber_db** = ] **'***subscriber_db***'**  
 구독 데이터베이스의 이름입니다. *subscriber_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@subscription_type** =] *subscription_type*  
 구독 유형입니다. *publication_type* 됩니다 **int**이며 기본값은 없습니다 수 있습니다 이러한 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|밀어넣기 구독|  
|**1**|끌어오기 구독|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pendingcmdcount**|**int**|구독에 대해 보류 중인 명령 수입니다.|  
|**estimatedprocesstime**|**int**|구독자에 보류 중인 명령을 모두 배달하는 데 필요할 것으로 예상되는 시간(초)입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_replmonitorsubscriptionpendingcmds** 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버만 합니다 **sysadmin** 고정된 서버 역할의 멤버나 배포자 합니다 **db_owner** 고정된 데이터베이스 역할의 배포 데이터베이스에서 실행할 수 있습니다 **sp_ replmonitorsubscriptionpendingcmds**합니다. 배포 데이터베이스를 사용 하는 게시를 실행할 수에 대 한 게시 액세스의 구성원 나열 **sp_replmonitorsubscriptionpendingcmds** 보류 중인 명령 게시에 대해 반환할 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
