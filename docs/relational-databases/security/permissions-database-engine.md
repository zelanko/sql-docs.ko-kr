---
title: 사용 권한(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 01/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseuser.permissions.database.f1--May use common.permissions
- sql13.swb.databaseuser.permissions.object.f1--May use common.permissions
helpviewer_keywords:
- REFERENCES permission
- permissions [SQL Server]
- security [SQL Server], permissions
- naming conventions [SQL Server]
ms.assetid: f28e3dea-24e6-4a81-877b-02ec4c7e36b9
caps.latest.revision: 76
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 85a62bd00ffc5a85ffe2ab62714202ff2f41cfd2
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39107109"
---
# <a name="permissions-database-engine"></a>사용 권한(데이터베이스 엔진)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 개체에는 보안 주체에 부여될 수 있는 연결된 사용 권한이 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 권한은 로그인 및 서버 역할에 할당된 서버 수준에서 관리되고 데이터베이스 사용자 및 데이터베이스 역할에 할당된 데이터베이스 수준에서 관리됩니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 대한 모델은 데이터베이스 권한에 대하여 동일한 시스템을 갖지만 서버 수준 권한은 사용할 수 없습니다. 이 항목에는 전체 권한 목록이 포함됩니다. 권한에 대한 일반적인 구현은 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하십시오.  
  
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]의 총 권한 수는 237개입니다. 대부분의 권한은 모든 플랫폼에 적용되지만 그렇지 않은 경우도 있습니다. 예를 들어 SQL Database에는 서버 수준 권한을 부여할 수 없으며 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]에는 몇 가지 권한만 적용됩니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 에서는 230개의 권한이 있습니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에서는 219개의 권한이 있습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서는 214개의 권한이 있습니다. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 에서는 195개의 권한이 있습니다. [sys.fn_builtin_permissions](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md) 항목은 최신 버전의 새로운 항목을 지정합니다.

권한을 이해했으면 [GRANT](../../t-sql/statements/grant-transact-sql.md), [REVOKE](../../t-sql/statements/revoke-transact-sql.md)및 [DENY](../../t-sql/statements/deny-transact-sql.md) 문을 사용하여 로그인 및 데이터베이스 수준 권한 사용자에게 서버 수준 권한을 적용합니다. 예를 들면 다음과 같습니다.   
```sql
GRANT SELECT ON OBJECT::HumanResources.Employee TO Larry;
REVOKE SELECT ON OBJECT::HumanResources.Employee TO Larry;
```   
권한 시스템 계획에 대한 자세한 내용은 [데이터베이스 엔진 권한 시작](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을 참조하세요.
  
##  <a name="_conventions"></a> 사용 권한 명명 규칙  
 다음은 사용 권한 이름 지정에 대한 일반적인 규칙 설명입니다.  
  
-   CONTROL  
  
     소유권과 같은 기능을 피부여자에게 줍니다. 피부여자는 보안 개체에 정의된 모든 사용 권한을 효율적으로 갖습니다. CONTROL이 부여된 보안 주체는 또한 보안 개체에 사용 권한을 부여할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 모델은 계층적이기 때문에 특정 범위에서 CONTROL에는 해당 범위 하의 모든 보안 개체에 대한 CONTROL이 내재적으로 포함됩니다. 예를 들어 데이터베이스의 CONTROL은 해당 데이터베이스에 대한 모든 사용 권한, 데이터베이스의 모든 어셈블리에 대한 모든 사용 권한, 데이터베이스의 모든 스키마에 대한 모든 사용 권한 및 데이터베이스 내의 모든 스키마 내에 있는 개체에 대한 모든 사용 권한을 나타냅니다.  
  
-   ALTER  
  
     특정 보안 개체의 소유권을 제외한 속성을 변경할 수 있는 사용 권한을 줍니다. 범위에 부여된 경우 ALTER는 또한 해당 범위 내에 포함된 임의의 보안 개체를 변경하고, 만들고, 삭제할 수 있는 기능을 부여합니다. 예를 들어 스키마의 ALTER 권한에는 스키마에서 개체를 만들고, 변경하고, 삭제할 수 있는 기능이 포함됩니다.  
  
-   ALTER ANY \<*Server Securable*>(여기서 *Server Securable*은 임의의 서버 보안 개체)  
  
     *Server Securable*의 개별 항목을 만들거나 변경하거나 삭제할 수 있는 기능을 제공합니다. 예를 들어 ALTER ANY LOGIN은 인스턴스의 모든 로그인을 만들거나 변경하거나 삭제할 수 있는 기능을 제공합니다.  
  
-   ALTER ANY \<*Database Securable*>(여기서 *Database Securable*은 데이터베이스 수준의 임의의 보안 개체)  
  
     *Database Securable*의 개별 항목을 만들거나(CREATE) 변경하거나(ALTER) 삭제(DROP)할 수 있는 기능을 제공합니다. 예를 들어 ALTER ANY SCHEMA는 데이터베이스의 모든 스키마를 만들거나 변경하거나 삭제할 수 있는 기능을 제공합니다.  
  
-   TAKE OWNERSHIP  
  
     피부여자가 부여된 보안 개체의 소유권을 갖도록 합니다.  
  
-   IMPERSONATE \<*Login*>  
  
     피부여자가 로그인을 가장하도록 합니다.  
  
-   IMPERSONATE \<*User*>  
  
     피부여자가 사용자를 가장하도록 합니다.  
  
-   CREATE \<*Server Securable*>  
  
     피부여자에게 *Server Securable*을 만들 수 있는 기능을 제공합니다.  
  
-   CREATE \<*Database Securable*>  
  
     피부여자에게 *Database Securable*을 만들 수 있는 기능을 제공합니다.  
  
-   CREATE \<*Schema-contained Securable*>  
  
     스키마가 포함된 보안 개체를 만들 수 있는 기능을 제공합니다. 하지만 특정 스키마에 보안 개체를 만들려면 스키마에 대한 ALTER 권한이 필요합니다.  
  
-   VIEW DEFINITION  
  
     피부여자가 메타데이터에 액세스하도록 합니다.  
  
-   REFERENCES  
  
     테이블에 대한 REFERENCES 권한은 해당 테이블을 참조하는 FOREIGN KEY 제약 조건을 만드는 데 필요합니다.  
  
     개체에 대한 REFERENCES 권한은 해당 개체를 참조하는 `WITH SCHEMABINDING` 절을 사용하여 FUNCTION 또는 VIEW를 만드는 데 필요합니다.  
  
## <a name="chart-of-sql-server-permissions"></a>SQL Server 사용 권한 차트  
[!INCLUDE[database-engine-permissions](../../includes/paragraph-content/database-engine-permissions.md)]
  
##  <a name="_securables"></a> 특정 보안 개체에 적용 가능한 사용 권한  
 다음 표에서는 주요 사용 권한 클래스와 사용 권한이 적용될 수 있는 보안 개체 종류를 나열합니다.  
  
|사용 권한|적용 대상|  
|----------------|----------------|  
|ALTER|TYPE을 제외한 모든 개체 클래스입니다.|  
|CONTROL|모든 개체 클래스 <br />AGGREGATE,<br />APPLICATION ROLE,<br />ASSEMBLY,<br />ASYMMETRIC KEY,<br />AVAILABILITY GROUP,<br />CERTIFICATE,<br />CONTRACT,<br />CREDENTIALS, DATABASE,<br />DATABASE SCOPED CREDENTIAL,<br /> DEFAULT,<br />ENDPOINT,<br />FULLTEXT CATALOG,<br />FULLTEXT STOPLIST,<br />FUNCTION,<br />LOGIN,<br />MESSAGE TYPE,<br />PROCEDURE,<br />QUEUE, <br />REMOTE SERVICE BINDING,<br />ROLE,<br />ROUTE,<br />RULE,<br />SCHEMA,<br />SEARCH PROPERTY LIST,<br />SERVER,<br />SERVER ROLE,<br />SERVICE,<br />SYMMETRIC KEY,<br />SYNONYM,<br />TABLE,<br />TYPE, USER,<br />VIEW 및<br />XML SCHEMA COLLECTION|  
|Delete|DATABASE SCOPED CONFIGURATION 및 SERVER를 제외한 전체 개체 클래스입니다.|  
|CREATE 문을 실행하기 전에|CLR 형식, 외부 스크립트, 프로시저([!INCLUDE[tsql](../../includes/tsql-md.md)] 및 CLR), 스칼라와 집계 함수([!INCLUDE[tsql](../../includes/tsql-md.md)] 및 CLR) 및 동의어|  
|IMPERSONATE|로그인 및 사용자|  
|INSERT|동의어, 테이블과 열, 뷰 및 열입니다. 데이터베이스, 스키마 또는 개체 수준에서 권한을 부여할 수 있습니다.|  
|RECEIVE|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 큐|  
|REFERENCES|AGGREGATE,<br />ASSEMBLY,<br />ASYMMETRIC KEY,<br />CERTIFICATE,<br />CONTRACT,<br />DATABASE,<br />DATABASE SCOPED CREDENTIAL,<br />FULLTEXT CATALOG,<br />FULLTEXT STOPLIST,<br />FUNCTION,<br />MESSAGE TYPE,<br />PROCEDURE,<br />QUEUE, <br />RULE,<br />SCHEMA,<br />SEARCH PROPERTY LIST,<br />SEQUENCE OBJECT, <br />SYMMETRIC KEY,<br />SYNONYM,<br />TABLE,<br />TYPE,<br />VIEW 및<br />XML SCHEMA COLLECTION|  
|SELECT|동의어, 테이블과 열, 뷰 및 열입니다. 데이터베이스, 스키마 또는 개체 수준에서 권한을 부여할 수 있습니다.|  
|TAKE OWNERSHIP|DATABASE SCOPED CONFIGURATION, LOGIN, SERVER 및 USER를 제외한 전체 개체 클래스입니다.|  
|UPDATE|동의어, 테이블과 열, 뷰 및 열입니다. 데이터베이스, 스키마 또는 개체 수준에서 권한을 부여할 수 있습니다.|  
|VIEW CHANGE TRACKING|스키마 및 테이블|  
|VIEW DEFINITION|DATABASE SCOPED CONFIGURATION 및 SERVER를 제외한 전체 개체 클래스입니다.|  
  
> [!CAUTION]  
>  설치 시 시스템 개체에 부여되는 기본 사용 권한은 발생할 수 있는 위협이 있는지 신중하게 평가되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 보안 강화의 일환으로 변경할 필요는 없습니다. 시스템 개체에 대한 사용 권한을 변경하면 기능이 제한 또는 중단될 수 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치가 지원되지 않는 상태가 될 수 있습니다.  
  
##  <a name="_permissions"></a> SQL Server 사용 권한  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 권한의 전체 목록을 제공합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 사용 권한은 지원되는 기본 보안 개체에만 사용할 수 있습니다. 서버 수준 사용 권한은 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 부여될 수 없지만 일부 경우에 데이터베이스 사용 권한을 대신 사용할 수 있습니다.  
  
|기본 보안 개체|기본 보안 개체에 대한 세부적 사용 권한|사용 권한 유형 코드|기본 보안 개체를 포함하는 보안 개체|기본 보안 개체의 세부적 사용 권한을 나타내는 컨테이너 보안 개체의 사용 권한|  
|--------------------|--------------------------------------------|--------------------------|--------------------------------------------|------------------------------------------------------------------------------------------|  
|APPLICATION ROLE|ALTER|AL|DATABASE|ALTER ANY APPLICATION ROLE|  
|APPLICATION ROLE|CONTROL|CL|DATABASE|CONTROL|  
|APPLICATION ROLE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|ASSEMBLY|ALTER|AL|DATABASE|ALTER ANY ASSEMBLY|  
|ASSEMBLY|CONTROL|CL|DATABASE|CONTROL|  
|ASSEMBLY|REFERENCES|RF|DATABASE|REFERENCES|  
|ASSEMBLY|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|ASSEMBLY|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|ASYMMETRIC KEY|ALTER|AL|DATABASE|ALTER ANY ASYMMETRIC KEY|  
|ASYMMETRIC KEY|CONTROL|CL|DATABASE|CONTROL|  
|ASYMMETRIC KEY|REFERENCES|RF|DATABASE|REFERENCES|  
|ASYMMETRIC KEY|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|ASYMMETRIC KEY|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|AVAILABILITY GROUP|ALTER|AL|SERVER|ALTER ANY AVAILABILITY GROUP|  
|AVAILABILITY GROUP|CONTROL|CL|SERVER|CONTROL SERVER|  
|AVAILABILITY GROUP|TAKE OWNERSHIP|TO|SERVER|CONTROL SERVER|  
|AVAILABILITY GROUP|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|CERTIFICATE|ALTER|AL|DATABASE|ALTER ANY CERTIFICATE|  
|CERTIFICATE|CONTROL|CL|DATABASE|CONTROL|  
|CERTIFICATE|REFERENCES|RF|DATABASE|REFERENCES|  
|CERTIFICATE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|CERTIFICATE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|CONTRACT|ALTER|AL|DATABASE|ALTER ANY CONTRACT|  
|CONTRACT|CONTROL|CL|DATABASE|CONTROL|  
|CONTRACT|REFERENCES|RF|DATABASE|REFERENCES|  
|CONTRACT|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|CONTRACT|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|DATABASE|ADMINISTER DATABASE BULK OPERATIONS|DABO|SERVER|CONTROL SERVER|
|DATABASE|ALTER|AL|SERVER|ALTER ANY DATABASE|  
|DATABASE|ALTER ANY APPLICATION ROLE|ALAR|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY ASSEMBLY|ALAS|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY ASYMMETRIC KEY|ALAK|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY CERTIFICATE|ALCF|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY COLUMN ENCRYPTION KEY|ALCK<br /><br /> 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ 현재 버전), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY COLUMN MASTER KEY|ALCM<br /><br /> 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ 현재 버전), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY CONTRACT|ALSC|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY DATABASE AUDIT|ALDA|SERVER|ALTER ANY SERVER AUDIT|  
|DATABASE|ALTER ANY DATABASE DDL TRIGGER|ALTG|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY DATABASE EVENT NOTIFICATION|ALED|SERVER|ALTER ANY EVENT NOTIFICATION|  
|DATABASE|ALTER ANY DATABASE EVENT SESSION|AADS<br /><br /> [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 적용됩니다.|SERVER|ALTER ANY EVENT SESSION|  
|DATABASE|ALTER ANY DATABASE SCOPED CONFIGURATION|ALDC<br /><br /> 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ 현재 버전), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY DATASPACE|ALDS|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY EXTERNAL DATA SOURCE|AEDS|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY EXTERNAL FILE FORMAT|AEFF|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY FULLTEXT CATALOG|ALFT|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY MASK|AAMK<br /><br /> 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ 현재 버전), SQL Database.|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY MESSAGE TYPE|ALMT|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY REMOTE SERVICE BINDING|ALSB|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY ROLE|ALRL|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY ROUTE|ALRT|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY SCHEMA|ALSM|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY SECURITY POLICY|ALSP<br /><br /> 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ 현재 버전), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY SENSITIVITY CLASSIFICATION|ALSP<br />적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](SQL Server vNext(15.x) ~ 현재 버전), SQL Database.|DATABASE|CONTROL SERVER|
|DATABASE|ALTER ANY SERVICE|ALSV|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY SYMMETRIC KEY|ALSK|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY USER|ALUS|SERVER|CONTROL SERVER|  
|DATABASE|AUTHENTICATE|AUTH|SERVER|AUTHENTICATE SERVER|  
|DATABASE|BACKUP DATABASE|BADB|SERVER|CONTROL SERVER|  
|DATABASE|BACKUP LOG|BALO|SERVER|CONTROL SERVER|  
|DATABASE|CHECKPOINT|CP|SERVER|CONTROL SERVER|  
|DATABASE|CONNECT|CO|SERVER|CONTROL SERVER|  
|DATABASE|CONNECT REPLICATION|CORP|SERVER|CONTROL SERVER|  
|DATABASE|CONTROL|CL|SERVER|CONTROL SERVER|  
|DATABASE|CREATE AGGREGATE|CRAG|SERVER|CONTROL SERVER|  
|DATABASE|CREATE ASSEMBLY|CRAS|SERVER|CONTROL SERVER|  
|DATABASE|CREATE ASYMMETRIC KEY|CRAK|SERVER|CONTROL SERVER|  
|DATABASE|CREATE CERTIFICATE|CRCF|SERVER|CONTROL SERVER|  
|DATABASE|CREATE CONTRACT|CRSC|SERVER|CONTROL SERVER|  
|DATABASE|CREATE DATABASE|CRDB|SERVER|CREATE ANY DATABASE|  
|DATABASE|CREATE DATABASE DDL EVENT NOTIFICATION|CRED|SERVER|CREATE DDL EVENT NOTIFICATION|  
|DATABASE|CREATE DEFAULT|CRDF|SERVER|CONTROL SERVER|  
|DATABASE|CREATE FULLTEXT CATALOG|CRFT|SERVER|CONTROL SERVER|  
|DATABASE|CREATE FUNCTION|CRFN|SERVER|CONTROL SERVER|  
|DATABASE|CREATE MESSAGE TYPE|CRMT|SERVER|CONTROL SERVER|  
|DATABASE|CREATE PROCEDURE|CRPR|SERVER|CONTROL SERVER|  
|DATABASE|CREATE QUEUE|CRQU|SERVER|CONTROL SERVER|  
|DATABASE|CREATE REMOTE SERVICE BINDING|CRSB|SERVER|CONTROL SERVER|  
|DATABASE|CREATE ROLE|CRRL|SERVER|CONTROL SERVER|  
|DATABASE|CREATE ROUTE|CRRT|SERVER|CONTROL SERVER|  
|DATABASE|CREATE RULE|CRRU|SERVER|CONTROL SERVER|  
|DATABASE|CREATE SCHEMA|CRSM|SERVER|CONTROL SERVER|  
|DATABASE|CREATE SERVICE|CRSV|SERVER|CONTROL SERVER|  
|DATABASE|CREATE SYMMETRIC KEY|CRSK|SERVER|CONTROL SERVER|  
|DATABASE|CREATE SYNONYM|CRSN|SERVER|CONTROL SERVER|  
|DATABASE|CREATE TABLE|CRTB|SERVER|CONTROL SERVER|  
|DATABASE|CREATE TYPE|CRTY|SERVER|CONTROL SERVER|  
|DATABASE|CREATE VIEW|CRVW|SERVER|CONTROL SERVER|  
|DATABASE|CREATE XML SCHEMA COLLECTION|CRXS|SERVER|CONTROL SERVER|  
|DATABASE|Delete|DL|SERVER|CONTROL SERVER|  
|DATABASE|CREATE 문을 실행하기 전에|EX|SERVER|CONTROL SERVER|  
|DATABASE|EXECUTE ANY EXTERNAL SCRIPT|EAES<br /><br /> 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ 현재 버전).|SERVER|CONTROL SERVER|  
|DATABASE|INSERT|IN|SERVER|CONTROL SERVER|  
|DATABASE|KILL DATABASE CONNECTION|KIDC<br /><br /> [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에만 적용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 ALTER ANY CONNECTION을 사용합니다.|SERVER|ALTER ANY CONNECTION|  
|DATABASE|REFERENCES|RF|SERVER|CONTROL SERVER|  
|DATABASE|SELECT|SL|SERVER|CONTROL SERVER|  
|DATABASE|SHOWPLAN|SPLN|SERVER|ALTER TRACE|  
|DATABASE|SUBSCRIBE QUERY NOTIFICATIONS|SUQN|SERVER|CONTROL SERVER|  
|DATABASE|TAKE OWNERSHIP|TO|SERVER|CONTROL SERVER|  
|DATABASE|UNMASK|UMSK<br /><br /> 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ 현재 버전), SQL Database.|SERVER|CONTROL SERVER|  
|DATABASE|UPDATE|UP|SERVER|CONTROL SERVER|  
|DATABASE|VIEW ANY COLUMN ENCRYPTION KEY DEFINITION|VWCK<br /><br /> 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ 현재 버전), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|VIEW SERVER STATE|  
|DATABASE|VIEW ANY COLUMN MASTER KEY DEFINITION|vWCM<br /><br /> 적용 대상: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ 현재 버전), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|VIEW SERVER STATE|  
|DATABASE|VIEW DATABASE STATE|VWDS|SERVER|VIEW SERVER STATE|  
|DATABASE|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|DATABASE SCOPED CREDENTIAL|ALTER|AL|DATABASE|CONTROL|
|DATABASE SCOPED CREDENTIAL|CONTROL|CL|DATABASE|CONTROL|
|DATABASE SCOPED CREDENTIAL|REFERENCES|RF|DATABASE|REFERENCES|
|DATABASE SCOPED CREDENTIAL|TAKE OWNERSHIP|TO|DATABASE|CONTROL|
|DATABASE SCOPED CREDENTIAL|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|
|ENDPOINT|ALTER|AL|SERVER|ALTER ANY ENDPOINT|  
|ENDPOINT|CONNECT|CO|SERVER|CONTROL SERVER|  
|ENDPOINT|CONTROL|CL|SERVER|CONTROL SERVER|  
|ENDPOINT|TAKE OWNERSHIP|TO|SERVER|CONTROL SERVER|  
|ENDPOINT|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|FULLTEXT CATALOG|ALTER|AL|DATABASE|ALTER ANY FULLTEXT CATALOG|  
|FULLTEXT CATALOG|CONTROL|CL|DATABASE|CONTROL|  
|FULLTEXT CATALOG|REFERENCES|RF|DATABASE|REFERENCES|  
|FULLTEXT CATALOG|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|FULLTEXT CATALOG|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|FULLTEXT STOPLIST|ALTER|AL|DATABASE|ALTER ANY FULLTEXT CATALOG|  
|FULLTEXT STOPLIST|CONTROL|CL|DATABASE|CONTROL|  
|FULLTEXT STOPLIST|REFERENCES|RF|DATABASE|REFERENCES|  
|FULLTEXT STOPLIST|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|FULLTEXT STOPLIST|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|Login|ALTER|AL|SERVER|ALTER ANY LOGIN|  
|Login|CONTROL|CL|SERVER|CONTROL SERVER|  
|Login|IMPERSONATE|IM|SERVER|CONTROL SERVER|  
|Login|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|MESSAGE TYPE|ALTER|AL|DATABASE|ALTER ANY MESSAGE TYPE|  
|MESSAGE TYPE|CONTROL|CL|DATABASE|CONTROL|  
|MESSAGE TYPE|REFERENCES|RF|DATABASE|REFERENCES|  
|MESSAGE TYPE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|MESSAGE TYPE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|OBJECT|ALTER|AL|SCHEMA|ALTER|  
|OBJECT|CONTROL|CL|SCHEMA|CONTROL|  
|OBJECT|DELETE|DL|SCHEMA|Delete|  
|OBJECT|CREATE 문을 실행하기 전에|EX|SCHEMA|CREATE 문을 실행하기 전에|  
|OBJECT|INSERT|IN|SCHEMA|INSERT|  
|OBJECT|RECEIVE|RC|SCHEMA|CONTROL|  
|OBJECT|REFERENCES|RF|SCHEMA|REFERENCES|  
|OBJECT|SELECT|SL|SCHEMA|SELECT|  
|OBJECT|TAKE OWNERSHIP|TO|SCHEMA|CONTROL|  
|OBJECT|UPDATE|UP|SCHEMA|UPDATE|  
|OBJECT|VIEW CHANGE TRACKING|VWCT|SCHEMA|VIEW CHANGE TRACKING|  
|OBJECT|VIEW DEFINITION|VW|SCHEMA|VIEW DEFINITION|  
|REMOTE SERVICE BINDING|ALTER|AL|DATABASE|ALTER ANY REMOTE SERVICE BINDING|  
|REMOTE SERVICE BINDING|CONTROL|CL|DATABASE|CONTROL|  
|REMOTE SERVICE BINDING|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|REMOTE SERVICE BINDING|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|ROLE|ALTER|AL|DATABASE|ALTER ANY ROLE|  
|ROLE|CONTROL|CL|DATABASE|CONTROL|  
|ROLE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|ROLE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|ROUTE|ALTER|AL|DATABASE|ALTER ANY ROUTE|  
|ROUTE|CONTROL|CL|DATABASE|CONTROL|  
|ROUTE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|ROUTE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|SEARCH PROPERTY LIST|ALTER|AL|SERVER|ALTER ANY FULLTEXT CATALOG|  
|SEARCH PROPERTY LIST|CONTROL|CL|SERVER|CONTROL|  
|SEARCH PROPERTY LIST|REFERENCES|RF|SERVER|REFERENCES|  
|SEARCH PROPERTY LIST|TAKE OWNERSHIP|TO|SERVER|CONTROL|  
|SEARCH PROPERTY LIST|VIEW DEFINITION|VW|SERVER|VIEW DEFINITION|  
|SCHEMA|ALTER|AL|DATABASE|ALTER ANY SCHEMA|  
|SCHEMA|CONTROL|CL|DATABASE|CONTROL|  
|SCHEMA|CREATE SEQUENCE|CRSO|DATABASE|CONTROL|  
|SCHEMA|Delete|DL|DATABASE|Delete|  
|SCHEMA|CREATE 문을 실행하기 전에|EX|DATABASE|CREATE 문을 실행하기 전에|  
|SCHEMA|INSERT|IN|DATABASE|INSERT|  
|SCHEMA|REFERENCES|RF|DATABASE|REFERENCES|  
|SCHEMA|SELECT|SL|DATABASE|SELECT|  
|SCHEMA|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|SCHEMA|UPDATE|UP|DATABASE|UPDATE|  
|SCHEMA|VIEW CHANGE TRACKING|VWCT|DATABASE|VIEW CHANGE TRACKING|  
|SCHEMA|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|SERVER|ADMINISTER BULK OPERATIONS|ADBO|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY AVAILABILITY GROUP|ALAG|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY CONNECTION|ALCO|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY CREDENTIAL|ALCD|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY DATABASE|ALDB|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY ENDPOINT|ALHE|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY EVENT NOTIFICATION|ALES|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY EVENT SESSION|AAES|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY LINKED SERVER|ALLS|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY LOGIN|ALLG|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY SERVER AUDIT|ALAA|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER ANY SERVER ROLE|ALSR|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER RESOURCES|ALRS|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER SERVER STATE|ALSS|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER SETTINGS|ALST|해당 사항 없음|해당 사항 없음|  
|SERVER|ALTER TRACE|ALTR|해당 사항 없음|해당 사항 없음|  
|SERVER|AUTHENTICATE SERVER|AUTH|해당 사항 없음|해당 사항 없음|  
|SERVER|CONNECT ANY DATABASE|CADB|해당 사항 없음|해당 사항 없음|  
|SERVER|CONNECT SQL|COSQ|해당 사항 없음|해당 사항 없음|  
|SERVER|CONTROL SERVER|CL|해당 사항 없음|해당 사항 없음|  
|SERVER|CREATE ANY DATABASE|CRDB|해당 사항 없음|해당 사항 없음|  
|SERVER|CREATE AVAILABILITY GROUP|CRAC|해당 사항 없음|해당 사항 없음|  
|SERVER|CREATE DDL EVENT NOTIFICATION|CRDE|해당 사항 없음|해당 사항 없음|  
|SERVER|CREATE ENDPOINT|CRHE|해당 사항 없음|해당 사항 없음|  
|SERVER|CREATE SERVER ROLE|CRSR|해당 사항 없음|해당 사항 없음|  
|SERVER|CREATE TRACE EVENT NOTIFICATION|CRTE|해당 사항 없음|해당 사항 없음|  
|SERVER|EXTERNAL ACCESS ASSEMBLY|XA|해당 사항 없음|해당 사항 없음|  
|SERVER|IMPERSONATE ANY LOGIN|IAL|해당 사항 없음|해당 사항 없음|  
|SERVER|SELECT ALL USER SECURABLES|SUS|해당 사항 없음|해당 사항 없음|  
|SERVER|SHUTDOWN|SHDN|해당 사항 없음|해당 사항 없음|  
|SERVER|UNSAFE ASSEMBLY|XU|해당 사항 없음|해당 사항 없음|  
|SERVER|VIEW ANY DATABASE|VWDB|해당 사항 없음|해당 사항 없음|  
|SERVER|VIEW ANY DEFINITION|VWAD|해당 사항 없음|해당 사항 없음|  
|SERVER|VIEW SERVER STATE|VWSS|해당 사항 없음|해당 사항 없음|  
|SERVER ROLE|ALTER|AL|SERVER|ALTER ANY SERVER ROLE|  
|SERVER ROLE|CONTROL|CL|SERVER|CONTROL SERVER|  
|SERVER ROLE|TAKE OWNERSHIP|TO|SERVER|CONTROL SERVER|  
|SERVER ROLE|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|SERVICE|ALTER|AL|DATABASE|ALTER ANY SERVICE|  
|SERVICE|CONTROL|CL|DATABASE|CONTROL|  
|SERVICE|SEND|SN|DATABASE|CONTROL|  
|SERVICE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|SERVICE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|SYMMETRIC KEY|ALTER|AL|DATABASE|ALTER ANY SYMMETRIC KEY|  
|SYMMETRIC KEY|CONTROL|CL|DATABASE|CONTROL|  
|SYMMETRIC KEY|REFERENCES|RF|DATABASE|REFERENCES|  
|SYMMETRIC KEY|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|SYMMETRIC KEY|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|TYPE|CONTROL|CL|SCHEMA|CONTROL|  
|TYPE|CREATE 문을 실행하기 전에|EX|SCHEMA|CREATE 문을 실행하기 전에|  
|TYPE|REFERENCES|RF|SCHEMA|REFERENCES|  
|TYPE|TAKE OWNERSHIP|TO|SCHEMA|CONTROL|  
|TYPE|VIEW DEFINITION|VW|SCHEMA|VIEW DEFINITION|  
|User|ALTER|AL|DATABASE|ALTER ANY USER|  
|User|CONTROL|CL|DATABASE|CONTROL|  
|User|IMPERSONATE|IM|DATABASE|CONTROL|  
|User|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|XML SCHEMA COLLECTION|ALTER|AL|SCHEMA|ALTER|  
|XML SCHEMA COLLECTION|CONTROL|CL|SCHEMA|CONTROL|  
|XML SCHEMA COLLECTION|CREATE 문을 실행하기 전에|EX|SCHEMA|CREATE 문을 실행하기 전에|  
|XML SCHEMA COLLECTION|REFERENCES|RF|SCHEMA|REFERENCES|  
|XML SCHEMA COLLECTION|TAKE OWNERSHIP|TO|SCHEMA|CONTROL|  
|XML SCHEMA COLLECTION|VIEW DEFINITION|VW|SCHEMA|VIEW DEFINITION|  
  
##  <a name="_algorithm"></a> 사용 권한 검사 알고리즘 요약  
 사용 권한 검사는 복잡할 수 있습니다. 사용 권한 검사 알고리즘에는 겹치는 그룹 멤버 자격과 소유권 체인이 포함됩니다. 둘 다 명시적 및 암시적 사용 권한이며 보안 가능한 엔터티가 포함된 보안 개체 클래스에 대한 사용 권한의 영향을 받을 수 있습니다. 알고리즘의 일반적인 프로세스는 관련된 사용 권한을 모두 수집하는 것입니다. DENY 차단이 발견되지 않는 경우 알고리즘에서는 충분한 액세스 권한을 제공하는 GRANT를 검색합니다. 알고리즘에는 세 가지 필수 요소인 **보안 컨텍스트**, **사용 권한 공간**및 **필요한 사용 권한**이 포함되어 있습니다.  
  
> [!NOTE]  
>  sa, dbo, 엔터티 소유자, information_schema, sys 또는 사용자 자신에 대한 권한을 부여, 거부 또는 취소할 수 없습니다.  
  
-   **보안 컨텍스트**  
  
     보안 컨텍스트는 사용 권한을 액세스 검사에 제공하는 보안 주체 그룹입니다. 이것은 EXECUTE AS 문 사용으로 보안 컨텍스트가 다른 로그인 또는 사용자로 변경되지 않는 한 현재 로그인 또는 사용자와 관련된 사용 권한입니다. 보안 컨텍스트에는 다음 보안 주체가 포함됩니다.  
  
    -   로그인  
  
    -   사용자  
  
    -   역할 멤버 자격  
  
    -   Windows 그룹 멤버 자격  
  
    -   모듈 서명이 사용되는 경우 사용자가 현재 실행 중인 모듈에 서명하는 데 사용된 인증서에 대한 모든 로그인 또는 사용자 계정과 해당 보안 주체와 관련된 역할 멤버 자격  
  
-   **사용 권한 공간**  
  
     사용 권한 공간은 보안 가능한 엔터티이며 보안 개체를 포함하는 보안 개체 클래스입니다. 예를 들어 테이블(보안 가능한 엔터티)은 스키마 보안 개체 클래스 및 데이터베이스 보안 개체 클래스에 포함됩니다. 액세스는 테이블 수준, 스키마 수준, 데이터베이스 수준 및 서버 수준 사용 권한의 영향을 받습니다. 자세한 내용은 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)을 참조하세요.  
  
-   **필요한 권한**  
  
     필요한 유형의 사용 권한입니다. 예를 들면 INSERT, UPDATE, DELETE, SELECT, EXECUTE, ALTER, CONTROL 등입니다.  
  
     다음 예에서와 같이 액세스에는 여러 사용 권한이 필요할 수 있습니다.  
  
    -   저장 프로시저를 사용하려면 저장 프로시저에 대한 EXECUTE 사용 권한과 저장 프로시저에서 참조되는 여러 테이블에 대한 INSERT 사용 권한이 모두 필요할 수 있습니다.  
  
    -   동적 관리 뷰를 사용하려면 뷰에 대한 VIEW SERVER STATE 및 SELECT 사용 권한이 모두 필요할 수 있습니다.  
  
### <a name="general-steps-of-the-algorithm"></a>알고리즘의 일반적인 단계  
 알고리즘에서 보안 개체에 대한 액세스 허용 여부를 결정할 때 알고리즘에서 사용하는 세부 단계는 관련된 보안 주체 및 보안 개체에 따라 다릅니다. 하지만 다음과 같은 일반적인 단계를 수행합니다.  
  
1.  로그인이 sysadmin 고정 서버 역할의 멤버인 경우 또는 사용자가 현재 데이터베이스의 dbo 사용자인 경우 사용 권한 검사를 무시합니다.  
  
2.  소유권 체인이 적용 가능하며 체인에 있는 이전 개체에 대한 액세스 검사가 보안 검사를 통과하는 경우 액세스를 허용합니다.  
  
3.  **보안 컨텍스트**를 만들 수 있도록 호출자와 관련된 서버 수준, 데이터베이스 수준 및 서명된 모듈 ID를 집계합니다.  
  
4.  해당 **보안 컨텍스트**의 경우 **사용 권한 공간**에 대해 부여되거나 거부된 모든 사용 권한을 수집합니다. 사용 권한은 명시적으로 GRANT, GRANT WITH GRANT 또는 DENY로 지정되거나 내포적/포괄적 사용 권한인 GRANT 또는 DENY로 지정될 수 있습니다. 예를 들어 스키마에 대한 CONTROL 권한은 테이블에 대한 CONTROL을 내포합니다. 또한 테이블에 대한 CONTROL은 SELECT를 내포합니다. 따라서 스키마에 대한 CONTROL이 부여된 경우 테이블에 대한 SELECT도 부여됩니다. 테이블에 대한 CONTROL이 거부된 경우 테이블에 대한 SELECT도 거부됩니다.  
  
    > [!NOTE]  
    >  열 수준 사용 권한의 GRANT는 개체 수준의 DENY보다 우선합니다.  
  
5.  **필요한 사용 권한**을 식별합니다.  
  
6.  **사용 권한 공간** 의 개체에 대한 **보안 컨텍스트** 에서 모든 ID에 대해 **필요한 사용 권한**이 직접적으로 또는 암시적으로 거부되는 경우 사용 권한 검사가 실패합니다.  
  
7.  **필요한 권한** 이 거부되지 않고 **사용 권한 공간** 의 모든 개체에 대한 **보안 컨텍스트** 에서 모든 ID에 대한 직접적 또는 암시적인 GRANT 또는 GRANT WITH GRANT 사용 권한이 **필요한 권한**에 포함되는 경우 사용 권한 검사가 통과합니다.  

## <a name="special-considerations-for-column-level-permissions"></a>열 수준 사용 권한에 대한 특별 고려 사항

*<table_name>(\<column _name>)* 구문을 사용하여 열 수준 사용 권한을 부여합니다. 예를 들어 다음과 같이 사용할 수 있습니다.
```sql
GRANT SELECT ON OBJECT::Customer(CustomerName) TO UserJoe;
```
테이블에서 DENY는 열에서 GRANT에 의해 재정의됩니다. 그러나 테이블에서 후속 DENY는 열 GRANT를 제거합니다. 
  
##  <a name="_examples"></a> 예  
 이 섹션의 예에서는 사용 권한 정보를 검색하는 방법을 보여 줍니다.  
  
### <a name="a-returning-the-complete-list-of-grantable-permissions"></a>1. 부여 가능한 사용 권한의 전체 목록 반환  
 다음 문에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 함수를 사용하여 모든 `fn_builtin_permissions` 사용 권한을 반환합니다. 자세한 내용은 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)를 참조하세요.  
  
```sql  
SELECT * FROM fn_builtin_permissions(default);  
GO  
```  
  
### <a name="b-returning-the-permissions-on-a-particular-class-of-objects"></a>2. 특정 개체 클래스의 사용 권한 반환  
 다음 예제에서는 `fn_builtin_permissions` 를 사용하여 보안 개체 범주에 사용할 수 있는 모든 사용 권한을 표시합니다. 다음 예에서는 어셈블리의 사용 권한을 반환합니다.  
  
```sql  
SELECT * FROM fn_builtin_permissions('assembly');  
GO    
```  
  
### <a name="c-returning-the-permissions-granted-to-the-executing-principal-on-an-object"></a>3. 개체의 실행 보안 주체에 부여된 사용 권한 반환  
 다음 예에서는 `fn_my_permissions` 를 사용하여 지정된 보안 개체에 대해 해당 보안 주체가 가진 유효 사용 권한의 목록을 반환합니다. 다음 예에서는 `Orders55`라는 개체의 사용 권한을 반환합니다. 자세한 내용은 [sys.fn_my_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)를 참조하세요.  
  
```sql  
SELECT * FROM fn_my_permissions('Orders55', 'object');  
GO  
```  
  
### <a name="d-returning-the-permissions-applicable-to-a-specified-object"></a>4. 지정된 개체에 적용할 수 있는 사용 권한 반환  
 다음 예에서는 `Yttrium`이라는 개체에 적용할 수 있는 사용 권한을 반환합니다. `OBJECT_ID` 개체의 ID를 검색하는 데 기본 제공 함수인 `Yttrium`가 사용됩니다.  
  
```sql  
SELECT * FROM sys.database_permissions   
    WHERE major_id = OBJECT_ID('Yttrium');  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
