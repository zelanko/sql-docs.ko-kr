---
title: GRANT 스키마 사용 권한(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- schemas [SQL Server], permissions
- permissions [SQL Server], schemas
- GRANT statement, schemas
- granting permissions [SQL Server], schemas
ms.assetid: b2aa1fc8-e7af-45d2-9f80-737543c8aa95
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 03fe0d161a6c8c7315812b92eb74f52b25a3a812
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33073310"
---
# <a name="grant-schema-permissions-transact-sql"></a>GRANT 스키마 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  스키마에 대한 사용 권한을 부여합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
GRANT permission  [ ,...n ] ON SCHEMA :: schema_name  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>인수  
 *permission*  
 스키마에 대해 부여할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하십시오.  
  
 ON SCHEMA **::** schema *_name*  
 사용 권한을 부여할 스키마를 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
 *database_principal*  
 사용 권한을 부여할 보안 주체를 지정합니다. 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   응용 프로그램 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 이 보안 주체에 제공됨을 나타냅니다.  
  
AS *granting_principal*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다. 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   응용 프로그램 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  일부 경우에서 ALTER 사용 권한과 REFERENCE 사용 권한의 조합을 사용하면 피부여자가 데이터를 보거나 권한 없는 함수를 실행할 수 있습니다. 예를 들어, 테이블에 대한 ALTER 사용 권한과 함수에 대한 REFERENCE 사용 권한을 가진 사용자는 함수를 통해 계산 열을 만들고 실행할 수 있습니다. 이 경우 계산 열에 대한 SELECT 사용 권한도 있어야 합니다.  
  
 스키마는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 아래에는 스키마에 부여할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|스키마 사용 권한|스키마 사용 권한에 포함된 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|-----------------------|----------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SCHEMA|  
|CONTROL|CONTROL|CONTROL|  
|CREATE SEQUENCE|ALTER|ALTER ANY SCHEMA|  
|Delete|CONTROL|Delete|  
|CREATE 문을 실행하기 전에|CONTROL|CREATE 문을 실행하기 전에|  
|INSERT|CONTROL|INSERT|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|CONTROL|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
> [!CAUTION]  
>  스키마에 대한 ALTER 사용 권한을 가진 사용자는 소유권 체인을 사용하여 사용자의 액세스가 명시적으로 거부된 보안 개체를 포함하여 다른 스키마의 보안 개체에 액세스할 수 있습니다. 이는 참조하는 개체를 소유하는 보안 주체가 참조된 개체도 소유한 경우 참조된 개체에 대한 사용 권한 검사를 소유권 체인이 무시하기 때문입니다. 스키마에 대한 ALTER 사용 권한을 가진 사용자는 스키마 소유자가 소유하는 프로시저, 동의어 및 뷰를 만들 수 있습니다. 이러한 개체는 소유권 체인을 통해 스키마 소유자가 소유한 다른 스키마의 정보에 액세스할 수 있습니다. 가능한 경우 스키마 소유자가 다른 스키마도 소유하는 경우 스키마에 대한 ALTER 사용 권한을 부여하지 않도록 해야 합니다.  
  
 예를 들어 이 문제는 다음과 같은 시나리오에서 발생할 수 있습니다. 이러한 시나리오에서는 U1이라는 사용자에게 S1 스키마에 대한 ALTER 사용 권한이 있다고 가정합니다. S2 스키마의 T1이라는 테이블 개체에 대한 U1 사용자의 액세스는 거부됩니다. S1 스키마와 S2 스키마는 같은 소유자가 소유합니다.  
  
 U1 사용자에게 데이터베이스에 대한 CREATE PROCEDURE 사용 권한과 S1 스키마에 대한 EXECUTE 사용 권한이 있습니다. 그러므로 U1 사용자는 저장 프로시저를 만든 다음 이 저장 프로시저에서 거부된 개체 T1에 액세스할 수 있습니다.  
  
 U1 사용자에게 데이터베이스에 대한 CREATE SYNONY 사용 권한과 S1 스키마에 대한 SELECT 사용 권한이 있습니다. 그러므로 U1 사용자는 S1 스키마에 거부된 개체 T1에 대한 동의어를 만든 다음 이 동의어를 사용하여 거부된 개체 T1에 액세스할 수 있습니다.  
  
 U1 사용자에게 데이터베이스에 대한 CREATE VIEW 사용 권한과 S1 스키마에 대한 SELECT 사용 권한이 있습니다. 그러므로 U1 사용자는 S1 스키마에 거부된 개체 T1의 데이터를 쿼리하는 뷰를 만든 다음 이 뷰를 사용하여 거부된 개체 T1에 액세스할 수 있습니다.  
  
 자세한 내용은 Microsoft 기술 자료 문서 번호 914847을 참조하십시오.  
  
## <a name="permissions"></a>사용 권한  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다.  
  
 AS 옵션을 사용하는 경우 다음과 같은 추가 요구 사항이 적용됩니다.  
  
|AS *granting_principal*|필요한 추가 사용 권한|  
|------------------------------|------------------------------------|  
|데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|Windows 로그인에 매핑된 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|Windows 그룹에 매핑된 데이터베이스 사용자|Windows 그룹의 멤버 자격, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|인증서에 매핑된 데이터베이스 사용자|db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|비대칭 키에 매핑된 데이터베이스 사용자|db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|서버 보안 주체에 매핑되지 않은 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|데이터베이스 역할|역할에 대한 ALTER 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|응용 프로그램 역할|역할에 대한 ALTER 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
  
 개체 소유자는 소유하고 있는 개체에 대한 사용 권한을 부여할 수 있습니다. 보안 개체에 대한 CONTROL 사용 권한을 가진 보안 주체는 해당 보안 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
 sysadmin 고정 서버 역할의 멤버와 같이 CONTROL SERVER 사용 권한이 부여된 사용자는 서버의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다. db_owner 고정 데이터베이스 역할의 멤버와 같이 데이터베이스에 대한 CONTROL 사용 권한이 부여된 사용자는 데이터베이스의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다. 스키마에 대한 CONTROL 권한이 부여된 사용자는 스키마 내의 모든 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-granting-insert-permission-on-schema-humanresources-to-guest"></a>1. 게스트에게 HumanResources 스키마에 대한 INSERT 사용 권한 부여  
  
```  
GRANT INSERT ON SCHEMA :: HumanResources TO guest;  
```  
  
### <a name="b-granting-select-permission-on-schema-person-to-database-user-wiljo"></a>2. 데이터베이스 사용자 WilJo에게 Person 스키마에 대한 SELECT 사용 권한 부여  
  
```  
GRANT SELECT ON SCHEMA :: Person TO WilJo WITH GRANT OPTION;  
```  
  
## <a name="see-also"></a>참고 항목  
 [DENY Schema Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)   
 [REVOKE Schema Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-schema-permissions-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  
