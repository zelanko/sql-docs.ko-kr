---
title: 효과적인 데이터베이스 엔진 사용 권한 결정 | Microsoft 문서
description: 현재 및 이전 사용 권한 시스템을 포함한 SQL Server 데이터베이스 엔진의 다양한 개체에 대한 사용 권한이 있는 사용자를 결정하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 01/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions, effective
- effective permissions
ms.assetid: 273ea09d-60ee-47f5-8828-8bdc7a3c3529
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3852c804ce8ab919072d8a2dbe23b4e0f11b8768
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463134"
---
# <a name="determining-effective-database-engine-permissions"></a>효과적인 데이터베이스 엔진 사용 권한 결정
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 문서에서는 SQL Server 데이터베이스 엔진의 다양한 개체에 대한 사용 권한이 있는 사용자를 결정하는 방법을 설명합니다. SQL Server는 데이터베이스 엔진에 대한 두 개의 사용 권한 시스템을 구현합니다. 고정된 역할의 이전 시스템은 사용 권한이 미리 구성되었습니다. SQL Server 2005부터 보다 유연하고 정확한 시스템을 사용할 수 있습니다. (이 문서의 정보는 SQL Server 2005부터 적용됩니다. SQL Server의 일부 버전에서는 일부 사용 권한 유형을 사용할 수 없습니다.)

> [!IMPORTANT]
>  * 유효 사용 권한은 두 권한 시스템을 집계한 것입니다. 
>  * 사용 권한 거부는 권한 부여를 재정의합니다. 
>  * 사용자가 sysadmin 고정 서버 역할의 멤버인 경우 사용 권한이 더 이상 확인되지 않으므로 거부도 적용되지 않습니다. 
>  * 이전 시스템과 새 시스템에는 유사성이 있습니다. 예를 들어 `sysadmin` 고정 서버 역할의 멤버 자격은 `CONTROL SERVER` 사용 권한이 있는 것과 비슷합니다. 하지만 시스템은 동일하지 않습니다. 예를 들어 로그인에 `CONTROL SERVER` 사용 권한만 있고 저장 프로시저가 `sysadmin` 고정 서버 역할의 멤버 자격을 확인할 경우에는 권한 검사가 실패합니다. 그 반대의 경우도 마찬가지입니다. 


## <a name="summary"></a>요약   
* 고정 서버 역할 또는 사용자 정의 서버 역할의 멤버 자격에서 서버 수준 사용 권한을 가져올 수 있습니다. 모든 사용자는 `public` 고정 서버 역할에 속하며 이 역할에 할당된 사용 권한을 받습니다.   
* 서버 수준 사용 권한은 로그인 또는 사용자 정의 서버 역할에 부여하는 사용 권한에서 가져올 수 있습니다.   
* 데이터베이스 수준 사용 권한은 각 데이터베이스의 고정 데이터베이스 역할 또는 사용자 정의 데이터베이스 역할의 멤버 자격에서 가져올 수 있습니다. 모든 사용자는 `public` 고정 데이터베이스 역할에 속하며 이 역할에 할당된 사용 권한을 받습니다.   
* 데이터베이스 수준 사용 권한은 각 데이터베이스의 사용자 또는 사용자 정의 데이터베이스 역할에 부여하는 사용 권한에서 가져올 수 있습니다.   
* 사용 권한은 `guest` 로그인 또는 `guest` 데이터베이스 사용자로부터 받을 수 있습니다(활성화된 경우). `guest` 로그인 및 사용자는 기본적으로 비활성화되어 있습니다.   
* Windows 사용자는 로그인 권한을 가질 수 있는 Windows 그룹의 멤버가 될 수 있습니다. SQL Server는 Windows 사용자가 연결되고 Windows 그룹의 보안 식별자를 사용하여 Windows 토큰을 제공할 때 Windows 그룹 멤버 자격을 알아냅니다. Windows 그룹 멤버 자격에 대한 자동 업데이트를 받거나 관리하지 않기 때문에 SQL Server는 Windows 그룹 멤버 자격에서 받는 Windows 사용자의 사용 권한을 확실하게 보고할 수 없습니다.   
* 사용 권한은 애플리케이션 역할을 전환하고 암호를 제공하여 획득할 수 있습니다.   
* 사용 권한은 `EXECUTE AS` 절에 나와 있는 저장 프로시저를 실행하여 획득할 수 있습니다.   
* 사용 권한은 `IMPERSONATE` 권한이 있는 로그인 또는 사용자에 의해 획득할 수 있습니다.   
* 로컬 컴퓨터 관리자 그룹의 멤버는 언제든지 해당 권한을 `sysadmin`으로 승격할 수 있습니다. (SQL Database에는 적용되지 않습니다.)  
* `securityadmin` 고정 서버 역할의 멤버는 다양한 해당 권한을 승격할 수 있으며 일부 경우에는 권한을 `sysadmin`으로 승격할 수 있습니다. (SQL Database에는 적용되지 않습니다.)   
* SQL Server 관리자는 모든 로그인 및 사용자에 대한 정보를 볼 수 있습니다. 권한이 충분하지 않은 사용자는 일반적으로 자신의 고유 ID에 대한 정보만 볼 수 있습니다.

## <a name="older-fixed-role-permission-system"></a>이전 고정 역할 사용 권한 시스템

고정 서버 역할과 고정 데이터베이스 역할에는 변경할 수 없는 미리 구성된 사용 권한이 있습니다. 고정 서버 역할의 멤버를 확인하려면 다음 쿼리를 실행합니다.    
> [!NOTE]
>  서버 수준 사용 권한을 사용할 수 없는 SQL Database 또는 Azure Synapse Analytics에는 적용되지 않습니다. `sys.server_principals`의 `is_fixed_role` 열이 SQL Server 2012에 추가되었습니다. 이전 버전의 SQL Server에는 필요하지 않습니다.  
> ```sql
> SELECT SP1.name AS ServerRoleName, 
>  isnull (SP2.name, 'No members') AS LoginName   
>  FROM sys.server_role_members AS SRM
>  RIGHT OUTER JOIN sys.server_principals AS SP1
>    ON SRM.role_principal_id = SP1.principal_id
>  LEFT OUTER JOIN sys.server_principals AS SP2
>    ON SRM.member_principal_id = SP2.principal_id
>  WHERE SP1.is_fixed_role = 1 -- Remove for SQL Server 2008
>  ORDER BY SP1.name;
> ```
> [!NOTE]
>  * 모든 로그인은 public 역할의 멤버이며 제거할 수 없습니다. 
>  * 이 쿼리는 master 데이터베이스의 테이블을 확인하지만 온-프레미스 제품의 모든 데이터베이스에서 실행할 수 있습니다. 

고정 데이터베이스 역할의 멤버를 확인하려면 각 데이터베이스에서 다음 쿼리를 실행합니다.
```sql
SELECT DP1.name AS DatabaseRoleName, 
   isnull (DP2.name, 'No members') AS DatabaseUserName 
 FROM sys.database_role_members AS DRM
 RIGHT OUTER JOIN sys.database_principals AS DP1
   ON DRM.role_principal_id = DP1.principal_id
 LEFT OUTER JOIN sys.database_principals AS DP2
   ON DRM.member_principal_id = DP2.principal_id
 WHERE DP1.is_fixed_role = 1
 ORDER BY DP1.name;
```
각 역할에 부여된 사용 권한을 이해하려면 온라인 설명서에 있는 그림에서 역할 설명을 참조하세요([서버 수준 역할](../../../relational-databases/security/authentication-access/server-level-roles.md) 및 [데이터베이스 수준 역할](../../../relational-databases/security/authentication-access/database-level-roles.md)).

## <a name="newer-granular-permission-system"></a>세분화된 최신 사용 권한 시스템

이 시스템은 유연하여 정확하게 설정하려고 하면 복잡해질 수 있습니다. 문제를 단순화하려면 역할을 만들고 역할에 사용 권한을 할당한 다음 역할에 사용자 그룹을 추가하는 것이 좋습니다. 또한 데이터베이스 개발 팀에서 스키마로 작업을 구분한 후 개별 테이블이나 프로시저 대신 전체 스키마에 역할 사용 권한을 부여하는 경우에는 더 용이합니다. 실제 시나리오는 복잡하며 비즈니스 요구 사항은 예기치 않은 보안 요구 사항을 만들 수 있습니다.   

[!INCLUDE[database-engine-permissions](../../../includes/paragraph-content/database-engine-permissions.md)]


### <a name="security-classes"></a>보안 클래스

서버 수준, 데이터베이스 수준, 스키마 수준 또는 개체 수준 등에서 사용 권한을 부여할 수 있습니다. 26개의 수준이 있습니다(클래스라고 함). 클래스의 전체 목록은 `APPLICATION ROLE`, `ASSEMBLY`, `ASYMMETRIC KEY`, `AVAILABILITY GROUP`, `CERTIFICATE`, `CONTRACT`, `DATABASE`, `DATABASE` `SCOPED CREDENTIAL`, `ENDPOINT`, `FULLTEXT CATALOG`, `FULLTEXT STOPLIST`, `LOGIN`, `MESSAGE TYPE`, `OBJECT`, `REMOTE SERVICE BINDING`, `ROLE`, `ROUTE`, `SCHEMA`, `SEARCH PROPERTY LIST`, `SERVER`, `SERVER ROLE`, `SERVICE`, `SYMMETRIC KEY`, `TYPE`, `USER`, `XML SCHEMA COLLECTION`입니다(알파벳순). (일부 클래스는 일부 유형의 SQL Server에서 사용할 수 없습니다.) 각 클래스에 대한 전체 정보를 제공하려면 다른 쿼리가 필요합니다.

### <a name="principals"></a>Principals

사용 권한은 보안 주체에 부여됩니다. 서버 역할, 로그인, 데이터베이스 역할 또는 사용자가 보안 주체가 될 수 있습니다. 로그인은 많은 Windows 사용자를 포함하는 Windows 그룹을 나타낼 수 있습니다. Windows 그룹은 SQL Server에서 유지 관리하지 않으므로 SQL Server에서 항상 Windows 그룹 멤버를 알 수는 없습니다. Windows 사용자가 SQL Server에 연결하는 경우 로그인 패킷에 사용자에 대한 Windows 그룹 멤버 자격 토큰이 포함됩니다.

Windows 사용자가 Windows 그룹을 기반으로 한 로그인을 사용하여 연결하는 경우, 개별 Windows 사용자를 나타내는 사용자 또는 로그인을 만드는 데 SQL Server가 필요한 작업이 있을 수 있습니다. 예를 들어 Windows 그룹(엔지니어)에 사용자(Mary, Todd, Pat)가 포함되고 엔지니어 그룹에 데이터베이스 사용자 계정이 있습니다. Mary가 사용 권한이 있고 테이블을 만드는 경우 사용자(Mary)를 테이블의 소유자로 만들 수 있습니다. 또는 Todd의 나머지 엔지니어 그룹 사용 권한이 거부되는 경우 사용자 Todd가 사용 권한 거부를 추적하도록 만들어야 합니다.

Windows 사용자(예: 엔지니어 및 관리자)는 둘 이상의 Windows 그룹의 멤버일 수 있습니다. 엔지니어 로그인에 부여되거나 거부된 사용 권한, 관리자 로그인에 부여되거나 거부된 사용 권한, 사용자에게 개별적으로 부여되거나 거부된 사용 권한 및 사용자가 멤버인 역할에 부여되거나 거부된 사용 권한은 유효 사용 권한에 대해 집계되고 평가됩니다. `HAS_PERMS_BY_NAME` 함수는 사용자 또는 로그인에 특정 사용 권한이 있는지 여부를 나타낼 수 있습니다. 그러나 사용 권한 부여 또는 사용 권한 거부의 원본을 확인하는 명확한 방법은 없습니다. 사용 권한 목록을 학습하고 시행착오를 거쳐야 합니다.

## <a name="useful-queries"></a>유용한 쿼리

### <a name="server-permissions"></a>서버 권한

다음 쿼리는 서버 수준에서 부여되거나 거부된 사용 권한 목록을 반환합니다. 이 쿼리는 master 데이터베이스에서 실행해야 합니다.   
> [!NOTE]
>  서버 수준 사용 권한은 SQL Database 또는 Azure Synapse Analytics에서 부여하거나 쿼리할 수 없습니다.   
> ```sql
> SELECT pr.type_desc, pr.name, 
>  isnull (pe.state_desc, 'No permission statements') AS state_desc, 
>  isnull (pe.permission_name, 'No permission statements') AS permission_name 
>  FROM sys.server_principals AS pr
>  LEFT OUTER JOIN sys.server_permissions AS pe
>    ON pr.principal_id = pe.grantee_principal_id
>  WHERE is_fixed_role = 0 -- Remove for SQL Server 2008
>  ORDER BY pr.name, type_desc;
> ```

### <a name="database-permissions"></a>데이터베이스 권한

다음 쿼리는 데이터베이스 수준에서 부여되거나 거부된 권한 목록을 반환합니다. 이 쿼리는 각 데이터베이스에서 실행해야 합니다.   
```sql
SELECT pr.type_desc, pr.name, 
 isnull (pe.state_desc, 'No permission statements') AS state_desc, 
 isnull (pe.permission_name, 'No permission statements') AS permission_name 
FROM sys.database_principals AS pr
LEFT OUTER JOIN sys.database_permissions AS pe
    ON pr.principal_id = pe.grantee_principal_id
WHERE pr.is_fixed_role = 0 
ORDER BY pr.name, type_desc;
```

사용 권한 테이블의 각 클래스를 보안 개체의 해당 클래스에 대한 관련 정보를 제공하는 다른 시스템 뷰에 조인할 수 있습니다. 예를 들어 다음 쿼리는 사용 권한의 영향을 받는 데이터베이스 개체의 이름을 제공합니다.    
```sql
SELECT pr.type_desc, pr.name, pe.state_desc, 
 pe.permission_name, s.name + '.' + oj.name AS Object, major_id
 FROM sys.database_principals AS pr
 JOIN sys.database_permissions AS pe
   ON pr.principal_id = pe.grantee_principal_id
 JOIN sys.objects AS oj
   ON oj.object_id = pe.major_id
 JOIN sys.schemas AS s
   ON oj.schema_id = s.schema_id
 WHERE class_desc = 'OBJECT_OR_COLUMN';
```
`HAS_PERMS_BY_NAME` 함수를 사용하여 특정 사용자(이 경우 `TestUser`)에게 사용 권한이 있는지 확인합니다. 예를 들면 다음과 같습니다.   
```sql
EXECUTE AS USER = 'TestUser';
SELECT HAS_PERMS_BY_NAME ('dbo.T1', 'OBJECT', 'SELECT');
REVERT;
```
구문에 대한 자세한 내용은 [HAS_PERMS_BY_NAME](../../../t-sql/functions/has-perms-by-name-transact-sql.md)을 참조하세요.

## <a name="see-also"></a>참고 항목:

[데이터베이스 엔진 권한 시작](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)    
[자습서: 데이터베이스 엔진 시작](../../../relational-databases/tutorial-getting-started-with-the-database-engine.md) 

