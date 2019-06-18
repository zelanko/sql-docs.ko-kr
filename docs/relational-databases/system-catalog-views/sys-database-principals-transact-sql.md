---
title: sys.database_principals (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_principals
- database_principals_TSQL
- sys.database_principals
- sys.database_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_principals catalog view
ms.assetid: 8cb239e9-eb8c-4109-9cec-0d35de95fa0e
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 512994ada852ea7807cc14ecd5b25d9acff56ffc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632692"
---
# <a name="sysdatabaseprincipals-transact-sql"></a>sys.database_principals(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 각 주체에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스 내에서 고유한 보안 주체의 이름입니다.|  
|**principal_id**|**int**|데이터베이스 내에서 고유한 보안 주체의 ID입니다.|  
|**type**|**char(1)**|보안 주체 유형입니다.<br /><br /> A = 응용 프로그램 역할<br /><br /> C = 인증서로 매핑된 사용자<br /><br /> E = Azure Active Directory에서 외부 사용자<br /><br /> G = Windows 그룹<br /><br /> K = 비대칭 키로 매핑된 사용자<br /><br /> R = 데이터베이스 역할<br /><br /> S = SQL 사용자<br /><br /> U = Windows 사용자<br /><br /> X = Azure Active Directory 그룹 또는 응용 프로그램에서 외부 그룹|  
|**type_desc**|**nvarchar(60)**|보안 주체 유형에 대한 설명입니다.<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|SQL 이름이 스키마를 지정하지 않을 때 사용되는 이름입니다. S, U 또는 A 유형의 보안 주체의 경우 Null입니다.|  
|**create_date**|**datetime**|보안 주체가 생성된 시간입니다.|  
|**modify_date**|**datetime**|보안 주체가 마지막으로 수정된 시간입니다.|  
|**owning_principal_id**|**int**|이 보안 주체를 소유하는 보안 주체의 ID입니다. 데이터베이스 역할을 제외한 모든 보안 주체를 소유 해야 합니다 **dbo**합니다.|  
|**sid**|**varbinary(85)**|보안 주체의 SID(보안 식별자)입니다.  SYS 및 INFORMATION SCHEMAS의 경우 NULL입니다.|  
|**is_fixed_role**|**bit**|1 인 경우이 행은 고정된 데이터베이스 역할 중 하나에 대 한 항목을 나타냅니다: db_owner, db_accessadmin, db_datareader, db_datawriter, db_ddladmin, db_securityadmin, db_backupoperator, db_denydatareader, db_denydatawriter 합니다.|  
|**authentication_type**|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 인증 유형을 나타냅니다. 가능한 값 및 해당 설명을 보려면은 다음과 같습니다.<br /><br /> 0 : 인증 안 함<br />1 : 인스턴스 인증<br />2 : 데이터베이스 인증<br />3 : Windows 인증|  
|**authentication_type_desc**|**nvarchar(60)**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 인증 유형에 대한 설명입니다. 가능한 값 및 해당 설명을 보려면은 다음과 같습니다.<br /><br /> NONE: 인증 안 함<br />인스턴스: 인스턴스 인증<br />데이터베이스: 데이터베이스 인증<br />WINDOWS: Windows 인증|  
|**default_language_name**|**sysname**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 보안 주체의 기본 언어를 나타냅니다.|  
|**default_language_lcid**|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 보안 주체의 기본 LCID를 나타냅니다.|  
|**allow_encrypted_value_modifications**|**bit**|**적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]까지<br /><br /> 대량 복사 작업에서 서버에 대한 암호화 메타데이터 검사를 표시하지 않습니다. 이 통해 데이터를 대량 복사를 사용 하 여 상시 암호화, 테이블 또는 데이터베이스 간에 데이터를 해독 하지 않고 암호화 된 사용자입니다. 기본값은 OFF입니다. |      
  
## <a name="remarks"></a>Remarks  
 합니다 *PasswordLastSetTime* 속성은 SQL Server의 지원 되는 모든 구성에서 사용할 수 있지만 Windows Server 2003 이상 모두 CHECK_POLICY 및 CHECK_ SQL Server를 실행 하는 경우에 다른 속성을 사용할 수 있습니다만 만료를 사용할 수 있습니다. 참조 [암호 정책](../../relational-databases/security/password-policy.md) 자세한 내용은 합니다.  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자는 자신의 사용자 이름, 시스템 사용자 및 고정 데이터베이스 역할을 볼 수 있습니다. 다른 사용자를 보려면 사용자에 대한 ALTER ANY USER 또는 사용 권한이 필요합니다. 사용자 정의 역할을 보려면 ALTER ANY ROLE 또는 역할의 멤버 자격이 필요합니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C: 데이터베이스 보안 주체의 모든 사용 권한 나열  
 다음 쿼리는 데이터베이스 보안 주체에 대해 명시적으로 부여되거나 거부된 사용 권한을 나열합니다.  
  
> [!IMPORTANT]  
>  고정된 데이터베이스 역할의 사용 권한을에 나타나지 않습니다 `sys.database_permissions`합니다. 따라서 데이터베이스 보안 주체가 여기에 나열되지 않은 추가 사용 권한을 가질 수 있습니다.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D: 데이터베이스 내의 스키마 개체에 대 한 사용 권한 나열  
 다음 쿼리는 조인은 `sys.database_principals` 하 고 `sys.database_permissions` 를 `sys.objects` 및 `sys.schemas` 목록 사용 권한에 특정 스키마 개체에 허용 또는 거부 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [포함 된 데이터베이스 사용자-이식 가능한 데이터베이스](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [Azure Active Directory 인증을 사용하여 SQL 데이터베이스에 연결](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  


