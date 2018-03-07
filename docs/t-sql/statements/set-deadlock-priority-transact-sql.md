---
title: SET DEADLOCK_PRIORITY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET DEADLOCK_PRIORITY
- DEADLOCK_PRIORITY_TSQL
- SET_DEADLOCK_PRIORITY_TSQL
- DEADLOCK_PRIORITY
dev_langs:
- TSQL
helpviewer_keywords:
- deadlocks [SQL Server], priority settings
- DEADLOCK_PRIORITY option
- locking [SQL Server], deadlocks
- priority deadlock settings [SQL Server]
- SET DEADLOCK_PRIORITY statement
ms.assetid: 810a3a8e-3da3-4bf9-bb15-7b069685a1b6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b80f18cb5440560b34924cad619af1f195f49a47
ms.sourcegitcommit: ed9335fe62c0c8d94ee87006c6957925d09ee301
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="set-deadlockpriority-transact-sql"></a>SET DEADLOCK_PRIORITY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  현재 세션이 다른 세션과 교착 상태에 있는 경우 현재 세션이 계속 실행되도록 하는 상대적 중요도를 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET DEADLOCK_PRIORITY { LOW | NORMAL | HIGH | <numeric-priority> | @deadlock_var | @deadlock_intvar }  
  
<numeric-priority> ::= { -10 | -9 | -8 | … | 0 | … | 8 | 9 | 10 }  
```  
  
## <a name="arguments"></a>인수  
 LOW  
 현재 세션이 교착 상태와 관련되어 있고 교착 상태 체인에 포함된 다른 세션의 교착 상태 우선 순위가 NORMAL이나 HIGH 또는 -5보다 큰 정수 값으로 설정되어 있는 경우 현재 세션이 교착 상태가 되도록 지정합니다. 다른 세션의 교착 상태 우선 순위가 -5보다 작은 정수 값으로 설정되어 있으면 현재 세션이 중지되지 않습니다. 또한 다른 세션의 교착 상태 우선 순위가 LOW나 -5와 동일한 정수 값으로 설정되어 있는 경우에도 현재 세션이 중지될 수 있도록 지정합니다.  
  
 NORMAL  
 교착 상태 체인에 포함된 다른 세션의 교착 상태 우선 순위가 HIGH 또는 0보다 큰 정수 값으로 설정되어 있는 경우 현재 세션이 교착 상태가 되도록 지정하지만 다른 세션의 교착 상태 우선 순위가 LOW 또는 0보다 작은 정수 값으로 설정되어 있는 경우 현재 세션이 교착 상태가 되지 않도록 지정합니다. 또한 다른 세션에서 교착 상태 우선 순위를 NORMAL 또는 0과 같은 정수 값으로 설정하면 현재 세션이 교착 상태가 될 수 있도록 지정합니다 NORMAL은 기본 우선 순위입니다.  
  
 HIGH  
 교착 상태 체인에 포함된 다른 세션에서 교착 상태 우선 순위를 5보다 큰 정수 값으로 설정하면 현재 세션이 교착 상태가 되도록 지정하거나 다른 세션에서 교착 상태 우선 순위를 HIGH 또는 5와 같은 정수 값으로 설정하면 현재 세션이 교착 상태가 될 수 있도록 지정합니다.  
  
 \<우선 순위가 숫자 >  
 21 수준의 교착 상태 우선 순위를 제공하는 정수 값 범위(-10 ~ 10)입니다. 교착 상태 세션에 포함된 다른 세션이 더 높은 교착 상태 우선 순위 값에서 실행되는 경우에는 현재 세션이 교착 상태가 되지만 다른 세션이 실행되는 교착 상태 우선 순위 값이 현재 세션의 값보다 낮은 경우에는 현재 세션이 교착 상태가 되지 않도록 지정합니다. 또한 다른 세션이 현재 세션과 동일한 교착 상태 우선 순위 값으로 실행되는 경우에는 현재 세션이 교착 상태가 될 수 있도록 지정합니다. LOW는 -5로, NORMAL은 0으로, HIGH는 5로 매핑됩니다.  
  
 **@***deadlock_var*  
 교착 상태 우선 순위를 지정하는 문자 변수입니다. 변수는 'LOW', 'NORMAL' 또는 'HIGH' 값으로 설정해야 합니다. 변수는 전체 문자열을 저장할 수 있을 만큼 커야 합니다.  
  
 **@***deadlock_intvar*  
 교착 상태 우선 순위를 지정하는 정수 변수입니다. 변수는 범위가 -10에서 10 사이인 정수 값으로 설정해야 합니다.  
  
## <a name="remarks"></a>주의  
 교착 상태는 두 세션이 모두 다른 세션에서 잠근 리소스에 액세스하려고 대기할 때 발생합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 두 세션이 교착 상태인 것이 감지되면 세션 중 하나를 교착 상태가 발생한 것으로 선택하여 교착 상태를 해결합니다. 교착 상태가 발생한 현재 트랜잭션이 롤백되고 교착 상태 오류 메시지 1205가 클라이언트로 반환됩니다. 이렇게 하면 해당 세션이 보유한 모든 잠금이 해제되어 다른 세션을 계속할 수 있습니다.  
  
 교착 상태가 발생한 것으로 선택하는 세션은 각 세션의 교착 상태 우선 순위에 따라 다릅니다.  
  
-   두 세션의 교착 상태 우선 순위가 같으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 교착 상태가 발생한 것으로 롤백하는 데 비용이 적게 드는 세션을 선택합니다. 예를 들어 두 세션의 교착 상태 우선 순위가 HIGH로 설정되어 있으면 인스턴스는 롤백하는 데 비용이 적게 드는 것으로 예상되는 세션을 교착 상태가 발생한 것으로 선택합니다. 각 트랜잭션에서 해당 시점에 쓴 로그 바이트 수를 비교 하 여 비용을 결정 합니다. (이 값 볼 수 있습니다이 "로그 사용"으로 교착 상태 그래프에).
  
-   세션의 교착 상태 우선 순위가 다르면 교착 상태 우선 순위가 가장 낮은 세션이 교착 상태가 발생한 것으로 선택됩니다.  
  
 SET DEADLOCK_PRIORITY 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 변수를 사용하여 교착 상태 우선 순위를 `LOW`로 설정합니다.  
  
```  
DECLARE @deadlock_var NCHAR(3);  
SET @deadlock_var = N'LOW';  
  
SET DEADLOCK_PRIORITY @deadlock_var;  
GO  
```  
  
 다음 예에서는 교착 상태 우선 순위를 `NORMAL`로 설정합니다.  
  
```  
SET DEADLOCK_PRIORITY NORMAL;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [@@LOCK_TIMEOUT&#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40; Transact SQL &#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
