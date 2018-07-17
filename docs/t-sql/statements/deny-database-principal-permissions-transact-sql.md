---
title: DENY 데이터베이스 보안 주체 사용 권한(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], permissions
- denying permissions [SQL Server], database roles
- denying permissions [SQL Server], database users
- permissions [SQL Server], database roles
- DENY statement, database roles
- database user permissions [SQL Server]
- permissions [SQL Server], application roles
- permissions [SQL Server], database users
- database permissions [SQL Server], denying
- DENY statement, application roles
- DENY statement, database users
- denying permissions [SQL Server], application roles
- application roles [SQL Server], permissions
ms.assetid: e2429a5d-e9be-4c05-be20-414d1038a63a
caps.latest.revision: 29
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: aa76a8c824b2390e54be422cdce5e668fee4c1e6
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36943109"
---
# <a name="deny-database-principal-permissions-transact-sql"></a>DENY 데이터베이스 보안 주체 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 사용자, 데이터베이스 역할 또는 응용 프로그램 역할에 대해 부여된 사용 권한을 거부합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DENY permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
     | [ ROLE :: database_role ]  
     | [ APPLICATION ROLE :: application_role ]  
    }  
    TO <database_principal> [ ,...n ]  
      [ CASCADE ]  
      [ AS <database_principal> ]  
  
<database_principal> ::=  
    Database_user   
  | Database_role   
  | Application_role   
  | Database_user_mapped_to_Windows_User   
  | Database_user_mapped_to_Windows_Group   
  | Database_user_mapped_to_certificate   
  | Database_user_mapped_to_asymmetric_key   
  | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>인수  
 *permission*  
 데이터베이스 보안 주체에 대해 거부할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 USER ::*database_user*  
 사용 권한을 거부할 사용자의 클래스 및 이름을 지정합니다. 범위 한정자(**::**)가 필요합니다.  
  
 ROLE ::*database_role*  
 사용 권한을 거부할 역할의 클래스 및 이름을 지정합니다. 범위 한정자(**::**)가 필요합니다.  
  
 APPLICATION ROLE ::*application_role*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 사용 권한을 거부할 응용 프로그램 역할의 클래스 및 이름을 지정합니다. 범위 한정자(**::**)가 필요합니다.  
  
 CASCADE  
 사용 권한이 거부된 보안 주체에게 사용 권한을 부여 받은 다른 보안 주체의 사용 권한도 거부됨을 나타냅니다.  
  
 AS \<database_principal>  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 취소하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다.  
  
 *Database_user*  
 데이터베이스 사용자를 지정합니다.  
  
 *Database_role*  
 데이터베이스 역할을 지정합니다.  
  
 *Application_role*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 응용 프로그램 역할을 지정합니다.  
  
 *Database_user_mapped_to_Windows_User*  
 Windows 사용자로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_Windows_Group*  
 Windows 그룹으로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_certificate*  
  인증서로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_asymmetric_key*  
  비대칭 키로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_with_no_login*  
 해당 서버 수준의 보안 주체가 없는 데이터베이스 사용자를 지정합니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="database-user-permissions"></a>데이터베이스 사용자 권한  
 데이터베이스 사용자는 사용 권한 계층에서 해당 사용자의 부모인 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 데이터베이스 사용자에 대해 거부할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|데이터베이스 사용자 권한|데이터베이스 사용자 권한에 포함된 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>데이터베이스 역할 사용 권한  
 데이터베이스 역할은 사용 권한 계층에서 해당 역할의 부모인 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 데이터베이스 역할에 대해 거부할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|데이터베이스 역할 사용 권한|데이터베이스 역할 사용 권한에 포함된 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>응용 프로그램 역할 사용 권한  
 응용 프로그램 역할은 사용 권한 계층에서 해당 역할의 부모인 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 응용 프로그램 역할에 대해 거부할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|응용 프로그램 역할 사용 권한|응용 프로그램 역할 사용 권한에 포함된 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>사용 권한  
 지정한 보안 주체에 대한 CONTROL 권한 또는 CONTROL 권한을 포함하는 상위 사용 권한이 필요합니다.  
  
 db_owner 고정 데이터베이스 역할의 멤버와 같이 데이터베이스에 대한 CONTROL 권한이 부여된 사용자는 데이터베이스의 모든 보안 개체에 대한 사용 권한을 거부할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-denying-control-permission-on-a-user-to-another-user"></a>1. 다른 사용자에게 사용자에 대한 CONTROL 권한 거부  
 다음 예에서는 사용자 `CONTROL`에 대해 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 사용자 `Wanida`에 대`RolandX` 권한을 거부합니다.  
  
```  
USE AdventureWorks2012;  
DENY CONTROL ON USER::Wanida TO RolandX;  
GO  
```  
  
### <a name="b-denying-view-definition-permission-on-a-role-to-a-user-to-which-it-was-granted-with-grant-option"></a>2. GRANT OPTION이 부여된 사용자에 대해 역할에 대한 VIEW DEFINITION 권한 거부  
 다음 예에서는 데이터베이스 사용자 `VIEW DEFINITION`에 대해 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 역할 `SammamishParking`에 대한 `JinghaoLiu` 권한을 거부합니다. 사용자 `CASCADE`에게 GRANT OPTION을 사용하여 VIEW DEFINITION 권한이 부여되었기 때문에 `JinghaoLiu` 옵션이 지정되었습니다.  
  
```  
USE AdventureWorks2012;  
DENY VIEW DEFINITION ON ROLE::SammamishParking   
    TO JinghaoLiu CASCADE;  
GO  
```  
  
### <a name="c-denying-impersonate-permission-on-a-user-to-an-application-role"></a>3. 응용 프로그램 역할에 대해 사용자에 대한 IMPERSONATE 권한 거부  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 응용 프로그램 역할 `IMPERSONATE`에 대해 사용자 `HamithaL`에 대한 `AccountsPayable17` 권한을 거부합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
```  
USE AdventureWorks2012;  
DENY IMPERSONATE ON USER::HamithaL TO AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>참고 항목  
 [GRANT 데이터베이스 보안 주체 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)   
 [REVOKE Database Principal Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
