---
title: GRANT Type Permissions(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
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
- permissions [SQL Server], types
- granting permissions [SQL Server], types
- GRANT statement, types
- type permissions [SQL Server]
ms.assetid: 14bd2fb3-1446-49c0-be87-c6a670317ed0
caps.latest.revision: 27
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7d3821d97198bdb69dd5ff49c357fc7aca8c25fc
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36941009"
---
# <a name="grant-type-permissions-transact-sql"></a>GRANT 유형 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  유형에 대한 사용 권한을 부여합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GRANT permission  [ ,...n ] ON TYPE :: [ schema_name . ] type_name  
    TO <database_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
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
 유형에 대해 부여할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 ON TYPE **::** [ *schema_name***.** ] *type_name*  
 사용 권한을 부여할 유형을 지정합니다. 범위 한정자(**::**)가 필요합니다. *schema_name*을 지정하지 않은 경우 기본 스키마가 사용됩니다. *schema_name*을 지정한 경우 스키마 범위 한정자(**.**)가 필요합니다.  
  
 \<database_principal>에 대해 사용 권한을 부여할 보안 주체를 지정합니다.  
  
 WITH GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 이 보안 주체에 제공됨을 나타냅니다.  
  
 \<database_principal>로서 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다.  
  
 *Database_user*  
 데이터베이스 사용자를 지정합니다.  
  
 *Database_role*  
 데이터베이스 역할을 지정합니다.  
  
 *Application_role*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지
  
 응용 프로그램 역할을 지정합니다.  
  
 *Database_user_mapped_to_Windows_User*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 Windows 사용자로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_Windows_Group*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 Windows 그룹으로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_certificate*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 인증서로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_asymmetric_key*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 비대칭 키로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_with_no_login*  
 해당 서버 수준의 보안 주체가 없는 데이터베이스 사용자를 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 유형은 사용 권한 계층에서 해당 유형의 부모인 스키마에 포함된 스키마 수준 보안 개체입니다.  
  
> [!IMPORTANT]  
>  **GRANT**, **DENY,** 및 **REVOKE** 권한은 시스템 형식에 적용되지 않습니다. 사용자 정의 형식에는 권한을 부여할 수 있습니다. 사용자 정의 형식에 대한 자세한 정보는 [SQL Server의 사용자 정의 형식 작업](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)을 참조합니다.  
  
 다음 표에는 유형에 대해 부여할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|유형 사용 권한|유형 사용 권한에 포함된 사용 권한|스키마 사용 권한에 포함된 사용 권한|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|CREATE 문을 실행하기 전에|CONTROL|CREATE 문을 실행하기 전에|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>사용 권한  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다.  
  
 AS 옵션을 사용하는 경우 다음과 같은 추가 요구 사항이 적용됩니다.  
  
|AS|필요한 추가 사용 권한|  
|--------|------------------------------------|  
|데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|Windows 로그인에 매핑된 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|Windows 그룹에 매핑된 데이터베이스 사용자|Windows 그룹의 멤버 자격, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|인증서에 매핑된 데이터베이스 사용자|**db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|비대칭 키에 매핑된 데이터베이스 사용자|**db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|서버 보안 주체에 매핑되지 않은 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|데이터베이스 역할|역할에 대한 ALTER 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|응용 프로그램 역할|역할에 대한 ALTER 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
  
## <a name="examples"></a>예  
 다음 예에서는 `VIEW DEFINITION`을 사용하여 사용자 `GRANT OPTION`에 대해 사용자 정의 형식 `PhoneNumber`에 대한 `KhalidR` 권한을 부여합니다. `PhoneNumber`는 `Telemarketing` 스키마에 있습니다.  
  
```  
GRANT VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    TO KhalidR WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [DENY Type Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [REVOKE 형식 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)   
 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

