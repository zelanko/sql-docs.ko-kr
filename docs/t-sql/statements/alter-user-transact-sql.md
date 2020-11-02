---
description: ALTER USER(Transact-SQL)
title: ALTER USER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_USER_TSQL
- ALTER USER
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database users
- ALTER USER statement
- renaming databases
- schemas [SQL Server], default
- database user names [SQL Server]
- names [SQL Server], database users
- default schemas
- modifying default schemas
ms.assetid: 344fc6ce-a008-47c8-a02e-47fae66cc590
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ecb1710f992535ca4e6ebca3a3f825c5e1bffc9a
ms.sourcegitcommit: d35d0901296580bfceda6e0ab2e14cf2b7e99a0f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92496973"
---
# <a name="alter-user-transact-sql"></a>ALTER USER(Transact-SQL)

데이터베이스 사용자의 이름을 바꾸거나 기본 스키마를 변경합니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-user-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-user-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-user-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](alter-user-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server"></a>SQL Server

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for SQL Server

ALTER USER userName
 WITH <set_item> [ ,...n ]
[;]

<set_item> ::=
NAME = newUserName
| DEFAULT_SCHEMA = { schemaName | NULL }
| LOGIN = loginName
| PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]
| DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }
| ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]
```

## <a name="arguments"></a>인수

 *userName* 이 데이터베이스 내에서 사용자를 식별하는 이름을 지정합니다.

 LOGIN **=** _loginName_ 사용자의 SID(보안 식별자)를 다른 로그인의 SID와 일치하도록 변경하여 사용자를 다른 로그인으로 다시 매핑합니다.

 NAME **=** _newUserName_ 이 사용자의 새 이름을 지정합니다. *newUserName* 은 현재 데이터베이스에 아직 없는 이름이어야 합니다.

 DEFAULT_SCHEMA **=** { *schemaName* | NULL } 서버에서 이 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색할 스키마를 지정합니다. 기본 스키마를 NULL로 설정하면 Windows 그룹에서 기본 스키마가 제거됩니다. Windows 사용자에는 NULL 옵션을 사용할 수 없습니다.

 PASSWORD **=** ' *password* '  **적용 대상** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

 변경할 사용자의 암호를 지정합니다. 암호는 대소문자를 구분합니다.

> [!NOTE]
> 이 옵션은 포함된 사용자에 대해서만 사용할 수 있습니다. 자세한 내용은 [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md) 및 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)를 참조하세요.

 OLD_PASSWORD **=** _'oldpassword'_ **적용 대상** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

 ' *암호* '로 바뀔 현재 사용자 암호입니다. 암호는 대소문자를 구분합니다. **ALTER ANY USER** 권한이 없으면 *OLD_PASSWORD* 가 있어야 암호를 변경할 수 있습니다. *OLD_PASSWORD* 를 요구하면 **IMPERSONATION** 권한을 가진 사용자가 암호를 변경할 수 없습니다.

> [!NOTE]
> 이 옵션은 포함된 사용자에 대해서만 사용할 수 있습니다.

 DEFAULT_LANGUAGE **=** _{ NONE \| \<lcid> \| \<language name> \| \<language alias> }_ **적용 대상** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상.

 사용자에게 할당할 기본 언어를 지정합니다. 이 옵션을 NONE으로 설정하면 기본 언어가 데이터베이스의 현재 기본 언어로 설정됩니다. 나중에 데이터베이스의 기본 언어가 변경되더라도 사용자의 기본 언어는 그대로 유지됩니다. *DEFAULT_LANGUAGE* 는 로컬 ID(lcid), 언어 이름 또는 언어 별칭이 될 수 있습니다.

> [!NOTE]
> 이 옵션은 포함된 데이터베이스에서 포함된 사용자에 대해서만 지정할 수 있습니다.

 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ]  **적용 대상** : [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

 대량 복사 작업에서 서버에 대한 암호화 메타데이터 검사를 표시하지 않습니다. 이를 통해 사용자는 데이터를 암호 해독하지 않고도 테이블이나 데이터베이스 사이에 암호화된 데이터를 대량 복사할 수 있습니다. 기본값은 OFF입니다.

> [!WARNING]
> 이 옵션을 부적절하게 사용할 경우 데이터가 손상될 수 있습니다. 자세한 내용은 [상시 암호화로 보호되는 중요한 데이터 마이그레이션](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)을 참조하세요.

## <a name="remarks"></a>설명

 기본 스키마는 서버에서 이 데이터베이스 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색하는 스키마가 됩니다. 달리 지정하지 않는 한 기본 스키마는 이 데이터베이스 사용자가 만든 개체의 소유자가 됩니다.

 사용자에게 기본 스키마가 있는 경우에는 해당 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없지만 사용자가 기본 스키마가 있는 그룹의 멤버인 경우에는 그룹의 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없고 사용자가 두 개 이상 그룹의 멤버인 경우 principle_id가 가장 낮고 명시적으로 설정된 기본 스키마가 있는 Windows 그룹의 기본 스키마가 사용자의 기본 스키마가 됩니다. 사용자의 기본 스키마를 확인할 수 없으면 **dbo** 스키마가 사용됩니다.

 DEFAULT_SCHEMA는 현재 데이터베이스에 없는 스키마로 설정할 수 있습니다. 따라서 해당 스키마가 생성되기 전에 DEFAULT_SCHEMA를 사용자에게 할당할 수 있습니다.

 인증서 또는 비대칭 키에 매핑된 사용자에는 DEFAULT_SCHEMA를 지정할 수 없습니다.

> [!IMPORTANT]
> 사용자가 **sysadmin** 고정 서버 역할의 멤버이면 DEFAULT_SCHEMA 값은 무시됩니다. **sysadmin** 고정 서버 역할의 모든 멤버는 기본 스키마가 `dbo`입니다.

 새 사용자 이름의 SID가 데이터베이스에 기록된 SID와 일치할 때만 Windows 로그인 또는 그룹에 매핑된 사용자의 이름을 변경할 수 있습니다. 이 검사는 데이터베이스에서 Windows 로그인의 스푸핑을 방지하는 데 도움이 됩니다.

 WITH LOGIN 절을 사용하면 사용자를 다른 로그인으로 다시 매핑할 수 있습니다. 로그인이 없는 사용자, 인증서로 매핑된 사용자 또는 비대칭 키에 매핑된 사용자는 이 절을 사용하여 다시 매핑할 수 없습니다. SQL 사용자 및 Windows 사용자(또는 그룹)만 다시 매핑할 수 있습니다. WITH LOGIN 절은 Windows 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인으로 변경하는 것과 같이 사용자 유형을 변경하는 데는 사용할 수 없습니다.

 다음 조건이 충족되면 사용자 이름이 로그인 이름으로 자동 변경됩니다.

- 사용자가 Windows 사용자입니다.

- 이름이 Windows 이름입니다(백슬래시 포함).

- 새 이름이 지정되지 않았습니다.

- 현재 이름이 로그인 이름과 다릅니다.

 위의 조건을 충족하지 않으면 사용자 이름이 변경되지 않으며 호출자가 NAME 절을 추가로 호출해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 인증서 또는 비대칭 키에 매핑된 사용자 이름에는 백 슬래시 문자(\\)를 사용할 수 없습니다.

> [!CAUTION]
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]

## <a name="security"></a>보안

> [!NOTE]
> **ALTER ANY USER** 권한이 있는 사용자는 모든 사용자의 기본 스키마를 변경할 수 있습니다. 스키마가 변경된 사용자는 자신도 모르는 사이 잘못된 테이블에서 데이터를 선택하거나 잘못된 스키마의 코드를 실행할 수 있습니다.

### <a name="permissions"></a>사용 권한

 사용자의 이름을 변경하려면 **ALTER ANY USER** 권한이 필요합니다.

 사용자의 대상 로그인을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 데이터베이스에 대한 **CONTROL** 권한이 있는 사용자의 사용자 이름을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 기본 스키마나 언어를 변경하려면 사용자에 대한 **ALTER** 권한이 필요합니다. 사용자는 자신의 기본 스키마 또는 언어를 변경할 수 있습니다.

## <a name="examples"></a>예제

모든 예제는 사용자 데이터베이스에서 실행됩니다.

### <a name="a-changing-the-name-of-a-database-user"></a>A. 데이터베이스 사용자의 이름 변경

 다음 예에서는 데이터베이스 사용자 `Mary5`의 이름을 `Mary51`로 변경합니다.

```sql
ALTER USER Mary5 WITH NAME = Mary51;
GO
```

### <a name="b-changing-the-default-schema-of-a-user"></a>B. 사용자의 기본 스키마 변경

 다음 예에서는 `Mary51` 사용자의 기본 스키마를 `Purchasing`으로 변경합니다.

```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;
GO
```

### <a name="c-changing-several-options-at-once"></a>C. 한 번에 여러 옵션 변경

 다음 예에서는 포함된 데이터베이스 사용자에 대해 여러 옵션을 하나의 문에서 변경합니다.

**적용 대상** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상

```sql
ALTER USER Philip
WITH NAME = Philipe
, DEFAULT_SCHEMA = Development
, PASSWORD = 'W1r77TT98%ab@#' OLD_PASSWORD = 'New Devel0per'
, DEFAULT_LANGUAGE= French ;
GO
```

## <a name="see-also"></a>참고 항목

- [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
- [DROP USER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
- [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)
- [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-user-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        **_\* SQL Database \*_**
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-user-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-user-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](alter-user-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-database"></a>SQL Database

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for Azure SQL Database

ALTER USER userName
 WITH <set_item> [ ,...n ]

<set_item> ::=
NAME = newUserName
| DEFAULT_SCHEMA = schemaName
| LOGIN = loginName
| ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]
[;]

-- Azure SQL Database Update Syntax
ALTER USER userName
 WITH <set_item> [ ,...n ]
[;]

<set_item> ::=
NAME = newUserName
| DEFAULT_SCHEMA = { schemaName | NULL }
| LOGIN = loginName
| PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]
| ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]

-- SQL Database syntax when connected to a federation member
ALTER USER userName
 WITH <set_item> [ ,... n ]
[;]

<set_item> ::=
 NAME = newUserName
```

## <a name="arguments"></a>인수

 *userName* 이 데이터베이스 내에서 사용자를 식별하는 이름을 지정합니다.

 LOGIN **=** _loginName_ 사용자의 SID(보안 식별자)를 다른 로그인의 SID와 일치하도록 변경하여 사용자를 다른 로그인으로 다시 매핑합니다.

 ALTER USER 문이 SQL 일괄 처리의 유일한 문인 경우 Azure SQL Database는 WITH LOGIN 절을 지원합니다. ALTER USER 문이 SQL 일괄 처리의 유일한 문이 아니거나 동적 SQL에서 실행되는 경우 WITH LOGIN 절이 지원되지 않습니다.

 NAME **=** _newUserName_ 이 사용자의 새 이름을 지정합니다. *newUserName* 은 현재 데이터베이스에 아직 없는 이름이어야 합니다.

 DEFAULT_SCHEMA **=** { *schemaName* | NULL } 서버에서 이 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색할 스키마를 지정합니다. 기본 스키마를 NULL로 설정하면 Windows 그룹에서 기본 스키마가 제거됩니다. Windows 사용자에는 NULL 옵션을 사용할 수 없습니다.

 PASSWORD **=** ' *password* '  **적용 대상** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

 변경할 사용자의 암호를 지정합니다. 암호는 대소문자를 구분합니다.

> [!NOTE]
> 이 옵션은 포함된 사용자에 대해서만 사용할 수 있습니다. 자세한 내용은 [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md) 및 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)를 참조하세요.

 OLD_PASSWORD **=** _'oldpassword'_ **적용 대상** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

 ' *암호* '로 바뀔 현재 사용자 암호입니다. 암호는 대소문자를 구분합니다. **ALTER ANY USER** 권한이 없으면 *OLD_PASSWORD* 가 있어야 암호를 변경할 수 있습니다. *OLD_PASSWORD* 를 요구하면 **IMPERSONATION** 권한을 가진 사용자가 암호를 변경할 수 없습니다.

> [!NOTE]
> 이 옵션은 포함된 사용자에 대해서만 사용할 수 있습니다.

 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ]  **적용 대상** : [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

 대량 복사 작업에서 서버에 대한 암호화 메타데이터 검사를 표시하지 않습니다. 이를 통해 사용자는 데이터를 암호 해독하지 않고도 테이블이나 데이터베이스 사이에 암호화된 데이터를 대량 복사할 수 있습니다. 기본값은 OFF입니다.

> [!WARNING]
> 이 옵션을 부적절하게 사용할 경우 데이터가 손상될 수 있습니다. 자세한 내용은 [상시 암호화로 보호되는 중요한 데이터 마이그레이션](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)을 참조하세요.

## <a name="remarks"></a>설명

 기본 스키마는 서버에서 이 데이터베이스 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색하는 스키마가 됩니다. 달리 지정하지 않는 한 기본 스키마는 이 데이터베이스 사용자가 만든 개체의 소유자가 됩니다.

 사용자에게 기본 스키마가 있는 경우에는 해당 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없지만 사용자가 기본 스키마가 있는 그룹의 멤버인 경우에는 그룹의 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없고 사용자가 두 개 이상 그룹의 멤버인 경우 principle_id가 가장 낮고 명시적으로 설정된 기본 스키마가 있는 Windows 그룹의 기본 스키마가 사용자의 기본 스키마가 됩니다. 사용자의 기본 스키마를 확인할 수 없으면 **dbo** 스키마가 사용됩니다.

 DEFAULT_SCHEMA는 현재 데이터베이스에 없는 스키마로 설정할 수 있습니다. 따라서 해당 스키마가 생성되기 전에 DEFAULT_SCHEMA를 사용자에게 할당할 수 있습니다.

 인증서 또는 비대칭 키에 매핑된 사용자에는 DEFAULT_SCHEMA를 지정할 수 없습니다.

> [!IMPORTANT]
> 사용자가 **sysadmin** 고정 서버 역할의 멤버이면 DEFAULT_SCHEMA 값은 무시됩니다. **sysadmin** 고정 서버 역할의 모든 멤버는 기본 스키마가 `dbo`입니다.

 새 사용자 이름의 SID가 데이터베이스에 기록된 SID와 일치할 때만 Windows 로그인 또는 그룹에 매핑된 사용자의 이름을 변경할 수 있습니다. 이 검사는 데이터베이스에서 Windows 로그인의 스푸핑을 방지하는 데 도움이 됩니다.

 WITH LOGIN 절을 사용하면 사용자를 다른 로그인으로 다시 매핑할 수 있습니다. 로그인이 없는 사용자, 인증서로 매핑된 사용자 또는 비대칭 키에 매핑된 사용자는 이 절을 사용하여 다시 매핑할 수 없습니다. SQL 사용자 및 Windows 사용자(또는 그룹)만 다시 매핑할 수 있습니다. WITH LOGIN 절은 Windows 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인으로 변경하는 것과 같이 사용자 유형을 변경하는 데는 사용할 수 없습니다.

 다음 조건이 충족되면 사용자 이름이 로그인 이름으로 자동 변경됩니다.

- 사용자가 Windows 사용자입니다.

- 이름이 Windows 이름입니다(백슬래시 포함).

- 새 이름이 지정되지 않았습니다.

- 현재 이름이 로그인 이름과 다릅니다.

 위의 조건을 충족하지 않으면 사용자 이름이 변경되지 않으며 호출자가 NAME 절을 추가로 호출해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 인증서 또는 비대칭 키에 매핑된 사용자 이름에는 백 슬래시 문자(\\)를 사용할 수 없습니다.

> [!CAUTION]
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]

## <a name="security"></a>보안

> [!NOTE]
> **ALTER ANY USER** 권한이 있는 사용자는 모든 사용자의 기본 스키마를 변경할 수 있습니다. 스키마가 변경된 사용자는 자신도 모르는 사이 잘못된 테이블에서 데이터를 선택하거나 잘못된 스키마의 코드를 실행할 수 있습니다.

### <a name="permissions"></a>사용 권한

 사용자의 이름을 변경하려면 **ALTER ANY USER** 권한이 필요합니다.

 사용자의 대상 로그인을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 데이터베이스에 대한 **CONTROL** 권한이 있는 사용자의 사용자 이름을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 기본 스키마나 언어를 변경하려면 사용자에 대한 **ALTER** 권한이 필요합니다. 사용자는 자신의 기본 스키마 또는 언어를 변경할 수 있습니다.

## <a name="examples"></a>예제

모든 예제는 사용자 데이터베이스에서 실행됩니다.

### <a name="a-changing-the-name-of-a-database-user"></a>A. 데이터베이스 사용자의 이름 변경

 다음 예에서는 데이터베이스 사용자 `Mary5`의 이름을 `Mary51`로 변경합니다.

```sql
ALTER USER Mary5 WITH NAME = Mary51;
GO
```

### <a name="b-changing-the-default-schema-of-a-user"></a>B. 사용자의 기본 스키마 변경

 다음 예에서는 `Mary51` 사용자의 기본 스키마를 `Purchasing`으로 변경합니다.

```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;
GO
```

### <a name="c-changing-several-options-at-once"></a>C. 한 번에 여러 옵션 변경

 다음 예에서는 포함된 데이터베이스 사용자에 대해 여러 옵션을 하나의 문에서 변경합니다.

```sql
ALTER USER Philip
WITHNAME = Philipe
, DEFAULT_SCHEMA = Development
, PASSWORD = 'W1r77TT98%ab@#' OLD_PASSWORD = 'New Devel0per';
GO
```

## <a name="see-also"></a>참고 항목

- [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
- [DROP USER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
- [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)
- [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-user-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-user-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        **_\* SQL Managed Instance \*_**
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-user-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](alter-user-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-sql-managed-instance"></a>Azure SQL Managed Instance

## <a name="syntax"></a>구문

> [!IMPORTANT]
> Azure AD 로그인을 사용하는 사용자에게 적용하는 경우 Azure SQL Managed Instance에 대해 `DEFAULT_SCHEMA = { schemaName | NULL }` 및 `DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }` 옵션만 지원됩니다.
> </br> </br> Azure SQL Managed Instance로 마이그레이션된 데이터베이스의 사용자를 다시 매핑하는 데 도움이 되는 새로운 구문 확장이 추가되었습니다. ALTER USER 구문은 Azure AD와 페더레이션 및 동기화된 도메인의 데이터베이스 사용자를 Azure AD 로그인에 매핑하는 데 도움이 됩니다.

```syntaxsql
-- Syntax for SQL Managed Instance
ALTER USER userName
 { WITH <set_item> [ ,...n ] | FROM EXTERNAL PROVIDER }
[;]

<set_item> ::=
NAME = newUserName
| DEFAULT_SCHEMA = { schemaName | NULL }
| LOGIN = loginName
| PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]
| DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }
| ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]

-- Users or groups that are migrated as federated and synchronized with Azure AD have the following syntax:

/** Applies to Windows users that were migrated and have the following user names:
- Windows user <domain\user>
- Windows group <domain\MyWindowsGroup>
- Windows alias <MyWindowsAlias>
**/

ALTER USER userName
 { WITH <set_item> [ ,...n ] | FROM EXTERNAL PROVIDER }
[;]

<set_item> ::=
 NAME = newUserName
| DEFAULT_SCHEMA = { schemaName | NULL }
| LOGIN = loginName
| DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }
```

## <a name="arguments"></a>인수

 *userName* 이 데이터베이스 내에서 사용자를 식별하는 이름을 지정합니다.

 LOGIN **=** _loginName_ 사용자의 SID(보안 식별자)를 다른 로그인의 SID와 일치하도록 변경하여 사용자를 다른 로그인으로 다시 매핑합니다.

 ALTER USER 문이 SQL 일괄 처리의 유일한 문인 경우 Azure SQL Database는 WITH LOGIN 절을 지원합니다. ALTER USER 문이 SQL 일괄 처리의 유일한 문이 아니거나 동적 SQL에서 실행되는 경우 WITH LOGIN 절이 지원되지 않습니다.

 NAME **=** _newUserName_ 이 사용자의 새 이름을 지정합니다. *newUserName* 은 현재 데이터베이스에 아직 없는 이름이어야 합니다.

 DEFAULT_SCHEMA **=** { *schemaName* | NULL } 서버에서 이 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색할 스키마를 지정합니다. 기본 스키마를 NULL로 설정하면 Windows 그룹에서 기본 스키마가 제거됩니다. Windows 사용자에는 NULL 옵션을 사용할 수 없습니다.

 PASSWORD **=** ' *password* '

 변경할 사용자의 암호를 지정합니다. 암호는 대소문자를 구분합니다.

> [!NOTE]
> 이 옵션은 포함된 사용자에 대해서만 사용할 수 있습니다. 자세한 내용은 [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md) 및 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)를 참조하세요.

 OLD_PASSWORD **=** _'oldpassword'_

 ' *암호* '로 바뀔 현재 사용자 암호입니다. 암호는 대소문자를 구분합니다. **ALTER ANY USER** 권한이 없으면 *OLD_PASSWORD* 가 있어야 암호를 변경할 수 있습니다. *OLD_PASSWORD* 를 요구하면 **IMPERSONATION** 권한을 가진 사용자가 암호를 변경할 수 없습니다.

> [!NOTE]
> 이 옵션은 포함된 사용자에 대해서만 사용할 수 있습니다.

 DEFAULT_LANGUAGE **=** _{ NONE | \<lcid> | \<language name> | \<language alias> }_

 사용자에게 할당할 기본 언어를 지정합니다. 이 옵션을 NONE으로 설정하면 기본 언어가 데이터베이스의 현재 기본 언어로 설정됩니다. 나중에 데이터베이스의 기본 언어가 변경되더라도 사용자의 기본 언어는 그대로 유지됩니다. *DEFAULT_LANGUAGE* 는 로컬 ID(lcid), 언어 이름 또는 언어 별칭이 될 수 있습니다.

> [!NOTE]
> 이 옵션은 포함된 데이터베이스에서 포함된 사용자에 대해서만 지정할 수 있습니다.

 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ]

 대량 복사 작업에서 서버에 대한 암호화 메타데이터 검사를 표시하지 않습니다. 이를 통해 사용자는 데이터를 암호 해독하지 않고도 테이블이나 데이터베이스 사이에 암호화된 데이터를 대량 복사할 수 있습니다. 기본값은 OFF입니다.

> [!WARNING]
> 이 옵션을 부적절하게 사용할 경우 데이터가 손상될 수 있습니다. 자세한 내용은 [상시 암호화로 보호되는 중요한 데이터 마이그레이션](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)을 참조하세요.

## <a name="remarks"></a>설명

 기본 스키마는 서버에서 이 데이터베이스 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색하는 스키마가 됩니다. 달리 지정하지 않는 한 기본 스키마는 이 데이터베이스 사용자가 만든 개체의 소유자가 됩니다.

 사용자에게 기본 스키마가 있는 경우에는 해당 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없지만 사용자가 기본 스키마가 있는 그룹의 멤버인 경우에는 그룹의 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없고 사용자가 두 개 이상 그룹의 멤버인 경우 principle_id가 가장 낮고 명시적으로 설정된 기본 스키마가 있는 Windows 그룹의 기본 스키마가 사용자의 기본 스키마가 됩니다. 사용자의 기본 스키마를 확인할 수 없으면 **dbo** 스키마가 사용됩니다.

 DEFAULT_SCHEMA는 현재 데이터베이스에 없는 스키마로 설정할 수 있습니다. 따라서 해당 스키마가 생성되기 전에 DEFAULT_SCHEMA를 사용자에게 할당할 수 있습니다.

 인증서 또는 비대칭 키에 매핑된 사용자에는 DEFAULT_SCHEMA를 지정할 수 없습니다.

> [!IMPORTANT]
> 사용자가 **sysadmin** 고정 서버 역할의 멤버이면 DEFAULT_SCHEMA 값은 무시됩니다. **sysadmin** 고정 서버 역할의 모든 멤버는 기본 스키마가 `dbo`입니다.

 새 사용자 이름의 SID가 데이터베이스에 기록된 SID와 일치할 때만 Windows 로그인 또는 그룹에 매핑된 사용자의 이름을 변경할 수 있습니다. 이 검사는 데이터베이스에서 Windows 로그인의 스푸핑을 방지하는 데 도움이 됩니다.

 WITH LOGIN 절을 사용하면 사용자를 다른 로그인으로 다시 매핑할 수 있습니다. 로그인이 없는 사용자, 인증서로 매핑된 사용자 또는 비대칭 키에 매핑된 사용자는 이 절을 사용하여 다시 매핑할 수 없습니다. SQL 사용자 및 Windows 사용자(또는 그룹)만 다시 매핑할 수 있습니다. WITH LOGIN 절은 Windows 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인으로 변경하는 것과 같이 사용자 유형을 변경하는 데는 사용할 수 없습니다. 유일한 예외는 Windows 사용자를 Azure AD 사용자로 변경하는 경우뿐입니다.

> [!NOTE]
> Azure SQL Managed Instance에서 Windows 로그인 만들기를 지원하지 않으므로 다음 규칙은 Azure SQL Managed Instance의 Windows 사용자에게는 적용되지 않습니다. WITH LOGIN 옵션은 Azure AD 로그인이 있는 경우에만 사용할 수 있습니다.

 다음 조건이 충족되면 사용자 이름이 로그인 이름으로 자동 변경됩니다.

- 사용자가 Windows 사용자입니다.

- 이름이 Windows 이름입니다(백슬래시 포함).

- 새 이름이 지정되지 않았습니다.

- 현재 이름이 로그인 이름과 다릅니다.

 위의 조건을 충족하지 않으면 사용자 이름이 변경되지 않으며 호출자가 NAME 절을 추가로 호출해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 인증서 또는 비대칭 키에 매핑된 사용자 이름에는 백 슬래시 문자(\\)를 사용할 수 없습니다.

> [!CAUTION]
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]

### <a name="remarks-for-windows-users-in-sql-on-premises-migrated-to-azure-sql-managed-instance"></a>Azure SQL Managed Instance로 마이그레이션된 SQL 온-프레미스의 Windows 사용자에 대한 주의 사항

이러한 주의 사항은 Azure AD와 페더레이션 및 동기화된 Windows 사용자로 인증하는 데 적용됩니다.

> [!NOTE]
> 생성 후 Azure SQL Managed Instance 기능의 Azure AD 관리자가 변경되었습니다. 자세한 내용은 [MI의 새 Azure AD 관리자 기능](/azure/sql-database/sql-database-aad-authentication-configure#new-azure-ad-admin-functionality-for-mi)을 참조하세요.

- Azure AD에 매핑되는 Windows 사용자 또는 그룹의 유효성 검사는 기본적으로 마이그레이션 목적에 사용되는 모든 버전의 ALTER USER 구문에서 Graph API를 통해 수행됩니다.
- 별칭이 지정된 온-프레미스 사용자(원래 Windows 계정에서 다른 이름을 사용)는 별칭이 지정된 이름을 유지합니다.
- Azure AD 인증의 경우 LOGIN 매개 변수는 Azure SQL Managed Instance에만 적용되며 SQL Database에서 사용할 수 없습니다.
- Azure AD 보안 주체에 대한 로그인을 보려면 다음 명령을 사용합니다. `select * from sys.server_principals`.
- 로그인의 지정된 형식이 `E` 또는 `X`인지 확인합니다.
- Azure AD 사용자에 대해 PASSWORD 옵션을 사용할 수 없습니다.
- 모든 마이그레이션 사례에서 Windows 사용자 또는 그룹의 역할 및 권한이 자동으로 새 Azure AD 사용자 또는 그룹으로 이전됩니다.
- 새 구문 확장 **FROM EXTERNAL PROVIDER** 은 SQL 온-프레미스의 Windows 사용자 및 그룹을 Azure AD 사용자 및 그룹으로 변경하는 데 사용할 수 있습니다. 이 확장을 사용하는 경우 Windows 도메인이 Azure AD와 페더레이션되어 있어야 하며 모든 Windows 도메인 구성원이 Azure AD에 있어야 합니다. **FROM EXTERNAL PROVIDER** 구문은 Azure SQL Managed Instance에 적용되며 Windows 사용자가 원래 SQL 인스턴스에 대한 로그인이 없고 독립 실행형 Azure AD 데이터베이스 사용자에 매핑되어야 하는 경우에 사용해야 합니다.
- 이 경우 허용되는 사용자 이름은 다음과 같습니다.
- Widows 사용자( _domain\user_ ).
- Windows 그룹( _MyWidnowsGroup_ ).
- Windows 별칭( _MyWindowsAlias_ ).
- ALTER 명령의 결과는 기존 사용자 이름을 기존 사용자 이름의 원래 SID를 기반으로 Azure AD에서 발견되는 해당 이름으로 바꿉니다. 변경된 이름이 데이터베이스의 메타데이터에 저장됩니다.
- ( _domain\user_ )가 Azure AD user@domain.com로 바뀝니다.
- ( _domain\\MyWidnowsGroup_ )이 Azure AD 그룹으로 바뀝니다.
- ( _MyWindowsAlias_ )는 변경되지 않은 상태로 유지되지만 이 사용자의 SID는 Azure AD에서 확인됩니다.

> [!NOTE]
> objectID로 변환된 원래 사용자의 SID를 Azure AD에서 찾을 수 없는 경우 ALTER USER 명령이 실패합니다.

- 변경된 사용자를 보려면 다음 명령을 사용합니다. `select * from sys.database_principals`
- 사용자가 지정한 유형 `E` 또는 `X`를 확인합니다.
- Windows 사용자를 Azure AD 사용자로 마이그레이션하는 데 NAME을 사용하는 경우 다음 제한 사항이 적용됩니다.
- 유효한 LOGIN을 지정해야 합니다.
- NAME은 Azure AD에서 확인되며 다음만 가능합니다.
- LOGIN의 이름.
- 별칭 - Azure AD에는 이름이 있을 수 없습니다.
- 다른 모든 경우에는 구문이 실패합니다.

## <a name="security"></a>보안

> [!NOTE]
> **ALTER ANY USER** 권한이 있는 사용자는 모든 사용자의 기본 스키마를 변경할 수 있습니다. 스키마가 변경된 사용자는 자신도 모르는 사이 잘못된 테이블에서 데이터를 선택하거나 잘못된 스키마의 코드를 실행할 수 있습니다.

### <a name="permissions"></a>사용 권한

 사용자의 이름을 변경하려면 **ALTER ANY USER** 권한이 필요합니다.

 사용자의 대상 로그인을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 데이터베이스에 대한 **CONTROL** 권한이 있는 사용자의 사용자 이름을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 기본 스키마나 언어를 변경하려면 사용자에 대한 **ALTER** 권한이 필요합니다. 사용자는 자신의 기본 스키마 또는 언어를 변경할 수 있습니다.

## <a name="examples"></a>예제

모든 예제는 사용자 데이터베이스에서 실행됩니다.

### <a name="a-changing-the-name-of-a-database-user"></a>A. 데이터베이스 사용자의 이름 변경

 다음 예에서는 데이터베이스 사용자 `Mary5`의 이름을 `Mary51`로 변경합니다.

```sql
ALTER USER Mary5 WITH NAME = Mary51;
GO
```

### <a name="b-changing-the-default-schema-of-a-user"></a>B. 사용자의 기본 스키마 변경

 다음 예에서는 `Mary51` 사용자의 기본 스키마를 `Purchasing`으로 변경합니다.

```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;
GO
```

### <a name="c-changing-several-options-at-once"></a>C. 한 번에 여러 옵션 변경

 다음 예에서는 포함된 데이터베이스 사용자에 대해 여러 옵션을 하나의 문에서 변경합니다.

```sql
ALTER USER Philip
WITH NAME = Philipe
, DEFAULT_SCHEMA = Development
, PASSWORD = 'W1r77TT98%ab@#' OLD_PASSWORD = 'New Devel0per'
, DEFAULT_LANGUAGE= French ;
GO
```

### <a name="d-map-the-user-in-the-database-to-an-azure-ad-login-after-migration"></a>D. 마이그레이션 후 데이터베이스의 사용자를 Azure AD 로그인에 매핑

다음 예제에서는 사용자 `westus/joe`를 Azure AD 사용자 `joe@westus.com`에 다시 매핑합니다. 이 예제는 관리되는 인스턴스에 이미 있는 로그인에 대한 것입니다. Azure SQL Managed Instance로 데이터베이스 마이그레이션을 완료하고 Azure AD 로그인을 사용하여 인증하려는 경우에 이를 수행해야 합니다.

```sql
ALTER USER [westus/joe] WITH LOGIN = joe@westus.com
```

### <a name="e-map-an-old-windows-user-in-the-database-without-a-login-in-azure-sql-managed-instance-to-an-azure-ad-user"></a>E. Azure SQL Managed Instance 로그인이 없는 데이터베이스의 기존 Windows 사용자를 Azure AD 사용자에게 매핑

다음 예제에서는 로그인이 없는 사용자 `westus/joe`를 Azure AD 사용자 `joe@westus.com`에 다시 매핑합니다. 페더레이션된 사용자가 Azure AD에 있어야 합니다.

```sql
ALTER USER [westus/joe] FROM EXTERNAL PROVIDER
```

### <a name="f-map-the-user-alias-to-an-existing-azure-ad-login"></a>F. 사용자 별칭을 기존 Azure AD 로그인에 매핑

다음 예제에서는 사용자 이름 `westus\joe`를 `joe_alias`에 다시 매핑합니다. 이 경우 해당 Azure AD 로그인은 `joe@westus.com`입니다.

```sql
ALTER USER [westus/joe] WITH LOGIN = joe@westus.com, name= joe_alias
```

### <a name="g-map-a-windows-group-that-was-migrated-in-azure-sql-managed-instance-to-an-azure-ad-group"></a>G. Azure SQL Managed Instance에서 마이그레이션된 Windows 그룹을 Azure AD 그룹에 매핑

다음 예제에서는 기존 온-프레미스 그룹 `westus\mygroup`을 관리되는 인스턴스의 Azure AD 그룹 `mygroup`에 다시 매핑합니다. 그룹이 Azure AD에 있어야 합니다.

```sql
ALTER USER [westus\mygroup] WITH LOGIN = mygroup
```

## <a name="see-also"></a>참고 항목

- [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
- [DROP USER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
- [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)
- [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)
- [자습서: T-SQL DDL 구문을 사용하여 SQL Server 온-프레미스 Windows 사용자 및 그룹을 SQL Managed Instance로 마이그레이션](/azure/sql-database/tutorial-managed-instance-azure-active-directory-migration)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-user-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-user-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-user-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_**
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System(PDW)](alter-user-transact-sql.md?view=aps-pdw-2016)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for Azure Synapse

ALTER USER userName
 WITH <set_item> [ ,...n ]

<set_item> ::=
 NAME = newUserName
 | LOGIN = loginName
 | DEFAULT_SCHEMA = schema_name
[;]
```

## <a name="arguments"></a>인수

 *userName* 이 데이터베이스 내에서 사용자를 식별하는 이름을 지정합니다.

 LOGIN **=** _loginName_ 사용자의 SID(보안 식별자)를 다른 로그인의 SID와 일치하도록 변경하여 사용자를 다른 로그인으로 다시 매핑합니다.

 ALTER USER 문이 SQL 일괄 처리의 유일한 문인 경우 Azure SQL Database는 WITH LOGIN 절을 지원합니다. ALTER USER 문이 SQL 일괄 처리의 유일한 문이 아니거나 동적 SQL에서 실행되는 경우 WITH LOGIN 절이 지원되지 않습니다.

 NAME **=** _newUserName_ 이 사용자의 새 이름을 지정합니다. *newUserName* 은 현재 데이터베이스에 아직 없는 이름이어야 합니다.

 DEFAULT_SCHEMA **=** { *schemaName* | NULL } 서버에서 이 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색할 스키마를 지정합니다. 기본 스키마를 NULL로 설정하면 Windows 그룹에서 기본 스키마가 제거됩니다. Windows 사용자에는 NULL 옵션을 사용할 수 없습니다.

## <a name="remarks"></a>설명

 기본 스키마는 서버에서 이 데이터베이스 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색하는 스키마가 됩니다. 달리 지정하지 않는 한 기본 스키마는 이 데이터베이스 사용자가 만든 개체의 소유자가 됩니다.

 사용자에게 기본 스키마가 있는 경우에는 해당 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없지만 사용자가 기본 스키마가 있는 그룹의 멤버인 경우에는 그룹의 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없고 사용자가 두 개 이상 그룹의 멤버인 경우 principle_id가 가장 낮고 명시적으로 설정된 기본 스키마가 있는 Windows 그룹의 기본 스키마가 사용자의 기본 스키마가 됩니다. 사용자의 기본 스키마를 확인할 수 없으면 **dbo** 스키마가 사용됩니다.

 DEFAULT_SCHEMA는 현재 데이터베이스에 없는 스키마로 설정할 수 있습니다. 따라서 해당 스키마가 생성되기 전에 DEFAULT_SCHEMA를 사용자에게 할당할 수 있습니다.

 인증서 또는 비대칭 키에 매핑된 사용자에는 DEFAULT_SCHEMA를 지정할 수 없습니다.

> [!IMPORTANT]
> 사용자가 **sysadmin** 고정 서버 역할의 멤버이면 DEFAULT_SCHEMA 값은 무시됩니다. **sysadmin** 고정 서버 역할의 모든 멤버는 기본 스키마가 `dbo`입니다.

 WITH LOGIN 절을 사용하면 사용자를 다른 로그인으로 다시 매핑할 수 있습니다. 로그인이 없는 사용자, 인증서로 매핑된 사용자 또는 비대칭 키에 매핑된 사용자는 이 절을 사용하여 다시 매핑할 수 없습니다. SQL 사용자 및 Windows 사용자(또는 그룹)만 다시 매핑할 수 있습니다. WITH LOGIN 절은 Windows 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인으로 변경하는 것과 같이 사용자 유형을 변경하는 데는 사용할 수 없습니다.

 다음 조건이 충족되면 사용자 이름이 로그인 이름으로 자동 변경됩니다.

- 새 이름이 지정되지 않았습니다.

- 현재 이름이 로그인 이름과 다릅니다.

 위의 조건을 충족하지 않으면 사용자 이름이 변경되지 않으며 호출자가 NAME 절을 추가로 호출해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 인증서 또는 비대칭 키에 매핑된 사용자 이름에는 백 슬래시 문자(\\)를 사용할 수 없습니다.

> [!CAUTION]
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]

## <a name="security"></a>보안

> [!NOTE]
> **ALTER ANY USER** 권한이 있는 사용자는 모든 사용자의 기본 스키마를 변경할 수 있습니다. 스키마가 변경된 사용자는 자신도 모르는 사이 잘못된 테이블에서 데이터를 선택하거나 잘못된 스키마의 코드를 실행할 수 있습니다.

### <a name="permissions"></a>사용 권한

 사용자의 이름을 변경하려면 **ALTER ANY USER** 권한이 필요합니다.

 사용자의 대상 로그인을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 데이터베이스에 대한 **CONTROL** 권한이 있는 사용자의 사용자 이름을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 기본 스키마나 언어를 변경하려면 사용자에 대한 **ALTER** 권한이 필요합니다. 사용자는 자신의 기본 스키마 또는 언어를 변경할 수 있습니다.

## <a name="examples"></a>예제

모든 예제는 사용자 데이터베이스에서 실행됩니다.

### <a name="a-changing-the-name-of-a-database-user"></a>A. 데이터베이스 사용자의 이름 변경

 다음 예에서는 데이터베이스 사용자 `Mary5`의 이름을 `Mary51`로 변경합니다.

```sql
ALTER USER Mary5 WITH NAME = Mary51;
GO
```

### <a name="b-changing-the-default-schema-of-a-user"></a>B. 사용자의 기본 스키마 변경

다음 예에서는 `Mary51` 사용자의 기본 스키마를 `Purchasing`으로 변경합니다.

```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;
GO
```

## <a name="see-also"></a>참고 항목

- [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
- [DROP USER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
- [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)
- [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

:::row:::
    :::column:::
        [SQL Server](alter-user-transact-sql.md?view=sql-server-2017)
    :::column-end:::
    :::column:::
        [SQL 데이터베이스](alter-user-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [SQL Managed Instance](alter-user-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](alter-user-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        **_\* Analytics<br />Platform System(PDW) \*_**
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="analytics-platform-system"></a>분석 플랫폼 시스템

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for Analytics Platform System

ALTER USER userName
 WITH <set_item> [ ,...n ]

<set_item> ::=
 NAME = newUserName
 | LOGIN = loginName
 | DEFAULT_SCHEMA = schema_name
[;]
```

## <a name="arguments"></a>인수

 *userName* 이 데이터베이스 내에서 사용자를 식별하는 이름을 지정합니다.

 LOGIN **=** _loginName_ 사용자의 SID(보안 식별자)를 다른 로그인의 SID와 일치하도록 변경하여 사용자를 다른 로그인으로 다시 매핑합니다.

 ALTER USER 문이 SQL 일괄 처리의 유일한 문인 경우 Azure SQL Database는 WITH LOGIN 절을 지원합니다. ALTER USER 문이 SQL 일괄 처리의 유일한 문이 아니거나 동적 SQL에서 실행되는 경우 WITH LOGIN 절이 지원되지 않습니다.

 NAME **=** _newUserName_ 이 사용자의 새 이름을 지정합니다. *newUserName* 은 현재 데이터베이스에 아직 없는 이름이어야 합니다.

 DEFAULT_SCHEMA **=** { *schemaName* | NULL } 서버에서 이 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색할 스키마를 지정합니다. 기본 스키마를 NULL로 설정하면 Windows 그룹에서 기본 스키마가 제거됩니다. Windows 사용자에는 NULL 옵션을 사용할 수 없습니다.

## <a name="remarks"></a>설명

 기본 스키마는 서버에서 이 데이터베이스 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색하는 스키마가 됩니다. 달리 지정하지 않는 한 기본 스키마는 이 데이터베이스 사용자가 만든 개체의 소유자가 됩니다.

 사용자에게 기본 스키마가 있는 경우에는 해당 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없지만 사용자가 기본 스키마가 있는 그룹의 멤버인 경우에는 그룹의 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없고 사용자가 두 개 이상 그룹의 멤버인 경우 principle_id가 가장 낮고 명시적으로 설정된 기본 스키마가 있는 Windows 그룹의 기본 스키마가 사용자의 기본 스키마가 됩니다. 사용자의 기본 스키마를 확인할 수 없으면 **dbo** 스키마가 사용됩니다.

 DEFAULT_SCHEMA는 현재 데이터베이스에 없는 스키마로 설정할 수 있습니다. 따라서 해당 스키마가 생성되기 전에 DEFAULT_SCHEMA를 사용자에게 할당할 수 있습니다.

 인증서 또는 비대칭 키에 매핑된 사용자에는 DEFAULT_SCHEMA를 지정할 수 없습니다.

> [!IMPORTANT]
> 사용자가 **sysadmin** 고정 서버 역할의 멤버이면 DEFAULT_SCHEMA 값은 무시됩니다. **sysadmin** 고정 서버 역할의 모든 멤버는 기본 스키마가 `dbo`입니다.

 WITH LOGIN 절을 사용하면 사용자를 다른 로그인으로 다시 매핑할 수 있습니다. 로그인이 없는 사용자, 인증서로 매핑된 사용자 또는 비대칭 키에 매핑된 사용자는 이 절을 사용하여 다시 매핑할 수 없습니다. SQL 사용자 및 Windows 사용자(또는 그룹)만 다시 매핑할 수 있습니다. WITH LOGIN 절은 Windows 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인으로 변경하는 것과 같이 사용자 유형을 변경하는 데는 사용할 수 없습니다.

 다음 조건이 충족되면 사용자 이름이 로그인 이름으로 자동 변경됩니다.

- 새 이름이 지정되지 않았습니다.

- 현재 이름이 로그인 이름과 다릅니다.

 위의 조건을 충족하지 않으면 사용자 이름이 변경되지 않으며 호출자가 NAME 절을 추가로 호출해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 인증서 또는 비대칭 키에 매핑된 사용자 이름에는 백 슬래시 문자(\\)를 사용할 수 없습니다.

> [!CAUTION]
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]

## <a name="security"></a>보안

> [!NOTE]
> **ALTER ANY USER** 권한이 있는 사용자는 모든 사용자의 기본 스키마를 변경할 수 있습니다. 스키마가 변경된 사용자는 자신도 모르는 사이 잘못된 테이블에서 데이터를 선택하거나 잘못된 스키마의 코드를 실행할 수 있습니다.

### <a name="permissions"></a>사용 권한

 사용자의 이름을 변경하려면 **ALTER ANY USER** 권한이 필요합니다.

 사용자의 대상 로그인을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 데이터베이스에 대한 **CONTROL** 권한이 있는 사용자의 사용자 이름을 변경하려면 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.

 기본 스키마나 언어를 변경하려면 사용자에 대한 **ALTER** 권한이 필요합니다. 사용자는 자신의 기본 스키마 또는 언어를 변경할 수 있습니다.

## <a name="examples"></a>예제

모든 예제는 사용자 데이터베이스에서 실행됩니다.

### <a name="a-changing-the-name-of-a-database-user"></a>A. 데이터베이스 사용자의 이름 변경

 다음 예에서는 데이터베이스 사용자 `Mary5`의 이름을 `Mary51`로 변경합니다.

```sql
ALTER USER Mary5 WITH NAME = Mary51;
GO
```

### <a name="b-changing-the-default-schema-of-a-user"></a>B. 사용자의 기본 스키마 변경
 다음 예에서는 `Mary51` 사용자의 기본 스키마를 `Purchasing`으로 변경합니다.

```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;
GO
```

## <a name="see-also"></a>참고 항목

- [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
- [DROP USER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
- [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)
- [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
- [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)

::: moniker-end
