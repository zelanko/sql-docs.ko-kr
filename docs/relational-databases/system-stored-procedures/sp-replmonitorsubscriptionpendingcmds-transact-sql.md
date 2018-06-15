---
title: sp_replmonitorsubscriptionpendingcmds (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c94d01031094e03ddde2fc9bcdf234729ecd11c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33001049"
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
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 게시된 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publication** =] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@subscriber** =] **'***구독자***'**  
 구독자의 이름입니다. *구독자* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@subscriber_db** = ] **'***subscriber_db***'**  
 구독 데이터베이스의 이름입니다. *subscriber_db* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@subscription_type** =] *subscription_type*  
 구독 유형입니다. *publication_type* 은 **int**, 기본값은 없으며 수 있습니다 이러한 값 중 하나 여야 합니다.  
  
|Value|설명|  
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
  
## <a name="remarks"></a>주의  
 **sp_replmonitorsubscriptionpendingcmds** 트랜잭션 복제와 함께 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할의 멤버나 배포자는 **db_owner** 고정된 데이터베이스 역할이 배포 데이터베이스에서 실행할 수 있는 **sp_ replmonitorsubscriptionpendingcmds**합니다. 한 게시 액세스 목록의 멤버 실행할 수 있는 배포 데이터베이스를 사용 하는 게시에 대 한 **sp_replmonitorsubscriptionpendingcmds** 보류 중인 해당 게시에 대 한 명령 돌아갑니다.  
  
## <a name="see-also"></a>관련 항목:  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
