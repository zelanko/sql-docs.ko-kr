---
title: sp_replmonitorsubscriptionpendingcmds (T-sql)
description: 트랜잭션 게시에 대 한 구독에서 보류 중인 명령 수에 대 한 정보를 반환 하는 sp_replmonitorsubscriptionpendingcmds 저장 프로시저에 대해 설명 합니다.
ms.custom: seo-lt-2019
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f8f07a38d612375030f43e2faf2194d4bc65bca8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786128"
---
# <a name="sp_replmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  트랜잭션 게시의 구독에 대해 보류 중인 명령의 수와 이러한 명령을 처리하는 데 걸리는 대략적인 예상 시간에 대한 정보를 반환합니다. 이 저장 프로시저는 반환된 각 구독에 대해 한 행을 반환합니다. 복제 모니터링에 사용되는 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 된 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscription_type = ] subscription_type`구독의 유형입니다. *publication_type* 은 **int**이며 기본값은 없고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
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
  
## <a name="remarks"></a>설명  
 **sp_replmonitorsubscriptionpendingcmds** 은 트랜잭션 복제와 함께 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버 또는 배포 데이터베이스에 있는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_replmonitorsubscriptionpendingcmds**을 실행할 수 있습니다. 배포 데이터베이스를 사용 하는 게시에 대 한 게시 액세스 목록의 멤버는 **sp_replmonitorsubscriptionpendingcmds** 를 실행 하 여 해당 게시에 대 한 보류 중인 명령을 반환할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
