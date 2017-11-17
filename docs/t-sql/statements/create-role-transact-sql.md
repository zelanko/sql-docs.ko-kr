---
title: "역할 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE ROLE
- DATABASE ROLE
- ROLE_TSQL
- DATABASE_ROLE_TSQL
- CREATE_ROLE_TSQL
- CREATE DATABASE ROLE
- ROLE
- CREATE_DATABASE_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], creating
- CREATE DATABASE ROLE statement
- roles [SQL Server], creating
- CREATE ROLE statement
ms.assetid: b0cd54ad-e81d-4d71-acec-8a6d7261ca08
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 21e3cca3d07d7f53d646b5dd052fd40d0fa2cc1a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-role-transact-sql"></a>CREATE ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스에 새 데이터베이스 역할을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE ROLE role_name [ AUTHORIZATION owner_name ]  
```  
  
## <a name="arguments"></a>인수  
 *role_name*  
 만들 역할의 이름입니다.  
  
 권한 부여 *owner_name*  
 새 역할을 소유할 데이터베이스 사용자나 역할입니다. 사용자를 지정하지 않으면 CREATE ROLE을 실행하는 사용자가 역할을 소유합니다.  
  
## <a name="remarks"></a>주의  
 역할은 데이터베이스 수준 보안 개체입니다. 역할을 만든 후 GRANT, DENY 및 REVOKE를 사용하여 역할의 데이터베이스 수준 사용 권한을 구성합니다. 데이터베이스 역할에 구성원을 추가 하려면 사용 하 여 [ALTER role&#40; Transact SQL &#41; ](../../t-sql/statements/alter-role-transact-sql.md). 자세한 내용은 참조 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)합니다.  
  
 데이터베이스 역할은 sys.database_role_members 및 sys.database_principals 카탈로그 뷰에 표시됩니다.  
  
 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 필요한 **CREATE ROLE** 의 구성원 자격이 있거나 데이터베이스에 대 한 권한이 **db_securityadmin** 고정된 데이터베이스 역할입니다. 사용 하는 경우는 **권한 부여** 옵션을 다음 권한은 필요 합니다.  
  
-   다른 사용자에게 역할의 소유권을 할당하려면 해당 사용자에 대한 IMPERSONATE 권한이 필요합니다.  
  
-   다른 역할에 역할의 소유권을 할당하려면 역할을 받는 역할의 멤버 자격이나 해당 역할에 대한 ALTER 권한이 필요합니다.  
  
-   응용 프로그램 역할에 역할의 소유권을 할당하려면 응용 프로그램 역할에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
다음 예에서는 모두 AdventureWorks 데이터베이스를 사용 합니다.   

### <a name="a-creating-a-database-role-that-is-owned-by-a-database-user"></a>1. 데이터베이스 사용자가 소유하는 데이터베이스 역할 만들기  
 다음 예에서는 `buyers` 사용자가 소유하는 `BenMiller` 데이터베이스 역할을 만듭니다.  
  
```  
CREATE ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-database-role-that-is-owned-by-a-fixed-database-role"></a>2. 고정 데이터베이스 역할이 소유하는 데이터베이스 역할 만들기  
 다음 예에서는 `auditors` 고정 데이터베이스 역할이 소유하는 `db_securityadmin` 데이터베이스 역할을 만듭니다.  
  
```  
CREATE ROLE auditors AUTHORIZATION db_securityadmin;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [ALTER role&#40; Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP role&#40; Transact SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  



