---
title: ALTER LOGIN (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_LOGIN_TSQL
- ALTER LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER LOGIN statement
- change password
- mapping logins [SQL Server]
- logins [SQL Server], modifying
- passwords [SQL Server], modifying
- names [SQL Server], logins
- modifying login accounts
ms.assetid: e247b84e-c99e-4af8-8b50-57586e1cb1c5
caps.latest.revision: 68
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9dd47cb63c56dbbfb5f31ea3f7b2c8d4f45e9d73
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-login-transact-sql"></a>ALTER LOGIN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
ALTER LOGIN login_name   
    {   
    <status_option>   
    | WITH <set_option> [ ,... ]  
    | <cryptographic_credential_option>  
    }   
[;]  
  
<status_option> ::=  
        ENABLE | DISABLE  
  
<set_option> ::=              
    PASSWORD = 'password' | hashed_password HASHED  
    [   
      OLD_PASSWORD = 'oldpassword'  
      | <password_option> [<password_option> ]   
    ]  
    | DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
    | NAME = login_name  
    | CHECK_POLICY = { ON | OFF }  
    | CHECK_EXPIRATION = { ON | OFF }  
    | CREDENTIAL = credential_name  
    | NO CREDENTIAL  
  
<password_option> ::=   
    MUST_CHANGE | UNLOCK  
  
<cryptographic_credentials_option> ::=   
    ADD CREDENTIAL credential_name  
  | DROP CREDENTIAL credential_name  
```  
  
```  
-- Syntax for Azure SQL Database  
  
ALTER LOGIN login_name   
  {   
      <status_option>   
    | WITH <set_option> [ ,.. .n ]   
  }   
[;]  
  
<status_option> ::=  
    ENABLE | DISABLE  
  
<set_option> ::=   
    PASSWORD ='password'   
    [  
      OLD_PASSWORD ='oldpassword'  
    ]   
    | NAME = login_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER LOGIN login_name   
    {   
    <status_option>   
    | WITH <set_option> [ ,... ]  
    }   
  
<status_option> ::=ENABLE | DISABLE  
  
<set_option> ::=              
    PASSWORD ='password'   
    [   
      OLD_PASSWORD ='oldpassword'  
      | <password_option> [<password_option> ]   
    ]  
    | NAME = login_name  
    | CHECK_POLICY = { ON | OFF }  
    | CHECK_EXPIRATION = { ON | OFF }   
      
<password_option> ::=   
    MUST_CHANGE | UNLOCK  
```  
  
## <a name="arguments"></a>인수  
 *login_name*  
 변경할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다. 도메인 이름은 [domain\user] 형식과 같이 대괄호로 묶어야 합니다.  
  
 ENABLE | DISABLE  
 로그인을 활성화하거나 비활성화합니다. 로그인 비활성화는 이미 연결된 로그인 동작에 영향을 주지 않습니다. (사용 하 여는 `KILL` 문을 기존 연결을 종료 합니다.) 비활성화된 로그인은 권한을 유지하며 계속 가장될 수 있습니다.  
  
 암호 **='***암호***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 변경할 로그인의 암호를 지정합니다. 암호는 대소문자를 구분합니다.  
  
 SQL 데이터베이스에 대 한 활성 연결에서 재인증 (데이터베이스 엔진에 의해 수행 됨)를 필요로 하는 지속적으로 10 시간 이상 마다. 데이터베이스 엔진 재인증 제출 된 원래 암호를 사용 하 고 없는 사용자 입력이 필요 합니다. 성능상의 이유로 SQL 데이터베이스에서 암호가 재설정 될 때 연결이 됩니다 다시 인증 연결 풀링으로 인해 연결이 재설정 하는 경우에 합니다. 이 온-프레미스 SQL Server의 동작과에서 다릅니다. 연결이 초기 인증 후 암호가 변경 된 경우 연결을 종료 해야 하 고 새 암호를 사용 하 여 새 연결 합니다. KILL DATABASE CONNECTION 권한이 있는 사용자 KILL 명령을 사용 하 여 SQL 데이터베이스에 대 한 연결을 명시적으로 종료 수 있습니다. 자세한 내용은 참조 [kill&#40; Transact SQL &#41; ](../../t-sql/language-elements/kill-transact-sql.md).  
  
 암호  **=**  *hashed_password*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 HASHED 키워드에만 적용됩니다. 만들 로그인에 대한 암호의 해시된 값을 지정합니다.  
  
> [!IMPORTANT]  
>  로그인 계정(또는 포함된 데이터베이스 사용자)이 연결되고 인증되면 해당 연결에 해당 로그인에 대한 ID 정보가 캐시됩니다. Windows 인증 로그인을 위해 Windows 그룹의 멤버 자격에 대한 정보가 포함됩니다. 연결이 유지되는 한 로그인의 ID가 인증된 상태로 유지됩니다. 암호 재설정이나 Windows 그룹 멤버 자격 변경 등의 ID 변경 사항을 적용하려면 인증 기관(Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])에서 로그오프한 후 다시 로그인해야 합니다. **sysadmin** 고정 서버 역할의 멤버나 **ALTER ANY CONNECTION** 권한이 있는 로그인은 **KILL** 명령을 사용하여 연결을 종료하고 다시 연결하도록 할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기 또는 쿼리 편집기 창에 다중 연결할 때 연결 정보를 다시 사용합니다. 다시 연결하도록 모든 연결을 닫습니다.  
  
 HASHED  
   
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. PASSWORD 인수 다음에 입력한 암호가 이미 해시되었음을 지정합니다. 이 옵션을 선택하지 않으면 암호가 데이터베이스에 저장되기 전에 해시됩니다. 이 옵션은 두 서버 간에 로그인을 동기화하는 데에만 사용해야 합니다. HASHED 옵션을 사용하여 정기적으로 암호를 변경하면 안 됩니다.  
  
 OLD_PASSWORD **='***oldpassword***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 새 암호가 할당될 로그인의 현재 암호입니다. 암호는 대소문자를 구분합니다.  
  
 MUST_CHANGE  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 이 옵션을 지정한 경우 변경한 로그인을 처음 사용할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 업데이트된 암호를 묻는 메시지를 표시합니다.  
  
 DEFAULT_DATABASE  **=**  *데이터베이스*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 로그인에 할당할 기본 데이터베이스를 지정합니다.  
  
 DEFAULT_LANGUAGE  **=**  *언어*  
 
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 로그인에 할당할 기본 언어를 지정합니다. 모든 SQL 데이터베이스 로그인에 대 한 기본 언어는 영어 및 변경할 수 없습니다. 기본 언어는 `sa` 에서 로그인의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] linux에서 영어 이지만 변경할 수 있습니다.  
  
 이름 = *login_name*  
 이름을 바꿀 로그인의 새 이름입니다. Windows 로그인인 경우 새 이름에 해당하는 Windows 보안 주체의 SID가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로그인에 연결된 SID와 일치해야 합니다. 새 이름을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 백슬래시 문자를 포함할 수 없습니다 (\\).  
  
 CHECK_EXPIRATION = {ON | **OFF** }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 이 로그인에 암호 만료 정책을 적용할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 CHECK_POLICY  **=**  { **ON** | OFF}  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행 중인 컴퓨터의 Windows  암호 정책을 이 로그인에 적용하도록 지정합니다. 기본값은 ON입니다.  
  
 자격 증명 = *credential_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑될 자격 증명의 이름입니다. 자격 증명이 서버에 이미 있어야 합니다. 자세한 내용은 참조 [자격 증명 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)합니다. Sa 로그인에 자격 증명을 매핑할 수 없습니다.  
  
 NO CREDENTIAL  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 서버 자격 증명에 대한 로그인의 기존 매핑을 모두 제거합니다. 자세한 내용은 참조 [자격 증명 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)합니다.  
  
 UNLOCK  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 잠긴 로그인을 잠금 해제하도록 지정합니다.  
  
 ADD CREDENTIAL  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 EKM(확장 가능 키 관리) 공급자 자격 증명을 로그인에 추가합니다. 자세한 내용은 참조 [확장 가능 키 관리 &#40; Ekm&#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 DROP CREDENTIAL  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
로그인에서는 확장 가능 키 관리 (EKM) 공급자 자격 증명을 제거합니다. 자세한 내용은 참조 하십시오. [확장 가능 키 관리 &#40; Ekm&#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>주의  
 CHECK_POLICY를 ON으로 설정하면 HASHED 인수를 사용할 수 없습니다.  
  
 CHECK_POLICY가 ON으로 변경되면 다음 동작이 수행됩니다.  
  
-   암호 기록이 현재 암호 해시 값으로 초기화됩니다.  
  
 CHECK_POLICY가 OFF로 변경되면 다음 동작이 수행됩니다.  
  
-   CHECK_EXPIRATION도 OFF로 설정됩니다.  
  
-   암호 기록이 삭제됩니다.  
  
-   값 *lockout_time* 다시 설정 됩니다.  
  
MUST_CHANGE를 지정한 경우에는 CHECK_EXPIRATION  및 CHECK_POLICY를 ON으로 설정해야 합니다. 그렇지 않으면 문이 실패합니다.  
  
CHECK_POLICY를 OFF로 설정한 경우에는 CHECK_EXPIRATION을 ON으로 설정할 수 없습니다. 이 옵션 조합을 사용하면 ALTER LOGIN 문이 실패합니다.  
  
ALTER_LOGIN에 DISABLE 인수를 사용하여 Windows 그룹에 대한 액세스를 거부할 수 없습니다. 예를 들어 ALTER_LOGIN [*domain\group*] DISABLE 다음과 같은 오류 메시지가 반환 됩니다.  
  
 "메시지 15151, 수준 16, 상태 1, 줄 1  
  
 "로그인을 변경할 수 없습니다 '*Domain\Group*' 때문에 존재 하지 않는 또는 권한이 없습니다."  
  
 이것은 의도적인 것입니다.  
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)], 한 연결을 인증 하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시 됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 데이터베이스에 최신 버전의 로그인 테이블에 있는지 확인 하려면 실행할 [DBCC FLUSHAUTHCACHE &#40; Transact SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 ALTER ANY LOGIN 권한이 필요합니다.  
  
 CREDENTIAL 옵션을 사용하는 경우에는 ALTER ANY CREDENTIAL 권한도 필요합니다.  
  
 변경 되는 로그인의 멤버인 경우는 **sysadmin** 고정된 서버 역할 또는 CONTROL SERVER 권한의 피부 여자에 게 CONTROL SERVER 권한도 필요 다음 변경 내용을 적용할 때:  
  
-   이전 암호를 제공하지 않고 암호를 다시 설정  
  
-   MUST_CHANGE, CHECK_POLICY 또는 CHECK_EXPIRATION 활성화  
  
-   로그인 이름 변경  
  
-   로그인 활성화 또는 비활성화  
  
-   로그인을 다른 자격 증명에 매핑  
  
 보안 주체는 자신이 소유하는 로그인의 암호, 기본 언어 및 기본 데이터베이스를 변경할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-enabling-a-disabled-login"></a>1. 비활성화 된 로그인 활성화  
 다음 예에서는 `Mary5` 로그인을 활성화합니다.  
  
```tsql  
ALTER LOGIN Mary5 ENABLE;  
```  
  
### <a name="b-changing-the-password-of-a-login"></a>2. 로그인 암호 변경  
 다음 예에서는 `Mary5` 로그인의 암호를 강력한 암호로 변경합니다.  
  
```tsql  
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';  
```  
  
### <a name="c-changing-the-name-of-a-login"></a>3. 로그인 이름 변경  
 다음 예에서는 `Mary5` 로그인의 이름을 `John2`로 변경합니다.  
  
```tsql  
ALTER LOGIN Mary5 WITH NAME = John2;  
```  
  
### <a name="d-mapping-a-login-to-a-credential"></a>4. 로그인을 자격 증명에 매핑  
 다음 예에서는 `John2` 로그인을 `Custodian04` 자격 증명에 매핑합니다.  
  
```tsql  
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;  
```  
  
### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>5. 로그인을 확장 가능 키 관리 자격 증명에 매핑  
 다음 예에서는 `Mary5` 로그인을 `EKMProvider1` EKM 자격 증명에 매핑합니다.  
  
 
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```tsql  
ALTER LOGIN Mary5  
ADD CREDENTIAL EKMProvider1;  
GO  
```  
  
### <a name="f-unlocking-a-login"></a>6. 로그인 잠금 해제  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 잠금을 해제하려면 ****를 원하는 계정 암호로 바꾸고 다음 문을 실행합니다.  
  
  
```tsql  
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;  

GO  
```  
  
 암호를 변경하지 않고 로그인의 잠금을 해제하려면 검사 정책을 해제한 다음 다시 설정합니다.  
  
```tsql  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;  
GO  
```  
  
### <a name="g-changing-the-password-of-a-login-using-hashed"></a>7. HASHED를 사용하여 로그인 암호 변경  
 다음 예에서는 `TestUser` 로그인의 암호를 이미 해시된 값으로 변경합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```tsql  
ALTER LOGIN TestUser WITH   
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;  
GO  
```  
  
 
  
## <a name="see-also"></a>관련 항목:  
 [자격 증명 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [DROP login&#40; Transact SQL &#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  



