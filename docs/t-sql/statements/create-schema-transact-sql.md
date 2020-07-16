---
title: CREATE SCHEMA(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_SCHEMA_TSQL
- SCHEMA
- CREATE SCHEMA
- SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- owners [SQL Server], schemas
- table creation [SQL Server], CREATE SCHEMA statement
- permissions [SQL Server], schemas
- schemas [SQL Server], creating
- CREATE SCHEMA statement
ms.assetid: df74fc36-20da-4efa-b412-c4e191786695
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f06c3e2b95fa571b26404a69653471738d7648ee
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86393001"
---
# <a name="create-schema-transact-sql"></a>CREATE SCHEMA(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스에 스키마를 만듭니다. CREATE SCHEMA 트랜잭션에서는 새 스키마 내에 테이블과 뷰를 만들고 해당 개체에 대한 GRANT, DENY 또는 REVOKE 권한을 설정할 수도 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE SCHEMA schema_name_clause [ <schema_element> [ ...n ] ]  
  
<schema_name_clause> ::=  
    {  
    schema_name  
    | AUTHORIZATION owner_name  
    | schema_name AUTHORIZATION owner_name  
    }  
  
<schema_element> ::=   
    {   
        table_definition | view_definition | grant_statement |   
        revoke_statement | deny_statement   
    }  
```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE SCHEMA schema_name [ AUTHORIZATION owner_name ] [;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *schema_name*  
 데이터베이스 내에서 스키마를 식별하는 이름입니다.  
  
 AUTHORIZATION *owner_name*  
 스키마를 소유하게 될 데이터베이스 수준 보안 주체의 이름을 지정합니다. 이 보안 주체는 다른 스키마를 소유할 수 있으며 현재 스키마를 기본 스키마로 사용하지 않을 수도 있습니다.  
  
 *table_definition*  
 스키마 내에서 테이블을 만드는 CREATE TABLE 문을 지정합니다. 이 문을 실행하는 보안 주체에게 현재 데이터베이스에 대한 CREATE TABLE 권한이 있어야 합니다.  
  
 *view_definition*  
 스키마 내에서 뷰를 만드는 CREATE VIEW 문을 지정합니다. 이 문을 실행하는 보안 주체에게 현재 데이터베이스에 대한 CREATE VIEW 권한이 있어야 합니다.  
  
 *grant_statement*  
 새 스키마를 제외한 모든 보안 개체에 대한 사용 권한을 부여하는 GRANT 문을 지정합니다.  
  
 *revoke_statement*  
 새 스키마를 제외한 모든 보안 개체에 대한 사용 권한을 취소하는 REVOKE 문을 지정합니다.  
  
 *deny_statement*  
 새 스키마를 제외한 모든 보안 개체에 대한 사용 권한을 거부하는 DENY 문을 지정합니다.  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]  
>  CREATE SCHEMA AUTHORIZATION을 포함하지만 이름을 지정하지 않는 문은 이전 버전과의 호환성을 위해서만 허용됩니다. 이 문은 오류를 일으키지 않지만 스키마를 만들지는 않습니다.  
  
 CREATE SCHEMA는 스키마와 이에 포함된 테이블 및 뷰를 만들 수 있으며 단일 문에서 모든 보안 개체에 대한 GRANT, REVOKE 또는 DENY 권한을 만들 수 있습니다. 이 문은 별도의 일괄 처리로 실행해야 합니다. CREATE SCHEMA 문으로 만드는 개체는 생성되는 스키마 내부에 생성됩니다.  
  
 CREATE SCHEMA 트랜잭션은 원자성을 갖습니다. CREATE SCHEMA 문을 실행하는 동안 오류가 발생하는 경우 지정한 보안 개체는 생성되지 않으며 사용 권한은 부여되지 않습니다.  
  
 CREATE SCHEMA로 만든 보안 개체는 다른 뷰를 참조하는 뷰를 제외하면 순서에 관계없이 나열할 수 있습니다. 다른 뷰를 참조하는 뷰의 경우에는 참조하는 뷰보다 참조되는 뷰를 먼저 만들어야 합니다.  
  
 따라서 GRANT 문은 개체를 만들기 전에 개체에 대한 사용 권한을 부여할 수 있으며 CREATE VIEW 문은 뷰가 참조하는 테이블을 만드는 CREATE TABLE 문에 앞서 표시될 수 있습니다. 또한 CREATE TABLE 문은 CREATE SCHEMA문에 나중에 정의된 테이블에 대한 외래 키를 선언할 수 있습니다.  
  
> [!NOTE]  
>  CREATE SCHEMA 문 내에서 DENY 및 REVOKE를 사용할 수 있습니다. DENY 및 REVOKE 절은 CREATE SCHEMA 문에 표시되는 순서대로 실행됩니다.  
  
 CREATE SCHEMA를 실행하는 보안 주체는 다른 데이터베이스 보안 주체를 생성될 스키마의 소유자로 지정할 수 있습니다. 이렇게 하려면 이 항목의 뒷부분에 나오는 "사용 권한" 섹션에서 설명하는 추가 사용 권한이 필요합니다.  
  
 새 스키마는 데이터베이스 수준 보안 주체인 데이터베이스 사용자, 데이터베이스 역할 또는 애플리케이션 역할 중 하나가 소유합니다. 스키마 내에서 만든 개체는 스키마 소유자가 소유하며 **sys.objects** 의 **principal_id**가 NULL입니다. 스키마 포함 개체의 소유권을 모든 데이터베이스 수준 보안 주체에게 이전할 수 있지만 스키마 소유자는 항상 스키마 내의 개체에 대한 CONTROL 권한을 갖고 있어야 합니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
 **암시적 스키마 및 사용자 만들기**  
  
 일부 경우에 사용자는 데이터베이스 사용자 계정(데이터베이스의 데이터베이스 보안 주체)이 없더라도 데이터베이스를 사용할 수 있습니다. 이는 다음과 같은 상황에서 발생할 수 있습니다.  
  
-   로그인에 **CONTROL SERVER** 권한이 있습니다.  
  
-   Windows 사용자는 개별 데이터베이스 사용자 계정(데이터베이스의 데이터베이스 보안 주체)을 갖지 않지만 데이터베이스 사용자 계정(Windows 그룹용 데이터베이스 보안 주체)을 갖는 Windows 그룹의 구성원으로 데이터베이스에 액세스합니다.  
  
 데이터베이스 사용자 계정이 없는 사용자는 기존 스키마를 지정하지 않고 개체를 만들 경우 해당 사용자에 대한 데이터베이스 보안 주체 및 기본 스키마가 데이터베이스에 자동으로 생성됩니다. 생성된 데이터베이스 보안 주체 및 스키마는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 때 사용자가 사용한 이름과 동일한 이름([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 이름 또는 Windows 사용자 이름)을 사용합니다.  
  
 이 동작은 Windows 그룹에 속한 사용자가 개체를 만들어 소유할 수 있도록 허용하므로 필요합니다. 그러나 스키마 및 사용자가 의도하지 않게 생성될 수 있습니다. 의도하지 않은 사용자 및 스키마 생성을 방지하려면 가능한 경우 데이터베이스 보안 주체를 명시적으로 만들어 기본 스키마를 할당하세요. 또는 데이터베이스에서 개체를 만들 때 두, 세 부분으로 구성된 개체 이름을 사용하여 기존 스키마를 명시적으로 지정합니다.  

> [!NOTE]
>  Azure Active Directory 사용자의 암시적 생성은 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]에서 가능하지 않습니다. 외부 공급자에서 Azure AD 사용자를 생성하면 AAD에서 사용자 상태를 확인해야 하므로 사용자 생성은 오류 2760과 함께 실패합니다. **지정한 스키마 이름 "\<user_name@domain>"이 없거나 사용할 권한이 없습니다.** 그리고 2759 오류: **이전 오류로 인해 CREATE SCHEMA가 실패했습니다.** 이러한 오류를 해결하려면 먼저 외부 공급자로부터 Azure AD 사용자를 만든 다음, 개체를 만드는 명령문을 다시 실행하십시오.
 
  
## <a name="deprecation-notice"></a>사용 중단 고지 사항  
 스키마 이름을 지정하지 않는 CREATE SCHEMA 문은 이전 버전과의 호환성을 위해 현재 지원됩니다. 이 문은 데이터베이스 내부에 실제로 스키마를 만들지는 않지만 테이블과 뷰를 만들고 사용 권한을 부여합니다. 스키마가 생성되지 않기 때문에 보안 주체에게는 이러한 이전 형식의 CREATE SCHEMA를 실행하는 데 CREATE SCHEMA 권한이 필요하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다음번 릴리스에서는 이 기능이 제거될 예정입니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 CREATE SCHEMA 권한이 필요합니다.  
  
 CREATE SCHEMA 문 내에서 지정한 개체를 만들려면 사용자에게 해당 CREATE 권한이 있어야 합니다.  
  
 다른 사용자를 생성되는 스키마의 소유자로 지정하려면 호출자에게 해당 사용자에 대한 IMPERSONATE 권한이 있어야 합니다. 데이터베이스 역할을 소유자로 지정하는 경우 호출자에게 해당 역할의 멤버 자격이나 해당 역할에 대한 ALTER 권한이 있어야 합니다.  
  
> [!NOTE]  
>  이전 버전과 호환되는 구문을 사용하면 스키마가 생성되지 않기 때문에 CREATE SCHEMA 권한이 확인되지 않습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-a-schema-and-granting-permissions"></a>A. 스키마 만들기 및 사용 권한 부여  
 다음 예에서는 `Sprockets`가 소유하고 `Annik` 테이블을 포함하는 `NineProngs` 스키마를 만듭니다. 이 문에서는 `SELECT`에게 `Mandar` 권한을 부여하고 `SELECT`에게는 `Prasanna` 권한을 거부합니다. `Sprockets` 및 `NineProngs`는 단일 문으로 생성됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE SCHEMA Sprockets AUTHORIZATION Annik  
    CREATE TABLE NineProngs (source int, cost int, partnumber int)  
    GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
    DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
GO   
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-creating-a-schema-and-a-table-in-the-schema"></a>B. 스키마 및 스키마에 테이블 만들기  
 다음 예에서는 `Sales` 스키마를 만든 다음, 해당 스키마에 `Sales.Region` 테이블을 만듭니다.  
  
```  
CREATE SCHEMA Sales;  
GO
  
CREATE TABLE Sales.Region   
(Region_id int NOT NULL,  
Region_Name char(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
```  
  
### <a name="c-setting-the-owner-of-a-schema"></a>C. 스키마 소유자 설정  
 다음 예에서는 `Mary`가 소유한 `Production` 스키마를 만듭니다.  
  
```  
CREATE SCHEMA Production AUTHORIZATION [Contoso\Mary];  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [DROP SCHEMA&#40;Transact-SQL&#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys,schemas&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [데이터베이스 스키마 만들기](../../relational-databases/security/authentication-access/create-a-database-schema.md)  
  
  


