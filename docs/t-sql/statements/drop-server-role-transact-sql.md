---
description: DROP SERVER ROLE(Transact-SQL)
title: DROP SERVER ROLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SERVER ROLE
- DROP_SERVER_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE, DROP
- DROP SERVER ROLE statement
ms.assetid: a2a1e6e6-e40c-4d6a-81be-d197b80bf226
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5a8f5b2204323c0da73371ba1298bc2b0f636e1a
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379666"
---
# <a name="drop-server-role-transact-sql"></a>DROP SERVER ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

  사용자 정의 서버 역할을 제거합니다.  
  
 사용자 정의 서버 역할은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 새로운 기능입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
DROP SERVER ROLE role_name  
```  
  
## <a name="arguments"></a>인수  
 *role_name*  
 서버에서 삭제할 사용자 정의 서버 역할을 지정합니다.  
  
## <a name="remarks"></a>설명  
 보안 개체를 소유한 사용자 정의 서버 역할을 서버에서 삭제할 수 없습니다. 보안 개체를 소유한 사용자 정의 서버 역할을 삭제하려면 먼저 해당 보안 개체의 소유권을 이전하거나 삭제해야 합니다.  
  
 멤버가 있는 사용자 정의 서버 역할은 삭제할 수 없습니다. 멤버가 있는 사용자 정의 서버 역할을 삭제하려면 먼저 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)을 사용하여 역할의 멤버를 제거해야 합니다.  
  
 고정 서버 역할은 제거할 수 없습니다.  
  
 [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) 카탈로그 뷰를 쿼리하여 역할 멤버 자격에 대한 정보를 볼 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 서버 역할에 대한 CONTROL 권한 또는 ALTER ANY SERVER ROLE 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-to-drop-a-server-role"></a>A. 서버 역할 삭제  
 다음 예에서는 서버 역할 `purchasing`을 삭제합니다.  
  
```sql  
DROP SERVER ROLE purchasing;  
GO  
```  
  
### <a name="b-to-view-role-membership"></a>B. 역할 멤버 자격 보기  
 역할 멤버 자격을 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **서버 역할(멤버**) 페이지를 사용하거나 다음 쿼리를 실행합니다.  
  
```sql  
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
### <a name="c-to-view-role-membership"></a>C. 역할 멤버 자격 보기  
 서버 역할이 다른 서버 역할을 소유하는지 여부를 확인하려면 다음 쿼리를 실행하십시오.  
  
```sql  
SELECT SP1.name AS RoleOwner, SP2.name AS Server_Role  
FROM sys.server_principals AS SP1  
JOIN sys.server_principals AS SP2  
    ON SP1.principal_id = SP2.owning_principal_id   
ORDER BY SP1.name ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
