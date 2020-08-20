---
description: sp_dropapprole(Transact-SQL)
title: sp_dropapprole (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropapprole_TSQL
- sp_dropapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropapprole
ms.assetid: ea1aefe6-8f7d-46e9-a3cb-7b037b393e73
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 9e02da3e5507b1376dba5ac170922a2bb9230054
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493323"
---
# <a name="sp_dropapprole-transact-sql"></a>sp_dropapprole(Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스에서 애플리케이션 역할을 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [DROP APPLICATION ROLE](../../t-sql/statements/drop-application-role-transact-sql.md) 을 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_dropapprole [@rolename = ] 'role'  
```  
  
## <a name="arguments"></a>인수  
`[ @rolename = ] 'role'` 제거할 응용 프로그램 역할입니다. *role* 은 **sysname**이며 기본값은 없습니다. 현재 데이터베이스에 *역할이* 있어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropapprole** 는 응용 프로그램 역할을 제거 하는 데만 사용할 수 있습니다. 보안 개체를 소유하는 역할은 삭제할 수 없습니다. 보안 개체를 소유한 애플리케이션 역할을 삭제하려면 먼저 보안 개체의 소유권을 이전하거나 보안 개체를 삭제해야 합니다.  
  
 사용자 정의 트랜잭션 내에서는 **sp_dropapprole** 을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER ANY APPLICATION ROLE 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 현재 데이터베이스에서 `SalesApp` 애플리케이션 역할을 제거합니다.  
  
```sql
EXEC sp_dropapprole 'SalesApp';  
```  
  
## <a name="see-also"></a>관련 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저 ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addapprole &#40;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [Transact-sql&#41;&#40;응용 프로그램 역할 삭제 ](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [Transact-sql&#41;sp_changeobjectowner &#40;](../../relational-databases/system-stored-procedures/sp-changeobjectowner-transact-sql.md)   
 [Transact-sql&#41;sp_setapprole &#40;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
