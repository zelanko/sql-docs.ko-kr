---
title: GRANTY 개체 사용 권한(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], objects
- GRANT statement, objects
ms.assetid: c001c2e7-d092-43d4-8fa6-693b3ec4c3ea
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a90add62cdda0e127d84a60fadf7f1f1578c7a0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050823"
---
# <a name="grant-object-permissions-transact-sql"></a>GRANT 개체 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  테이블, 뷰, 테이블 반환 함수, 저장 프로시저, 확장 저장 프로시저, 스칼라 함수, 집계 함수, 서비스 큐 또는 동의어에 대한 사용 권한을 부여합니다.  
  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
GRANT <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
    TO <database_principal> [ ,...n ]   
    [ WITH GRANT OPTION ]  
    [ AS <database_principal> ]  
  
<permission> ::=  
    ALL [ PRIVILEGES ] | permission [ ( column [ ,...n ] ) ]  
  
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
 스키마 포함 개체에 대해 부여할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 ALL  
 ALL을 부여하더라도 일부 가능한 사용 권한은 부여되지 않습니다. ALL을 부여하는 것은 지정된 개체에 적용할 수 있는 모든 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92 사용 권한을 부여하는 것과 동일합니다. ALL의 의미는 다음과 같이 달라집니다.  
  
- 스칼라 함수 사용 권한: EXECUTE, REFERENCES  
- 테이블 반환 함수 사용 권한: DELETE, INSERT, REFERENCES, SELECT, UPDATE  
- 저장 프로시저 사용 권한: EXECUTE  
- 테이블 사용 권한: DELETE, INSERT, REFERENCES, SELECT, UPDATE  
- 뷰 사용 권한: DELETE, INSERT, REFERENCES, SELECT, UPDATE  
  
PRIVILEGES  
 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92 호환성을 위해 포함되었습니다. ALL의 동작을 변경하지 않습니다.  
  
*column*  
 사용 권한을 부여할 테이블, 뷰 또는 테이블 반환 함수의 열 이름을 지정합니다. 괄호 ( )가 필요합니다. SELECT, REFERENCES 및 UPDATE 사용 권한만 열에 대해 부여할 수 있습니다. *column*은 권한 절에 지정하거나 보안 이름 뒤에 지정할 수 있습니다.  
  
> [!CAUTION]  
>  테이블 수준의 DENY는 열 수준의 GRANT보다 우선하지 않습니다. 사용 권한 계층에서의 이러한 불일치는 이전 버전과의 호환성을 위해 유지되었습니다.  
  
 ON [ OBJECT :: ] [ *schema_name* ] . *object_name*  
 사용 권한을 거부할 개체를 지정합니다. *schema_name*을 지정한 경우 OBJECT 구는 선택 사항입니다. OBJECT 구가 사용된 경우 범위 한정자(::)가 필요합니다. *schema_name*을 지정하지 않은 경우 기본 스키마가 사용됩니다. *schema_name*을 지정하지 않은 경우 기본 스키마 범위 한정자(.)가 사용됩니다.  
  
 TO \<database_principal>  
 사용 권한을 부여할 보안 주체를 지정합니다.  
  
 WITH GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 이 보안 주체에 제공됨을 나타냅니다.  
  
 \<database_principal>로서 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다.  
  
 *Database_user*  
 데이터베이스 사용자를 지정합니다.  
  
 *Database_role*  
 데이터베이스 역할을 지정합니다.  
  
 *Application_role*  
 애플리케이션 역할을 지정합니다.  
  
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
  
> [!IMPORTANT]  
>  일부 경우에서 ALTER 사용 권한과 REFERENCE 사용 권한의 조합을 사용하면 피부여자가 데이터를 보거나 권한 없는 함수를 실행할 수 있습니다. 예를 들어 테이블에 대한 ALTER 권한과 함수에 대한 REFERENCE 권한을 가진 사용자는 함수를 통해 계산 열을 만들고 실행할 수 있습니다. 이 경우 계산 열에 대한 SELECT 사용 권한도 필요합니다.  
  
 개체에 대한 정보는 다양한 카탈로그 뷰에 표시됩니다. 자세한 내용은 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)을 참조하세요.  
  
 개체는 사용 권한 계층에서 해당 개체의 부모인 스키마에 포함된 스키마 수준 보안 개체입니다. 다음 표에는 개체에 대해 부여할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|개체 사용 권한|개체 사용 권한에 포함된 사용 권한|스키마 사용 권한에 포함된 사용 권한|  
|-----------------------|----------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|Delete|CONTROL|Delete|  
|CREATE 문을 실행하기 전에|CONTROL|CREATE 문을 실행하기 전에|  
|INSERT|CONTROL|INSERT|  
|RECEIVE|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|RECEIVE|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|VIEW CHANGE TRACKING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>사용 권한  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다.  
  
 AS 옵션을 사용하는 경우 다음과 같은 추가 요구 사항이 적용됩니다.  
  
|AS|필요한 추가 사용 권한|  
|--------|------------------------------------|  
|데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|Windows 로그인에 매핑된 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|Windows 그룹에 매핑된 데이터베이스 사용자|Windows 그룹의 멤버 자격, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|인증서에 매핑된 데이터베이스 사용자|db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|비대칭 키에 매핑된 데이터베이스 사용자|db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|서버 보안 주체에 매핑되지 않은 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|데이터베이스 역할|역할에 대한 ALTER 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|애플리케이션 역할|역할에 대한 ALTER 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
  
## <a name="examples"></a>예  
  
### <a name="a-granting-select-permission-on-a-table"></a>1\. 테이블에 대한 SELECT 사용 권한 부여  
 다음 예에서는 사용자 `SELECT`에게 `RosaQdM` 데이터베이스의 `Person.Address` 테이블에 대한 `AdventureWorks2012` 사용 권한을 부여합니다.  
  
```  
GRANT SELECT ON OBJECT::Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-a-stored-procedure"></a>2\. 저장 프로시저에 대한 EXECUTE 사용 권한 부여  
 다음 예에서는 `EXECUTE`이라는 애플리케이션 역할에 대해 저장 프로시저 `HumanResources.uspUpdateEmployeeHireInfo`에 대한 `Recruiting11` 사용 권한을 부여합니다.  
  
```  
USE AdventureWorks2012;   
GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO   
```  
  
### <a name="c-granting-references-permission-on-a-view-with-grant-option"></a>C. GRANT OPTION을 지정하여 뷰에 대한 REFERENCES 사용 권한 부여  
 다음 예에서는 `REFERENCES`을 지정하여 사용자 `BusinessEntityID`에게 `HumanResources.vEmployee` 뷰의 `Wanida` 열에 대한 `GRANT OPTION` 사용 권한을 부여합니다.  
  
```  
GRANT REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    TO Wanida WITH GRANT OPTION;  
GO  
```  
  
### <a name="d-granting-select-permission-on-a-table-without-using-the-object-phrase"></a>D. OBJECT 구를 사용하지 않고 테이블에 대한 SELECT 사용 권한 부여  
 다음 예에서는 사용자 `SELECT`에게 `RosaQdM` 데이터베이스의 `Person.Address` 테이블에 대한 `AdventureWorks2012` 사용 권한을 부여합니다.  
  
```  
GRANT SELECT ON Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="e-granting-select-permission-on-a-table-to-a-domain-account"></a>E. 도메인 계정에 테이블에 대한 SELECT 사용 권한 부여  
 다음 예에서는 사용자 `SELECT`에게 `AdventureWorks2012\RosaQdM` 데이터베이스의 `Person.Address` 테이블에 대한 `AdventureWorks2012` 사용 권한을 부여합니다.  
  
```  
GRANT SELECT ON Person.Address TO [AdventureWorks2012\RosaQdM];  
GO  
```  
  
### <a name="f-granting-execute-permission-on-a-procedure-to-a-role"></a>F. 역할에 프로시저에 대한 EXECUTE 사용 권한 부여  
 다음 예에서는 역할을 만든 다음 이 역할에 `EXECUTE` 데이터베이스의 `uspGetBillOfMaterials` 프로시저에 대한 `AdventureWorks2012` 사용 권한을 부여합니다.  
  
```  
CREATE ROLE newrole ;  
GRANT EXECUTE ON dbo.uspGetBillOfMaterials TO newrole ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [DENY 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [REVOKE 개체 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  

