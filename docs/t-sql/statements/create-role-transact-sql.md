---
title: CREATE ROLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 234fe7a9d26c91bc5b390997f56c9dcb050561aa
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86392861"
---
# <a name="create-role-transact-sql"></a>CREATE ROLE(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스에 새 데이터베이스 역할을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
CREATE ROLE role_name [ AUTHORIZATION owner_name ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *role_name*  
 만들 역할의 이름입니다.  
  
 AUTHORIZATION *owner_name*  
 새 역할을 소유할 데이터베이스 사용자나 역할입니다. 사용자를 지정하지 않으면 CREATE ROLE을 실행하는 사용자가 역할을 소유합니다. 역할의 소유자 또는 소유 역할의 멤버는 역할의 멤버를 추가하거나 제거할 수 있습니다.
  
## <a name="remarks"></a>설명  
 역할은 데이터베이스 수준 보안 개체입니다. 역할을 만든 후 GRANT, DENY 및 REVOKE를 사용하여 역할의 데이터베이스 수준 사용 권한을 구성합니다. 데이터베이스 역할에 멤버를 추가하려면 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)를 사용합니다. 자세한 내용은 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)을 참조하세요.  
  
 데이터베이스 역할은 sys.database_role_members 및 sys.database_principals 카탈로그 뷰에 표시됩니다.  
  
 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 **CREATE ROLE**이나 **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격이 필요합니다. **AUTHORIZATION** 옵션을 사용할 경우 다음 권한도 필요합니다.  
  
-   다른 사용자에게 역할의 소유권을 할당하려면 해당 사용자에 대한 IMPERSONATE 권한이 필요합니다.  
  
-   다른 역할에 역할의 소유권을 할당하려면 역할을 받는 역할의 멤버 자격이나 해당 역할에 대한 ALTER 권한이 필요합니다.  
  
-   애플리케이션 역할에 역할의 소유권을 할당하려면 애플리케이션 역할에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
다음 예에서는 모두 AdventureWorks 데이터베이스를 사용합니다.   

### <a name="a-creating-a-database-role-that-is-owned-by-a-database-user"></a>A. 데이터베이스 사용자가 소유하는 데이터베이스 역할 만들기  
 다음 예에서는 `buyers` 사용자가 소유하는 `BenMiller` 데이터베이스 역할을 만듭니다.  
  
```sql  
CREATE ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-database-role-that-is-owned-by-a-fixed-database-role"></a>B. 고정 데이터베이스 역할이 소유하는 데이터베이스 역할 만들기  
 다음 예에서는 `auditors` 고정 데이터베이스 역할이 소유하는 `db_securityadmin` 데이터베이스 역할을 만듭니다.  
  
```sql  
CREATE ROLE auditors AUTHORIZATION db_securityadmin;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  


