---
title: sys.dm_qn_subscriptions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_qn_subscriptions
- dm_qn_subscriptions_TSQL
- sys.dm_qn_subscriptions
- sys.dm_qn_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_qn_subscriptions dynamic management view
ms.assetid: a3040ce6-f5af-48fc-8835-c418912f830c
author: stevestein
ms.author: sstein
ms.openlocfilehash: e0d725d37470f28847feb296194abd98fce9ae4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061917"
---
# <a name="query-notifications---sysdmqnsubscriptions"></a>쿼리 알림-sys.dm_qn_subscriptions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버에서 활성 쿼리 알림 구독에 관한 정보를 반환합니다. 이 뷰를 사용하여 서버 또는 지정된 데이터베이스의 활성 구독을 확인하거나 지정된 서버 보안 주체를 확인할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|구독의 ID입니다.|  
|**database_id**|**int**|알림 쿼리가 실행된 데이터베이스의 ID입니다. 이 데이터베이스에 이 구독과 관련된 정보가 저장됩니다.|  
|**sid**|**varbinary(85)**|이 구독을 만들고 소유하는 서버 보안 주체의 보안 ID입니다.|  
|**object_id**|**int**|구독 매개 변수에 관한 정보를 저장하는 내부 테이블의 ID입니다.|  
|**created**|**datetime**|구독을 만든 날짜와 시간입니다.|  
|**timeout**|**int**|구독의 제한 시간(초)입니다. 이 시간이 경과하면 알림이 발생하도록 플래그가 지정됩니다.<br /><br /> 참고: 실제 발생 시간 지정된 된 제한 시간 보다 클 수 있습니다. 그러나을 무효화 하는 변경이 나타나면 구독 지정된 된 제한 시간 후 되기 전에 발생 구독 발생에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변경 된 시간에 발생 하도록 발생 합니다.|  
|**상태**|**int**|구독의 상태를 나타냅니다. 코드 목록은 설명 아래의 표를 참조하십시오.|  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|켜짐|type|  
|----------|--------|--------|----------|  
|**sys.dm_qn_subscriptions**|**sys.databases**|**database_id**|다 대 일|  
|**sys.dm_qn_subscriptions**|**sys.internal_tables**|**object_id**|다 대 일|  
  
## <a name="remarks"></a>설명  
 상태 코드가 0이면 상태가 정의되지 않은 것입니다.  
  
 다음 상태 코드는 변경으로 인해 구독이 발생했음을 나타냅니다.  
  
|코드|보조 상태|Info|  
|----------|------------------|----------|  
|65798|데이터가 변경되어 구독이 발생했습니다.|삽입으로 인해 구독이 트리거되었습니다.|  
|65799|데이터가 변경되어 구독이 발생했습니다.|DELETE|  
|65800|데이터가 변경되어 구독이 발생했습니다.|Update|  
|65801|데이터가 변경되어 구독이 발생했습니다.|병합|  
|65802|데이터가 변경되어 구독이 발생했습니다.|테이블 자르기|  
|66048|제한 시간이 만료되어 구독이 발생했습니다.|정의되지 않은 정보 모드입니다.|  
|66315|개체가 변경되어 구독이 발생했습니다.|개체 또는 사용자가 삭제되었습니다.|  
|66316|개체가 변경되어 구독이 발생했습니다.|개체가 변경되었습니다.|  
|66565|데이터베이스가 분리 또는 삭제되어 구독이 발생했습니다.|서버 또는 데이터베이스가 다시 시작되었습니다.|  
|66571|데이터베이스가 분리 또는 삭제되어 구독이 발생했습니다.|개체 또는 사용자가 삭제되었습니다.|  
|66572|데이터베이스가 분리 또는 삭제되어 구독이 발생했습니다.|개체가 변경되었습니다.|  
|67341|서버에 리소스가 부족하여 구독이 트리거되었습니다.|서버에 리소스가 부족하여 구독이 트리거되었습니다.|  
  
 다음 상태 코드는 구독을 만들지 못했음을 나타냅니다.  
  
|코드|보조 상태|Info|  
|----------|------------------|----------|  
|132609|문이 지원되지 않아 구독을 만들지 못했습니다.|쿼리가 너무 복잡합니다.|  
|132610|문이 지원되지 않아 구독을 만들지 못했습니다.|구독에 대해 잘못된 문입니다.|  
|132611|문이 지원되지 않아 구독을 만들지 못했습니다.|구독에 대해 잘못된 집합 옵션입니다.|  
|132612|문이 지원되지 않아 구독을 만들지 못했습니다.|잘못된 격리 수준입니다.|  
|132622|문이 지원되지 않아 구독을 만들지 못했습니다.|내부적으로 사용됩니다.|  
|132623|문이 지원되지 않아 구독을 만들지 못했습니다.|테이블당 템플릿 제한을 초과했습니다.|  
  
 다음 상태 코드는 내부적으로 사용되며 삭제 및 초기화 확인 모드로 분류됩니다.  
  
|코드|보조 상태|Info|  
|----------|------------------|----------|  
|198656|내부적으로 사용되는 삭제 및 초기화 확인 모드입니다.|정의되지 않은 정보 모드입니다.|  
|198928|구독이 제거되었습니다.|데이터베이스가 연결되어 구독이 발생했습니다.|  
|198929|구독이 제거되었습니다.|사용자가 삭제되어 구독이 발생했습니다.|  
|198930|구독이 제거되었습니다.|다시 구독으로 인해 구독이 삭제되었습니다.|  
|198931|구독이 제거되었습니다.|구독이 중지되었습니다.|  
|199168|구독이 활성화되어 있습니다.|정의되지 않은 정보 모드입니다.|  
|199424|구독이 초기화되었지만 아직 활성화되지 않았습니다.|정의되지 않은 정보 모드입니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
> [!NOTE]  
>  사용자에게 VIEW SERVER STATE 권한이 없다면 이 뷰는 현재 사용자가 소유한 구독에 관한 정보를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-return-active-query-notification-subscriptions-for-the-current-user"></a>A. 현재 사용자에 대한 활성 쿼리 알림 구독 반환  
 다음 예에서는 현재 사용자의 활성 쿼리 알림 구독을 반환합니다. 사용자에게 VIEW SERVER STATE 권한이 있을 경우 서버의 모든 활성 구독이 반환됩니다.  
  
```  
SELECT id, database_id, sid, object_id, created, timeout, status  
FROM sys.dm_qn_subscriptions;  
GO  
```  
  
### <a name="b-returning-active-query-notification-subscriptions-for-a-specified-user"></a>2\. 지정된 사용자에 대한 활성 쿼리 알림 구독 반환  
 다음 예에서는 로그인 `Ruth0`으로 구독된 활성 쿼리 알림 구독을 반환합니다.  
  
```  
SELECT id, database_id, sid, object_id, created, timeout, status  
FROM sys.dm_qn_subscriptions  
WHERE sid = SUSER_SID('Ruth0');  
GO  
```  
  
### <a name="c-returning-internal-table-metadata-for-query-notification-subscriptions"></a>3\. 쿼리 알림 구독에 대한 내부 테이블 메타데이터 반환  
 다음 예에서는 쿼리 알림 구독에 대한 내부 테이블 메타데이터를 반환합니다.  
  
```  
SELECT qn.id AS query_subscription_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.dm_qn_subscriptions AS qn ON it.object_id = qn.object_id  
WHERE it.internal_type_desc = 'QUERY_NOTIFICATION';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [쿼리 알림 관련된 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/92eb22d8-33f3-4c17-b32e-e23acdfbd8f4)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;TRANSACT-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)  
  
  
