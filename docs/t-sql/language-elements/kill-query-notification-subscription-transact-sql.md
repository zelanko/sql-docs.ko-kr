---
title: KILL QUERY NOTIFICATION SUBSCRIPTION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION
- KILL_QUERY_NOTIFICATION_SUBSCRIPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION statement
- removing subscriptions
- subscriptions [SQL Server query notifications], stopping
- query notifications [SQL Server], subscriptions
ms.assetid: 8aeadf51-286c-4748-bef2-d25858b250bf
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2cb16e1a8abe807149caed9e5b520cae0d8f44c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982215"
---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  인스턴스에서 쿼리 알림 구독을 제거합니다. 이 문을 사용하면 특정 구독이나 모든 구독을 제거할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
## <a name="arguments"></a>인수  
 ALL  
 인스턴스에서 모든 구독을 제거합니다.  
  
 *subscription_id*  
 구독 ID가 *subscription_id*인 구독을 제거합니다.  
  
## <a name="remarks"></a>Remarks  
 KILL QUERY NOTIFICATION SUBSCRIPTION 문은 알림 메시지를 표시하지 않고 쿼리 알림 구독을 제거합니다.  
  
 *subscription_id*는 [sys.dm_qn_subscriptions&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md) 동적 관리 뷰에 표시되는 구독 ID입니다.  
  
 지정된 구독 ID가 존재하지 않으면 문에서 오류가 발생합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 명령문을 실행할 수 있는 권한은 **sysadmin** 고정 서버 역할의 멤버에게만 부여됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-removing-all-query-notification-subscriptions-in-the-instance"></a>1\. 인스턴스에서 모든 쿼리 알림 구독 제거  
 다음 예에서는 인스턴스에서 모든 쿼리 알림 구독을 제거합니다.  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION ALL ;  
```  
  
### <a name="b-removing-a-single-query-notification-subscription"></a>2\. 단일 쿼리 알림 구독 제거  
 다음 예에서는 ID가 `73`인 쿼리 알림 구독을 제거합니다.  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION 73 ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.dm_qn_subscriptions&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  
