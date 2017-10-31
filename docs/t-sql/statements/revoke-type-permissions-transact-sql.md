---
title: "REVOKE 유형 사용 권한 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, types
- permissions [SQL Server], types
- type permissions [SQL Server]
ms.assetid: 3969c7e9-ca10-4c67-971b-25d2dfccf650
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7421493593b931d8178e2b4b3377ef7d9fcdd80
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-type-permissions-transact-sql"></a>REVOKE 유형 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  유형에 대한 사용 권한을 취소합니다.  
  
  ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON TYPE :: [ schema_name ]. type_name   
    { FROM | TO } <database_principal> [ ,...n ]   
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
 *사용 권한*  
 유형에 대해 취소할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 형식에 **::** [ *schema_name* ] **합니다.** *type_name*  
 사용 권한을 취소할 유형을 지정합니다. 범위 한정자 (**::**)가 필요 합니다. 경우 *schema_name* 를 지정 하지 않으면 기본 스키마가 사용 됩니다. 경우 *schema_name* 지정 된 스키마 범위 한정자 (**.**)가 필요 합니다.  
  
 {에서 | (를) \<데이터베이스 _ 보안 주체 > 있는 사용 권한을 취소할 보안 주체를 지정 합니다.  
  
 GRANT OPTION  
 지정한 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한이 취소됨을 나타냅니다. 사용 권한 자체는 취소되지 않습니다.  
  
> [!IMPORTANT]  
>  보안 주체에 GRANT 옵션 없이 지정된 사용 권한이 있는 경우 사용 권한 자체가 취소됩니다.  
  
 CASCADE  
 사용 권한이 취소된 보안 주체에게 사용 권한을 부여 받거나 거부당한 다른 보안 주체의 사용 권한도 취소됨을 나타냅니다.  
  
> [!CAUTION]  
>  WITH GRANT OPTION을 부여 받은 사용 권한이 연계되어 취소되면 해당 사용 권한의 GRANT 및 DENY가 모두 취소됩니다.  
  
 AS \<데이터베이스 _ 보안 주체 >이 쿼리를 실행 하는 보안 주체는 권한을 부여할 권한을 취소 파생 되는 보안 주체를 지정 합니다.  
  
 *Database_user*  
 데이터베이스 사용자를 지정합니다.  
  
 *Database_role*  
 데이터베이스 역할을 지정합니다.  
  
 *Application_role*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 응용 프로그램 역할을 지정합니다.  
  
 *Database_user_mapped_to_Windows_User*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Windows 사용자로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_Windows_Group*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Windows 그룹으로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_certificate*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 인증서로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_mapped_to_asymmetric_key*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 비대칭 키로 매핑된 데이터베이스 사용자를 지정합니다.  
  
 *Database_user_with_no_login*  
 해당 서버 수준의 보안 주체가 없는 데이터베이스 사용자를 지정합니다.  
  
## <a name="remarks"></a>주의  
 유형은 사용 권한 계층에서 해당 유형의 부모인 스키마에 포함된 스키마 수준 보안 개체입니다.  
  
> [!IMPORTANT]  
>  **GRANT**, **DENY** 및 **해지** 권한은 시스템 형식에 적용 되지 않습니다. 사용자 정의 형식에는 권한을 부여할 수 있습니다. 사용자 정의 형식에 대 한 자세한 내용은 참조 [SQL Server의 사용자 정의 형식 작업](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)합니다.  
  
 다음 표에는 유형에 대해 취소할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|유형 사용 권한|유형 사용 권한에 포함된 사용 권한|스키마 사용 권한에 포함된 사용 권한|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|CREATE 문을 실행하기 전에|CONTROL|CREATE 문을 실행하기 전에|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 해당 유형에 대한 CONTROL 권한이 필요합니다. AS 절을 사용하는 경우 지정한 보안 주체가 키를 소유해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 사용자 `VIEW DEFINITION`로부터 사용자 정의 형식 `PhoneNumber`에 대한 `KhalidR` 권한을 취소합니다. `CASCADE` 옵션은 `VIEW DEFINITION` 권한도 `KhalidR`이 부여한 보안 주체로부터 취소됨을 나타냅니다. `PhoneNumber`는 스키마 `Telemarketing`에 있습니다.  
  
```  
REVOKE VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    FROM KhalidR CASCADE;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [GRANT 유형 사용 권한 &#40; Transact SQL &#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)   
 [DENY 유형 사용 권한 &#40; Transact SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [보안 개체](../../relational-databases/security/securables.md)  
  
  


