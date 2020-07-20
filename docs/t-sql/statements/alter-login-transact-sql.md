---
title: ALTER LOGIN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0610ec89a4475b9eb60922b1d52c7005d5692bb0
ms.sourcegitcommit: 7ce4a81c1b91239c8871c50f97ecaf387f439f6c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86217801"
---
# <a name="alter-login-transact-sql"></a>ALTER LOGIN(Transact-SQL)

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정의 속성을 변경합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="click-a-product"></a>제품을 클릭하세요.

다음 행에서 관심이 있는 제품 이름을 클릭합니다. 클릭하면 웹페이지의 여기에서 클릭한 제품에 적절한 다른 콘텐츠를 표시합니다.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||||
|-|-|-|-|-|
|**_\* SQL Server \*_** &nbsp;|[SQL Database<br />단일 데이터베이스/탄력적 풀](alter-login-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />관리되는 인스턴스](alter-login-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](alter-login-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System(PDW)](alter-login-transact-sql.md?view=aps-pdw-2016)
||||||

&nbsp;

## <a name="sql-server"></a>SQL Server

## <a name="syntax"></a>구문

```syntaxsql
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

## <a name="arguments"></a>인수

*login_name* 변경할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다. 도메인 이름은 [domain\user] 형식과 같이 대괄호로 묶어야 합니다.

ENABLE | DISABLE 로그인을 사용하거나 사용하지 않도록 설정합니다. 로그인 비활성화는 이미 연결된 로그인 동작에 영향을 주지 않습니다. (기존 연결을 종료하려면 `KILL` 문을 사용합니다.) 비활성화된 로그인은 권한을 유지하며 계속 가장될 수 있습니다.

PASSWORD **='** _password_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 변경할 로그인의 암호를 지정합니다. 암호는 대소문자를 구분합니다.

PASSWORD **=** _hashed\_password_ HASHED 키워드에만 적용됩니다. 만들 로그인에 대한 암호의 해시된 값을 지정합니다.

> [!IMPORTANT]
> 로그인 계정(또는 포함된 데이터베이스 사용자)이 연결되고 인증되면 해당 연결에 해당 로그인에 대한 ID 정보가 캐시됩니다. Windows 인증 로그인을 위해 Windows 그룹의 멤버 자격에 대한 정보가 포함됩니다. 연결이 유지되는 한 로그인의 ID가 인증된 상태로 유지됩니다. 암호 재설정이나 Windows 그룹 멤버 자격 변경 등의 ID 변경 사항을 적용하려면 인증 기관(Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])에서 로그오프한 후 다시 로그인해야 합니다. **sysadmin** 고정 서버 역할의 멤버나 **ALTER ANY CONNECTION** 권한이 있는 로그인은 **KILL** 명령을 사용하여 연결을 종료하고 다시 연결하도록 할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기 또는 쿼리 편집기 창에 다중 연결할 때 연결 정보를 다시 사용합니다. 다시 연결하도록 모든 연결을 닫습니다.

HASHED [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. PASSWORD 인수 다음에 입력한 암호가 이미 해시되었음을 지정합니다. 이 옵션을 선택하지 않으면 암호가 데이터베이스에 저장되기 전에 해시됩니다. 이 옵션은 두 서버 간에 로그인을 동기화하는 데에만 사용해야 합니다. HASHED 옵션을 사용하여 정기적으로 암호를 변경하면 안 됩니다.

OLD_PASSWORD **='** _oldpassword_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 새 암호가 할당될 로그인의 현재 암호입니다. 암호는 대소문자를 구분합니다.

MUST_CHANGE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 이 옵션을 지정한 경우 변경한 로그인을 처음 사용할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 업데이트된 암호를 묻는 메시지를 표시합니다.

DEFAULT_DATABASE **=** _database_ 로그인에 할당할 기본 데이터베이스를 지정합니다.

DEFAULT_LANGUAGE **=** _language_ 로그인에 할당할 기본 언어를 지정합니다. 모든 SQL Database 로그인의 기본 언어는 영어이며 변경할 수 없습니다. Linux의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 `sa` 로그인의 기본 언어는 영어지만 변경할 수 있습니다.

NAME = *login_name* 이름을 바꿀 로그인의 새 이름입니다. Windows 로그인인 경우 새 이름에 해당하는 Windows 보안 주체의 SID가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로그인에 연결된 SID와 일치해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 새 이름에는 백슬래시(\\)를 사용할 수 없습니다.

CHECK_EXPIRATION = { ON | **OFF** } [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 이 로그인에 암호 만료 정책을 적용할지 여부를 지정합니다. 기본값은 OFF입니다.

CHECK_POLICY **=** { **ON** | OFF } [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 컴퓨터의 Windows 암호 정책을 이 로그인에 적용하도록 지정합니다. 기본값은 ON입니다.

CREDENTIAL = *credential_name*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑할 자격 증명의 이름입니다. 자격 증명이 서버에 이미 있어야 합니다. 자세한 내용은 [자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)을 참조하세요. 자격 증명은 sa 로그인으로 매핑할 수 없습니다.

NO CREDENTIAL 서버 자격 증명에 대한 로그인의 기존 매핑을 모두 제거합니다. 자세한 내용은 [자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)을 참조하세요.

UNLOCK [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 잠긴 로그인을 잠금 해제하도록 지정합니다.

ADD CREDENTIAL EKM(확장 가능 키 관리) 공급자 자격 증명을 로그인에 추가합니다. 자세한 내용은 [EKM(확장 가능 키 관리)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)을 참조하세요.

DROP CREDENTIAL EKM(확장 가능 키 관리) 공급자 자격 증명을 로그인에서 제거합니다. 자세한 내용은 [EKM(확장 가능 키 관리)](../.. /relational-databases/security/encryption/extensible-key-management-ekm.md)를 참조하세요.

## <a name="remarks"></a>설명

CHECK_POLICY를 ON으로 설정하면 HASHED 인수를 사용할 수 없습니다.

CHECK_POLICY가 ON으로 변경되면 다음 동작이 수행됩니다.

- 암호 기록이 현재 암호 해시 값으로 초기화됩니다.

  CHECK_POLICY가 OFF로 변경되면 다음 동작이 수행됩니다.

- CHECK_EXPIRATION도 OFF로 설정됩니다.
- 암호 기록이 삭제됩니다.
- *lockout_time*의 값이 재설정됩니다.

MUST_CHANGE를 지정한 경우에는 CHECK_EXPIRATION  및 CHECK_POLICY를 ON으로 설정해야 합니다. 그렇지 않으면 문이 실패합니다.

CHECK_POLICY를 OFF로 설정한 경우에는 CHECK_EXPIRATION을 ON으로 설정할 수 없습니다. 이 옵션 조합을 사용하면 ALTER LOGIN 문이 실패합니다.

ALTER LOGIN에 DISABLE 인수를 사용하여 Windows 그룹에 대한 액세스를 거부할 수 없습니다. 예를 들어 ALTER LOGIN [*domain\group*] DISABLE은 다음 오류 메시지를 반환합니다.

    `"Msg 15151, Level 16, State 1, Line 1
    "Cannot alter the login '*Domain\Group*', because it does not exist or you do not have permission."`

    This is by design.
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 강제 실행하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.

## <a name="permissions"></a>사용 권한

ALTER ANY LOGIN 권한이 필요합니다.

CREDENTIAL 옵션을 사용하는 경우에는 ALTER ANY CREDENTIAL 권한도 필요합니다.

변경되는 로그인이 **sysadmin** 고정 서버 역할의 멤버이거나 CONTROL SERVER 권한의 피부여자인 경우에는 다음과 같은 변경을 수행할 때 CONTROL SERVER 권한도 필요합니다.

- 이전 암호를 제공하지 않고 암호를 다시 설정
- MUST_CHANGE, CHECK_POLICY 또는 CHECK_EXPIRATION 활성화
- 로그인 이름 변경
- 로그인 활성화 또는 비활성화
- 로그인을 다른 자격 증명에 매핑

보안 주체는 자신이 소유하는 로그인의 암호, 기본 언어 및 기본 데이터베이스를 변경할 수 있습니다.

## <a name="examples"></a>예제

### <a name="a-enabling-a-disabled-login"></a>A. 비활성화된 로그인 활성화

다음 예에서는 `Mary5` 로그인을 활성화합니다.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. 로그인 암호 변경

다음 예에서는 `Mary5` 로그인의 암호를 강력한 암호로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-password-of-a-login-when-logged-in-as-the-login"></a>C. 로그인으로 로그인할 때 로그인 암호 변경

현재 로그인되어 있는 로그인 암호의 변경을 시도하지만 `ALTER ANY LOGIN` 권한이 없는 경우 `OLD_PASSWORD` 옵션을 지정해야 합니다.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>' OLD_PASSWORD = '<oldWeakPasswordHere>';
```

### <a name="d-changing-the-name-of-a-login"></a>D. 로그인 이름 변경

다음 예에서는 `Mary5` 로그인의 이름을 `John2`로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="e-mapping-a-login-to-a-credential"></a>E. 로그인을 자격 증명에 매핑

다음 예에서는 `John2` 로그인을 `Custodian04` 자격 증명에 매핑합니다.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="f-mapping-a-login-to-an-extensible-key-management-credential"></a>F. 로그인을 확장 가능 키 관리 자격 증명에 매핑

다음 예에서는 `Mary5` 로그인을 `EKMProvider1` EKM 자격 증명에 매핑합니다.

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. 로그인 잠금 해제

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 잠금을 해제하려면 \*\*\*\*를 원하는 계정 암호로 바꾸고 다음 문을 실행합니다.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

암호를 변경하지 않고 로그인의 잠금을 해제하려면 검사 정책을 해제한 다음 다시 설정합니다.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. HASHED를 사용하여 로그인 암호 변경

다음 예에서는 `TestUser` 로그인의 암호를 이미 해시된 값으로 변경합니다.

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

## <a name="see-also"></a>참고 항목

- [자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM(확장 가능 키 관리)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-login-transact-sql.md?view=sql-server-2017)|**_\*SQL Database<br />단일 데이터베이스/탄력적 풀\*_**|[SQL Database<br />관리되는 인스턴스](alter-login-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](alter-login-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System(PDW)](alter-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-single-databaseelastic-pool"></a>Azure SQL Database 단일 데이터베이스/탄력적 풀

## <a name="sql-server"></a>SQL Server

## <a name="syntax"></a>구문

```syntaxsql
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

## <a name="arguments"></a>인수

*login_name* 변경할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다. 도메인 이름은 [domain\user] 형식과 같이 대괄호로 묶어야 합니다.

ENABLE | DISABLE 로그인을 사용하거나 사용하지 않도록 설정합니다. 로그인 비활성화는 이미 연결된 로그인 동작에 영향을 주지 않습니다. (기존 연결을 종료하려면 `KILL` 문을 사용합니다.) 비활성화된 로그인은 권한을 유지하며 계속 가장될 수 있습니다.

PASSWORD **='** _password_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 변경할 로그인의 암호를 지정합니다. 암호는 대소문자를 구분합니다.

SQL Database에 대한 활성 연결을 지속하기 위해서는 적어도 10시간 마다 다시 인증해야 합니다(데이터베이스 엔진에서 수행됨). 데이터베이스 엔진은 원래 제출된 암호를 사용하여 다시 인증을 시도하며, 사용자 입력은 필요하지 않습니다. 성능상의 이유로 암호를 SQL Database에서 다시 설정한 경우 연결 풀링으로 인해 연결이 재설정되더라도 연결은 다시 인증되지 않습니다. 이는 온-프레미스 SQL Server의 동작과 다릅니다. 초기에 연결을 인증한 후 암호를 변경하면 연결을 종료하고 새 암호를 사용하여 새 연결을 설정해야 합니다. KILL DATABASE CONNECTION 권한이 있는 사용자는 KILL 명령을 사용하여 SQL Database에 대한 연결을 명시적으로 종료할 수 있습니다. 자세한 내용은 [KILL](../../t-sql/language-elements/kill-transact-sql.md)을 참조하세요.

> [!IMPORTANT]
> 로그인 계정(또는 포함된 데이터베이스 사용자)이 연결되고 인증되면 해당 연결에 해당 로그인에 대한 ID 정보가 캐시됩니다. Windows 인증 로그인을 위해 Windows 그룹의 멤버 자격에 대한 정보가 포함됩니다. 연결이 유지되는 한 로그인의 ID가 인증된 상태로 유지됩니다. 암호 재설정이나 Windows 그룹 멤버 자격 변경 등의 ID 변경 사항을 적용하려면 인증 기관(Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])에서 로그오프한 후 다시 로그인해야 합니다. **sysadmin** 고정 서버 역할의 멤버나 **ALTER ANY CONNECTION** 권한이 있는 로그인은 **KILL** 명령을 사용하여 연결을 종료하고 다시 연결하도록 할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기 또는 쿼리 편집기 창에 다중 연결할 때 연결 정보를 다시 사용합니다. 다시 연결하도록 모든 연결을 닫습니다.

OLD_PASSWORD **='** _oldpassword_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 새 암호가 할당될 로그인의 현재 암호입니다. 암호는 대소문자를 구분합니다.

NAME = *login_name* 이름을 바꿀 로그인의 새 이름입니다. Windows 로그인인 경우 새 이름에 해당하는 Windows 보안 주체의 SID가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로그인에 연결된 SID와 일치해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 새 이름에는 백슬래시(\\)를 사용할 수 없습니다.

## <a name="remarks"></a>설명

[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 강제 실행하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.

## <a name="permissions"></a>사용 권한

ALTER ANY LOGIN 권한이 필요합니다.

변경되는 로그인이 **sysadmin** 고정 서버 역할의 멤버이거나 CONTROL SERVER 권한의 피부여자인 경우에는 다음과 같은 변경을 수행할 때 CONTROL SERVER 권한도 필요합니다.

- 이전 암호를 제공하지 않고 암호를 다시 설정
- 로그인 이름 변경
- 로그인 활성화 또는 비활성화
- 로그인을 다른 자격 증명에 매핑

보안 주체는 자체 로그인에 대한 암호를 변경할 수 있습니다.

## <a name="examples"></a>예제

이러한 예제에는 다른 SQL 제품 사용에 대한 예제도 포함되어 있습니다. 위에서 지원되는 인수를 참조하세요.

### <a name="a-enabling-a-disabled-login"></a>A. 비활성화된 로그인 활성화

다음 예에서는 `Mary5` 로그인을 활성화합니다.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. 로그인 암호 변경

다음 예에서는 `Mary5` 로그인의 암호를 강력한 암호로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-name-of-a-login"></a>C. 로그인 이름 변경

다음 예에서는 `Mary5` 로그인의 이름을 `John2`로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="d-mapping-a-login-to-a-credential"></a>D. 로그인을 자격 증명에 매핑

다음 예에서는 `John2` 로그인을 `Custodian04` 자격 증명에 매핑합니다.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. 로그인을 확장 가능 키 관리 자격 증명에 매핑

다음 예에서는 `Mary5` 로그인을 `EKMProvider1` EKM 자격 증명에 매핑합니다.


**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. 로그인 잠금 해제

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 잠금을 해제하려면 \*\*\*\*를 원하는 계정 암호로 바꾸고 다음 문을 실행합니다.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

암호를 변경하지 않고 로그인의 잠금을 해제하려면 검사 정책을 해제한 다음 다시 설정합니다.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. HASHED를 사용하여 로그인 암호 변경

다음 예에서는 `TestUser` 로그인의 암호를 이미 해시된 값으로 변경합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

## <a name="see-also"></a>참고 항목

- [자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM(확장 가능 키 관리)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-login-transact-sql.md?view=sql-server-2017)|[SQL Database<br />단일 데이터베이스/탄력적 풀](alter-login-transact-sql.md?view=azuresqldb-current)|**_\* SQL Database<br />관리되는 인스턴스 \*_**|[Azure Synapse<br />Analytics](alter-login-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System(PDW)](alter-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Azure SQL Database Managed Instance

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for SQL Server and Azure SQL Database managed instance

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

> [!NOTE]
> 생성 후 관리형 인스턴스 기능에 대한 Azure AD 관리자가 변경되었습니다. 자세한 내용은 [MI의 새 Azure AD 관리자 기능](/azure/sql-database/sql-database-aad-authentication-configure#new-azure-ad-admin-functionality-for-mi)을 참조하세요.

```syntaxsql
-- Syntax for Azure SQL Database managed instance using Azure AD logins

ALTER LOGIN login_name
  {
      <status_option>
    | WITH <set_option> [ ,.. .n ]
  }
[;]

<status_option> ::=
    ENABLE | DISABLE

<set_option> ::=
     DEFAULT_DATABASE = database
   | DEFAULT_LANGUAGE = language
```

## <a name="arguments"></a>인수

### <a name="arguments-applicable-to-sql-and-azure-ad-logins"></a>SQL 및 Azure AD 로그인에 적용 가능한 인수

*login_name* 변경할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다. Azure AD 로그인은 user@domain으로 지정해야 합니다. 예를 들어 john.smith@contoso.com이나 Azure AD 그룹 또는 애플리케이션 이름으로 지정합니다. Azure AD 로그인의 경우 *login_name*은 master 데이터베이스에서 만든 기존 Azure AD 로그인과 일치해야 합니다.

ENABLE | DISABLE 로그인을 사용하거나 사용하지 않도록 설정합니다. 로그인 비활성화는 이미 연결된 로그인 동작에 영향을 주지 않습니다. (기존 연결을 종료하려면 `KILL` 문을 사용합니다.) 비활성화된 로그인은 권한을 유지하며 계속 가장될 수 있습니다.

DEFAULT_DATABASE **=** _database_ 로그인에 할당할 기본 데이터베이스를 지정합니다.

DEFAULT_LANGUAGE **=** _language_ 로그인에 할당할 기본 언어를 지정합니다. 모든 SQL Database 로그인의 기본 언어는 영어이며 변경할 수 없습니다. Linux의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 `sa` 로그인의 기본 언어는 영어지만 변경할 수 있습니다.

### <a name="arguments-applicable-only-to-sql-logins"></a>SQL 로그인에만 적용되는 인수

PASSWORD **='** _password_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 변경할 로그인의 암호를 지정합니다. 암호는 대소문자를 구분합니다. 암호는 Azure AD 로그인과 같이 외부 로그인과 함께 사용할 때도 적용되지 않습니다.

SQL Database에 대한 활성 연결을 지속하기 위해서는 적어도 10시간 마다 다시 인증해야 합니다(데이터베이스 엔진에서 수행됨). 데이터베이스 엔진은 원래 제출된 암호를 사용하여 다시 인증을 시도하며, 사용자 입력은 필요하지 않습니다. 성능상의 이유로 암호를 SQL Database에서 다시 설정한 경우 연결 풀링으로 인해 연결이 재설정되더라도 연결은 다시 인증되지 않습니다. 이는 온-프레미스 SQL Server의 동작과 다릅니다. 초기에 연결을 인증한 후 암호를 변경하면 연결을 종료하고 새 암호를 사용하여 새 연결을 설정해야 합니다. KILL DATABASE CONNECTION 권한이 있는 사용자는 KILL 명령을 사용하여 SQL Database에 대한 연결을 명시적으로 종료할 수 있습니다. 자세한 내용은 [KILL](../../t-sql/language-elements/kill-transact-sql.md)을 참조하세요.

PASSWORD **=** _hashed\_password_ HASHED 키워드에만 적용됩니다. 만들 로그인에 대한 암호의 해시된 값을 지정합니다.

HASHED [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. PASSWORD 인수 다음에 입력한 암호가 이미 해시되었음을 지정합니다. 이 옵션을 선택하지 않으면 암호가 데이터베이스에 저장되기 전에 해시됩니다. 이 옵션은 두 서버 간에 로그인을 동기화하는 데에만 사용해야 합니다. HASHED 옵션을 사용하여 정기적으로 암호를 변경하면 안 됩니다.

OLD_PASSWORD **='** _oldpassword_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 새 암호가 할당될 로그인의 현재 암호입니다. 암호는 대소문자를 구분합니다.

MUST_CHANGE<br>
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 이 옵션을 지정한 경우 변경한 로그인을 처음 사용할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 업데이트된 암호를 묻는 메시지를 표시합니다.

NAME = *login_name* 이름을 바꿀 로그인의 새 이름입니다. 로그인이 Windows 로그인인 경우 새 이름에 해당하는 Windows 보안 주체의 SID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로그인과 연결된 SID와 일치해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 새 이름에는 백슬래시(\\)를 사용할 수 없습니다.

CHECK_EXPIRATION = { ON | **OFF** } [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 이 로그인에 암호 만료 정책을 적용할지 여부를 지정합니다. 기본값은 OFF입니다.

CHECK_POLICY **=** { **ON** | OFF } [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 컴퓨터의 Windows 암호 정책을 이 로그인에 적용하도록 지정합니다. 기본값은 ON입니다.

CREDENTIAL = *credential_name*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑할 자격 증명의 이름입니다. 자격 증명이 서버에 이미 있어야 합니다. 자세한 내용은 [자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)을 참조하세요. 자격 증명은 sa 로그인으로 매핑할 수 없습니다.

NO CREDENTIAL 서버 자격 증명에 대한 로그인의 기존 매핑을 모두 제거합니다. 자세한 내용은 [자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)을 참조하세요.

UNLOCK [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 잠긴 로그인을 잠금 해제하도록 지정합니다.

ADD CREDENTIAL EKM(확장 가능 키 관리) 공급자 자격 증명을 로그인에 추가합니다. 자세한 내용은 [EKM(확장 가능 키 관리)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)을 참조하세요.

DROP CREDENTIAL EKM(확장 가능 키 관리) 공급자 자격 증명을 로그인에서 제거합니다. 자세한 내용은 [EKM(확장 가능 키 관리)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)을 참조하세요.

## <a name="remarks"></a>설명

CHECK_POLICY를 ON으로 설정하면 HASHED 인수를 사용할 수 없습니다.

CHECK_POLICY가 ON으로 변경되면 다음 동작이 수행됩니다.

- 암호 기록이 현재 암호 해시 값으로 초기화됩니다.

  CHECK_POLICY가 OFF로 변경되면 다음 동작이 수행됩니다.

- CHECK_EXPIRATION도 OFF로 설정됩니다.
- 암호 기록이 삭제됩니다.
- *lockout_time*의 값이 재설정됩니다.

MUST_CHANGE를 지정한 경우에는 CHECK_EXPIRATION  및 CHECK_POLICY를 ON으로 설정해야 합니다. 그렇지 않으면 문이 실패합니다.

CHECK_POLICY를 OFF로 설정한 경우에는 CHECK_EXPIRATION을 ON으로 설정할 수 없습니다. 이 옵션 조합을 사용하면 ALTER LOGIN 문이 실패합니다.

ALTER_LOGIN에 DISABLE 인수를 사용하여 Windows 그룹에 대한 액세스를 거부할 수 없습니다. 이것은 의도적인 것입니다. 예를 들어 ALTER_LOGIN [*domain\group*] DISABLE은 다음 오류 메시지를 반환합니다.

    `"Msg 15151, Level 16, State 1, Line 1
    "Cannot alter the login '*Domain\Group*', because it does not exist or you do not have permission."`

[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 강제 실행하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.

## <a name="permissions"></a>사용 권한

ALTER ANY LOGIN 권한이 필요합니다.

CREDENTIAL 옵션을 사용하는 경우에는 ALTER ANY CREDENTIAL 권한도 필요합니다.

변경되는 로그인이 **sysadmin** 고정 서버 역할의 멤버이거나 CONTROL SERVER 권한의 피부여자인 경우에는 다음과 같은 변경을 수행할 때 CONTROL SERVER 권한도 필요합니다.

- 이전 암호를 제공하지 않고 암호를 다시 설정
- MUST_CHANGE, CHECK_POLICY 또는 CHECK_EXPIRATION 활성화
- 로그인 이름 변경
- 로그인 활성화 또는 비활성화
- 로그인을 다른 자격 증명에 매핑

보안 주체는 자신이 소유하는 로그인의 암호, 기본 언어 및 기본 데이터베이스를 변경할 수 있습니다.

`sysadmin` 권한이 있는 SQL 주체만 Azure AD 로그인에 대해 ALTER LOGIN 명령을 실행할 수 있습니다.

## <a name="examples"></a>예제

이러한 예제에는 다른 SQL 제품 사용에 대한 예제도 포함되어 있습니다. 위에서 지원되는 인수를 참조하세요.

### <a name="a-enabling-a-disabled-login"></a>A. 비활성화된 로그인 활성화

다음 예에서는 `Mary5` 로그인을 활성화합니다.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. 로그인 암호 변경

다음 예에서는 `Mary5` 로그인의 암호를 강력한 암호로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-name-of-a-login"></a>C. 로그인 이름 변경

다음 예에서는 `Mary5` 로그인의 이름을 `John2`로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="d-mapping-a-login-to-a-credential"></a>D. 로그인을 자격 증명에 매핑

다음 예에서는 `John2` 로그인을 `Custodian04` 자격 증명에 매핑합니다.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. 로그인을 확장 가능 키 관리 자격 증명에 매핑

다음 예에서는 `Mary5` 로그인을 `EKMProvider1` EKM 자격 증명에 매핑합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 및 Azure SQL Database Managed Instance.

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. 로그인 잠금 해제

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 잠금을 해제하려면 \*\*\*\*를 원하는 계정 암호로 바꾸고 다음 문을 실행합니다.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

암호를 변경하지 않고 로그인의 잠금을 해제하려면 검사 정책을 해제한 다음 다시 설정합니다.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. HASHED를 사용하여 로그인 암호 변경

다음 예에서는 `TestUser` 로그인의 암호를 이미 해시된 값으로 변경합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 및 Azure SQL Database Managed Instance.

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

### <a name="h-disabling-the-login-of-an-azure-ad-user"></a>H. Azure AD 사용자의 로그인을 사용하지 않도록 설정

다음 예제에서는 Azure AD 사용자 joe@contoso.com의 로그인을 사용하지 않도록 설정합니다.

```sql
ALTER LOGIN [joe@contoso.com] DISABLE
```

## <a name="see-also"></a>참고 항목

- [자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM(확장 가능 키 관리)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-login-transact-sql.md?view=sql-server-2017)|[SQL Database<br />단일 데이터베이스/탄력적 풀](alter-login-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />관리되는 인스턴스](alter-login-transact-sql.md?view=azuresqldb-mi-current)|**_\* Azure Synapse<br />Analytics \*_**|[Analytics Platform<br />System(PDW)](alter-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for Azure Synapse

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

## <a name="arguments"></a>인수

*login_name* 변경할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다. 도메인 이름은 [domain\user] 형식과 같이 대괄호로 묶어야 합니다.

ENABLE | DISABLE 로그인을 사용하거나 사용하지 않도록 설정합니다. 로그인 비활성화는 이미 연결된 로그인 동작에 영향을 주지 않습니다. (기존 연결을 종료하려면 `KILL` 문을 사용합니다.) 비활성화된 로그인은 권한을 유지하며 계속 가장될 수 있습니다.

PASSWORD **='** _password_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 변경할 로그인의 암호를 지정합니다. 암호는 대소문자를 구분합니다.

SQL Database에 대한 활성 연결을 지속하기 위해서는 적어도 10시간 마다 다시 인증해야 합니다(데이터베이스 엔진에서 수행됨). 데이터베이스 엔진은 원래 제출된 암호를 사용하여 다시 인증을 시도하며, 사용자 입력은 필요하지 않습니다. 성능상의 이유로 암호를 SQL Database에서 다시 설정한 경우 연결 풀링으로 인해 연결이 재설정되더라도 연결은 다시 인증되지 않습니다. 이는 온-프레미스 SQL Server의 동작과 다릅니다. 초기에 연결을 인증한 후 암호를 변경하면 연결을 종료하고 새 암호를 사용하여 새 연결을 설정해야 합니다. KILL DATABASE CONNECTION 권한이 있는 사용자는 KILL 명령을 사용하여 SQL Database에 대한 연결을 명시적으로 종료할 수 있습니다. 자세한 내용은 [KILL](../../t-sql/language-elements/kill-transact-sql.md)을 참조하세요.

> [!IMPORTANT]
> 로그인 계정(또는 포함된 데이터베이스 사용자)이 연결되고 인증되면 해당 연결에 해당 로그인에 대한 ID 정보가 캐시됩니다. Windows 인증 로그인을 위해 Windows 그룹의 멤버 자격에 대한 정보가 포함됩니다. 연결이 유지되는 한 로그인의 ID가 인증된 상태로 유지됩니다. 암호 재설정이나 Windows 그룹 멤버 자격 변경 등의 ID 변경 사항을 적용하려면 인증 기관(Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])에서 로그오프한 후 다시 로그인해야 합니다. **sysadmin** 고정 서버 역할의 멤버나 **ALTER ANY CONNECTION** 권한이 있는 로그인은 **KILL** 명령을 사용하여 연결을 종료하고 다시 연결하도록 할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기 또는 쿼리 편집기 창에 다중 연결할 때 연결 정보를 다시 사용합니다. 다시 연결하도록 모든 연결을 닫습니다.

OLD_PASSWORD **='** _oldpassword_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 새 암호가 할당될 로그인의 현재 암호입니다. 암호는 대소문자를 구분합니다.

NAME = *login_name* 이름을 바꿀 로그인의 새 이름입니다. Windows 로그인인 경우 새 이름에 해당하는 Windows 보안 주체의 SID가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로그인에 연결된 SID와 일치해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 새 이름에는 백슬래시(\\)를 사용할 수 없습니다.

## <a name="remarks"></a>설명

[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 적용하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.

## <a name="permissions"></a>사용 권한

ALTER ANY LOGIN 권한이 필요합니다.

변경되는 로그인이 **sysadmin** 고정 서버 역할의 멤버이거나 CONTROL SERVER 권한의 피부여자인 경우에는 다음과 같은 변경을 수행할 때 CONTROL SERVER 권한도 필요합니다.

- 이전 암호를 제공하지 않고 암호를 다시 설정
- 로그인 이름 변경
- 로그인 활성화 또는 비활성화
- 로그인을 다른 자격 증명에 매핑

보안 주체는 자체 로그인에 대한 암호를 변경할 수 있습니다.

## <a name="examples"></a>예제

이러한 예제에는 다른 SQL 제품 사용에 대한 예제도 포함되어 있습니다. 위에서 지원되는 인수를 참조하세요.

### <a name="a-enabling-a-disabled-login"></a>A. 비활성화된 로그인 활성화

다음 예에서는 `Mary5` 로그인을 활성화합니다.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. 로그인 암호 변경

다음 예에서는 `Mary5` 로그인의 암호를 강력한 암호로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-name-of-a-login"></a>C. 로그인 이름 변경

다음 예에서는 `Mary5` 로그인의 이름을 `John2`로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="d-mapping-a-login-to-a-credential"></a>D. 로그인을 자격 증명에 매핑

다음 예에서는 `John2` 로그인을 `Custodian04` 자격 증명에 매핑합니다.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. 로그인을 확장 가능 키 관리 자격 증명에 매핑

다음 예에서는 `Mary5` 로그인을 `EKMProvider1` EKM 자격 증명에 매핑합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. 로그인 잠금 해제

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 잠금을 해제하려면 \*\*\*\*를 원하는 계정 암호로 바꾸고 다음 문을 실행합니다.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

암호를 변경하지 않고 로그인의 잠금을 해제하려면 검사 정책을 해제한 다음 다시 설정합니다.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. HASHED를 사용하여 로그인 암호 변경

다음 예에서는 `TestUser` 로그인의 암호를 이미 해시된 값으로 변경합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

## <a name="see-also"></a>참고 항목

- [자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM(확장 가능 키 관리)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-login-transact-sql.md?view=sql-server-2017)|[SQL Database<br />단일 데이터베이스/탄력적 풀](alter-login-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />관리되는 인스턴스](alter-login-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](alter-login-transact-sql.md?view=azure-sqldw-latest)|**_\* Analytics<br />Platform System(PDW) \*_**

&nbsp;

## <a name="analytics-platform-system"></a>분석 플랫폼 시스템

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for Analytics Platform System

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

*login_name* 변경할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다. 도메인 이름은 [domain\user] 형식과 같이 대괄호로 묶어야 합니다.

ENABLE | DISABLE 로그인을 사용하거나 사용하지 않도록 설정합니다. 로그인 비활성화는 이미 연결된 로그인 동작에 영향을 주지 않습니다. (기존 연결을 종료하려면 `KILL` 문을 사용합니다.) 비활성화된 로그인은 권한을 유지하며 계속 가장될 수 있습니다.

PASSWORD **='** _password_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 변경할 로그인의 암호를 지정합니다. 암호는 대소문자를 구분합니다.

> [!IMPORTANT]
> 로그인 계정(또는 포함된 데이터베이스 사용자)이 연결되고 인증되면 해당 연결에 해당 로그인에 대한 ID 정보가 캐시됩니다. Windows 인증 로그인을 위해 Windows 그룹의 멤버 자격에 대한 정보가 포함됩니다. 연결이 유지되는 한 로그인의 ID가 인증된 상태로 유지됩니다. 암호 재설정이나 Windows 그룹 멤버 자격 변경 등의 ID 변경 사항을 적용하려면 인증 기관(Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])에서 로그오프한 후 다시 로그인해야 합니다. **sysadmin** 고정 서버 역할의 멤버나 **ALTER ANY CONNECTION** 권한이 있는 로그인은 **KILL** 명령을 사용하여 연결을 종료하고 다시 연결하도록 할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기 또는 쿼리 편집기 창에 다중 연결할 때 연결 정보를 다시 사용합니다. 다시 연결하도록 모든 연결을 닫습니다.

OLD_PASSWORD **='** _oldpassword_ **'** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 새 암호가 할당될 로그인의 현재 암호입니다. 암호는 대소문자를 구분합니다.

MUST_CHANGE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 이 옵션을 지정한 경우 변경한 로그인을 처음 사용할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 업데이트된 암호를 묻는 메시지를 표시합니다.

NAME = *login_name* 이름을 바꿀 로그인의 새 이름입니다. 로그인이 Windows 로그인인 경우 새 이름에 해당하는 Windows 보안 주체의 SID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로그인과 연결된 SID와 일치해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 새 이름에는 백슬래시(\\)를 사용할 수 없습니다.

CHECK_EXPIRATION = { ON | **OFF** } [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 이 로그인에 암호 만료 정책을 적용할지 여부를 지정합니다. 기본값은 OFF입니다.

CHECK_POLICY **=** { **ON** | OFF } [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 컴퓨터의 Windows 암호 정책을 이 로그인에 적용하도록 지정합니다. 기본값은 ON입니다.

UNLOCK [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에만 적용됩니다. 잠긴 로그인을 잠금 해제하도록 지정합니다.

## <a name="remarks"></a>설명

CHECK_POLICY를 ON으로 설정하면 HASHED 인수를 사용할 수 없습니다.

CHECK_POLICY가 ON으로 변경되면 다음 동작이 수행됩니다.

- 암호 기록이 현재 암호 해시 값으로 초기화됩니다.

  CHECK_POLICY가 OFF로 변경되면 다음 동작이 수행됩니다.

- CHECK_EXPIRATION도 OFF로 설정됩니다.
- 암호 기록이 삭제됩니다.
- *lockout_time*의 값이 재설정됩니다.

MUST_CHANGE를 지정한 경우에는 CHECK_EXPIRATION  및 CHECK_POLICY를 ON으로 설정해야 합니다. 그렇지 않으면 문이 실패합니다.

CHECK_POLICY를 OFF로 설정한 경우에는 CHECK_EXPIRATION을 ON으로 설정할 수 없습니다. 이 옵션 조합을 사용하면 ALTER LOGIN 문이 실패합니다.

ALTER_LOGIN에 DISABLE 인수를 사용하여 Windows 그룹에 대한 액세스를 거부할 수 없습니다. 이것은 의도적인 것입니다. 예를 들어 ALTER_LOGIN [*domain\group*] DISABLE은 다음 오류 메시지를 반환합니다.

    `"Msg 15151, Level 16, State 1, Line 1
    "Cannot alter the login '*Domain\Group*', because it does not exist or you do not have permission."`

[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 강제 실행하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.

## <a name="permissions"></a>사용 권한

ALTER ANY LOGIN 권한이 필요합니다.

CREDENTIAL 옵션을 사용하는 경우에는 ALTER ANY CREDENTIAL 권한도 필요합니다.

변경되는 로그인이 **sysadmin** 고정 서버 역할의 멤버이거나 CONTROL SERVER 권한의 피부여자인 경우에는 다음과 같은 변경을 수행할 때 CONTROL SERVER 권한도 필요합니다.

- 이전 암호를 제공하지 않고 암호를 다시 설정
- MUST_CHANGE, CHECK_POLICY 또는 CHECK_EXPIRATION 활성화
- 로그인 이름 변경
- 로그인 활성화 또는 비활성화
- 로그인을 다른 자격 증명에 매핑

보안 주체는 자신이 소유하는 로그인의 암호, 기본 언어 및 기본 데이터베이스를 변경할 수 있습니다.

## <a name="examples"></a>예제

이러한 예제에는 다른 SQL 제품 사용에 대한 예제도 포함되어 있습니다. 위에서 지원되는 인수를 참조하세요.

### <a name="a-enabling-a-disabled-login"></a>A. 비활성화된 로그인 활성화

다음 예에서는 `Mary5` 로그인을 활성화합니다.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. 로그인 암호 변경

다음 예에서는 `Mary5` 로그인의 암호를 강력한 암호로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-name-of-a-login"></a>C. 로그인 이름 변경

다음 예에서는 `Mary5` 로그인의 이름을 `John2`로 변경합니다.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="d-mapping-a-login-to-a-credential"></a>D. 로그인을 자격 증명에 매핑

다음 예에서는 `John2` 로그인을 `Custodian04` 자격 증명에 매핑합니다.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. 로그인을 확장 가능 키 관리 자격 증명에 매핑

다음 예에서는 `Mary5` 로그인을 `EKMProvider1` EKM 자격 증명에 매핑합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. 로그인 잠금 해제

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 잠금을 해제하려면 \*\*\*\*를 원하는 계정 암호로 바꾸고 다음 문을 실행합니다.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

암호를 변경하지 않고 로그인의 잠금을 해제하려면 검사 정책을 해제한 다음 다시 설정합니다.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. HASHED를 사용하여 로그인 암호 변경

다음 예에서는 `TestUser` 로그인의 암호를 이미 해시된 값으로 변경합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

## <a name="see-also"></a>참고 항목

- [자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM(확장 가능 키 관리)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
