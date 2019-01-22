---
title: CREATE USER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WITHOUT_LOGIN_TSQL
- CREATE_USER_TSQL
- SQL13.SWB.DATABASEUSER.OWNEDSCHEMAS.F1
- WITHOUT LOGIN
- CREATE USER
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- adding users
- WITHOUT LOGIN [SQL Server]
- CREATE USER statement
- database user additions [SQL Server]
- USER WITHOUT LOGIN [SQL Server]
- users [SQL Server], adding
- users [SQL Server]
ms.assetid: 01de7476-4b25-4d58-85b7-1118fe64aa80
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0f3f0b40e022db23cfcd650c5f2da4a5a14082d1
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54327584"
---
# <a name="create-user-transact-sql"></a>CREATE USER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스에 사용자를 추가합니다. 12가지 유형의 사용자가 가장 기본적인 구문 샘플과 함께 아래 나열되어 있습니다.  
  
**마스터의 로그인 기반 사용자** - 가장 일반적인 사용자 유형입니다.  
  
-   Windows Active Directory 계정을 기반으로 하는 로그인 기반 사용자입니다. `CREATE USER [Contoso\Fritz];`     
-   Windows 그룹을 기반으로 하는 로그인 기반 사용자 `CREATE USER [Contoso\Sales];`   
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 로그인 기반 사용자 `CREATE USER Mary;`  
  
**데이터베이스에서 인증하는 사용자** - 데이터베이스의 이식성을 높이기 위해 사용하는 것이 좋습니다.  
 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]에 항상 허용됩니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에 포함된 데이터베이스에서만 사용할 수 있습니다.  
  
-   로그인이 없는 Windows 사용자 기반 사용자 `CREATE USER [Contoso\Fritz];`    
-   로그인이 없는 Windows 그룹 기반 사용자 `CREATE USER [Contoso\Sales];`  
-   Azure Active Directory 사용자에 기반한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 또는 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]의 사용자. `CREATE USER [Contoso\Fritz] FROM EXTERNAL PROVIDER;`     

-   암호가 있는 포함된 데이터베이스 사용자 ([!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]에서 사용할 수 없습니다.) `CREATE USER Mary WITH PASSWORD = '********';`   
  
**Windows 그룹 로그인을 통해 연결하는 Windows 보안 주체 기반 사용자**  
  
-   로그인이 없지만 Windows 그룹의 멤버 자격을 통해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결할 수 있는 Windows 사용자 기반 사용자 `CREATE USER [Contoso\Fritz];`  
  
-   로그인이 없지만 다른 Windows 그룹의 멤버 자격을 통해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결할 수 있는 Windows 그룹 기반 사용자 `CREATE USER [Contoso\Fritz];`  
  
**인증할 수 없는 사용자** - 이러한 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 로그인할 수 없습니다.  
  
-   로그인이 없는 사용자. 로그인할 수는 없지만 권한을 부여받을 수 있습니다. `CREATE USER CustomApp WITHOUT LOGIN;`    
-   인증서 기반 사용자. 로그인할 수는 없지만 권한을 부여받고 모듈에 서명할 수 있습니다. `CREATE USER TestProcess FOR CERTIFICATE CarnationProduction50;`  
-   비대칭 키 기반 사용자. 로그인할 수는 없지만 권한을 부여받고 모듈에 서명할 수 있습니다. `CREATE User TestProcess FROM ASYMMETRIC KEY PacificSales09;`   
 
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, and Azure SQL Database Managed Instance
  
-- Syntax Users based on logins in master  
CREATE USER user_name   
    [   
        { FOR | FROM } LOGIN login_name   
    ]  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
-- Users that authenticate at the database  
CREATE USER   
    {  
      windows_principal [ WITH <options_list> [ ,... ] ]  
  
    | user_name WITH PASSWORD = 'password' [ , <options_list> [ ,... ]   
    | Azure_Active_Directory_principal FROM EXTERNAL PROVIDER   
    }  
  
 [ ; ]  
  
-- Users based on Windows principals that connect through Windows group logins  
CREATE USER   
    {   
          windows_principal [ { FOR | FROM } LOGIN windows_principal ]  
        | user_name { FOR | FROM } LOGIN windows_principal  
}  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
-- Users that cannot authenticate   
CREATE USER user_name   
    {  
         WITHOUT LOGIN [ WITH <limited_options_list> [ ,... ] ]  
       | { FOR | FROM } CERTIFICATE cert_name   
       | { FOR | FROM } ASYMMETRIC KEY asym_key_name   
    }  
 [ ; ]  
  
<options_list> ::=  
      DEFAULT_SCHEMA = schema_name  
    | DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }  
    | SID = sid   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
<limited_options_list> ::=  
      DEFAULT_SCHEMA = schema_name ]   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
-- SQL Database syntax when connected to a federation member  
CREATE USER user_name  
[;]

-- Syntax for users based on Azure AD logins for Azure SQL Database Managed Instance
CREATE USER user_name   
    [   { FOR | FROM } LOGIN login_name  ]  
    | FROM EXTERNAL PROVIDER
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  

<limited_options_list> ::=  
      DEFAULT_SCHEMA = schema_name 
    | DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ] 
```

> [!IMPORTANT]
> SQL Database Managed Instance에 대한 Azure AD 로그인은 **공개 미리 보기**에 있습니다.

```  
-- Syntax for Azure SQL Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM } { LOGIN login_name }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]

CREATE USER Azure_Active_Directory_principal FROM EXTERNAL PROVIDER  
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]
``` 
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM }  
      {   
        LOGIN login_name   
      }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *user_name*  
 이 데이터베이스 내에서 사용자를 식별하는 이름을 지정합니다. *user_name*은 **sysname**입니다. 최대 128자까지 지정할 수 있습니다. Windows 보안 주체 기반 사용자를 만드는 경우 다른 사용자 이름을 지정하지 않으면 Windows 보안 주체 이름이 사용자 이름이 됩니다.  
  
 LOGIN *login_name*  
 데이터베이스 사용자를 만들 로그인을 지정합니다. *login_name*은 서버에서 유효한 로그인이어야 합니다. Windows 보안 주체(사용자 또는 그룹)를 기반으로 하는 로그인이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 로그인일 수 있습니다. 이 SQL Server 로그인이 데이터베이스에 들어가면 생성 중인 데이터베이스 사용자의 이름과 ID를 획득합니다. Windows 보안 주체에서 매핑된 로그인을 만들 때는 **[**_\<domainName\>_**\\**_\<loginName\>_**]** 형식을 사용하세요. 예제는 [구문 요약](#SyntaxSummary)을 참조하세요.  
  
 CREATE USER 문이 SQL 일괄 처리의 유일한 문인 경우 Microsoft Azure SQL Database는 WITH LOGIN 절을 지원합니다. CREATE USER 문이 SQL 일괄 처리의 유일한 문이 아니거나 동적 SQL에서 실행되는 경우 WITH LOGIN 절이 지원되지 않습니다.  
  
 WITH DEFAULT_SCHEMA = *schema_name*  
 서버에서 이 데이터베이스 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색하는 스키마를 지정합니다.  
  
 '*windows_principal*'  
 데이터베이스 사용자를 만들 Windows 보안 주체를 지정합니다. *windows_principal*은 Windows 사용자 또는 Windows 그룹일 수 있습니다. *windows_principal*에 로그인이 없어도 사용자가 만들어집니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 때 *windows_principal*에 로그인이 없는 경우 Windows 보안 주체가 로그인이 있는 Windows 그룹의 멤버 자격을 통해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 인증하거나, 연결 문자열에서 포함된 데이터베이스를 초기 카탈로그로 지정해야 합니다. Windows 보안 주체에서 사용자를 만들 때는 **[**_\<domainName\>_**\\**_\<loginName\>_**]** 형식을 사용하세요. 예제는 [구문 요약](#SyntaxSummary)을 참조하세요. Active Directory 사용자에 기반한 사용자는 21자 미만의 이름으로 제한됩니다.
  
 '*Azure_Active_Directory_principal*'  
 **적용 대상**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]  
  
 데이터베이스 사용자를 만들 Azure Active Directory 보안 주체를 지정합니다. *Azure_Active_Directory_principal*은 Azure Active Directory 사용자, Azure Active Directory 그룹 또는 Azure Active Directory 애플리케이션이 될 수 있습니다. (Azure Active Directory 사용자는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 Windows 인증 로그인을 가질 수 없으며 데이터베이스 사용자만 가능합니다.) 연결 문자열은 포함된 데이터베이스를 초기 카탈로그로 지정해야 합니다.

 사용자는 도메인 보안 주체의 전체 별칭을 사용합니다.   
 
-   `CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;`  
  
-   `CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;`

 보안 그룹은 보안 그룹의 *표시 이름*을 사용합니다. *Nurses* 보안 그룹은 다음을 사용합니다.  
  
-   `CREATE USER [Nurses] FROM EXTERNAL PROVIDER;`  
  
 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL 데이터베이스에 연결](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)을 참조하세요.  
  
WITH PASSWORD = '*password*'  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 포함된 데이터베이스에서만 사용할 수 있습니다. 만들 사용자의 암호를 지정합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 저장된 암호 정보는 솔트 암호의 SHA-512를 사용하여 계산됩니다.  
  
WITHOUT LOGIN  
 사용자가 기존 로그인에 매핑되지 않도록 지정합니다.  
  
CERTIFICATE *cert_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 데이터베이스 사용자를 만들 인증서를 지정합니다.  
  
ASYMMETRIC KEY *asym_key_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 데이터베이스 사용자를 만들 비대칭 키를 지정합니다.  
  
DEFAULT_LANGUAGE = *{ NONE | \<lcid> | \<language name> | \<language alias> }*  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  
  
 새 사용자의 기본 언어를 지정합니다. 사용자의 기본 언어가 지정된 경우 데이터베이스의 기본 언어가 나중에 변경되더라도 사용자의 기본 언어는 지정된 대로 유지됩니다. 기본 언어를 지정하지 않으면 사용자의 기본 언어는 데이터베이스의 기본 언어가 됩니다. 사용자의 기본 언어가 지정되지 않은 경우 데이터베이스의 기본 언어가 나중에 변경되면 사용자의 기본 언어는 데이터베이스의 새 기본 언어로 변경됩니다.  
  
> [!IMPORTANT]  
>  *DEFAULT_LANGUAGE*는 포함된 데이터베이스 사용자에 대해서만 사용됩니다.  
  
SID = *sid*  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 포함된 데이터베이스의 암호가 있는 사용자([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증)에만 적용됩니다. 새 데이터베이스 사용자의 SID를 지정합니다. 이 옵션을 선택하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 자동으로 SID를 할당합니다. SID 매개 변수를 사용하여 여러 데이터베이스에 ID(SID)가 동일한 사용자를 만듭니다. 이 옵션은 여러 데이터베이스에 사용자를 만들어 Always On 장애 조치(failover)를 준비하려는 경우에 유용합니다. 사용자의 SID를 확인하려면 sys.database_principals를 쿼리합니다.  
  
ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ]  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]까지  
  
 대량 복사 작업에서 서버에 대한 암호화 메타데이터 검사를 표시하지 않습니다. 이를 통해 사용자는 데이터를 암호 해독하지 않고도 테이블이나 데이터베이스 사이에 암호화된 데이터를 대량 복사할 수 있습니다. 기본값은 OFF입니다.  
  
> [!WARNING]  
>  이 옵션을 부적절하게 사용할 경우 데이터가 손상될 수 있습니다. 자세한 내용은 [상시 암호화로 보호되는 중요한 데이터 마이그레이션](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 FOR LOGIN을 생략하면 새 데이터베이스 사용자는 같은 이름의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑됩니다.  
  
 기본 스키마는 서버에서 이 데이터베이스 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색하는 스키마가 됩니다. 달리 지정하지 않는 한 기본 스키마는 이 데이터베이스 사용자가 만든 개체의 소유자가 됩니다.  
  
 사용자에게 기본 스키마가 있는 경우에는 해당 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없지만 사용자가 기본 스키마가 있는 그룹의 멤버인 경우에는 그룹의 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없고 사용자가 두 개 이상 그룹의 멤버인 경우 principle_id가 가장 낮고 명시적으로 설정된 기본 스키마가 있는 Windows 그룹의 기본 스키마가 사용자의 기본 스키마가 됩니다. 사용할 수 있는 기본 스키마 중 하나를 기본 설정 스키마로 명시적으로 선택할 수는 없습니다. 사용자의 기본 스키마를 확인할 수 없으면 **dbo** 스키마가 사용됩니다.  
  
 DEFAULT_SCHEMA는 가리키는 스키마가 만들어지기 전에 설정될 수 있습니다.  
  
 인증서 또는 비대칭 키에 매핑된 사용자를 생성할 때는 DEFAULT_SCHEMA를 지정할 수 없습니다.  
  
 사용자가 sysadmin 고정 서버 역할의 멤버이면 DEFAULT_SCHEMA 값은 무시됩니다. sysadmin 고정 서버 역할의 모든 멤버는 기본 스키마가 `dbo`입니다.  
  
 WITHOUT LOGIN 절은 SQL Server 로그인에 매핑되지 않는 사용자를 만듭니다. guest와 같은 다른 데이터베이스에 연결할 수 있습니다. 로그인이 없는 사용자에게 사용 권한을 할당할 수 있으며 보안 컨텍스트가 로그인이 없는 사용자로 변경되면 원래 사용자가 로그인이 없는 사용자의 사용 권한을 받습니다. [D. 로그인 없이 사용자 만들기 및 사용](#withoutLogin) 예제를 참조하세요.  
  
 Windows 보안 주체에 매핑되는 사용자만 백슬래시 문자(**\\**)를 포함할 수 있습니다.
  
 게스트 사용자가 이미 모든 데이터베이스 내에 있기 때문에 CREATE USER를 사용하여 게스트 사용자를 만들 수 없습니다. 다음과 같이 CONNECT 권한을 부여하여 게스트 사용자를 사용할 수 있습니다.  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
 데이터베이스 사용자 정보는 [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) 카탈로그 뷰에 표시됩니다.

SQL Database Managed Instance에서 서버 수준 Azure AD 로그인을 생성하기 위해 새 구문 확장인 **FROM EXTERNAL PROVIDER**를 사용할 수 있습니다. Azure AD 로그인은 데이터베이스 수준 Azure AD 보안 주체를 서버 수준 Azure AD 로그인에 매핑되도록 합니다. Azure AD 로그인으로 Azure AD 사용자를 만들려면 다음 구문을 사용합니다.

`CREATE USER [AAD_principal] FROM LOGIN [Azure AD login]`

Azure SQL Database Managed Instance 인스턴스에서 사용자를 만들 때 login_name은 기존 Azure AD 로그인과 일치해야 하며, 그렇지 않으면 **FROM EXTERNAL PROVIDER** 절을 사용하면 마스터 에서 마스터 데이터베이스에 로그인하지 않고 Azure AD 사용자만 생성됩니다. 예를 들어 이 명령은 다음이 포함된 사용자를 만듭니다.

`CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER`
  
##  <a name="SyntaxSummary"></a> 구문 요약  
 **마스터의 로그인 기반 사용자**  
  
 다음 목록에서는 로그인 기반 사용자에 대해 사용할 수 있는 구문을 보여 줍니다. 기본 스키마 옵션은 나열되지 않습니다.  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FOR LOGIN SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FROM LOGIN SQLAUTHLOGIN`  
  
**데이터베이스에서 인증하는 사용자**  
  
 다음 목록에서는 포함된 데이터베이스에서만 사용할 수 있는 사용자에 대한 구문을 보여 줍니다. 생성된 사용자는 **master** 데이터베이스의 로그인에 연결되지 않습니다. 기본 스키마 및 언어 옵션은 나열되지 않습니다.  
  
> [!IMPORTANT]  
>  이 구문은 사용자에게 데이터베이스에 대한 액세스 권한을 부여하며 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 새로운 액세스 권한도 부여합니다.  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER Barry WITH PASSWORD = 'sdjklalie8rew8337!$d'`  
  
**마스터에 로그인이 없는 Windows 보안 주체 기반 사용자**  
  
 다음 목록은 Windows 그룹을 통해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 액세스하지만 **master**에 로그인이 없는 사용자에 대한 구문을 보여 줍니다. 이 구문은 모든 유형의 데이터베이스에서 사용할 수 있습니다. 기본 스키마 및 언어 옵션은 나열되지 않습니다.  
  
 이 구문은 마스터의 로그인을 기반으로 하는 사용자와 유사하지만 이 범주의 사용자는 마스터에 로그인을 가지고 있지 않습니다. 사용자는 Windows 그룹 로그인을 통해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 액세스할 수 있어야 합니다.  
  
 이 구문은 Windows 보안 주체를 기반으로 하는 포함된 데이터베이스 사용자와 유사하지만 이 범주의 사용자는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 새로운 액세스 권한을 부여받지 않습니다.  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
  
**인증할 수 없는 사용자**  
  
 다음 목록에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로그인할 수 없는 사용자에 대한 구문을 보여 줍니다.  
  
-   `CREATE USER RIGHTSHOLDER WITHOUT LOGIN`  
-   `CREATE USER CERTUSER FOR CERTIFICATE SpecialCert`  
-   `CREATE USER CERTUSER FROM CERTIFICATE SpecialCert`  
-   `CREATE USER KEYUSER FOR ASYMMETRIC KEY SecureKey`  
-   `CREATE USER KEYUSER FROM ASYMMETRIC KEY SecureKey`  
  
## <a name="security"></a>보안  
 사용자를 만들면 데이터베이스에 대한 액세스 권한이 부여되지만 데이터베이스 내부의 개체에 대한 액세스 권한은 자동으로 부여되지 않습니다. 사용자를 만든 후에는 대개 데이터베이스 개체에 액세스할 수 있는 권한이 있는 데이터베이스 역할에 사용자를 추가하거나 사용자에게 개체 사용 권한을 부여합니다. 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.  
  
### <a name="special-considerations-for-contained-databases"></a>포함된 데이터베이스에 대한 특별 고려 사항  
 포함된 데이터베이스에 연결하는 경우 사용자에게 **master** 데이터베이스의 로그인이 없으면 연결 문자열에 포함된 데이터베이스 이름이 초기 카탈로그로 포함되어야 합니다. 암호가 있는 포함된 데이터베이스 사용자의 경우 언제나 초기 카탈로그 매개 변수를 지정해야 합니다.  
  
 포함된 데이터베이스에서 사용자를 만들면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스로부터 데이터베이스를 분리하는 데 도움이 됩니다. 데이터베이스를 분리하면 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 데이터베이스를 쉽게 이동할 수 있습니다. 자세한 내용은 [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md) 및 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)를 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 기반 데이터베이스 사용자를 암호가 있는 포함된 데이터베이스 사용자로 변경하려면 [sp_migrate_user_to_contained&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)를 참조하세요.  
  
 포함된 데이터베이스에서 사용자는 **master** 데이터베이스의 로그인을 가질 필요가 없습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 관리자는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 수준이 아니라 데이터베이스 수준에서 포함된 데이터베이스에 대한 액세스 권한을 부여할 수 있음을 이해해야 합니다. 자세한 내용은 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)를 참조하세요.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 포함된 데이터베이스 사용자를 사용하는 경우, 서버 수준 방화벽 규칙 대신 데이터베이스 수준 방화벽 규칙을 사용하여 액세스를 구성합니다. 자세한 내용은 [sp_set_database_firewall_rule&#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)을 참조하세요.
 
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 포함된 데이터베이스 사용자에 대해 SSMS는 Multi-Factor Authentication을 지원할 수 있습니다. 자세한 내용은 [SQL Database 및 SQL Data Warehouse를 사용한 Azure AD MFA에 대한 SSMS 지원](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)을 참조하세요.  
  
### <a name="permissions"></a>Permissions  
 데이터베이스에 대한 ALTER ANY USER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-database-user-based-on-a-sql-server-login"></a>1. SQL Server 로그인 기반 데이터베이스 사용자 만들기  
 다음 예에서는 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이라는 `AbolrousHazem` 로그인을 만든 다음 `AbolrousHazem`에 이에 해당하는 `AdventureWorks2012`이라는 데이터베이스 사용자를 만듭니다.  
  
```  
CREATE LOGIN AbolrousHazem   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
```   
사용자 데이터베이스로 변경합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `USE AdventureWorks2012` 문을 사용합니다. [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 사용자 데이터베이스에 새 연결을 만들어야 합니다.

```   
CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
GO   
```  
  
### <a name="b-creating-a-database-user-with-a-default-schema"></a>2. 기본 스키마로 데이터베이스 사용자 만들기  
 다음 예에서는 암호를 사용하여 `WanidaBenshoof`라는 서버 로그인을 만든 다음 기본 스키마인 `Wanida`을 사용하여 해당 데이터베이스 사용자 `Marketing`를 만듭니다.  
  
```  
CREATE LOGIN WanidaBenshoof   
    WITH PASSWORD = '8fdKJl3$nlNv3049jsKK';  
USE AdventureWorks2012;  
CREATE USER Wanida FOR LOGIN WanidaBenshoof   
    WITH DEFAULT_SCHEMA = Marketing;  
GO  
```  
  
### <a name="c-creating-a-database-user-from-a-certificate"></a>3. 인증서에서 데이터베이스 사용자 만들기  
 다음 예에서는 `JinghaoLiu` 인증서에서 데이터베이스 사용자 `CarnationProduction50`를 만듭니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
USE AdventureWorks2012;  
CREATE CERTIFICATE CarnationProduction50  
    WITH SUBJECT = 'Carnation Production Facility Supervisors',  
    EXPIRY_DATE = '11/11/2011';  
GO  
CREATE USER JinghaoLiu FOR CERTIFICATE CarnationProduction50;  
GO   
```  
  
###  <a name="withoutLogin"></a> 4. 로그인이 없는 사용자 만들기 및 사용  
 다음 예에서는 `CustomApp` 로그인에 매핑되지 않는 데이터베이스 사용자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 만듭니다. 그런 다음 `adventure-works\tengiz0` 사용자를 가장하도록 사용자에게 `CustomApp` 권한을 부여합니다.  
  
```  
USE AdventureWorks2012 ;  
CREATE USER CustomApp WITHOUT LOGIN ;  
GRANT IMPERSONATE ON USER::CustomApp TO [adventure-works\tengiz0] ;  
GO   
```  
  
 `CustomApp` 자격 증명을 사용하기 위해 사용자 `adventure-works\tengiz0`이 다음 문을 실행합니다.  
  
```  
EXECUTE AS USER = 'CustomApp' ;  
GO  
```  
  
 `adventure-works\tengiz0` 자격 증명으로 다시 돌아가려면 사용자는 다음 문을 실행합니다.  
  
```  
REVERT ;  
GO  
```  
  
### <a name="e-creating-a-contained-database-user-with-password"></a>E. 암호가 있는 포함된 데이터베이스 사용자 만들기  
 다음 예에서는 암호가 있는 포함된 데이터베이스 사용자를 만듭니다. 이 예는 포함된 데이터베이스에서만 실행할 수 있습니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 DEFAULT_LANGUAGE가 삭제된 경우 이 예제가 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에서 동작합니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER Carlo  
WITH PASSWORD='RN92piTCh%$!~3K9844 Bl*'  
    , DEFAULT_LANGUAGE=[Brazilian]  
    , DEFAULT_SCHEMA=[dbo]  
GO   
```  
  
### <a name="f-creating-a-contained-database-user-for-a-domain-login"></a>F. 도메인 로그인에 대한 포함된 데이터베이스 사용자 만들기  
 다음 예에서는 Contoso라는 도메인의 Fritz라는 로그인에 대한 포함된 데이터베이스 사용자를 만듭니다. 이 예는 포함된 데이터베이스에서만 실행할 수 있습니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER [Contoso\Fritz] ;  
GO   
```  
  
### <a name="g-creating-a-contained-database-user-with-a-specific-sid"></a>G. 특정 SID가 있는 포함된 데이터베이스 사용자 만들기  
 다음 예에서는 CarmenW라는 SQL Server 인증 포함된 데이터베이스 사용자를 만듭니다. 이 예는 포함된 데이터베이스에서만 실행할 수 있습니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER CarmenW WITH PASSWORD = 'a8ea v*(Rd##+'  
, SID = 0x01050000000000090300000063FF0451A9E7664BA705B10E37DDC4B7;  
  
```  
  
### <a name="h-creating-a-user-to-copy-encrypted-data"></a>H. 암호화된 데이터를 복사할 사용자 만들기  
 다음 예에서는 Always Encrypted 기능으로 보호되는 데이터를 암호화된 열이 있는 테이블 집합에서 암호화된 열이 있는 또 다른 테이블 집합으로(동일하거나 다른 데이터베이스에 있음) 복사할 수 있는 사용자를 만듭니다.  자세한 내용은 [상시 암호화로 보호되는 중요한 데이터 마이그레이션](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)을 참조하세요.  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]까지  
  
```  
CREATE USER [Chin]   
WITH   
      DEFAULT_SCHEMA = dbo  
    , ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON ;  
```

### <a name="i-create-an-azure-ad-user-from-an-azure-ad-login-in-sql-database-managed-instance"></a>9. SQL Database Managed Instance의 Azure AD 로그인에서 Azure AD 사용자 만들기

 Azure AD 로그인으로 Azure AD 사용자를 만들려면 다음 구문을 사용합니다.

 `sysadmin` 역할로 부여된 Azure AD 로그인을 사용하여 Managed Instance에 로그인합니다. 다음은 로그인 bob@contoso.com에서 Azure AD 사용자 bob@contoso.com을 만듭니다. 이 로그인은 [CREATE LOGIN](create-login-transact-sql.md#d-creating-a-login-for-a-federated-azure-ad-account) 예제에서 생성되었습니다.

```sql
CREATE USER [bob@contoso.com] FROM LOGIN [bob@contoso.com];
GO
```

> [!IMPORTANT]
> Azure AD 로그인에서 **USER**를 만들 때 **LOGIN**에서 *user_name*을 동일한 *login_name*으로 지정합니다.

그룹인 Azure AD 로그인에서 Azure AD 사용자를 그룹으로 만드는 것이 지원됩니다.

```sql
CREATE USER [AAD group] FROM LOGIN [AAD group];
GO
```

그룹인 Azure AD 로그인에서 Azure AD 사용자를 생성할 수도 있습니다.

```sql
CREATE USER [bob@contoso.com] FROM LOGIN [AAD group];
GO
```

### <a name="j-create-an-azure-ad-user-without-an-aad-login-for-the-database"></a>J. 데이터베이스에 대한 AAD 로그인 없이 Azure AD 사용자 만들기

다음 구문은 SQL Database Managed Instance 데이터베이스(포함된 사용자)에서 Azure AD 사용자 bob@contoso.com을 만드는 데 사용됩니다.

```sql
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
GO
```

## <a name="next-steps"></a>다음 단계  
사용자가 생성되면 [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) 문을 사용하여 데이터베이스 역할에 사용자를 추가하는 것이 좋습니다.  
테이블에 액세스할 수 있도록 역할에 [GRANT 개체 사용 권한](../../t-sql/statements/grant-object-permissions-transact-sql.md)을 수행할 수도 있습니다. SQL Server 보안 모델에 대한 일반적인 내용은 [사용 권한](../../relational-databases/security/permissions-database-engine.md)을 참조하세요.   
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 사용자 만들기](../../relational-databases/security/authentication-access/create-a-database-user.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [ALTER USER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)   
 [Azure Active Directory 인증을 사용하여 SQL Database에 연결](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)   
 [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  


