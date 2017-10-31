---
title: ALTER ROLE (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3eaee2d346eda964545caa60cd7168b531f47ad9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-role-transact-sql"></a>ALTER ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  추가 또는 데이터베이스 역할에서 멤버를 제거 하거나 사용자 정의 데이터베이스 역할의 이름을 변경 합니다.  
  
> [!NOTE]  
>  역할을 변경 하려면 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]를 사용 하 여 [sp_addrolemember &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 및 [sp_droprolemember &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server (starting with 2012) and Azure SQL Database  
  
ALTER ROLE  role_name  
{  
       ADD MEMBER database_principal  
    |  DROP MEMBER database_principal  
    |  WITH NAME = new_name  
}  
[;]  
```  
  
 
```  
-- Syntax for SQL Server 2008 only  
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *role_name*  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2008부터 시작)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 변경 하려면 데이터베이스 역할을 지정 합니다.  
  
 멤버 추가 *데이터베이스 _ 보안 주체*l  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2012부터 시작)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 데이터베이스 역할의 구성원에 게는 데이터베이스 보안 주체를 추가 하려면 지정 합니다.  
  
-   *데이터베이스 _ 보안 주체* 데이터베이스 사용자 또는 사용자 정의 데이터베이스 역할입니다.  
  
-   *데이터베이스 _ 보안 주체* 고정된 데이터베이스 역할 또는 서버 보안 주체일 수 없습니다.  
  
DROP MEMBER *데이터베이스 _ 보안 주체*  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2012부터 시작)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 데이터베이스 역할의 멤버 자격에서 데이터베이스 보안 주체를 제거 하도록 지정 합니다.  
  
-   *데이터베이스 _ 보안 주체* 데이터베이스 사용자 또는 사용자 정의 데이터베이스 역할입니다.  
  
-   *데이터베이스 _ 보안 주체* 고정된 데이터베이스 역할 또는 서버 보안 주체일 수 없습니다.  
  
이름의 = *new_name*  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2008부터 시작)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 사용자 정의 데이터베이스 역할의 이름을 변경 하려면 지정 합니다. 새 이름이 데이터베이스에 이미 존재 하지 해야 합니다.  
  
 데이터베이스 역할의 이름을 변경하더라도 역할의 ID 번호, 소유자 또는 사용 권한은 변경되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 이 명령을 실행 하려면 하나 이상의 이러한 사용 권한 또는 멤버 자격이 필요 합니다.  
  
-   **ALTER** 역할에 대 한 권한  
-   **ALTER ANY ROLE** 데이터베이스에 대 한 권한  
-   멤버 자격이 **db_securityadmin** 고정된 데이터베이스 역할  
  
또한 고정된 데이터베이스 역할의 멤버 자격을 변경 하려면:  
  
-   멤버 자격이 **db_owner** 고정된 데이터베이스 역할  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 고정된 데이터베이스 역할의 이름을 변경할 수 없습니다.  
  
## <a name="metadata"></a>메타데이터  
 이러한 시스템 뷰는 데이터베이스 역할 및 데이터베이스 보안 주체에 대 한 정보를 포함합니다.  
  
-   [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>예  
  
### <a name="a-change-the-name-of-a-database-role"></a>1. 데이터베이스 역할의 이름 변경  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2008부터 시작)  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 다음 예에서는 `buyers` 역할의 이름을 `purchasing`으로 변경합니다. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>2. 역할 구성원 추가 또는 제거  
 **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2012부터 시작)  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 이 예에서는 라는 데이터베이스 역할을 만든 `Sales`합니다. 구성원 자격과 Barry 라는 데이터베이스 사용자를 추가 하 고 Barry 구성원을 제거 하는 방법을 보여 줍니다. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [역할 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP role&#40; Transact SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  

