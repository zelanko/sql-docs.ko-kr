---
title: sp_syspolicy_purge_health_state (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_purge_health_state_TSQL
- sp_syspolicy_purge_health_state
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_purge_health_state
ms.assetid: 4ba4aa91-4c19-41c7-b70d-5fd9d0e89a5e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6c07d71e2ab4c9fe39882476eef25674718a17c7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85639572"
---
# <a name="sp_syspolicy_purge_health_state-transact-sql"></a>sp_syspolicy_purge_health_state(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  정책 기반 관리의 정책 상태를 삭제합니다. 정책 상태는 개체 탐색기 내에 표시되는 시각적 표시기(빨강 "X"가 있는 스크롤 기호)로, 이를 통해 정책 평가에 실패한 노드를 쉽게 확인할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_purge_health_state [ @target_tree_root_with_id = ] 'target_tree_root_with_id'  
```  
  
## <a name="arguments"></a>인수  
`[ @target_tree_root_with_id = ] 'target_tree_root_with_id'`상태를 지울 개체 탐색기의 노드를 나타냅니다. *target_tree_root_with_id* 은 **nvarchar (400)** 이며 기본값은 NULL입니다.  
  
 msdb.dbo.syspolicy_system_health_state 시스템 뷰의 target_query_expression_with_id 열에 있는 값을 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syspolicy_purge_health_state는 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 매개 변수를 지정하지 않고 이 저장 프로시저를 실행하면 개체 탐색기의 모든 노드에 대해 시스템 상태가 삭제됩니다.  
  
## <a name="permissions"></a>사용 권한  
 PolicyAdministratorRole 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
> [!IMPORTANT]  
>  자격 증명의 승격 가능: Policy관리자 역할 역할의 사용자는 서버 트리거를 만들고 인스턴스 작업에 영향을 줄 수 있는 정책 실행을 예약할 수 있습니다 [!INCLUDE[ssDE](../../includes/ssde-md.md)] . 예를 들어 PolicyAdministratorRole 역할의 사용자는 대부분의 개체가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 생성되지 않도록 할 수 있는 정책을 만들 수 있습니다. 이렇게 자격 증명을 승격할 수 있기 때문에 PolicyAdministratorRole 역할은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성을 제어할 수 있도록 신뢰할 수 있는 사용자에게만 부여되어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 개체 탐색기의 지정한 노드에 대한 상태를 삭제합니다.  
  
```  
EXEC msdb.dbo.sp_syspolicy_purge_health_state @target_tree_root_with_id = 'Server/Database[@ID=7]';  
  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;정책 기반 관리 저장 프로시저](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)  
  
  
