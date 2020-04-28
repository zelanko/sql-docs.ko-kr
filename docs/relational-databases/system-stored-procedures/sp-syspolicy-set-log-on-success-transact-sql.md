---
title: sp_syspolicy_set_log_on_success (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_set_log_on_success_TSQL
- sp_syspolicy_set_log_on_success
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_set_log_on_success
ms.assetid: 6b33383b-5949-488a-a911-59299a270f46
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 95053570a7ded118d2a298b417b361dd8d3dd2be
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68035434"
---
# <a name="sp_syspolicy_set_log_on_success-transact-sql"></a>sp_syspolicy_set_log_on_success(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  성공한 정책 평가가 정책 기반 관리의 정책 기록 로그에 로깅되는지 여부를 지정합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_set_log_on_success [ @value = ] value  
```  
  
## <a name="arguments"></a>인수  
`[ @value = ] value`성공한 정책 평가가 로깅 되는지 여부를 결정 합니다. *value* 는 **sqlvariant**이며 다음 값 중 하나일 수 있습니다.  
  
-   0 또는 'false' = 성공한 정책 평가가 로깅되지 않습니다.  
  
-   1 또는 'true' = 성공한 정책 평가가 로깅됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syspolicy_set_log_on_success는 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 *Value* 가 0 또는 ' f a l s e '로 설정 되 면 실패 한 정책 평가만 로깅됩니다.  
  
## <a name="permissions"></a>사용 권한  
 PolicyAdministratorRole 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
> **중요!!** 자격 증명의 승격 가능: Policy관리자 역할 역할의 사용자는 서버 트리거를 만들고 인스턴스 작업에 영향을 줄 수 있는 정책 실행을 예약할 수 [!INCLUDE[ssDE](../../includes/ssde-md.md)]있습니다. 예를 들어 PolicyAdministratorRole 역할의 사용자는 대부분의 개체가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 생성되지 않도록 할 수 있는 정책을 만들 수 있습니다. 이렇게 자격 증명을 승격할 수 있기 때문에 PolicyAdministratorRole 역할은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성을 제어할 수 있도록 신뢰할 수 있는 사용자에게만 부여되어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 성공한 정책 평가를 로깅하도록 설정합니다.  
  
```  
EXEC msdb.dbo.sp_syspolicy_set_log_on_success @value = 1;  
  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;정책 기반 관리 저장 프로시저](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_syspolicy_configure &#40;](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md)  
  
  
