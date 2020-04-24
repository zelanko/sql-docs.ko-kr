---
title: ALTER ROLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_ROLE_TSQL
- ALTER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database roles
- ALTER ROLE statement
- renaming database roles
- database roles [SQL Server], modifying
- names [SQL Server], database roles
ms.assetid: e1e83caa-17cc-4871-b2db-2711339fb64f
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2af9386dc25fec5309d13d64f02ec8997f60792d
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81626984"
---
# <a name="alter-role-transact-sql"></a>ALTER ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스 역할에 멤버를 추가하거나 데이터베이스 역할에서 멤버를 제거하거나 사용자 정의 데이터베이스 역할의 이름을 변경합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 멤버를 추가 또는 삭제하는 역할을 변경하려면 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 및 [sp_droprolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)를 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server (starting with 2012) and Azure SQL Database  
  
ALTER ROLE  role_name  
{  
       ADD MEMBER database_principal  
    |  DROP MEMBER database_principal  
    |  WITH NAME = new_name  
}  
[;]  
```  
  
 
```syntaxsql
-- Syntax for SQL Server 2008, Azure SQL Data Warehouse and Parallel Data Warehouse
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *role_name*  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](2008부터), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 변경할 데이터베이스 역할을 지정합니다.  
  
 ADD MEMBER *database_principal*  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](2012부터), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 데이터베이스 보안 주체를 데이터베이스 역할의 멤버 자격에 추가하도록 지정합니다.  
  
-   *database_principal*은 데이터베이스 사용자 또는 사용자 정의 데이터베이스 역할입니다.  
  
-   *database_principal*은 고정 데이터베이스 역할 또는 서버 보안 주체일 수 없습니다.  
  
DROP MEMBER *database_principal*  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](2012부터), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 데이터베이스 역할의 멤버 자격에서 데이터베이스 보안 주체를 제거하도록 지정합니다.  
  
-   *database_principal*은 데이터베이스 사용자 또는 사용자 정의 데이터베이스 역할입니다.  
  
-   *database_principal*은 고정 데이터베이스 역할 또는 서버 보안 주체일 수 없습니다.  
  
WITH NAME = *new_name*  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](2008부터), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 사용자 정의 데이터베이스 역할의 이름을 변경하도록 지정합니다. 새 이름은 데이터베이스에 없는 이름이어야 합니다.  
  
 데이터베이스 역할의 이름을 변경하더라도 역할의 ID 번호, 소유자 또는 사용 권한은 변경되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 명령을 실행하려면 다음 권한이나 멤버 자격 중 하나 이상이 필요합니다.  
  
-   역할에 대한 **ALTER** 권한  
-   데이터베이스에 대한 **ALTER ANY ROLE** 권한  
-   **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격  
  
또한, 고정 데이터베이스 역할의 멤버를 변경하려면 다음이 필요합니다.  
  
-   **db_owner** 고정 데이터베이스 역할의 멤버 자격  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 고정 데이터베이스 역할의 이름은 변경할 수 없습니다.  
  
## <a name="metadata"></a>메타데이터  
 이 시스템 뷰에는 데이터베이스 역할 및 데이터베이스 보안 주체에 대한 정보가 포함됩니다.  
  
-   [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>예  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. 데이터베이스 역할의 이름 변경  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](2008부터), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 다음 예에서는 `buyers` 역할의 이름을 `purchasing`으로 변경합니다.   이 예제에서는 [AdventureWorks](https://msftdbprodsamples.codeplex.com/) 예제 데이터베이스에서 실행할 수 있습니다.
  
```sql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. 역할 멤버 추가 또는 제거  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](2012부터), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 다음 예에서는 `Sales`라는 데이터베이스 역할을 만듭니다. Barry라는 데이터베이스 사용자를 멤버 자격에 추가한 다음, Barry라는 멤버를 제거하는 방법을 보여줍니다.   이 예제에서는 [AdventureWorks](https://msftdbprodsamples.codeplex.com/) 예제 데이터베이스에서 실행할 수 있습니다.
  
```sql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
