---
description: sys.database_principals(Transact-SQL)
title: sys.database_principals (Transact-sql) | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cf190b2c0a973db9e2955cd928e1b716d847d26b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467024"
---
# <a name="sysdatabase_principals-transact-sql"></a>sys.database_principals(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 각 주체에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스 내에서 고유한 보안 주체의 이름입니다.|  
|**principal_id**|**int**|데이터베이스 내에서 고유한 보안 주체의 ID입니다.|  
|**type**|**char(1)**|보안 주체 유형입니다.<br /><br /> A = 애플리케이션 역할<br /><br /> C = 인증서로 매핑된 사용자<br /><br /> E = Azure Active Directory의 외부 사용자<br /><br /> G = Windows 그룹<br /><br /> K = 비대칭 키로 매핑된 사용자<br /><br /> R = 데이터베이스 역할<br /><br /> S = SQL 사용자<br /><br /> U = Windows 사용자<br /><br /> X = Azure Active Directory 그룹 또는 응용 프로그램의 외부 그룹|  
|**type_desc**|**nvarchar(60)**|보안 주체 유형에 대한 설명입니다.<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|SQL 이름이 스키마를 지정하지 않을 때 사용되는 이름입니다. S, U 또는 A 유형의 보안 주체의 경우 Null입니다.|  
|**create_date**|**datetime**|보안 주체가 생성된 시간입니다.|  
|**modify_date**|**datetime**|보안 주체가 마지막으로 수정된 시간입니다.|  
|**owning_principal_id**|**int**|이 보안 주체를 소유하는 보안 주체의 ID입니다. 기본적으로 모든 고정 데이터베이스 역할은 **dbo** 가 소유 합니다.|  
|**s**|**varbinary(85)**|보안 주체의 SID(보안 식별자)입니다.  SYS 및 INFORMATION SCHEMAS의 경우 NULL입니다.|  
|**is_fixed_role**|**bit**|1 인 경우이 행은 고정 데이터베이스 역할 중 하나의 항목 (db_owner, db_accessadmin, db_datareader, db_datawriter, db_ddladmin, db_securityadmin, db_backupoperator, db_denydatareader, db_denydatawriter에 대 한 항목을 나타냅니다.|  
|**authentication_type**|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 인증 유형을 나타냅니다. 다음은 가능한 값과 그에 대 한 설명입니다.<br /><br /> 0: 인증 안 함<br />1: 인스턴스 인증<br />2: 데이터베이스 인증<br />3: Windows 인증<br />4: Azure Active Directory 인증|  
|**authentication_type_desc**|**nvarchar(60)**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 인증 유형에 대한 설명입니다. 다음은 가능한 값과 그에 대 한 설명입니다.<br /><br /> 없음: 인증 안 함<br />인스턴스: 인스턴스 인증<br />데이터베이스: 데이터베이스 인증<br />WINDOWS: Windows 인증<br />외부: Azure Active Directory 인증|  
|**default_language_name**|**sysname**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 이 보안 주체의 기본 언어를 나타냅니다.|  
|**default_language_lcid**|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 이 보안 주체의 기본 LCID를 나타냅니다.|  
|**allow_encrypted_value_modifications**|**bit**|**적용 대상**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 이상, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> 대량 복사 작업에서 서버에 대한 암호화 메타데이터 검사를 표시하지 않습니다. 이를 통해 사용자는 데이터의 암호를 해독 하지 않고 테이블 또는 데이터베이스 간에 Always Encrypted를 사용 하 여 암호화 된 데이터를 대량 복사할 수 있습니다. 기본값은 OFF입니다. |      
  
## <a name="remarks"></a>설명  
 *PasswordLastSetTime* 속성은 지원 되는 모든 SQL Server 구성에서 사용할 수 있지만 다른 속성은 SQL Server Windows Server 2003 이상에서 실행 중이 고 CHECK_POLICY와 CHECK_EXPIRATION 모두 사용 하도록 설정 된 경우에만 사용할 수 있습니다. 자세한 내용은 [암호 정책](../../relational-databases/security/password-policy.md) 을 참조 하세요.
Principal_id의 값은 보안 주체가 삭제 된 경우 다시 사용 될 수 있으므로 계속 해 서 늘어난 것이 보장 되지 않습니다.
  
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C: 데이터베이스 보안 주체의 모든 사용 권한 나열  
 다음 쿼리는 데이터베이스 보안 주체에 대해 명시적으로 부여되거나 거부된 사용 권한을 나열합니다.  
  
> [!IMPORTANT]  
>  고정 데이터베이스 역할의 사용 권한은에 표시 되지 않습니다 `sys.database_permissions` . 따라서 데이터베이스 보안 주체가 여기에 나열되지 않은 추가 사용 권한을 가질 수 있습니다.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D: 데이터베이스 내의 스키마 개체에 대 한 사용 권한 나열  
 다음 쿼리는 및에 조인 하 고 `sys.database_principals` `sys.database_permissions` `sys.objects` `sys.schemas` 특정 스키마 개체에 부여 되거나 거부 된 사용 권한을 나열 합니다.  
  
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
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [포함 된 데이터베이스 사용자-데이터베이스를 이식 가능 하 게 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [Azure Active Directory 인증을 사용하여 SQL Database에 연결](/azure/azure-sql/database/authentication-aad-overview)  
  
