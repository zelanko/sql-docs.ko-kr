---
title: GRANT Database Scoped Credential(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- GRANT DATABASE SCOPED CREDENTIAL
- GRANT_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], database scoped credential
- permissions [SQL Server], database scoped credential
- database scoped credential [SQL Server], permissions
- GRANT statement, database scoped credentials
ms.assetid: 501f2c8a-6aeb-41af-bf0b-974d17af33c0
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a30b96b42aabdd8511dcad542fed498c4ca26516
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589277"
---
# <a name="grant-database-scoped-credential-permissions-transact-sql"></a>GRANT Database Scoped Credential Permissions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  데이터베이스 범위 자격 증명에 대한 사용 권한을 부여합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
GRANT permission  [ ,...n ]    
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
## <a name="arguments"></a>인수  
 *permission*  
 데이터베이스 범위 자격 증명에 대해 부여할 수 있는 사용 권한을 지정합니다. 아래와 같습니다.  
  
 데이터베이스 범위 자격 증명에서 **::**_credential_name_  
 사용 권한을 부여하는 데이터베이스 범위 자격 증명을 지정합니다. 범위 한정자 "::"이 필요합니다.  
  
 *database_principal*  
 사용 권한을 부여할 보안 주체를 지정합니다. 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   애플리케이션 역할  
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
-   애플리케이션 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 범위 자격 증명은 사용 권한 계층에서 해당 사용자의 부모인 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 아래에는 데이터베이스 범위 자격 증명에 대해 부여할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|데이터베이스 범위 자격 증명 사용 권한|데이터베이스 범위 자격 증명 사용 권한에 포함된 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다.  
  
 AS 옵션을 사용하는 경우 다음과 같은 추가 요구 사항이 적용됩니다.  
  
|AS *granting_principal*|필요한 추가 사용 권한|  
|------------------------------|------------------------------------|  
|데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|Windows 로그인에 매핑된 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|Windows 그룹에 매핑된 데이터베이스 사용자|Windows 그룹의 멤버 자격, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|인증서에 매핑된 데이터베이스 사용자|**db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|비대칭 키에 매핑된 데이터베이스 사용자|**db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|서버 보안 주체에 매핑되지 않은 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|데이터베이스 역할|역할에 대한 ALTER 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
|애플리케이션 역할|역할에 대한 ALTER 권한, **db_securityadmin** 고정 데이터베이스 역할의 멤버 자격, **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 **sysadmin** 고정 서버 역할의 멤버 자격.|  
  
 개체 소유자는 소유하고 있는 개체에 대한 사용 권한을 부여할 수 있습니다. 보안 개체에 대한 CONTROL 사용 권한을 가진 보안 주체는 해당 보안 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
 **sysadmin** 고정 서버 역할의 멤버와 같이 CONTROL SERVER 권한이 부여된 사용자는 서버의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다. **db_owner** 고정 데이터베이스 역할의 멤버와 같이 데이터베이스에 대한 CONTROL 권한이 부여된 사용자는 데이터베이스의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다. 스키마에 대한 CONTROL 권한이 부여된 사용자는 스키마 내의 모든 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE 데이터베이스 범위 자격 증명(Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [DENY 데이터베이스 범위 자격 증명(Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
