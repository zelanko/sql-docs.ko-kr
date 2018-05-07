---
title: sp_syspolicy_subscribe_to_policy_category (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_subscribe_to_policy_category
- sp_syspolicy_subscribe_to_policy_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_subscribe_to_policy_category
ms.assetid: de88cc49-bcc8-4dc6-8e59-ad85cfbfb2fb
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1d507bd8107474d50f0f99d12f88ddf971b21b25
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spsyspolicysubscribetopolicycategory-transact-sql"></a>sp_syspolicy_subscribe_to_policy_category(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 데이터베이스에 대한 정책 범주 구독을 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_subscribe_to_policy_category [ @policy_category = ] 'policy_category'  
```  
  
## <a name="arguments"></a>인수  
 [  **@policy_category=** ] **'***policy_category***'**  
 데이터베이스에서 구독하도록 할 정책 범주의 이름입니다. *policy_category* 은 **sysname**, 이며 필수입니다.  
  
 에 대 한 값을 가져오려면 *policy_category*, msdb.dbo.syspolicy_policy_categories 시스템 뷰를 쿼리 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_syspolicy_subscribe_to_policy_category는 정책 범주 구독을 추가할 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 지정한 데이터베이스에 대해 'Finance' 정책 범주에 대한 구독을 추가합니다.  
  
```  
USE <database_name>;  
  
EXEC sys.sp_syspolicy_subscribe_to_policy_category @policy_category = N'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [정책 기반 관리 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_unsubscribe_from_policy_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)  
  
  
