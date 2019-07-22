---
title: GRANT Symmetric Key Permissions(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], permissions
- permissions [SQL Server], symmetric keys
- encryption [SQL Server], symmetric keys
- GRANT statement, symmetric keys
- cryptography [SQL Server], symmetric keys
- granting permissions [SQL Server], symmetric keys
ms.assetid: 5c61557f-67ae-4e55-b86d-713575b27cea
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a7c592af7f2971cc637c9049b8ca06a92a2f3c05
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050772"
---
# <a name="grant-symmetric-key-permissions-transact-sql"></a>GRANT 대칭 키 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  대칭 키에 대한 사용 권한을 부여합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GRANT permission [ ,...n ]    
    ON SYMMETRIC KEY :: symmetric_key_name   
    TO <database_principal> [ ,...n ] [ WITH GRANT OPTION ]  
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
 대칭 키에 부여할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 ON SYMMETRIC KEY ::*asymmetric_key_name*  
 사용 권한을 부여할 대칭 키를 지정합니다. 범위 한정자(::)가 필요합니다.  
  
 TO \<*database_principal*>  
 사용 권한을 부여할 보안 주체를 지정합니다.  
  
 WITH GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 이 보안 주체에 제공됨을 나타냅니다.  
  
 \<database_principal>로서 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다.  
  
 *Database_user*  
 데이터베이스 사용자를 지정합니다.  
  
 *Database_role*  
 데이터베이스 역할을 지정합니다.  
  
 *Application_role*  
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
 대칭 키에 대한 정보는 [sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 대칭 키는 사용 권한 계층에서 해당 대칭 키의 부모인 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 대칭 키에 부여할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|대칭 키 사용 권한|대칭 키 사용 권한에 포함된 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|------------------------------|-----------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SYMMETRIC KEY|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
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
|애플리케이션 역할|역할에 대한 ALTER 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
  
 보안 개체에 대한 CONTROL 사용 권한을 가진 보안 주체는 해당 보안 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
 sysadmin 고정 서버 역할의 멤버와 같이 CONTROL SERVER 사용 권한이 부여된 사용자는 서버의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다. db_owner 고정 데이터베이스 역할의 멤버와 같이 데이터베이스에 대한 CONTROL 사용 권한이 부여된 사용자는 데이터베이스의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스 사용자 `ALTER`에 대칭 키 `SamInventory42`에 대한 `HamidS` 권한을 부여합니다.  
  
```  
USE AdventureWorks2012;  
GRANT ALTER ON SYMMETRIC KEY::SamInventory42 TO HamidS;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [DENY 대칭 키 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)   
 [REVOKE Symmetric Key Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-symmetric-key-permissions-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

