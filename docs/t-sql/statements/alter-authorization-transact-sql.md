---
title: ALTER AUTHORIZATION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_AUTHORIZATION_TSQL
- ALTER AUTHORIZATION
dev_langs:
- TSQL
helpviewer_keywords:
- owners [SQL Server], transferring
- modifying entity ownership
- full-text search [SQL Server], permissions
- owners [SQL Server], entities
- ALTER AUTHORIZATION statement
- entity ownership [SQL Server]
- transferring ownership
- search property lists [SQL Server], permissions
- TAKE OWNERSHIP
ms.assetid: 8c805ae2-91ed-4133-96f6-9835c908f373
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6855f45379f113f91c54b46e3d1c77a913c853f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730711"
---
# <a name="alter-authorization-transact-sql"></a>ALTER AUTHORIZATION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  보안 개체의 소유권을 변경합니다.    
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>구문    
    
```    
-- Syntax for SQL Server  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
        OBJECT | ASSEMBLY | ASYMMETRIC KEY | AVAILABILITY GROUP | CERTIFICATE     
      | CONTRACT | TYPE | DATABASE | ENDPOINT | FULLTEXT CATALOG     
      | FULLTEXT STOPLIST | MESSAGE TYPE | REMOTE SERVICE BINDING    
      | ROLE | ROUTE | SCHEMA | SEARCH PROPERTY LIST | SERVER ROLE     
      | SERVICE | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

```
-- Syntax for SQL Database  
  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
      OBJECT | ASSEMBLY | ASYMMETRIC KEY | CERTIFICATE     
    | TYPE | DATABASE | FULLTEXT CATALOG     
    | FULLTEXT STOPLIST     
    | ROLE | SCHEMA | SEARCH PROPERTY LIST     
    | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

    
```    
-- Syntax for Azure SQL Data Warehouse  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      schema_name    
    | [ schema_name. ] object_name    
}    
```    
    
```    
-- Syntax for Parallel Data Warehouse  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      DATABASE     
    | SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      database_name 
    | schema_name    
    | [ schema_name. ] object_name    
}    
```    
    
## <a name="arguments"></a>인수    
\<class_type> 소유자가 변경될 엔터티의 보안 개체 클래스입니다. OBJECT가 기본값입니다.    
    
|||    
|-|-|    
|OBJECT|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Data Warehouse, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]까지.|    
|ASSEMBLY|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
|ASYMMETRIC KEY|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
|AVAILABILITY GROUP |**적용 대상**: SQL Server 2012부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지.|
|CERTIFICATE|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
|CONTRACT|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지.|    
|DATABASE|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지. 자세한 내용은 아래의 [데이터베이스에 대한 ALTER AUTHORIZATION](#AlterDB) 섹션 참조하세요.|    
|엔드포인트|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지.|    
|FULLTEXT CATALOG|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
|FULLTEXT STOPLIST|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
|MESSAGE TYPE|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지.|    
|REMOTE SERVICE BINDING|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지.|    
|ROLE|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
|ROUTE|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지.|    
|SCHEMA|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Data Warehouse, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]까지.|    
|SEARCH PROPERTY LIST|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
|SERVER ROLE|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지.|    
|SERVICE|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지.|    
|SYMMETRIC KEY|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
|TYPE|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
|XML SCHEMA COLLECTION|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지.|    
    
 *entity_name*    
 엔터티의 이름입니다.    
    
 *principal_name* | 스키마 소유자    
 엔터티를 소유하게 될 보안 주체의 이름입니다. 데이터베이스 보안 주체 즉, 데이터베이스 사용자 또는 역할이 데이터베이스 개체를 소유해야 합니다. 서버 보안 주체(로그인)가 서버 개체(예: 데이터베이스)를 소유해야 합니다. **스키마 소유자**를 *principal_name*으로 지정하여 개체의 스키마를 소유하는 보안 주체가 해당 개체를 소유하도록 표시합니다.    
    
## <a name="remarks"></a>Remarks    
 ALTER AUTHORIZATION을 사용하면 소유자가 있는 엔터티의 소유권을 변경할 수 있습니다. 데이터베이스 수준 엔터티의 소유권은 데이터베이스 수준의 모든 보안 주체에게 이전할 수 있습니다. 서버 수준 엔터티의 소유권은 서버 수준 보안 주체에게만 이전할 수 있습니다.    
    
> [!IMPORTANT]    
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 사용자는 다른 데이터베이스 사용자가 소유한 스키마에 포함된 OBJECT 또는 TYPE을 소유할 수 있습니다. 이 동작은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 변경되었습니다. 자세한 내용은 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md) 및 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)을 참조하세요.    
    
 "object" 형식의 스키마 수준 엔터티인 테이블, 뷰, 함수, 프로시저, 큐 및 동의어 엔터티의 소유권은 이전할 수 있습니다.    
    
 연결된 서버, 통계, 제약 조건, 규칙, 기본값, 트리거, [!INCLUDE[ssSB](../../includes/sssb-md.md)] 큐, 자격 증명, 파티션 함수, 파티션 구성표, 데이터베이스 마스터 키, 서비스 마스터 키 및 이벤트 알림 엔터티의 소유권은 이전할 수 없습니다.    
    
 서버, 로그인, 사용자, 응용 프로그램 역할 및 열 보안 개체 클래스의 멤버 소유권은 이전할 수 없습니다.    
    
 SCHEMA OWNER 옵션은 스키마 수준 엔터티의 소유권을 이전하는 경우에만 유효합니다. SCHEMA OWNER는 엔터티의 소유권을 엔터티가 속한 스키마의 소유자에게 이전합니다. 스키마 수준 엔터티는 OBJECT, TYPE 또는 XML SCHEMA COLLECTION 클래스뿐입니다.    
    
 대상 엔터티가 데이터베이스가 아니고 엔터티가 새 소유자에게 이전되는 경우 대상에 대한 모든 사용 권한이 삭제됩니다.    
    
> [!CAUTION]    
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 스키마 동작이 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 다르게 변경되었습니다. 스키마가 데이터베이스 사용자와 같다고 가정하는 코드에서 올바른 결과가 반환되지 않을 수도 있습니다. sysobjects를 비롯한 이전 카탈로그 뷰는 CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION 등의 DDL 문이 사용된 데이터베이스에서 사용하지 않아야 합니다. 이러한 문이 사용된 데이터베이스에서는 새 카탈로그 뷰를 사용해야 합니다. 새 카탈로그 뷰는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에 도입된 보안 주체와 스키마 분리를 고려합니다. 카탈로그 뷰에 대한 자세한 내용은 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)를 참조하세요.    
    
 다음 사항도 유의해야 합니다.    
    
> [!IMPORTANT]    
>  개체의 소유자를 확인하는 신뢰할 수 있는 유일한 방법은 **sys.objects** 카탈로그 뷰를 쿼리하는 것입니다. 형식의 소유자를 확인하는 신뢰할 수 있는 유일한 방법은 TYPEPROPERTY 함수를 사용하는 것입니다.    
    
## <a name="special-cases-and-conditions"></a>특수 상황과 상태    
 다음 표에서는 인증 변경에 적용되는 특수 상황, 예외 및 상태를 보여 줍니다.    
    
|클래스|조건|    
|-----------|---------------|    
|OBJECT|트리거, 제약 조건, 규칙, 기본값, 통계, 시스템 개체, 큐, 인덱싱된 뷰 또는 인덱싱된 뷰가 있는 테이블의 소유권을 변경할 수 없습니다.|    
|SCHEMA|소유권이 이전될 때 명시적 소유자가 없는 스키마 수준 개체에 대한 권한이 삭제됩니다. sys, dbo 또는 information_schema의 소유자를 변경할 수 없습니다.|    
|TYPE|sys 또는 information_schema에 속하는 TYPE의 소유권을 변경할 수 없습니다.|    
|CONTRACT, MESSAGE TYPE 또는 SERVICE|시스템 엔터티의 소유권을 변경할 수 없습니다.|    
|SYMMETRIC KEY|전역 임시 키의 소유권을 변경할 수 없습니다.|    
|CERTIFICATE 또는 ASYMMETRIC KEY|이러한 엔터티의 소유권을 역할이나 그룹에 이전할 수 없습니다.|    
|엔드포인트|보안 주체는 로그인이어야 합니다.|    
  
## <a name="AlterDB"></a> 데이터베이스에 대한 ALTER AUTHORIZATION  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
### <a name="for-sql-server"></a>SQL Server의 경우.  
**새 소유자 요구 사항:**   
새 소유자 보안 주체는 다음 중 하나여야 합니다.  
-   SQL Server 인증 로그인입니다.  
-   Windows 사용자(그룹이 아닌)를 나타내는 Windows 인증 로그인입니다.  
-   Windows 그룹을 나타내는 Windows 인증 로그인을 통해 인증하는 Windows 사용자입니다.  
  
**ALTER AUTHORIZATION 문을 실행하는 사용자 요구 사항:**  
**sysadmin** 고정 서버 역할의 구성원이 아닌 경우 최소한 데이터베이스에 대한 TAKE OWNERSHIP 권한과 함께 새 소유자 로그인에 대한 IMPERSONATE 권한이 있어야 합니다.   

### <a name="for-azure-sql-database"></a>Azure SQL 데이터베이스의 경우.  
**새 소유자 요구 사항:**   
새 소유자 보안 주체는 다음 중 하나여야 합니다.  
-   SQL Server 인증 로그인입니다.  
-   Azure AD에 있는 페더레이션 사용자(그룹이 아닌)입니다.  
-   Azure AD에 있는 응용 프로그램 또는 관리 사용자(그룹이 아닌)입니다.    

> [!NOTE]  
> 새 소유자는 Azure Active Directory 사용자인 경우 새 소유자가 새 DBO가 될 데이터베이스에서 사용자로 존재할 수 없습니다. 이러한 Azure AD 사용자는 새 사용자에게 데이터베이스 소유권을 변경하는 ALTER AUTHORIZATION 문을 실행하기 전에 먼저 데이터베이스에서 제거되어야 합니다. SQL Database를 사용하여 Azure Active Directory 사용자 구성에 대한 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Database 또는 SQL Data Warehouse에 연결](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)을 참조하세요.   
  
**ALTER AUTHORIZATION 문을 실행하는 사용자 요구 사항:**  
해당 데이터베이스의 소유자를 변경하려면 대상 데이터베이스에 연결해야 합니다.  

다음과 같은 형식의 계정이 데이터베이스의 소유자를 변경할 수 있습니다. 
* 서버 수준 보안 주체 로그인입니다. (논리 서버를 만들 때 SQL Azure 관리자가 프로비전합니다.)  
* Azure SQL Server용 Azure Active Directory 관리자입니다.   
* 현재 데이터베이스 소유자입니다.   
 
  
다음 테이블은 요구 사항에 대한 요약입니다.  
  
실행기  |대상  |결과    
---------|---------|---------  
SQL Server 인증 로그인     |SQL Server 인증 로그인         |성공  
SQL Server 인증 로그인     |Azure AD 사용자         |실패           
Azure AD 사용자     |SQL Server 인증 로그인         |성공           
Azure AD 사용자     |Azure AD 사용자         |성공           
  
데이터베이스의 Azure AD 소유자를 확인하려면 사용자 데이터베이스에서(이 예제의 `testdb`에서) 다음의 Transact-SQL 명령을 실행합니다.  
    
```    
SELECT CAST(owner_sid as uniqueidentifier) AS Owner_SID   
FROM sys.databases   
WHERE name = 'testdb';  
```    
    
출력은 `richel@cqclinic.onmicrosoft.com`에 할당된 Azure AD ObjectID에 해당하는 식별자(예, 6D8B81F6-7C79-444C-8858-4AF896C03C67) 입니다  
SQL Server 인증 로그인 사용자가 데이터베이스 소유자인 경우 해당 데이터베이스 소유자를 확인하려면 마스터 데이터베이스에서 다음 명령문을 실행합니다.  
    
```    
SELECT d.name, d.owner_sid, sl.name   
FROM sys.databases AS d  
JOIN sys.sql_logins AS sl  
ON d.owner_sid = sl.sid;  
    
```    
  
### <a name="best-practice"></a>최선의 구현 방법  
  
데이터베이스의 개별 소유자로 Azure AD 사용자를 사용하는 대신 **db_owner** 고정된 데이터베이스 역할의 구성원으로 Azure AD 그룹을 사용합니다. 다음 단계에서는 데이터베이스 소유자로 비활성화된 로그인을 구성하고 Azure Active Directory 그룹(`mydbogroup`)을 **db_owner** 역할의 멤버가 되게 하는 방법을 보여줍니다. 
1.  Azure AD 관리자로서 SQL Server에 로그인해 데이터베이스의 소유자를 비활성화된 SQL Server 인증 로그인으로 변경합니다. 예를 들어 사용자 데이터베이스에서 다음을 실행 합니다.  
  ```    
  ALTER AUTHORIZATION ON database::testdb TO DisabledLogin;  
  ```    
2.  데이터베이스를 소유하고 사용자 데이터베이스에 사용자로서 추가해야 하는 Azure AD 그룹을 만듭니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  ```    
  CREATE USER [mydbogroup] FROM EXTERNAL PROVIDER;  
  ```    
3.  사용자 데이터베이스에서 Azure AD 그룹을 나타내는 사용자를 **db_owner** 고정 데이터베이스 역할에 추가합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  ```    
  ALTER ROLE db_owner ADD MEMBER mydbogroup;  
  ```    
  
이제 `mydbogroup` 구성원은 **db_owner** 역할의 구성원으로서 데이터베이스를 중앙 관리할 수 있습니다.  
- 이 그룹의 구성원이 Azure AD 그룹에서 제거되는 경우 이 데이터베이스 대한 dbo 권한이 자동으로 해제됩니다.  
- 마찬가지로 새 멤버가 `mydbogroup` Azure AD 그룹에 추가되는 경우 자동으로 데이터베이스에 대한 dbo 액세스 권한을 취득합니다.  
  
특정 사용자에게 효과적인 dbo 권한이 있는지를 확인하려면 사용자가 다음 명령문을 실행하게 합니다.  
    
```    
SELECT IS_MEMBER ('db_owner');  
```    
  
반환 값 1은 사용자가 역할의 멤버라는 것을 나타냅니다.  
   
    
## <a name="permissions"></a>Permissions    
 엔터티에 대한 TAKE OWNERSHIP 권한이 필요합니다. 새 소유자가 이 문을 실행하는 사용자가 아니면 1) 새 소유자가 사용자이거나 로그인인 경우 새 소유자에 대한 IMPERSONATE 권한, 2) 새 소유자가 역할인 경우 역할의 멤버 자격이나 역할에 대한 ALTER 권한 또는 3) 새 소유자가 응용 프로그램 역할인 경우 응용 프로그램 역할에 대한 ALTER 권한도 필요합니다.    
    
## <a name="examples"></a>예    
    
### <a name="a-transfer-ownership-of-a-table"></a>1. 테이블의 소유권 이전    
 다음 예에서는 `Sprockets` 테이블의 소유권을 `MichikoOsada` 사용자에게 이전합니다. 테이블은 `Parts` 스키마 내부에 있습니다.    
    
```    
ALTER AUTHORIZATION ON OBJECT::Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
 쿼리가 다음과 같을 수도 있습니다.    
    
```    
ALTER AUTHORIZATION ON Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
 개체 스키마가 문의 일부로 포함되지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 사용자 기본 스키마에서 개체를 찾게 됩니다. 예를 들어 다음과 같이 사용할 수 있습니다.    
    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
```    
    
### <a name="b-transfer-ownership-of-a-view-to-the-schema-owner"></a>2. 뷰 소유권을 스키마 소유자에게 이전    
 다음 예에서는 `ProductionView06` 뷰의 소유권을 뷰가 포함된 스키마의 소유자에게 이전합니다. 뷰는 `Production` 스키마 내부에 있습니다.    
    
```    
ALTER AUTHORIZATION ON OBJECT::Production.ProductionView06 TO SCHEMA OWNER;    
GO    
```    
    
### <a name="c-transfer-ownership-of-a-schema-to-a-user"></a>3. 스키마의 소유권을 사용자에게 이전    
 다음 예에서는 `SeattleProduction11` 스키마의 소유권을 `SandraAlayo` 사용자에게 이전합니다.    
    
```    
ALTER AUTHORIZATION ON SCHEMA::SeattleProduction11 TO SandraAlayo;    
GO    
```    
    
### <a name="d-transfer-ownership-of-an-endpoint-to-a-sql-server-login"></a>4. 엔드포인트의 소유권을 SQL Server 로그인에게 이전    
 다음 예에서는 `CantabSalesServer1` 엔드포인트의 소유권을 `JaePak`에게 이전합니다. 엔드포인트는 서버 수준의 보안 개체이므로 서버 수준 보안 주체에게만 소유권을 이전할 수 있습니다.    
    
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지    
    
```    
ALTER AUTHORIZATION ON ENDPOINT::CantabSalesServer1 TO JaePak;    
GO    
```    
    
### <a name="e-changing-the-owner-of-a-table"></a>5. 테이블의 소유자 변경    
 다음 각 예제는 `Parts` 데이터베이스에서 `Sprockets` 테이블의 소유자를 `MichikoOsada` 데이터베이스 사용자로 변경합니다.    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON dbo.Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::dbo.Sprockets TO MichikoOsada;    
```    
    
### <a name="f-changing-the-owner-of-a-database"></a>6. 데이터베이스의 소유자 변경    
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지.    
    
 다음 예에서는 `Parts` 데이터베이스의 소유자를 로그인 `MichikoOsada`로 변경합니다.    
    
```    
ALTER AUTHORIZATION ON DATABASE::Parts TO MichikoOsada;    
```    
  
### <a name="g-changing-the-owner-of-a-sql-database-to-an-azure-ad-user"></a>7. SQL 데이터베이스의 소유자를 Azure AD 사용자로 변경  
다음 예에서는 `cqclinic.onmicrosoft.com` Active Directory로 지명된 조직에서 SQL Server용 Azure Active Directory 관리자가 현재 데이터베이스의 소유권을 `targetDB` 변경하고, 다음 명령을 사용해 AAD 사용자를 `richel@cqclinic.onmicorsoft.com` 새 데이터베이스 소유자로 만들 수 있습니다.  
    
```    
ALTER AUTHORIZATION ON database::targetDB TO [rachel@cqclinic.onmicrosoft.com];   
```    
    
 Azure AD 사용자의 경우 사용자 이름을 묶는 대괄호가 사용돼야 함을 유의하십시오.  
  
    
## <a name="see-also"></a>참고 항목    
 [OBJECTPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)     
 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)     
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)    
 
