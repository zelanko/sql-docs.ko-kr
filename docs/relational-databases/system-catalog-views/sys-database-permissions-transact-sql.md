---
description: sys.database_permissions(Transact-SQL)
title: sys.database_permissions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_permissions
- sys.database_permissions_TSQL
- database_permissions_TSQL
- sys.database_permissions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_permissions catalog view
ms.assetid: c1e261f8-6cb0-4759-b5f1-5ec233602655
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0af3adae81e4f0bb9489e3534427dfe03efebf09
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475254"
---
# <a name="sysdatabase_permissions-transact-sql"></a>sys.database_permissions(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  데이터베이스에 있는 각 사용 권한이나 열 예외 권한에 대해 행을 반환합니다. 열에는 해당 개체 수준 사용 권한과는 다른 모든 사용 권한에 대한 행이 있습니다. 열 사용 권한이 해당 개체 사용 권한과 동일한 경우 해당 개체에 대 한 행이 없으며 적용 되는 권한은 개체의 사용 권한입니다.  
  
> [!IMPORTANT]  
>  열 수준 사용 권한은 동일한 엔터티의 개체 수준 사용 권한을 대체합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|사용 권한이 있는 클래스를 식별합니다.<br /><br /> 0 = 데이터베이스<br />1 = 개체 또는 열<br />3 = 스키마<br />4 = 데이터베이스 보안 주체<br />5 = 어셈블리 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상.<br />6 = 형식<br />10 = XML 스키마 컬렉션- <br />                      **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br />15 = 메시지 유형- **이상에 적용 됩니다**. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]<br />16 = 서비스 계약- **이상에 적용 됩니다**. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]<br />17 = 서비스 **적용** 대상: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br />18 = 원격 서비스 바인딩- **이상에 적용** 됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]<br />19 = 경로 **적용** 대상: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상.<br />23 = 전체 텍스트 카탈로그-이상 **에 적용** 됩니다 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .<br />24 = 대칭 키- **적용** 대상: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br />25 = 인증서- **적용** 대상: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상.<br />26 = 비대칭 키-적용 대상: 이상 **에 적용 됩니다** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .|  
|**class_desc**|**nvarchar(60)**|사용 권한이 있는 클래스에 대한 설명입니다.<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN<br /><br /> SCHEMA<br /><br /> DATABASE_PRINCIPAL<br /><br /> ASSEMBLY<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> MESSAGE_TYPE<br /><br /> SERVICE_CONTRACT<br /><br /> SERVICE<br /><br /> REMOTE_SERVICE_BINDING<br /><br /> ROUTE<br /><br /> FULLTEXT_CATALOG<br /><br /> SYMMETRIC_KEYS<br /><br /> 인증서<br /><br /> ASYMMETRIC_KEY|  
|**major_id**|**int**|사용 권한이 존재하는 항목의 ID입니다. 이는 클래스에 따라 해석됩니다. 일반적으로 **major_id** 는 클래스가 나타내는 항목에 적용 되는 id의 종류입니다. <br /><br /> 0 = 데이터베이스 자체 <br /><br /> >0 = 사용자 개체에 대 한 Object-IDs <br /><br /> \<0 = 시스템 개체에 대 한 Object-IDs |  
|**minor_id**|**int**|사용 권한이 존재하는 항목의 보조 ID입니다. 이는 클래스에 따라 해석됩니다. 개체 클래스에 사용할 수 있는 하위 범주가 없기 때문에 **minor_id** 은 종종 0입니다. 그렇지 않으면 테이블의 열 ID입니다.|  
|**grantee_principal_id**|**int**|사용 권한이 부여된 데이터베이스 보안 주체 ID입니다.|  
|**grantor_principal_id**|**int**|사용 권한 부여자의 데이터베이스 보안 주체 ID입니다.|  
|**type**|**char (4)**|데이터베이스 사용 권한의 유형입니다. 사용 권한 유형 목록은 다음 표를 참조하세요.|  
|**permission_name**|**nvarchar(128)**|사용 권한 이름입니다.|  
|**state**|**char(1)**|사용 권한 상태입니다.<br /><br /> D = 거부<br /><br /> R = 취소<br /><br /> G = 허용<br /><br /> W = Grant 옵션을 사용하여 허용|  
|**state_desc**|**nvarchar(60)**|사용 권한 상태에 대한 설명입니다.<br /><br /> 거부<br /><br /> REVOKE<br /><br /> GRANT<br /><br /> GRANT_WITH_GRANT_OPTION|  

## <a name="database-permissions"></a>데이터베이스 권한   
다음과 같은 유형의 사용 권한을 사용할 수 있습니다.
  
|사용 권한 유형|사용 권한 이름|보안 개체에 적용되는 항목|  
|---------------------|---------------------|--------------------------|  
|AADS |ALTER ANY DATABASE EVENT SESSION |DATABASE |  
|AAMK |ALTER ANY MASK |DATABASE |  
|AEDS |ALTER ANY EXTERNAL DATA SOURCE |DATABASE |  
|AEFF |ALTER ANY EXTERNAL FILE FORMAT |DATABASE |  
|AL|ALTER|APPLICATION ROLE, ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, REMOTE SERVICE BINDING, ROLE, ROUTE, SCHEMA, SERVICE, SYMMETRIC KEY, USER, XML SCHEMA COLLECTION|  
|ALAK|ALTER ANY ASYMMETRIC KEY|DATABASE|  
|ALAR|ALTER ANY APPLICATION ROLE|DATABASE|  
|ALAS|ALTER ANY ASSEMBLY|DATABASE|  
|ALCF|ALTER ANY CERTIFICATE|DATABASE|  
|ALDS|ALTER ANY DATASPACE|DATABASE|  
|ALED|ALTER ANY DATABASE EVENT NOTIFICATION|DATABASE|  
|ALFT|ALTER ANY FULLTEXT CATALOG|DATABASE|  
|ALMT|ALTER ANY MESSAGE TYPE|DATABASE|  
|ALRL|ALTER ANY ROLE|DATABASE|  
|ALRT|ALTER ANY ROUTE|DATABASE|  
|ALSB|ALTER ANY REMOTE SERVICE BINDING|DATABASE|  
|ALSC|ALTER ANY CONTRACT|DATABASE|  
|ALSK|ALTER ANY SYMMETRIC KEY|DATABASE|  
|ALSM|ALTER ANY SCHEMA|DATABASE|  
|ALSV|ALTER ANY SERVICE|DATABASE|  
|ALTG|ALTER ANY DATABASE DDL TRIGGER|DATABASE|  
|ALUS|ALTER ANY USER|DATABASE|  
|AUTH|AUTHENTICATE|DATABASE|  
|BADB|BACKUP DATABASE|DATABASE|  
|BALO|BACKUP LOG|DATABASE|  
|CL|CONTROL|APPLICATION ROLE, ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, REMOTE SERVICE BINDING, ROLE, ROUTE, SCHEMA, SERVICE, SYMMETRIC KEY, TYPE, USER, XML SCHEMA COLLECTION|  
|CO|CONNECT|DATABASE|  
|CORP|CONNECT REPLICATION|DATABASE|  
|CP|CHECKPOINT|DATABASE|  
|CRAG|CREATE AGGREGATE|DATABASE|  
|CRAK|CREATE ASYMMETRIC KEY|DATABASE|  
|CRAS|CREATE ASSEMBLY|DATABASE|  
|CRCF|CREATE CERTIFICATE|DATABASE|  
|CRDB|CREATE DATABASE|DATABASE|  
|CRDF|CREATE DEFAULT|DATABASE|  
|CRED|CREATE DATABASE DDL EVENT NOTIFICATION|DATABASE|  
|CRFN|CREATE FUNCTION|DATABASE|  
|CRFT|CREATE FULLTEXT CATALOG|DATABASE|  
|CRMT|CREATE MESSAGE TYPE|DATABASE|  
|CRPR|CREATE PROCEDURE|DATABASE|  
|CRQU|CREATE QUEUE|DATABASE|  
|CRRL|CREATE ROLE|DATABASE|  
|CRRT|CREATE ROUTE|DATABASE|  
|CRRU|CREATE RULE|DATABASE|  
|CRSB|CREATE REMOTE SERVICE BINDING|DATABASE|  
|CRSC|CREATE CONTRACT|DATABASE|  
|CRSK|CREATE SYMMETRIC KEY|DATABASE|  
|CRSM|CREATE SCHEMA|DATABASE|  
|CRSN|CREATE SYNONYM|DATABASE|  
|CRSO|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> CREATE SEQUENCE|DATABASE|  
|CRSV|CREATE SERVICE|DATABASE|  
|CRTB|CREATE TABLE|DATABASE|  
|CRTY|CREATE TYPE|DATABASE|  
|CRVW|CREATE VIEW|DATABASE|  
|CRXS|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> CREATE XML SCHEMA COLLECTION|DATABASE|  
|DABO |ADMINISTER DATABASE BULK OPERATIONS | DATABASE |
|DL|Delete|DATABASE, OBJECT, SCHEMA|  
|EAES |EXECUTE ANY EXTERNAL SCRIPT |DATABASE |
|EX|CREATE 문을 실행하기 전에|ASSEMBLY, DATABASE, OBJECT, SCHEMA, TYPE, XML SCHEMA COLLECTION|  
|IM|IMPERSONATE|USER|  
|IN|INSERT|DATABASE, OBJECT, SCHEMA|  
|RC|RECEIVE|OBJECT|  
|RF|REFERENCES|ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, SCHEMA, SYMMETRIC KEY, TYPE, XML SCHEMA COLLECTION|  
|SL|SELECT|DATABASE, OBJECT, SCHEMA|  
|SN|SEND|SERVICE|  
|SPLN|SHOWPLAN|DATABASE|  
|SUQN|SUBSCRIBE QUERY NOTIFICATIONS|DATABASE|  
|TO|TAKE OWNERSHIP|ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, REMOTE SERVICE BINDING, ROLE, ROUTE, SCHEMA, SERVICE, SYMMETRIC KEY, TYPE, XML SCHEMA COLLECTION|  
|UP|UPDATE|DATABASE, OBJECT, SCHEMA|  
|VW|VIEW DEFINITION|APPLICATION ROLE, ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, REMOTE SERVICE BINDING, ROLE, ROUTE, SCHEMA, SERVICE, SYMMETRIC KEY, TYPE, USER, XML SCHEMA COLLECTION|  
|VWCK |VIEW ANY COLUMN ENCRYPTION KEY DEFINITION|DATABASE |  
|VWCM |VIEW ANY COLUMN MASTER KEY DEFINITION|DATABASE |  
|VWCT|VIEW CHANGE TRACKING|TABLE, SCHEMA|  
|VWDS|VIEW DATABASE STATE|DATABASE|  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자는 자산의 권한을 볼 수 있습니다. 다른 사용자에 대한 사용 권한을 보려면 로그인할 때 VIEW DEFINITION, ALTER ANY USER, 또는 사용 권한이 필요합니다. 사용자 정의 역할을 보려면 ALTER ANY ROLE 또는 역할(예: 공용)의 멤버 자격이 필요합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-all-the-permissions-of-database-principals"></a>A: 데이터베이스 보안 주체의 모든 사용 권한 나열  
 다음 쿼리는 데이터베이스 보안 주체에 대해 명시적으로 부여되거나 거부된 사용 권한을 나열합니다.  
  
> [!IMPORTANT]  
>  고정 데이터베이스 역할의 사용 권한은 sys.database_permissions에 나타나지 않습니다. 따라서 데이터베이스 보안 주체가 여기에 나열되지 않은 추가 사용 권한을 가질 수 있습니다.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="b-listing-permissions-on-schema-objects-within-a-database"></a>B: 데이터베이스 내의 스키마 개체에 대 한 사용 권한 나열  
 다음 쿼리는 sys.database_principals 및 sys.database_permissions를 sys.objects 및 sys.schemas에 조인하여 특정 스키마 개체에 부여되거나 거부된 사용 권한을 나열합니다.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
    
  
## <a name="see-also"></a>참고 항목  
 [Securables](../../relational-databases/security/securables.md)   
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  


