---
title: CREATE SERVER ROLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SERVER_ROLE_TSQL
- CREATE SERVER ROLE
- SERVER ROLE
- CREATE_SERVER_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE
- SERVER ROLE, CREATE
- CREATE SERVER ROLE statement
- ROLE
- user-defined server roles [SQL Server]
- roles, server
ms.assetid: 30c92f80-f7f6-4a84-ae89-16e69add0de6
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c5c9a7d6cefa19dcb94f20a65e532bc6dad6bf3c
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36940811"
---
# <a name="create-server-role-transact-sql"></a>CREATE SERVER ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  새로운 사용자 정의 서버 역할을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE SERVER ROLE role_name [ AUTHORIZATION server_principal ]  
```  
  
## <a name="arguments"></a>인수  
 *role_name*  
 만들 서버 역할의 이름입니다.  
  
 AUTHORIZATION *server_principal*  
 새 서버 역할을 소유할 로그인입니다. 로그인을 지정하지 않으면 CREATE SERVER ROLE을 실행하는 로그인이 서버 역할을 소유합니다.  
  
## <a name="remarks"></a>Remarks  
 서버 역할은 서버 수준 보안 개체입니다. 서버 역할을 만든 후 GRANT, DENY 및 REVOKE를 사용하여 역할의 서버 수준 사용 권한을 구성합니다. 서버 역할에 로그인을 추가하거나 서버 역할에서 로그인을 제거하려면 [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)을 사용합니다. 서버 역할을 삭제하려면 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)을 사용합니다. 자세한 내용은 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)를 참조하세요.  
  
 [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) 및 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 카탈로그 뷰를 쿼리하여 서버 역할을 볼 수 있습니다.  
  
 데이터베이스 수준 보안 개체에서는 서버 역할에 사용 권한을 부여할 수 없습니다. 데이터베이스 역할을 만들려면 [CREATE ROLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)을 참조하세요.  
  
 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 CREATE SERVER ROLE 권한 또는 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
 로그인의 경우 *server_principal* 에 대한 IMPERSONATE이 필요하고 *server_principal*로 사용되는 서버 역할의 경우 ALTER 권한이 필요합니다. 또는 server_principal로 사용되는 Windows 그룹의 멤버 자격이 필요합니다.  
  
 이 역할은 개체 형식이 서버 역할로 설정된 감사 서버 계정 관리 및 추가할 이벤트 유형을 실행합니다.  
  
 AUTHORIZATION 옵션을 사용하여 서버 역할 소유권을 할당할 경우 다음 사용 권한도 필요합니다.  
  
-   다른 로그인에 서버 역할의 소유권을 할당하려면 해당 로그인에 대한 IMPERSONATE 권한이 필요합니다.  
  
-   다른 서버 역할에 서버 역할의 소유권을 할당하려면 받는 서버 역할의 멤버 자격이나 해당 서버 역할에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-server-role-that-is-owned-by-a-login"></a>1. 로그인이 소유하는 서버 역할 만들기  
 다음 예에서는 `buyers` 로그인이 소유하는 `BenMiller` 서버 역할을 만듭니다.  
  
```  
USE master;  
CREATE SERVER ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-server-role-that-is-owned-by-a-fixed-server-role"></a>2. 고정 서버 역할이 소유하는 서버 역할 만들기  
 다음 예에서는 `auditors` 고정 서버 역할이 소유하는 `securityadmin` 서버 역할을 만듭니다.  
  
```  
USE master;  
CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  
