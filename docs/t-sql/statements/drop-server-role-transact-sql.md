---
title: DROP SERVER ROLE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c493ed6556bde690f6b4a9ec6b46aeb3ceb59ae
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-server-role-transact-sql"></a>DROP SERVER ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

  사용자 정의 서버 역할을 제거합니다.  
  
 사용자 정의 서버 역할은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 새로운 기능입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Parallel Data Warehouse  
  
DROP SERVER ROLE role_name  
```  
  
## <a name="arguments"></a>인수  
 *role_name*  
 서버에서 삭제할 사용자 정의 서버 역할을 지정합니다.  
  
## <a name="remarks"></a>주의  
 보안 개체를 소유한 사용자 정의 서버 역할을 서버에서 삭제할 수 없습니다. 보안 개체를 소유한 사용자 정의 서버 역할을 삭제하려면 먼저 해당 보안 개체의 소유권을 이전하거나 삭제해야 합니다.  
  
 멤버가 있는 사용자 정의 서버 역할은 삭제할 수 없습니다. 멤버가 포함 된 사용자 정의 서버 역할을 삭제 하려면 먼저 제거 해야 역할의 멤버를 사용 하 여 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)합니다.  
  
 고정 서버 역할은 제거할 수 없습니다.  
  
 쿼리하여 역할 멤버 자격에 대 한 정보를 볼 수는 [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
## <a name="permissions"></a>Permissions  
 서버 역할에 대한 CONTROL 권한 또는 ALTER ANY SERVER ROLE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-to-drop-a-server-role"></a>1. 서버 역할 삭제  
 다음 예에서는 서버 역할 `purchasing`을 삭제합니다.  
  
```  
DROP SERVER ROLE purchasing;  
GO  
```  
  
### <a name="b-to-view-role-membership"></a>2. 역할 멤버 자격 보기  
 역할 멤버 자격을 보려면 사용 하 여는 **서버 역할 (멤버**) 페이지에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 하거나 다음 쿼리를 실행 합니다.  
  
```  
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
### <a name="c-to-view-role-membership"></a>3. 역할 멤버 자격 보기  
 서버 역할이 다른 서버 역할을 소유하는지 여부를 확인하려면 다음 쿼리를 실행하십시오.  
  
```  
SELECT SP1.name AS RoleOwner, SP2.name AS Server_Role  
FROM sys.server_principals AS SP1  
JOIN sys.server_principals AS SP2  
    ON SP1.principal_id = SP2.owning_principal_id   
ORDER BY SP1.name ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER role&#40; Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [역할 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP role&#40; Transact SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
