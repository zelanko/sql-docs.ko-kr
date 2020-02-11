---
title: sp_droprole (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprole
- sp_droprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2573019948a326c9171fc83d62428e7e2f888eb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933814"
---
# <a name="sp_droprole-transact-sql"></a>sp_droprole(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 데이터베이스 역할을 제거합니다.  
  
> [!IMPORTANT]  
>  에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **sp_droprole** 은 DROP ROLE 문으로 바뀌었습니다. **sp_droprole** 는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와의 호환성을 위해서만 포함 되었으며 이후 릴리스에서는 지원 되지 않을 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>인수  
`[ @rolename = ] 'role'`현재 데이터베이스에서 제거할 데이터베이스 역할의 이름입니다. *role* 은 **sysname**이며 기본값은 없습니다. 현재 데이터베이스에 *역할이* 이미 있어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **Sp_droprole**를 사용 하 여 데이터베이스 역할만 제거할 수 있습니다.  
  
 기존 멤버가 있는 데이터베이스 역할은 제거할 수 없습니다. 데이터베이스 역할을 제거하려면 먼저 데이터베이스 역할의 모든 멤버를 제거해야 합니다. 역할에서 사용자를 제거 하려면 **sp_droprolemember**을 사용 합니다. 사용자가 여전히 역할의 멤버인 경우 **sp_droprole** 해당 멤버를 표시 합니다.  
  
 고정 역할 및 **public** 역할은 제거할 수 없습니다.  
  
 역할이 보안 개체를 소유하고 있는 경우에는 해당 역할을 제거할 수 없습니다. 보안 개체를 소유한 애플리케이션 역할을 삭제하려면 먼저 보안 개체의 소유권을 이전하거나 보안 개체를 삭제해야 합니다. 제거하지 않아야 하는 개체의 소유자를 변경하려면 ALTER AUTHORIZATION을 사용하십시오.  
  
 사용자 정의 트랜잭션 내에서는 **sp_droprole** 을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 역할에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Sales` 애플리케이션 역할을 제거합니다.  
  
```  
EXEC sp_droprole 'Sales';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addrole &#40;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [DROP ROLE &#40;Transact-sql&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Transact-sql&#41;sp_dropapprole &#40;](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
