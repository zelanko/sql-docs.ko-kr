---
description: sp_syspolicy_delete_policy_execution_history(Transact-SQL)
title: sp_syspolicy_delete_policy_execution_history (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_delete_policy_execution_history
- sp_syspolicy_delete_policy_execution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_execution_history
ms.assetid: fe651af9-267e-45ec-b4e7-4b0698fb1be3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 99a17425f74b1ae2f5db7c4a6002e27ca7780f21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485631"
---
# <a name="sp_syspolicy_delete_policy_execution_history-transact-sql"></a>sp_syspolicy_delete_policy_execution_history(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  정책 기반 관리에서 정책의 실행 기록을 삭제합니다. 이 저장 프로시저를 사용하여 특정 정책 또는 모든 정책의 실행 기록을 삭제하거나 특정 날짜 이전의 실행 기록을 삭제할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_delete_policy_execution_history [ @policy_id = ] policy_id ]  
    [ , [ @oldest_date = ] 'oldest_date' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @policy_id = ] policy_id` 실행 기록을 삭제 하려는 정책의 식별자입니다. *policy_id* 는 **int**이며 필수입니다. NULL일 수 있습니다.  
  
`[ @oldest_date = ] 'oldest_date'` 정책 실행 기록을 유지 하려는 가장 오래 된 날짜입니다. 이 날짜 이전의 실행 기록은 모두 삭제됩니다. *oldest_date* 은 **datetime**이며 필수입니다. NULL일 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syspolicy_delete_policy_execution_history는 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 *Policy_id*에 대 한 값을 가져오고 실행 기록 날짜를 보려면 다음 쿼리를 사용할 수 있습니다.  
  
```  
SELECT a.name AS N'policy_name', b.policy_id, b.start_date, b.end_date  
FROM msdb.dbo.syspolicy_policies AS a   
INNER JOIN msdb.dbo.syspolicy_policy_execution_history AS b  
ON a.policy_id = b.policy_id  
```  
  
 하나 또는 두 값 모두 NULL을 지정하면 다음 동작이 적용됩니다.  
  
-   모든 정책 실행 기록을 삭제 하려면 *policy_id* 및 *oldest_date*에 대해 모두 NULL을 지정 합니다.  
  
-   특정 정책에 대 한 모든 정책 실행 기록을 삭제 하려면 *policy_id*의 정책 식별자를 지정 하 고 NULL을 *oldest_date*로 지정 합니다.  
  
-   특정 날짜 이전의 모든 정책에 대 한 정책 실행 기록을 삭제 하려면 *policy_id*에 대해 NULL을 지정 하 고 *oldest_date*날짜를 지정 합니다.  
  
 정책 실행 기록을 보관하려면 개체 탐색기에서 정책 기록 로그를 열고 실행 기록을 파일로 내보냅니다. 정책 기록 로그에 액세스 하려면 **관리**를 확장 하 고 **정책 관리**를 마우스 오른쪽 단추로 클릭 한 다음 **기록 보기**를 클릭 합니다.  
  
## <a name="permissions"></a>사용 권한  
 PolicyAdministratorRole 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
> [!IMPORTANT]  
>  자격 증명의 승격 가능: Policy관리자 역할 역할의 사용자는 서버 트리거를 만들고 인스턴스 작업에 영향을 줄 수 있는 정책 실행을 예약할 수 있습니다 [!INCLUDE[ssDE](../../includes/ssde-md.md)] . 예를 들어 PolicyAdministratorRole 역할의 사용자는 대부분의 개체가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 생성되지 않도록 할 수 있는 정책을 만들 수 있습니다. 이렇게 자격 증명을 승격할 수 있기 때문에 PolicyAdministratorRole 역할은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성을 제어할 수 있도록 신뢰할 수 있는 사용자에게만 부여되어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 ID가 7인 정책에 대해 특정 날짜 이전의 정책 실행 기록을 삭제합니다.  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_execution_history @policy_id = 7  
, @oldest_date = '2009-02-16 16:00:00.000';  
  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [Transact-sql&#41;&#40;정책 기반 관리 저장 프로시저 ](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_syspolicy_set_config_history_retention &#40;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [Transact-sql&#41;sp_syspolicy_purge_history &#40;](../../relational-databases/system-stored-procedures/sp-syspolicy-purge-history-transact-sql.md)  
  
  
