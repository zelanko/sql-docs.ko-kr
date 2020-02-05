---
title: CREATE APPLICATION ROLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPLICATION_ROLE_TSQL
- CREATE APPLICATION ROLE
- sql13.swb.applicationrole.permissions.f1
- APPLICATION
- APPLICATION ROLE
- CREATE_APPLICATION_ROLE_TSQL
- APPLICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE APPLICATION ROLE statement
- application roles [SQL Server], creating
ms.assetid: 647386da-ee80-41cf-86c9-dd590f9d66b6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dc3caf4c1643405cc7db31e2a9c76cf70456b272
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73064590"
---
# <a name="create-application-role-transact-sql"></a>CREATE APPLICATION ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에 애플리케이션 역할을 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE APPLICATION ROLE application_role_name   
    WITH PASSWORD = 'password' [ , DEFAULT_SCHEMA = schema_name ]  
```  
  
## <a name="arguments"></a>인수  
 *application_role_name*  
 애플리케이션 역할의 이름을 지정합니다. 이 이름은 데이터베이스의 다른 보안 주체를 참조하는 데 사용된 이름이 아니어야 합니다.  
  
 PASSWORD **='** _password_ **'**  
 데이터베이스 사용자가 애플리케이션 역할을 활성화하는 데 사용할 암호를 지정합니다. 항상 강력한 암호를 사용해야 합니다. *password*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다.  
  
 DEFAULT_SCHEMA **=** _schema\_name_  
 서버가 이 역할에 대한 개체의 이름을 확인할 때 검색할 첫 번째 스키마를 지정합니다. DEFAULT_SCHEMA를 정의하지 않으면 애플리케이션 역할이 기본 스키마로 DBO를 사용합니다. *schema_name*은 데이터베이스에 존재하지 않는 스키마일 수 있습니다.  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]  
>  애플리케이션 역할 암호가 설정된 경우 암호 복잡성이 검사됩니다. 애플리케이션 역할을 호출하는 애플리케이션은 해당 암호를 저장해야 합니다. 애플리케이션 역할 암호는 항상 암호화된 상태로 저장되어야 합니다.  
  
 애플리케이션 역할은 [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 애플리케이션 역할을 사용하는 방법은 [애플리케이션 역할](../../relational-databases/security/authentication-access/application-roles.md)을 참조하십시오.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER ANY APPLICATION ROLE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 암호 `weekly_receipts` 및 기본 스키마로 `987Gbv876sPYY5m23`가 있는 `Sales`라는 애플리케이션 역할을 만듭니다.  
  
```sql  
CREATE APPLICATION ROLE weekly_receipts   
    WITH PASSWORD = '987G^bv876sPY)Y5m23'   
    , DEFAULT_SCHEMA = Sales;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [애플리케이션 역할](../../relational-databases/security/authentication-access/application-roles.md)   
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [ALTER APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [암호 정책](../../relational-databases/security/password-policy.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
