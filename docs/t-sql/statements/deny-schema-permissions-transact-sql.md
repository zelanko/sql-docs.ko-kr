---
title: DENY Schema Permissions(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [SQL Server], schemas
- schemas [SQL Server], permissions
- permissions [SQL Server], schemas
- DENY statement, schemas
ms.assetid: 300a67c4-d226-4653-9e9f-7ae4d53fcf33
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 37b88f07571029e39080f38c1406ab89ec73b0a3
ms.sourcegitcommit: c3b190f8f87a4c80bc9126bb244896197a6dc453
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852878"
---
# <a name="deny-schema-permissions-transact-sql"></a>DENY 스키마 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

스키마에 대한 사용 권한을 거부합니다.  
  

![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql
DENY permission  [ ,...n ] } ON SCHEMA :: schema_name  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>인수  
*permission*  
스키마에 대해 거부할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 문서의 뒤에 나오는 주의 섹션을 참조하세요.  
  
ON SCHEMA **::** schema *_name*  
사용 권한이 거부된 스키마를 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
*database_principal*  
사용 권한이 거부된 보안 주체를 지정합니다. *database_principal*은 다음 보안 주체 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   애플리케이션 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체로 매핑되지 않은 데이터베이스 사용자  
  
CASCADE  
지정된 *database_principal*이 권한을 부여한 다른 모든 보안 주체에 대한 권한을 거부합니다.
  
*denying_principal*  
이 쿼리를 실행하는 보안 주체가 사용 권한을 거부하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다. *denying_principal*은 다음 보안 주체 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   애플리케이션 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체로 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>Remarks  
스키마는 데이터베이스 수준 보안 개체입니다. 사용 권한 계층의 부모인 데이터베이스에 의해 포함됩니다. 다음 표에는 스키마에서 거부될 수 있는 가장 구체적이고 제한된 사용 권한이 나열되어 있습니다. 표는 암시적으로 포함하는 보다 일반적인 사용 권한을 보여줍니다.  
  
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
  
## <a name="permissions"></a>Permissions  
스키마에 대한 CONTROL 권한이 필요합니다. AS 옵션을 사용하는 경우 지정한 보안 주체가 스키마를 소유해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[CREATE SCHEMA&#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
[DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
[사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
[보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
[sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
[HAS_PERMS_BY_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  
