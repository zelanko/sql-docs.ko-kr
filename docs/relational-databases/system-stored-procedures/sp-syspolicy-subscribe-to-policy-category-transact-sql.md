---
title: sp_syspolicy_subscribe_to_policy_category (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_subscribe_to_policy_category
- sp_syspolicy_subscribe_to_policy_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_subscribe_to_policy_category
ms.assetid: de88cc49-bcc8-4dc6-8e59-ad85cfbfb2fb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 06ab045b4ac0e7cecd62cdb8092860c3389e5f1f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752763"
---
# <a name="sp_syspolicy_subscribe_to_policy_category-transact-sql"></a>sp_syspolicy_subscribe_to_policy_category(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  지정된 데이터베이스에 대한 정책 범주 구독을 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_subscribe_to_policy_category [ @policy_category = ] 'policy_category'  
```  
  
## <a name="arguments"></a>인수  
`[ @policy_category = ] 'policy_category'`데이터베이스에서 구독할 정책 범주의 이름입니다. *policy_category* 는 **sysname**이며 필수입니다.  
  
 *Policy_category*에 대 한 값을 가져오려면 msdb.dbo.syspolicy_policy_categories 시스템 뷰를 쿼리 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syspolicy_subscribe_to_policy_category는 정책 범주 구독을 추가할 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 지정한 데이터베이스에 대해 'Finance' 정책 범주에 대한 구독을 추가합니다.  
  
```  
USE <database_name>;  
  
EXEC sys.sp_syspolicy_subscribe_to_policy_category @policy_category = N'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;정책 기반 관리 저장 프로시저](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_syspolicy_unsubscribe_from_policy_category &#40;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)  
  
  
