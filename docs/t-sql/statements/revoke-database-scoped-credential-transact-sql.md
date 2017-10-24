---
title: "REVOKE 데이터베이스 범위 자격 증명 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- REVOKE DATABASE SCOPED CREDENTIAL
- REVOKE_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statements, database scoped credentials
- revoking permissions [SQL Server], database scoped credentials
ms.assetid: b73233c5-9afa-48ca-ba34-a9f86b9b1d2e
caps.latest.revision: 2
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d05f1829878d31593c56f65dd25660bec9dfa23e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-database-scoped-credential-transact-sql"></a>REVOKE 데이터베이스 범위 자격 증명 (Transact SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

  데이터베이스 범위 자격 증명에 대 한 권한을 취소합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>인수  
 GRANT OPTION FOR  
 지정된 사용 권한을 부여할 수 있는 권한이 취소됨을 나타냅니다. 사용 권한 자체는 취소되지 않습니다.  
  
> [!IMPORTANT]  
>  보안 주체에 GRANT 옵션 없이 지정된 사용 권한이 있는 경우 사용 권한 자체가 취소됩니다.  
  
 *사용 권한*  
 데이터베이스 범위 자격 증명에 취소할 수 있는 사용 권한을 지정 합니다. 아래와 같습니다.  
  
 ON 인증서 **::***credential_name*  
 사용 권한이 취소 되 고 데이터베이스 범위 자격 증명을 지정 합니다. 범위 한정자 "::"이 필요합니다.  
  
 *데이터베이스 _ 보안 주체*  
 사용 권한을 취소할 보안 주체를 지정합니다. 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
  
-   데이터베이스 역할  
  
-   응용 프로그램 역할  
  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
  
-   인증서에 매핑된 데이터베이스 사용자  
  
-   비대칭 키에 매핑된 데이터베이스 사용자  
  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
 CASCADE  
 사용 권한이 취소된 보안 주체에게 권한을 부여 받은 다른 보안 주체의 사용 권한도 취소됨을 나타냅니다.  
  
> [!CAUTION]  
>  WITH GRANT OPTION을 부여 받은 사용 권한이 연계되어 취소되면 해당 사용 권한의 GRANT 및 DENY가 모두 취소됩니다.  
  
 AS *revoking_principal*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 취소하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다. 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
  
-   데이터베이스 역할  
  
-   응용 프로그램 역할  
  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
  
-   인증서에 매핑된 데이터베이스 사용자  
  
-   비대칭 키에 매핑된 데이터베이스 사용자  
  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>주의  
 데이터베이스 범위 자격 증명은 데이터베이스 수준 보안 개체 사용 권한 계층에서 부모 데이터베이스에 포함 된 합니다. 데이터베이스 범위 자격 증명에 취소할 수 있는 가장 구체적이 고 제한 된 사용 권한은 암시적으로 포함 하는 보다 일반적인 사용 권한과 함께, 다음과 같습니다.  
  
|데이터베이스 범위 자격 증명 사용 권한|포함 된 데이터베이스 범위 자격 증명 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 데이터베이스 범위 자격 증명에 대 한 CONTROL 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [REVOKE (Transact SQL)](../../t-sql/statements/revoke-transact-sql.md)      
 [GRANT 데이터베이스 범위 자격 증명 (Transact SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)   
 [DENY 데이터베이스 범위 자격 증명 (Transact SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

