---
title: sp_resyncmergesubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resyncmergesubscription_TSQL
- sp_resyncmergesubscription
helpviewer_keywords:
- sp_resyncmergesubscription
ms.assetid: e04d464a-60ab-4b39-a710-c066025708e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: e77488a379543dd6f2749a07048fa67a92d530ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041035"
---
# <a name="spresyncmergesubscription-transact-sql"></a>sp_resyncmergesubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 구독을 사용자가 지정한 알려진 유효성 검사 상태로 다시 동기화합니다. 이를 통해 마지막으로 유효성 검사에 성공한 시간 또는 지정한 날짜 등의 특정 시점으로 구독 데이터베이스를 강제 수렴 또는 동기화할 수 있습니다. 이 방법으로 구독을 다시 동기화할 경우 스냅샷이 다시 적용되지 않습니다. 이 저장 프로시저는 스냅샷 복제 구독이나 트랜잭션 복제 구독에는 사용되지 않습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 또는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_resyncmergesubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @resync_type = ] resync_type ]  
    [ , [ @resync_date_str = ] resync_date_string ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다. NULL 값은 저장 프로시저가 게시자에서 실행될 경우 유효합니다. 저장 프로시저를 구독자에서 실행할 경우 게시자를 지정해야 합니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 NULL입니다. NULL 값은 저장 프로시저가 게시 데이터베이스의 게시자에서 실행될 경우 유효합니다. 저장 프로시저를 구독자에서 실행할 경우 게시자를 지정해야 합니다.  
  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시*됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'` 구독자의 이름이입니다. *구독자* 됩니다 **sysname**, 기본값은 NULL입니다. NULL 값은 저장 프로시저가 구독자에서 실행될 경우 유효합니다. 저장 프로시저를 게시자에서 실행할 경우 구독자를 지정해야 합니다.  
  
`[ @subscriber_db = ] 'subscriber_db'` 구독 데이터베이스의 이름이입니다. *subscription_db* 됩니다 **sysname**, 기본값은 NULL입니다. NULL 값은 저장 프로시저가 구독 데이터베이스의 구독자에서 실행될 경우 유효합니다. 저장 프로시저를 게시자에서 실행할 경우 구독자를 지정해야 합니다.  
  
`[ @resync_type = ] resync_type` 다시 동기화가 시작 시기를 정의 합니다. *resync_type* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|초기 스냅샷 후부터 동기화가 시작됩니다. 초기 스냅샷 이후의 모든 변경 내용이 구독자에 다시 적용되므로 가장 리소스 집약적인 옵션입니다.|  
|**1**|마지막으로 성공한 유효성 검사 이후부터 동기화가 시작됩니다. 마지막으로 성공한 유효성 검사 이후에 시작된 모든 새로운 또는 완료되지 않은 생성은 구독자에 다시 적용됩니다.|  
|**2**|지정한 날짜부터 동기화가 시작 됩니다 *resync_date_str*합니다. 이 날짜 이후에 시작된 모든 새로운 또는 완료되지 않은 생성은 구독자에 다시 적용됩니다.|  
  
`[ @resync_date_str = ] resync_date_string` 에 다시 동기화가 시작 하는 경우 날짜를 정의 합니다. *resync_date_string* 됩니다 **nvarchar(30)** , 기본값은 NULL입니다. 이 매개 변수는 때를 *resync_type* 의 값인 **2**합니다. 지정한 날짜 표현으로 변환할 **날짜/시간** 값입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_resyncmergesubscription** 병합 복제에 사용 됩니다.  
  
 값이 **0** 에 대 한 합니다 *resync_type* 초기 스냅숏 이후의 모든 변경 내용을 다시 적용을 하는 매개 변수 수 있지만 훨씬 덜 전체 다시 초기화 보다 리소스를 많이 사용 합니다. 예를 들어 초기 스냅샷이 한 달 전에 전달되었다면 이 값은 지난 달부터의 데이터를 다시 적용합니다. 초기 스냅샷이 1GB의 데이터를 가지고 있으나 지난 달부터의 변경 사항의 양은 2MB의 변경된 데이터를 가진다면 그 데이터를 다시 적용하는 것이 전체 1GB의 스냅샷을 다시 적용하는 것보다 효율적입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_resyncmergesubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
