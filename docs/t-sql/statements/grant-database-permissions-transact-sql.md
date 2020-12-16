---
description: GRANT 데이터베이스 사용 권한(Transact-SQL)
title: GRANT Database Permissions(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server]
- database permissions [SQL Server]
- granting permissions [SQL Server], databases
- permissions [SQL Server], databases
- database permissions [SQL Server], granting
- GRANT statement, databases
ms.assetid: 499e5ed6-945c-4791-ab45-68dec0b9c289
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5dc5771af62394dfd8c69bba4faaa52b07b4a5bb
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489943"
---
# <a name="grant-database-permissions-transact-sql"></a>GRANT 데이터베이스 사용 권한(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스에 대한 사용 권한을 부여합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql

GRANT <permission> [ ,...n ]
    TO <database_principal> [ ,...n ] [ WITH GRANT OPTION ]
    [ AS <database_principal> ]

<permission>::=
permission | ALL [ PRIVILEGES ]

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

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

*permission* 데이터베이스에 대해 부여할 수 있는 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.

ALL 이 옵션은 모든 가능한 권한을 부여하지 않습니다. ALL을 부여하는 것은 다음 사용 권한을 부여하는 것과 동일합니다. BACKUP DATABASE, BACKUP LOG, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE, CREATE VIEW.

PRIVILEGES ANSI-92 준수를 위해 포함됩니다. ALL의 동작을 변경하지 않습니다.

WITH GRANT OPTION 지정된 권한을 다른 보안 주체에게 부여할 수 있는 권한도 이 보안 주체에 제공됨을 나타냅니다.

AS \<database_principal> 이 쿼리를 실행하는 보안 주체의 사용 권한 부여 권한이 파생되는 다른 보안 주체를 지정합니다.

*Database_user* 데이터베이스 사용자를 지정합니다.

*Database_role* 데이터베이스 역할을 지정합니다.

*Application_role*
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]

애플리케이션 역할을 지정합니다.

*Database_user_mapped_to_Windows_User*
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

Windows 사용자로 매핑된 데이터베이스 사용자를 지정합니다.

*Database_user_mapped_to_Windows_Group*
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

Windows 그룹으로 매핑된 데이터베이스 사용자를 지정합니다.

*Database_user_mapped_to_certificate*
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

인증서로 매핑된 데이터베이스 사용자를 지정합니다.

*Database_user_mapped_to_asymmetric_key*
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상

비대칭 키로 매핑된 데이터베이스 사용자를 지정합니다.

*Database_user_with_no_login* 해당하는 서버 수준 보안 주체가 없는 데이터베이스 사용자를 지정합니다.

## <a name="remarks"></a>설명

> [!IMPORTANT]
> 일부 경우에서 ALTER 사용 권한과 REFERENCE 사용 권한의 조합을 사용하면 피부여자가 데이터를 보거나 권한 없는 함수를 실행할 수 있습니다. 예를 들면 다음과 같습니다. 테이블에 대한 ALTER 권한과 함수에 대한 REFERENCE 권한을 가진 사용자는 함수를 통해 계산 열을 만들고 실행할 수 있습니다. 이 경우 계산 열에 대한 SELECT 사용 권한도 있어야 합니다.

데이터베이스는 사용 권한 계층에서 해당 데이터베이스의 부모인 서버에 포함된 보안 개체입니다. 다음 표에는 데이터베이스에 대해 부여할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.

|데이터베이스 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|서버 사용 권한에 포함된 사용 권한|
|-------------------------|------------------------------------|----------------------------------|
|ADMINISTER DATABASE BULK OPERATIONS<br/>**적용 대상:** [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].|CONTROL|CONTROL SERVER|
|ALTER|CONTROL|ALTER ANY DATABASE|
|ALTER ANY APPLICATION ROLE|ALTER|CONTROL SERVER|
|ALTER ANY ASSEMBLY|ALTER|CONTROL SERVER|
|ALTER ANY ASYMMETRIC KEY|ALTER|CONTROL SERVER|
|ALTER ANY CERTIFICATE|ALTER|CONTROL SERVER|
|ALTER ANY COLUMN ENCRYPTION KEY|ALTER|CONTROL SERVER|
|ALTER ANY COLUMN MASTER KEY DEFINITION|ALTER|CONTROL SERVER|
|ALTER ANY CONTRACT|ALTER|CONTROL SERVER|
|ALTER ANY DATABASE AUDIT|ALTER|ALTER ANY SERVER AUDIT|
|ALTER ANY DATABASE DDL TRIGGER|ALTER|CONTROL SERVER|
|ALTER ANY DATABASE EVENT NOTIFICATION|ALTER|ALTER ANY EVENT NOTIFICATION|
|ALTER ANY DATABASE EVENT SESSION<br />**적용 대상**: [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].|ALTER|ALTER ANY EVENT SESSION|
|ALTER ANY DATABASE SCOPED CONFIGURATION<br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|CONTROL|CONTROL SERVER|
|ALTER ANY DATASPACE|ALTER|CONTROL SERVER|
|ALTER ANY EXTERNAL DATA SOURCE|ALTER|CONTROL SERVER|
|ALTER ANY EXTERNAL FILE FORMAT|ALTER|CONTROL SERVER|
|ALTER ANY EXTERNAL LIBRARY <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].|CONTROL|CONTROL SERVER |
|ALTER ANY FULLTEXT CATALOG|ALTER|CONTROL SERVER|
|ALTER ANY MASK|CONTROL|CONTROL SERVER|
|ALTER ANY MESSAGE TYPE|ALTER|CONTROL SERVER|
|ALTER ANY REMOTE SERVICE BINDING|ALTER|CONTROL SERVER|
|ALTER ANY ROLE|ALTER|CONTROL SERVER|
|ALTER ANY ROUTE|ALTER|CONTROL SERVER|
|ALTER ANY SCHEMA|ALTER|CONTROL SERVER|
|ALTER ANY SECURITY POLICY<br /> **적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|CONTROL|CONTROL SERVER|
|ALTER ANY SERVICE|ALTER|CONTROL SERVER|
|ALTER ANY SYMMETRIC KEY|ALTER|CONTROL SERVER|
|ALTER ANY USER|ALTER|CONTROL SERVER|
|AUTHENTICATE|CONTROL|AUTHENTICATE SERVER|
|BACKUP DATABASE|CONTROL|CONTROL SERVER|
|BACKUP LOG|CONTROL|CONTROL SERVER|
|CHECKPOINT|CONTROL|CONTROL SERVER|
|CONNECT|CONNECT REPLICATION|CONTROL SERVER|
|CONNECT REPLICATION|CONTROL|CONTROL SERVER|
|CONTROL|CONTROL|CONTROL SERVER|
|CREATE AGGREGATE|ALTER|CONTROL SERVER|
|CREATE ANY EXTERNAL LIBRARY <br /> **적용 대상**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].|CONTROL|CONTROL SERVER |
|CREATE ASSEMBLY|ALTER ANY ASSEMBLY|CONTROL SERVER|
|CREATE ASYMMETRIC KEY|ALTER ANY ASYMMETRIC KEY|CONTROL SERVER|
|CREATE CERTIFICATE|ALTER ANY CERTIFICATE|CONTROL SERVER|
|CREATE CONTRACT|ALTER ANY CONTRACT|CONTROL SERVER|
|CREATE DATABASE|CONTROL|CREATE ANY DATABASE|
|CREATE DATABASE DDL EVENT NOTIFICATION|ALTER ANY DATABASE EVENT NOTIFICATION|CREATE DDL EVENT NOTIFICATION|
|CREATE DEFAULT|ALTER|CONTROL SERVER|
|CREATE FULLTEXT CATALOG|ALTER ANY FULLTEXT CATALOG|CONTROL SERVER|
|CREATE FUNCTION|ALTER|CONTROL SERVER|
|CREATE MESSAGE TYPE|ALTER ANY MESSAGE TYPE|CONTROL SERVER|
|CREATE PROCEDURE|ALTER|CONTROL SERVER|
|CREATE QUEUE|ALTER|CONTROL SERVER|
|CREATE REMOTE SERVICE BINDING|ALTER ANY REMOTE SERVICE BINDING|CONTROL SERVER|
|CREATE ROLE|ALTER ANY ROLE|CONTROL SERVER|
|CREATE ROUTE|ALTER ANY ROUTE|CONTROL SERVER|
|CREATE RULE|ALTER|CONTROL SERVER|
|CREATE SCHEMA|ALTER ANY SCHEMA|CONTROL SERVER|
|CREATE SERVICE|ALTER ANY SERVICE|CONTROL SERVER|
|CREATE SYMMETRIC KEY|ALTER ANY SYMMETRIC KEY|CONTROL SERVER|
|CREATE SYNONYM|ALTER|CONTROL SERVER|
|CREATE TABLE|ALTER|CONTROL SERVER|
|CREATE TYPE|ALTER|CONTROL SERVER|
|CREATE VIEW|ALTER|CONTROL SERVER|
|CREATE XML SCHEMA COLLECTION|ALTER|CONTROL SERVER|
|Delete|CONTROL|CONTROL SERVER|
|CREATE 문을 실행하기 전에|CONTROL|CONTROL SERVER|
|EXECUTE ANY EXTERNAL SCRIPT <br /> **적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)].|CONTROL|CONTROL SERVER|
|EXECUTE EXTERNAL SCRIPT <br /> **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)].|EXECUTE ANY EXTERNAL SCRIPT|CONTROL SERVER|
|INSERT|CONTROL|CONTROL SERVER|
|KILL DATABASE CONNECTION<br />**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|CONTROL|ALTER ANY CONNECTION|
|REFERENCES|CONTROL|CONTROL SERVER|
|SELECT|CONTROL|CONTROL SERVER|
|SHOWPLAN|CONTROL|ALTER TRACE|
|SUBSCRIBE QUERY NOTIFICATIONS|CONTROL|CONTROL SERVER|
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|
|UNMASK|CONTROL|CONTROL SERVER|
|UPDATE|CONTROL|CONTROL SERVER|
|VIEW ANY COLUMN ENCRYPTION KEY DEFINITION|CONTROL|VIEW ANY DEFINITION|
|VIEW ANY COLUMN MASTER KEY DEFINITION|CONTROL|VIEW ANY DEFINITION|
|VIEW DATABASE STATE|CONTROL|VIEW SERVER STATE|
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|

## <a name="permissions"></a>사용 권한

사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다.

AS 옵션을 사용하는 경우 다음과 같은 추가 요구 사항이 적용됩니다.

|AS *granting_principal*|필요한 추가 사용 권한|
|------------------------------|------------------------------------|
|데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|
|Windows 로그인에 매핑된 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|
|Windows 그룹에 매핑된 데이터베이스 사용자|Windows 그룹의 멤버 자격, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|
|인증서에 매핑된 데이터베이스 사용자|db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|
|비대칭 키에 매핑된 데이터베이스 사용자|db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|
|서버 보안 주체에 매핑되지 않은 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|
|데이터베이스 역할|역할에 대한 ALTER 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|
|애플리케이션 역할|역할에 대한 ALTER 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|

개체 소유자는 소유하고 있는 개체에 대한 사용 권한을 부여할 수 있습니다. 보안 개체에 대한 CONTROL 권한을 가진 보안 주체는 해당 보안 개체에 대한 사용 권한을 부여할 수 있습니다.

sysadmin 고정 서버 역할의 멤버와 같이 CONTROL SERVER 사용 권한이 부여된 사용자는 서버의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다.

## <a name="examples"></a>예제

### <a name="a-granting-permission-to-create-tables"></a>A. 테이블을 만들기 위한 사용 권한 부여

다음 예에서는 사용자 `MelanieK`에게 `AdventureWorks` 데이터베이스에 대한 `CREATE TABLE` 권한을 부여합니다.

```sql
USE AdventureWorks;
GRANT CREATE TABLE TO MelanieK;
GO
```

### <a name="b-granting-showplan-permission-to-an-application-role"></a>B. 애플리케이션 역할에 SHOWPLAN 사용 권한 부여

 다음 예에서는 `SHOWPLAN` 애플리케이션 역할에 `AdventureWorks2012` 데이터베이스에 대한 `AuditMonitor` 권한을 부여합니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

```sql
USE AdventureWorks2012;
GRANT SHOWPLAN TO AuditMonitor;
GO
```

### <a name="c-granting-create-view-with-grant-option"></a>C. GRANT OPTION을 지정하여 CREATE VIEW 부여

 다음 예에서는 다른 보안 주체에게 `CREATE VIEW`를 부여할 수 있는 권한이 있는 사용자 `AdventureWorks2012`에게 `CarmineEs` 데이터베이스에 대한 `CREATE VIEW` 권한을 부여합니다.

```sql
USE AdventureWorks2012;
GRANT CREATE VIEW TO CarmineEs WITH GRANT OPTION;
GO
```

### <a name="d-granting-control-permission-to-a-database-user"></a>D. 데이터베이스 사용자에게 CONTROL 권한 부여

 다음 예에서는 데이터베이스 사용자 `Sarah`에게 `AdventureWorks2012` 데이터베이스의 `CONTROL` 권한을 부여합니다. 사용자가 데이터베이스에 존재해야 하며 컨텍스트가 데이터베이스로 설정되어야 합니다.

```sql
USE AdventureWorks2012;
GRANT CONTROL ON DATABASE::AdventureWorks2012 TO Sarah;
GO
```

## <a name="see-also"></a>참고 항목

- [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)
- [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md)
- [GRANT](../../t-sql/statements/grant-transact-sql.md)
- [권한](../../relational-databases/security/permissions-database-engine.md)
- [보안 주체](../../relational-databases/security/authentication-access/principals-database-engine.md)
