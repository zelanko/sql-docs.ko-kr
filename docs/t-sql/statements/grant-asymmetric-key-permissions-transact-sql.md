---
title: GRANT Asymmetric Key Permissions(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], asymmetric keys
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- GRANT statement, asymmetric keys
ms.assetid: a70e2ee6-59b0-4543-b883-e9cbae6199be
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f128cbf86d30cabe0aa00ce7033b7cd5b04c93e3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68065599"
---
# <a name="grant-asymmetric-key-permissions-transact-sql"></a>GRANT 비대칭 키 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  비대칭 키에 대한 사용 권한을 부여합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
GRANT { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
       TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>인수  
 *permission*  
 비대칭 키에 부여할 수 있는 사용 권한을 지정합니다. 아래와 같습니다.  
  
 ON ASYMMETRIC KEY **::** _asymmetric_key_name_  
 사용 권한을 부여할 비대칭 키를 지정합니다. 범위 한정자 "::"이 필요합니다.  
  
 *database_principal*  
 사용 권한을 부여할 보안 주체를 지정합니다. 다음 중 하나  
  
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
 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다. 다음 중 하나  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   애플리케이션 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>설명  
 비대칭 키는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 아래에는 비대칭 키에 부여할 수 있는 가장 제한적인 사용 권한이 이러한 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|비대칭 키 권한|비대칭 키 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>사용 권한  
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
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
