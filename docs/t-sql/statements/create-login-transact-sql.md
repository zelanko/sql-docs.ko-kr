---
title: CREATE LOGIN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_LOGIN_TSQL
- CREATE LOGIN
- LOGIN_TSQL
- LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], logins
- mapping logins [SQL Server]
- logins [SQL Server], creating
- CREATE LOGIN statement
- permissions [SQL Server], logins
- Windows domain accounts [SQL Server]
- re-hashing passwords
- certificates [SQL Server], logins
ms.assetid: eb737149-7c92-4552-946b-91085d8b1b01
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 410cd9444cec90f5d6357e2084bab47f5ab25d37
ms.sourcegitcommit: 8664c2452a650e1ce572651afeece2a4ab7ca4ca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56828373"
---
# <a name="create-login-transact-sql"></a>CREATE LOGIN(Transact-SQL)

SQL Server, SQL Database, SQL Data Warehouse 또는 Analytics Platform System 데이터베이스에 대한 로그인을 만듭니다. 특정 버전에 대한 구문, 인수, 설명, 사용 권한 및 예제는 다음 탭 중 하나를 클릭합니다.

구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하십시오.

## <a name="click-a-product"></a>제품을 클릭하세요.

다음 행에서 관심이 있는 제품 이름을 클릭합니다. 클릭하면 웹페이지의 여기에서 클릭한 제품에 적절한 다른 콘텐츠를 표시합니다.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||||
|-|-|-|-|-|
|**_\* SQL Server \*_** &nbsp;|[SQL Database<br />단일 데이터베이스/탄력적 풀](create-login-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />관리되는 인스턴스](create-login-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-login-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System(PDW)](create-login-transact-sql.md?view=aps-pdw-2016)
||||||

&nbsp;

## <a name="sql-server"></a>SQL Server

## <a name="syntax"></a>구문

```
-- Syntax for SQL Server
CREATE LOGIN login_name { WITH <option_list1> | FROM <sources> }

<option_list1> ::=
    PASSWORD = { 'password' | hashed_password HASHED } [ MUST_CHANGE ]
    [ , <option_list2> [ ,... ] ]

<option_list2> ::=
    SID = sid
    | DEFAULT_DATABASE = database
    | DEFAULT_LANGUAGE = language
    | CHECK_EXPIRATION = { ON | OFF}
    | CHECK_POLICY = { ON | OFF}
    | CREDENTIAL = credential_name

<sources> ::=
    WINDOWS [ WITH <windows_options>[ ,... ] ]
    | CERTIFICATE certname
    | ASYMMETRIC KEY asym_key_name
  
<windows_options> ::=
    DEFAULT_DATABASE = database
    | DEFAULT_LANGUAGE = language
```

## <a name="arguments"></a>인수

*login_name* 만들 로그인 이름을 지정합니다. 로그인에는 SQL Server 로그인, Windows 로그인, 인증서 매핑 로그인 및 비대칭 키 매핑 로그인의 네 가지 유형이 있습니다. Windows 도메인 계정에서 매핑된 로그인을 만들 경우 Windows 2000 이전 버전의 사용자 로그온 이름을 [\<domainName>\\<login_name>] 형식으로 사용해야 합니다. login_name@DomainName 형식의 UPN은 사용할 수 없습니다. 이 문서의 뒷부분에 나오는 예 4를 참조하세요. 인증 로그인은 **sysname** 형식이고 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 하며 '**\\**'을 포함할 수 없습니다. Windows 로그인은 '**\\**'를 포함할 수 없습니다. Active Directory 사용자에 기반한 로그인은 21자 미만의 이름으로 제한됩니다.

PASSWORD **=**'*password*' SQL Server 로그인에만 적용됩니다. 만들 로그인의 암호를 지정합니다. 강력한 암호를 사용하세요. 자세한 내용은 [강력한 암호](../../relational-databases/security/strong-passwords.md) 및 [암호 정책](../../relational-databases/security/password-policy.md)을 참조하세요. SQL Server 2012(11.x)부터 저장된 암호 정보는 솔트 암호의 SHA-512를 사용하여 계산됩니다.

암호는 대소문자를 구분합니다. 암호의 길이는 항상 8자 이상이어야 하며 128자를 초과할 수 없습니다. 암호에는 a-z, A-Z, 0-9 및 영숫자가 아닌 대부분의 문자를 포함할 수 있습니다. 암호는 홑따옴표 또는 *login_name*을 포함할 수 없습니다.

PASSWORD **=** *hashed\_password* HASHED 키워드에만 적용됩니다. 만들 로그인에 대한 암호의 해시된 값을 지정합니다.

HASHED는 SQL Server 로그인에만 적용됩니다. PASSWORD 인수 다음에 입력한 암호가 이미 해시되었음을 지정합니다. 이 옵션을 선택하지 않으면 암호로 입력한 문자열이 데이터베이스에 저장되기 전에 해시됩니다. 이 옵션은 두 서버 간에 데이터베이스를 마이그레이션하는 데에만 사용해야 합니다. HASHED 옵션을 사용하여 새 로그인을 만들면 안 됩니다. HASHED 옵션은 SQL 7 또는 그 이전 버전에서 만든 해시와 함께 사용할 수 없습니다.

MUST_CHANGE는 SQL Server 로그인에만 적용됩니다. 이 옵션을 선택한 경우 새 로그인을 처음 사용할 때 SQL Server에서는 새 암호를 묻는 메시지를 표시합니다.

CREDENTIAL **=**_credential\_name_ 새 SQL Server 로그인에 매핑할 자격 증명의 이름입니다. 자격 증명이 서버에 이미 있어야 합니다. 현재 이 옵션은 자격 증명을 로그인에 연결하는 역할만 합니다. 자격 증명은 시스템 관리자(sa) 로그인에 매핑할 수 없습니다.

SID = *sid* 로그인을 다시 만드는데 사용됩니다. SQL Server 인증 로그인에만 적용되고 Windows 인증 로그인에는 적용되지 않습니다. 새 SQL Server 인증 로그인의 SID를 지정합니다. 이 옵션을 사용하지 않으면 SQL Server에서 자동으로 SID를 할당합니다. SID 구조는 SQL Server 버전에 따라 달라집니다. SQL Server 로그인 SID: GUID에 기반한 16바이트(**binary(16)**) 리터럴 값입니다. `SID = 0x14585E90117152449347750164BA00A7`)을 입력합니다.

DEFAULT_DATABASE **=**_database_ 로그인에 할당할 기본 데이터베이스를 지정합니다. 이 옵션을 선택하지 않으면 기본 데이터베이스가 master로 설정됩니다.

DEFAULT_LANGUAGE **=**_language_ 로그인에 할당할 기본 언어를 지정합니다. 이 옵션을 선택하지 않으면 기본 언어가 서버의 현재 기본 언어로 설정됩니다. 나중에 서버의 기본 언어가 변경되더라도 로그인의 기본 언어는 그대로 유지됩니다.

CHECK_EXPIRATION **=** { ON | **OFF** } SQL Server 로그인에만 적용됩니다. 이 로그인에 암호 만료 정책을 적용할지 여부를 지정합니다. 기본값은 OFF입니다.

CHECK_POLICY **=** { **ON** | OFF } SQL Server 로그인에만 적용됩니다. SQL Server가 실행 중인 컴퓨터의 Windows 암호 정책을 이 로그인에 적용하도록 지정합니다. 기본값은 ON입니다.

Windows 정책에 따라 강력한 암호가 필요한 경우에는 암호에 다음 네 가지 문자 중 세 가지 이상을 포함해야 합니다.

- 대문자(A-Z)
- 소문자(a-z)
- 숫자(0-9)
- 영숫자가 아닌 문자 중 하나(예:  공백,  _,  @,  *,  ^,  %,  !,  $,  #  또는 &)

WINDOWS 로그인이 Windows 로그인에 매핑되도록 지정합니다.

CERTIFICATE *certname* 이 로그인과 연결될 인증서의 이름을 지정합니다. 이 인증서는 master 데이터베이스에 이미 있어야 합니다.

ASYMMETRIC KEY *asym_key_name* 이 로그인과 연결될 비대칭 키의 이름을 지정합니다. 이 키는 master 데이터베이스에 이미 있어야 합니다.

## <a name="remarks"></a>Remarks

- 암호는 대소문자를 구분합니다.
- SQL Server 로그인을 만들 때만 암호를 미리 해시할 수 있습니다.
- MUST_CHANGE를 지정한 경우에는 CHECK_EXPIRATION  및 CHECK_POLICY를 ON으로 설정해야 합니다. 그렇지 않으면 문이 실패합니다.
- CHECK_POLICY = OFF와 CHECK_EXPIRATION = ON의 조합은 지원되지 않습니다.
- CHECK_POLICY를 OFF로 설정하면 *lockout_time*이 재설정되고 CHECK_EXPIRATION이 OFF로 설정됩니다.

> [!IMPORTANT]
> CHECK_EXPIRATION 및 CHECK_POLICY는 Windows Server 2003 이상 버전에서만 적용됩니다. 자세한 내용은 [Password Policy](../../relational-databases/security/password-policy.md)을 참조하세요.

- 인증서나 비대칭 키에서 만든 로그인은 코드 서명 용도로만 사용되며 SQL Server에 연결할 때는 사용할 수 없습니다. 인증서나 비대칭 키가 master 데이터베이스에 이미 있는 경우에만 인증서나 비대칭 키에서 로그인을 만들 수 있습니다.
- 로그인을 전송하는 스크립트는 [SQL Server 2005와 SQL Server 2008 인스턴스 간에 로그인 및 암호를 전송하는 방법](https://support.microsoft.com/kb/918992)을 참조하세요.
- 로그인을 만들면 새 로그인이 자동으로 사용하도록 설정되고 해당 로그인에 서버 수준 **CONNECT SQL** 권한이 부여됩니다.
- 액세스를 허용하려면 서버의 [인증 모드](../../relational-databases/security/choose-an-authentication-mode.md)가 로그인 형식과 일치해야 합니다.
- 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.

## <a name="permissions"></a>Permissions

- 서버의 **ALTER ANY LOGIN** 권한 또는 **securityadmin** 고정 서버 역할의 멤버 자격이 있는 사용자만 로그인을 만들 수 있습니다. 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) 및 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles을 참조하세요.
- **CREDENTIAL** 옵션을 사용하는 경우에는 서버에 대한 **ALTER ANY CREDENTIAL** 권한도 필요합니다.

## <a name="after-creating-a-login"></a>로그인을 만든 후

로그인을 만든 후 해당 로그인으로 SQL Server에 연결할 수 있지만 이 로그인은 **public** 역할에 부여된 권한만 있습니다. 다음 작업 중 일부를 수행하는 것이 좋습니다.

- 데이터베이스에 연결하려면 로그인에 대한 데이터베이스 사용자를 만듭니다. 자세한 내용은 [CREATE USER](../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.
- [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md)을 사용하여 사용자 정의 서버 역할을 만듭니다. **ALTER SERVER ROLE** ... **ADD MEMBER**를 사용하여 사용자 정의 서버 역할에 새 로그인을 추가합니다. 자세한 내용은 [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) 및 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)을 참조하세요.
- **sp_addsrvrolemember**를 사용하여 고정 서버 역할에 로그인을 추가합니다. 자세한 내용은 [서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md) 및 [sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)을 참조하세요.
- **GRANT** 문을 사용하여 새 로그인 또는 해당 로그인을 포함한 역할에 서버 수준 권한을 부여합니다. 자세한 내용은 [GRANT](../../t-sql/statements/grant-transact-sql.md)를 참조하십시오.

## <a name="examples"></a>예

### <a name="a-creating-a-login-with-a-password"></a>1. 암호로 로그인 만들기

다음 예에서는 특정 사용자에 대한 로그인을 만들고 암호를 할당합니다.

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';
GO
```

### <a name="b-creating-a-login-with-a-password-that-must-be-changed"></a>2. 변경해야 하는 암호로 로그인 만들기

다음 예에서는 특정 사용자에 대한 로그인을 만들고 암호를 할당합니다. `MUST_CHANGE` 옵션을 사용하는 경우 사용자는 서버에 처음 연결할 때 이 암호를 변경해야 합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'
    MUST_CHANGE, CHECK_EXPIRATION = ON;
GO
```

> [!NOTE]
> CHECK_EXPIRATION이 해제되어 있을 때는 MUST_CHANGE 옵션을 사용할 수 없습니다.

### <a name="c-creating-a-login-mapped-to-a-credential"></a>C. 자격 증명에 매핑된 로그인 만들기

다음 예에서는 사용자를 사용하여 특정 사용자에 대한 로그인을 만듭니다. 이 로그인은 자격 증명에 매핑됩니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>',
    CREDENTIAL = <credentialName>;
GO
```

### <a name="d-creating-a-login-from-a-certificate"></a>D. 인증서에서 로그인 만들기

다음 예제에서는 마스터의 인증서에서 특정 사용자에 대한 로그인을 만듭니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

```sql
USE MASTER;
CREATE CERTIFICATE <certificateName>
    WITH SUBJECT = '<login_name> certificate in master database',
    EXPIRY_DATE = '12/05/2025';
GO
CREATE LOGIN <login_name> FROM CERTIFICATE <certificateName>;
GO
```

### <a name="e-creating-a-login-from-a-windows-domain-account"></a>E. Windows 도메인 계정에서 로그인 만들기

다음 예에서는 Windows 도메인 계정을 사용하여 로그인을 만듭니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

```sql
CREATE LOGIN [<domainName>\<login_name>] FROM WINDOWS;
GO
```

### <a name="f-creating-a-login-from-a-sid"></a>F. SID에서 로그인 만들기

다음 예제에서는 우선 SQL Server 인증 로그인을 만들고 로그인의 SID를 결정합니다.

```sql
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

쿼리는 0x241C11948AEEB749B0D22646DB1A19F2를 SID로 반환합니다. 쿼리는 다른 값을 반환합니다. 다음 문은 로그인을 삭제한 후 로그인을 다시 만듭니다. 이전 쿼리의 SID를 사용합니다.

```sql
DROP LOGIN TestLogin;
GO

CREATE LOGIN TestLogin
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;

SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

## <a name="see-also"></a>참고 항목

- [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [보안 주체](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [암호 정책](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](create-login-transact-sql.md?view=sql-server-2017)|**_\*SQL Database<br />단일 데이터베이스/탄력적 풀\*_**|[SQL Database<br />관리되는 인스턴스](create-login-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-login-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System(PDW)](create-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-single-databaseelastic-pool"></a>Azure SQL Database 단일 데이터베이스/탄력적 풀

## <a name="syntax"></a>구문

```
-- Syntax for Azure SQL Database
CREATE LOGIN login_name
 { WITH <option_list> }

<option_list> ::=
    PASSWORD = { 'password' }
    [ , SID = sid ]
```

## <a name="arguments"></a>인수

*login_name* 만들 로그인 이름을 지정합니다. Azure SQL Database 단일 데이터베이스/탄력적 풀은 SQL 로그인만 지원합니다.

PASSWORD **='** password**'* 만들 SQL 로그인의 암호를 지정합니다. 강력한 암호를 사용하세요. 자세한 내용은 [강력한 암호](../../relational-databases/security/strong-passwords.md) 및 [암호 정책](../../relational-databases/security/password-policy.md)을 참조하세요. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 저장된 암호 정보는 솔트 암호의 SHA-512를 사용하여 계산됩니다.

암호는 대소문자를 구분합니다. 암호의 길이는 항상 8자 이상이어야 하며 128자를 초과할 수 없습니다. 암호에는 a-z, A-Z, 0-9 및 영숫자가 아닌 대부분의 문자를 포함할 수 있습니다. 암호는 홑따옴표 또는 *login_name*을 포함할 수 없습니다.

SID = *sid* 로그인을 다시 만드는데 사용됩니다. SQL Server 인증 로그인에만 적용되고 Windows 인증 로그인에는 적용되지 않습니다. 새 SQL Server 인증 로그인의 SID를 지정합니다. 이 옵션을 사용하지 않으면 SQL Server에서 자동으로 SID를 할당합니다. SID 구조는 SQL Server 버전에 따라 달라집니다. SQL Database의 경우 `0x01060000000000640000000000000000`과 GUID를 나타내는 16바이트로 구성된 32바이트(**binary(32)**) 리터럴입니다. `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`)을 입력합니다.

## <a name="remarks"></a>Remarks

- 암호는 대소문자를 구분합니다.
- 로그인을 전송하는 스크립트는 [SQL Server 2005와 SQL Server 2008 인스턴스 간에 로그인 및 암호를 전송하는 방법](https://support.microsoft.com/kb/918992)을 참조하세요.
- 로그인을 만들면 새 로그인이 자동으로 사용하도록 설정되고 해당 로그인에 서버 수준 **CONNECT SQL** 권한이 부여됩니다.
- 액세스를 허용하려면 서버의 [인증 모드](../../relational-databases/security/choose-an-authentication-mode.md)가 로그인 형식과 일치해야 합니다.
- 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.

## <a name="login"></a>로그인

### <a name="sql-database-logins"></a>SQL Database 로그인

**CREATE LOGIN** 문은 일괄 처리의 유일한 명령문이어야 합니다.

**sqlcmd**와 같이 SQL Database에 연결하는 몇 가지 방법에서는 *\<login>*@*\<server>* 표기법을 사용하여 SQL Database 서버 이름을 연결 문자열의 로그인 이름에 추가해야 합니다. 예를 들어 로그인이 `login1`이고 SQL Database 서버의 정규화된 이름이 `servername.database.windows.net`인 경우 연결 문자열의 *username* 매개 변수는 `login1@servername`이어야 합니다. *username* 매개 변수의 총 길이는 128문자이므로 *login_name*은 127문자에서 서버 이름의 길이를 뺀 길이로 제한됩니다. 이 예에서는 `login_name`이 10자이므로 `servername`에는 117자까지만 사용할 수 있습니다.

SQL Database에서 로그인을 만들려면 마스터 데이터베이스에 연결해야 합니다.

SQL Server 규칙을 사용하여 \<loginname>@\<servername> 형식의 SQL Server 인증 로그인을 만들 수 있습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버가 **myazureserver**이고 로그인이 **myemail@live.com**인 경우 로그인을 **myemail@live.com@myazureserver**로 제공해야 합니다.

SQL Database에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 강제 실행하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.

SQL Database 로그인에 대한 자세한 내용은 [Windows Azure SQL Database에서 데이터베이스 및 로그인 관리](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)를 참조하세요.

## <a name="permissions"></a>Permissions

프로비전 프로세스를 통해 만들어진 서버 수준의 보안 주체 로그인이나 master 데이터베이스에서 `loginmanager` 데이터베이스 역할이 할당된 멤버만 새 로그인을 만들 수 있습니다. 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) 및 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).<https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles>을 참조하세요.

## <a name="logins"></a>로그인

- 서버의 **ALTER ANY LOGIN** 권한 또는 **securityadmin** 고정 서버 역할의 멤버 자격이 있어야 합니다. 서버의 **ALTER ANY LOGIN** 권한 또는 securityadmin 고정 서버 역할의 멤버 자격이 있는 Azure AD(Azure Active Directory) 계정만 이 명령을 실행할 수 있음
- Azure SQL Database 서버에 사용된 동일한 디렉터리 내에서 Azure AD의 구성원이어야 함

## <a name="after-creating-a-login"></a>로그인을 만든 후

로그인을 만든 후 해당 로그인으로 SQL Database에 연결할 수 있지만 이 로그인은 **public** 역할에 부여된 권한만 있습니다. 다음 작업 중 일부를 수행하는 것이 좋습니다.

- 데이터베이스에 연결하려면 해당 데이터베이스에서 로그인에 대한 데이터베이스 사용자를 만듭니다. 자세한 내용은 [CREATE USER](../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.
- 데이터베이스에서 사용자에게 권한을 부여하려면 **ALTER SERVER ROLE** ... **ADD MEMBER** 문을 사용하여 기본 제공 데이터베이스 역할 중 하나 또는 사용자 지정 역할에 사용자를 추가하거나 [GRANT](../../t-sql/statements/grant-transact-sql.md) 문을 사용하여 사용자에게 권한을 직접 부여합니다. 자세한 내용은 [비관리자 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#non-administrator-users), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles 및 [GRANT](grant-transact-sql.md) 문을 참조합니다.
- 서버 차원의 사용 권한을 부여하려면 master 데이터베이스에서 데이터베이스 사용자를 만들고 **ALTER SERVER ROLE** ... **ADD MEMBER** 문을 사용하여 관리 서버 역할 중 하나에 사용자를 추가합니다. 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) 및 [서버 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles)을 참조하세요.
- **GRANT** 문을 사용하여 새 로그인 또는 해당 로그인을 포함한 역할에 서버 수준 권한을 부여합니다. 자세한 내용은 [GRANT](../../t-sql/statements/grant-transact-sql.md)를 참조하십시오.

## <a name="examples"></a>예

### <a name="a-creating-a-login-with-a-password"></a>1. 암호로 로그인 만들기

다음 예에서는 특정 사용자에 대한 로그인을 만들고 암호를 할당합니다.

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';
GO
```

### <a name="b-creating-a-login-from-a-sid"></a>2. SID에서 로그인 만들기

다음 예제에서는 우선 SQL Server 인증 로그인을 만들고 로그인의 SID를 결정합니다.

```sql
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';

SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

쿼리는 0x241C11948AEEB749B0D22646DB1A19F2를 SID로 반환합니다. 쿼리는 다른 값을 반환합니다. 다음 문은 로그인을 삭제한 후 로그인을 다시 만듭니다. 이전 쿼리의 SID를 사용합니다.

```sql
DROP LOGIN TestLogin;
GO

CREATE LOGIN TestLogin
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;

SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

## <a name="see-also"></a>참고 항목

- [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [보안 주체](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [암호 정책](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](create-login-transact-sql.md?view=sql-server-2017)|[SQL Database<br />단일 데이터베이스/탄력적 풀](create-login-transact-sql.md?view=azuresqldb-current)|**_\*SQL Database<br />관리되는 인스턴스\*_**|[SQL Data<br />Warehouse](create-login-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System(PDW)](create-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Azure SQL Database 관리되는 인스턴스

## <a name="syntax"></a>구문

```sql
-- Syntax for Azure SQL Database managed instance
CREATE LOGIN login_name [FROM EXTERNAL PROVIDER] { WITH <option_list> [,..]}

<option_list> ::=
    PASSWORD = {'password'}
    | SID = sid
    | DEFAULT_DATABASE = database
    | DEFAULT_LANGUAGE = language
```

> [!IMPORTANT]
> SQL Database 관리되는 인스턴스에 대한 Azure AD 로그인은 **공개 미리 보기**로 제공됩니다. 이 구문은 **FROM EXTERNAL PROVIDER** 구문과 함께 도입되었습니다.

## <a name="arguments"></a>인수

*login_name* **FROM EXTERNAL PROVIDER** 절과 함께 사용될 때 로그인은 Azure AD(Active Directory) 사용자, 그룹 또는 애플리케이션인 Azure AD 보안 주체를 지정합니다. 그렇지 않으면 로그인은 생성된 SQL 로그인의 이름을 나타냅니다.

FROM EXTERNAL PROVIDER </br>
Azure AD 인증을 위한 로그인임을 지정합니다.

PASSWORD **=** '*password*' 만들 SQL 로그인의 암호를 지정합니다. 강력한 암호를 사용하세요. 자세한 내용은 [강력한 암호](../../relational-databases/security/strong-passwords.md) 및 [암호 정책](../../relational-databases/security/password-policy.md)을 참조하세요. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 저장된 암호 정보는 솔트 암호의 SHA-512를 사용하여 계산됩니다.

암호는 대소문자를 구분합니다. 암호의 길이는 항상 8자 이상이어야 하며 128자를 초과할 수 없습니다. 암호에는 a-z, A-Z, 0-9 및 영숫자가 아닌 대부분의 문자를 포함할 수 있습니다. 암호는 홑따옴표 또는 *login_name*을 포함할 수 없습니다.

SID **=** *sid* 로그인을 다시 만드는데 사용됩니다. SQL Server 인증 로그인에만 적용됩니다. 새 SQL Server 인증 로그인의 SID를 지정합니다. 이 옵션을 사용하지 않으면 SQL Server에서 자동으로 SID를 할당합니다. SID 구조는 SQL Server 버전에 따라 달라집니다. SQL Database의 경우 `0x01060000000000640000000000000000`과 GUID를 나타내는 16바이트로 구성된 32바이트(**binary(32)**) 리터럴입니다. `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`)을 입력합니다.

## <a name="remarks"></a>Remarks

- 암호는 대소문자를 구분합니다.
- Azure AD 계정에 매핑된 서버 수준 보안 주체를 만들기 위한 새 구문이 도입되었습니다(**FROM EXTERNAL PROVIDER**).
- **FROM EXTERNAL PROVIDER**가 지정된 경우:

  - login_name은 현재 Azure SQL 관리되는 인스턴스로 Azure AD에서 액세스할 수 있는 기존 Azure AD 계정(사용자, 그룹 또는 애플리케이션)을 나타내야 합니다.
  - **PASSWORD** 옵션은 사용할 수 없습니다.
  - 현재 첫 번째 Azure AD 로그인은 위의 구문을 사용하여 `sysadmin`인 표준 SQL Server 계정(비 Azure AD)에 의해 생성되어야 합니다.
  - SQL Database 관리되는 인스턴스에 대한 Azure AD 관리자를 사용하여 Azure AD 로그인을 만들 때 다음 오류가 발생합니다.</br>
      `Msg 15247, Level 16, State 1, Line 1
      User does not have permission to perform this action.`
  - 이는 **공개 미리 보기**의 알려진 제한 사항이며 나중에 수정될 예정입니다.
  - 첫 번째 Azure AD 로그인이 생성되면 이 로그인은 필요한 권한이 부여 받은 후 다른 Azure AD 로그인을 만들 수 있습니다.
- 기본적으로 **FROM EXTERNAL PROVIDER** 절을 생략하면 일반 SQL 로그인이 생성됩니다.
- Azure AD 사용자에 매핑된 로그인의 경우 Azure AD 로그인은 sys.server_principals에 표시되며 형식 열 값은 **E**로 설정되고 type_desc는 **EXTERNAL_LOGIN**으로 설정되거나, Azure AD 그룹에 매핑된 로그인의 경우 형식 열 값은 **X**로 설정되고 type_desc 값은 **EXTERNAL_GROUP**으로 설정됩니다.
- 로그인을 전송하는 스크립트는 [SQL Server 2005와 SQL Server 2008 인스턴스 간에 로그인 및 암호를 전송하는 방법](https://support.microsoft.com/kb/918992)을 참조하세요.
- 로그인을 만들면 새 로그인이 자동으로 사용하도록 설정되고 해당 로그인에 서버 수준 **CONNECT SQL** 권한이 부여됩니다.

## <a name="logins-and-permissions"></a>로그인 및 사용 권한

프로비전 프로세스를 통해 만들어진 서버 수준의 보안 주체 로그인이나 master 데이터베이스에서 `securityadmin` 또는 `sysadmin` 데이터베이스 역할이 할당된 멤버만 새 로그인을 만들 수 있습니다. 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) 및 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)을 참조하세요.

기본적으로 마스터에 새로 생성된 Azure AD 로그인에 부여된 표준 권한은 다음과 같습니다. **SQL 연결** 및 **모든 데이터베이스 보기**.

### <a name="sql-database-managed-instance-logins"></a>SQL Database 관리되는 인스턴스 로그인

- 서버의 **ALTER ANY LOGIN** 권한이나 고정 서버 역할 `securityadmin` 또는 `sysadmin` 중 하나의 멤버 자격이 있어야 합니다. 서버의 **ALTER ANY LOGIN** 권한 또는 해당 역할 중 하나의 멤버 자격이 있는 Azure AD(Azure Active Directory) 계정만 create 명령을 실행할 수 있습니다.
- 로그인이 SQL 보안 주체인 경우 `sysadmin` 역할의 일부인 로그인만 create 명령을 사용하여 Azure AD 계정에 대한 로그인을 만들 수 있습니다.
- Azure SQL 관리되는 인스턴스에 사용된 동일한 디렉터리 내에서 Azure AD의 구성원이어야 합니다.

## <a name="after-creating-a-login"></a>로그인을 만든 후

로그인을 만든 후 해당 로그인으로 SQL Database 관리되는 인스턴스에 연결할 수 있지만 이 로그인은 **public** 역할에 부여된 권한만 있습니다. 다음 작업 중 일부를 수행하는 것이 좋습니다.

- Azure AD 로그인으로 Azure AD 사용자를 만들려면 [CREATE USER](../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.
- 데이터베이스에서 사용자에게 권한을 부여하려면 **ALTER SERVER ROLE** ... **ADD MEMBER** 문을 사용하여 기본 제공 데이터베이스 역할 중 하나 또는 사용자 지정 역할에 사용자를 추가하거나 [GRANT](../../t-sql/statements/grant-transact-sql.md) 문을 사용하여 사용자에게 권한을 직접 부여합니다. 자세한 내용은 [비관리자 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#non-administrator-users), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles 및 [GRANT](grant-transact-sql.md) 문을 참조합니다.
- 서버 차원의 사용 권한을 부여하려면 master 데이터베이스에서 데이터베이스 사용자를 만들고 **ALTER SERVER ROLE** ... **ADD MEMBER** 문을 사용하여 관리 서버 역할 중 하나에 사용자를 추가합니다. 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) 및 [서버 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles)을 참조하세요.
  - `ALTER SERVER ROLE sysadmin ADD MEMBER [AzureAD_Login_name]` 명령을 사용하여 Azure AD 로그인에 `sysadmin` 역할을 추가합니다.
- **GRANT** 문을 사용하여 새 로그인 또는 해당 로그인을 포함한 역할에 서버 수준 권한을 부여합니다. 자세한 내용은 [GRANT](../../t-sql/statements/grant-transact-sql.md)를 참조하십시오.

## <a name="limitations"></a>제한 사항

- 데이터베이스 소유자로 Azure AD 그룹에 매핑된 Azure AD 로그인을 설정할 수 없습니다.
- [EXECUTE AS](execute-as-transact-sql.md) 절과 같이 다른 Azure AD 보안 주체를 사용하는 Azure AD 서버 수준 보안 주체의 가장이 지원됩니다.
- `sysadmin` 역할의 일부인 SQL 서버 수준 보안 주체(로그인)만 Azure AD 보안 주체를 대상으로 다음 작업을 실행할 수 있습니다.
  - 사용자로 실행
  - 로그인으로 실행

## <a name="examples"></a>예

### <a name="a-creating-a-login-with-a-password"></a>1. 암호로 로그인 만들기

다음 예에서는 특정 사용자에 대한 로그인을 만들고 암호를 할당합니다.

 ```sql
 CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';
 GO
 ```

### <a name="b-creating-a-login-from-a-sid"></a>2. SID에서 로그인 만들기

 다음 예제에서는 우선 SQL Server 인증 로그인을 만들고 로그인의 SID를 결정합니다.

 ```sql
 CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';

 SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';
 GO
 ```

쿼리는 0x241C11948AEEB749B0D22646DB1A19F2를 SID로 반환합니다. 쿼리는 다른 값을 반환합니다. 다음 문은 로그인을 삭제한 후 로그인을 다시 만듭니다. 이전 쿼리의 SID를 사용합니다.

 ```sql
 DROP LOGIN TestLogin;
 GO

 CREATE LOGIN TestLogin
 WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;

 SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';
 GO
 ```

### <a name="c-creating-a-login-for-a-local-azure-ad-account"></a>C. 로컬 Azure AD 계정에 대한 로그인 만들기

 다음 예제에서는 *myaad*의 Azure AD에 있는 Azure AD 계정 joe@myaad.onmicrosoft.com에 대한 로그인을 만듭니다.

```sql
CREATE LOGIN [joe@myaad.onmicrosoft.com] FROM EXTERNAL PROVIDER
GO
```

### <a name="d-creating-a-login-for-a-federated-azure-ad-account"></a>D. 페더레이션된 Azure AD 계정에 대한 로그인 만들기

 다음 예제에서는 *contoso*라는 Azure AD에 있는 페더레이션된 Azure AD 계정 bob@contoso.com에 대한 로그인을 만듭니다. 사용자 bob은 게스트 사용자일 수도 있습니다.

```sql
CREATE LOGIN [bob@contoso.com] FROM EXTERNAL PROVIDER
GO
```

### <a name="e-creating-a-login-for-an-azure-ad-group"></a>E. Azure AD 그룹에 대한 로그인 만들기

 다음 예제에서는 *myaad*의 Azure AD에 있는 Azure AD 그룹 *mygroup*에 대한 로그인을 만듭니다.

```sql
CREATE LOGIN [mygroup] FROM EXTERNAL PROVIDER
GO
```

### <a name="f-creating-a-login-for-an-azure-ad-application"></a>F. Azure AD 애플리케이션에 대한 로그인 만들기

다음 예제에서는 *myaad*의 Azure AD에 있는 Azure AD 애플리케이션 *myapp*에 대한 로그인을 만듭니다.

```sql
CREATE LOGIN [myapp] FROM EXTERNAL PROVIDER
```

### <a name="g-check-newly-added-logins"></a>G. 새로 추가된 로그인 확인

새로 추가된 로그인을 확인하려면 다음 T-SQL 명령을 실행합니다.

```sql
SELECT *
FROM sys.server_principals;
GO
```

## <a name="see-also"></a>참고 항목

- [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [보안 주체](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [암호 정책](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](create-login-transact-sql.md?view=sql-server-2017)|[SQL Database<br />단일 데이터베이스/탄력적 풀](create-login-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />관리되는 인스턴스](create-login-transact-sql.md?view=azuresqldb-mi-current)|**_\* SQL Data<br />Warehouse \*_**|[Analytics Platform<br />System(PDW)](create-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스

## <a name="syntax"></a>구문

```
-- Syntax for Azure SQL Data Warehouse
CREATE LOGIN login_name
 { WITH <option_list> }

<option_list> ::=
    PASSWORD = { 'password' }
    [ , SID = sid ]
```

## <a name="arguments"></a>인수

*login_name* 만들 로그인 이름을 지정합니다. Azure SQL Database는 SQL 로그인만 지원합니다.

PASSWORD **='** password**'* 만들 SQL 로그인의 암호를 지정합니다. 강력한 암호를 사용하세요. 자세한 내용은 [강력한 암호](../../relational-databases/security/strong-passwords.md) 및 [암호 정책](../../relational-databases/security/password-policy.md)을 참조하세요. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 저장된 암호 정보는 솔트 암호의 SHA-512를 사용하여 계산됩니다.

암호는 대소문자를 구분합니다. 암호의 길이는 항상 8자 이상이어야 하며 128자를 초과할 수 없습니다. 암호에는 a-z, A-Z, 0-9 및 영숫자가 아닌 대부분의 문자를 포함할 수 있습니다. 암호는 홑따옴표 또는 *login_name*을 포함할 수 없습니다.

 SID = *sid* 로그인을 다시 만드는데 사용됩니다. SQL Server 인증 로그인에만 적용되고 Windows 인증 로그인에는 적용되지 않습니다. 새 SQL Server 인증 로그인의 SID를 지정합니다. 이 옵션을 사용하지 않으면 SQL Server에서 자동으로 SID를 할당합니다. SID 구조는 SQL Server 버전에 따라 달라집니다. SQL Data Warehouse의 경우 `0x01060000000000640000000000000000`과 GUID를 나타내는 16바이트로 구성된 32바이트(**binary(32)**) 리터럴입니다. `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`)을 입력합니다.

## <a name="remarks"></a>Remarks

- 암호는 대소문자를 구분합니다.
- 로그인을 전송하는 스크립트는 [SQL Server 2005와 SQL Server 2008 인스턴스 간에 로그인 및 암호를 전송하는 방법](https://support.microsoft.com/kb/918992)을 참조하세요.
- 로그인을 만들면 새 로그인이 자동으로 사용하도록 설정되고 해당 로그인에 서버 수준 **CONNECT SQL** 권한이 부여됩니다.
- 액세스를 허용하려면 서버의 [인증 모드](../../relational-databases/security/choose-an-authentication-mode.md)가 로그인 형식과 일치해야 합니다.
- 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.

## <a name="logins"></a>로그인

**CREATE LOGIN** 문은 일괄 처리의 유일한 명령문이어야 합니다.

**sqlcmd**와 같이 SQL Data Warehouse에 연결하는 몇 가지 방법에서는 *\<login>*@*\<server>* 표기법을 사용하여 SQL Data Warehouse 서버 이름을 연결 문자열의 로그인 이름에 추가해야 합니다. 예를 들어 로그인이 `login1`이고 SQL Data Warehouse 서버의 정규화된 이름이 `servername.database.windows.net`인 경우 연결 문자열의 *username* 매개 변수는 `login1@servername`이어야 합니다. *username* 매개 변수의 총 길이는 128문자이므로 *login_name*은 127문자에서 서버 이름의 길이를 뺀 길이로 제한됩니다. 이 예에서는 `login_name`이 10자이므로 `servername`에는 117자까지만 사용할 수 있습니다.

SQL Data Warehouse에서 로그인을 만들려면 master 데이터베이스에 연결해야 합니다.

SQL Server 규칙을 사용하여 \<loginname>@\<servername> 형식의 SQL Server 인증 로그인을 만들 수 있습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버가 **myazureserver**이고 로그인이 **myemail@live.com**인 경우 로그인을 **myemail@live.com@myazureserver**로 제공해야 합니다.

SQL Data Warehouse에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 강제 실행하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.

SQL Data Warehouse 로그인에 대한 자세한 내용은 [Windows Azure SQL Database에서 데이터베이스 및 로그인 관리](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)를 참조하세요.

## <a name="permissions"></a>Permissions

프로비전 프로세스를 통해 만들어진 서버 수준의 보안 주체 로그인이나 master 데이터베이스에서 `loginmanager` 데이터베이스 역할이 할당된 멤버만 새 로그인을 만들 수 있습니다. 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) 및 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).<https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles>을 참조하세요.

## <a name="after-creating-a-login"></a>로그인을 만든 후

로그인을 만든 후 해당 로그인으로 SQL Data Warehouse에 연결할 수 있지만 이 로그인은 **public** 역할에 부여된 권한만 있습니다. 다음 작업 중 일부를 수행하는 것이 좋습니다.

- 데이터베이스에 연결하려면 로그인에 대한 데이터베이스 사용자를 만듭니다. 자세한 내용은 [CREATE USER](../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.
- 데이터베이스에서 사용자에게 권한을 부여하려면 **ALTER SERVER ROLE** ... **ADD MEMBER** 문을 사용하여 기본 제공 데이터베이스 역할 중 하나 또는 사용자 지정 역할에 사용자를 추가하거나 [GRANT](grant-transact-sql.md) 문을 사용하여 사용자에게 권한을 직접 부여합니다. 자세한 내용은 [비관리자 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#non-administrator-users), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles 및 [GRANT](grant-transact-sql.md) 문을 참조합니다.
- 서버 차원의 사용 권한을 부여하려면 master 데이터베이스에서 데이터베이스 사용자를 만들고 **ALTER SERVER ROLE** ... **ADD MEMBER** 문을 사용하여 관리 서버 역할 중 하나에 사용자를 추가합니다. 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) 및 [서버 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles)을 참조하세요.

- **GRANT** 문을 사용하여 새 로그인 또는 해당 로그인을 포함한 역할에 서버 수준 권한을 부여합니다. 자세한 내용은 [GRANT](../../t-sql/statements/grant-transact-sql.md)를 참조하십시오.

## <a name="examples"></a>예

### <a name="a-creating-a-login-with-a-password"></a>1. 암호로 로그인 만들기

다음 예에서는 특정 사용자에 대한 로그인을 만들고 암호를 할당합니다.

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';
GO
```

### <a name="b-creating-a-login-from-a-sid"></a>2. SID에서 로그인 만들기

 다음 예제에서는 우선 SQL Server 인증 로그인을 만들고 로그인의 SID를 결정합니다.

```sql
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';

SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

쿼리는 0x241C11948AEEB749B0D22646DB1A19F2를 SID로 반환합니다. 쿼리는 다른 값을 반환합니다. 다음 문은 로그인을 삭제한 후 로그인을 다시 만듭니다. 이전 쿼리의 SID를 사용합니다.

```sql
DROP LOGIN TestLogin;
GO

CREATE LOGIN TestLogin
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;

SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

## <a name="see-also"></a>참고 항목

- [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [보안 주체](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [암호 정책](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](create-login-transact-sql.md?view=sql-server-2017)|[SQL Database<br />단일 데이터베이스/탄력적 풀](create-login-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />관리되는 인스턴스](create-login-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-login-transact-sql.md?view=azure-sqldw-latest)|**_\* Analytics<br />Platform System(PDW) \*_**

&nbsp;

## <a name="analytics-platform-system"></a>분석 플랫폼 시스템

## <a name="syntax"></a>구문

```
-- Syntax for Analytics Platform System
CREATE LOGIN loginName { WITH <option_list1> | FROM WINDOWS }

<option_list1> ::=
    PASSWORD = { 'password' } [ MUST_CHANGE ]
    [ , <option_list> [ ,... ] ]
  
<option_list> ::=
      CHECK_EXPIRATION = { ON | OFF}
    | CHECK_POLICY = { ON | OFF}
```

## <a name="arguments"></a>인수

*login_name* 만들 로그인 이름을 지정합니다. 로그인에는 SQL Server 로그인, Windows 로그인, 인증서 매핑 로그인 및 비대칭 키 매핑 로그인의 네 가지 유형이 있습니다. Windows 도메인 계정에서 매핑된 로그인을 만들 경우 Windows 2000 이전 버전의 사용자 로그온 이름을 [\<domainName>\\<login_name>] 형식으로 사용해야 합니다. login_name@DomainName 형식의 UPN은 사용할 수 없습니다. 이 문서의 뒷부분에 나오는 예 4를 참조하세요. 인증 로그인은 **sysname** 형식이고 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 하며 '**\\**'을 포함할 수 없습니다. Windows 로그인은 '**\\**'를 포함할 수 없습니다. Active Directory 사용자에 기반한 로그인은 21자 미만의 이름으로 제한됩니다.

PASSWORD **='**_password_' SQL Server 로그인에만 적용됩니다. 만들 로그인의 암호를 지정합니다. 강력한 암호를 사용하세요. 자세한 내용은 [강력한 암호](../../relational-databases/security/strong-passwords.md) 및 [암호 정책](../../relational-databases/security/password-policy.md)을 참조하세요. SQL Server 2012(11.x)부터 저장된 암호 정보는 솔트 암호의 SHA-512를 사용하여 계산됩니다.

암호는 대소문자를 구분합니다. 암호의 길이는 항상 8자 이상이어야 하며 128자를 초과할 수 없습니다. 암호에는 a-z, A-Z, 0-9 및 영숫자가 아닌 대부분의 문자를 포함할 수 있습니다. 암호는 홑따옴표 또는 *login_name*을 포함할 수 없습니다.

MUST_CHANGE는 SQL Server 로그인에만 적용됩니다. 이 옵션을 선택한 경우 새 로그인을 처음 사용할 때 SQL Server에서는 새 암호를 묻는 메시지를 표시합니다.

CHECK_EXPIRATION **=** { ON | **OFF** } SQL Server 로그인에만 적용됩니다. 이 로그인에 암호 만료 정책을 적용할지 여부를 지정합니다. 기본값은 OFF입니다.

CHECK_POLICY **=** { **ON** | OFF } SQL Server 로그인에만 적용됩니다. SQL Server가 실행 중인 컴퓨터의 Windows 암호 정책을 이 로그인에 적용하도록 지정합니다. 기본값은 ON입니다.

Windows 정책에 따라 강력한 암호가 필요한 경우에는 암호에 다음 네 가지 문자 중 세 가지 이상을 포함해야 합니다.

- 대문자(A-Z)
- 소문자(a-z)
- 숫자(0-9)
- 영숫자가 아닌 문자 중 하나(예:  공백,  _,  @,  *,  ^,  %,  !,  $,  #  또는 &)

WINDOWS 로그인이 Windows 로그인에 매핑되도록 지정합니다.

## <a name="remarks"></a>Remarks

- 암호는 대소문자를 구분합니다.
- MUST_CHANGE를 지정한 경우에는 CHECK_EXPIRATION  및 CHECK_POLICY를 ON으로 설정해야 합니다. 그렇지 않으면 문이 실패합니다.
- CHECK_POLICY = OFF와 CHECK_EXPIRATION = ON의 조합은 지원되지 않습니다.
- CHECK_POLICY를 OFF로 설정하면 *lockout_time*이 재설정되고 CHECK_EXPIRATION이 OFF로 설정됩니다.

> [!IMPORTANT]
> CHECK_EXPIRATION 및 CHECK_POLICY는 Windows Server 2003 이상 버전에서만 적용됩니다. 자세한 내용은 [Password Policy](../../relational-databases/security/password-policy.md)을 참조하세요.

- 로그인을 전송하는 스크립트는 [SQL Server 2005와 SQL Server 2008 인스턴스 간에 로그인 및 암호를 전송하는 방법](https://support.microsoft.com/kb/918992)을 참조하세요.
- 로그인을 만들면 새 로그인이 자동으로 사용하도록 설정되고 해당 로그인에 서버 수준 **CONNECT SQL** 권한이 부여됩니다.
- 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.

## <a name="permissions"></a>Permissions

서버의 **ALTER ANY LOGIN** 권한 또는 **securityadmin** 고정 서버 역할의 멤버 자격이 있는 사용자만 로그인을 만들 수 있습니다. 자세한 내용은 [서버 수준 역할](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) 및 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).<https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles>을 참조하세요.

## <a name="after-creating-a-login"></a>로그인을 만든 후

로그인을 만든 후 해당 로그인으로 SQL Data Warehouse에 연결할 수 있지만 이 로그인은 **public** 역할에 부여된 권한만 있습니다. 다음 작업 중 일부를 수행하는 것이 좋습니다.

- 데이터베이스에 연결하려면 로그인에 대한 데이터베이스 사용자를 만듭니다. 자세한 내용은 [CREATE USER](../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.
- [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md)을 사용하여 사용자 정의 서버 역할을 만듭니다. **ALTER SERVER ROLE** ... **ADD MEMBER**를 사용하여 사용자 정의 서버 역할에 새 로그인을 추가합니다. 자세한 내용은 [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) 및 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)을 참조하세요.
- **sp_addsrvrolemember**를 사용하여 고정 서버 역할에 로그인을 추가합니다. 자세한 내용은 [서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md) 및 [sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)을 참조하세요.
- **GRANT** 문을 사용하여 새 로그인 또는 해당 로그인을 포함한 역할에 서버 수준 권한을 부여합니다. 자세한 내용은 [GRANT](../../t-sql/statements/grant-transact-sql.md)를 참조하십시오.

## <a name="examples"></a>예

### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. 암호를 사용하여 SQL Server 인증 로그인 만들기

다음 예제에서는 암호 `A2c3456`을 사용하여 로그인 `Mary7`을 만듭니다.

```sql
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;
```

### <a name="h-using-options"></a>H. USING 옵션

다음 예제에서는 암호 및 몇 개의 선택적 인수를 사용하여 로그인 `Mary8`을 만듭니다.

```sql
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,
CHECK_EXPIRATION = ON,
CHECK_POLICY = ON;
```

### <a name="i-creating-a-login-from-a-windows-domain-account"></a>9. Windows 도메인 계정에서 로그인 만들기

다음 예제에서는 `Contoso` 도메인의 `Mary`라는 Windows 도메인 계정에서 로그인을 만듭니다.

```sql
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;
GO
```

## <a name="see-also"></a>참고 항목

- [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [보안 주체](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [암호 정책](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)

---

::: moniker-end
