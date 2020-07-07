---
title: sys. database_role_members (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_role_members_TSQL
- sys.database_role_members
- database_role_members_TSQL
- database_role_members
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_role_members catalog view
ms.assetid: ed1b019d-ca48-4db3-85df-cf6d2db591cf
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9669462c83252af8c4526ddda0f155cdcb6b8a92
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011984"
---
# <a name="sysdatabase_role_members-transact-sql"></a>sys.database_role_members(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  각 데이터베이스 역할의 각 멤버에 대해 행을 반환합니다.  데이터베이스 사용자, 응용 프로그램 역할 및 기타 데이터베이스 역할은 데이터베이스 역할의 멤버일 수 있습니다. 역할에 멤버를 추가 하려면 [ALTER role](../../t-sql/statements/alter-role-transact-sql.md) 문을 옵션과 함께 사용 `ADD MEMBER` 합니다. 값의 이름을 반환 하려면 [database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) 와 조인 `principal_id` 합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**role_principal_id**|**int**|역할의 데이터베이스 보안 주체 ID입니다.|  
|**member_principal_id**|**int**|멤버의 데이터베이스 보안 주체 ID입니다.|  
  
## <a name="permissions"></a>권한  
 모든 사용자는 자신의 역할 멤버 자격을 볼 수 있습니다. 다른 역할 멤버 자격을 보려면 `db_securityadmin` 고정 데이터베이스 역할 또는 데이터베이스의 멤버 자격이 필요 합니다 `VIEW DEFINITION` .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 쿼리는 데이터베이스 역할의 멤버를 반환 합니다.  
  
```  
SELECT DP1.name AS DatabaseRoleName,   
   isnull (DP2.name, 'No members') AS DatabaseUserName   
 FROM sys.database_role_members AS DRM  
 RIGHT OUTER JOIN sys.database_principals AS DP1  
   ON DRM.role_principal_id = DP1.principal_id  
 LEFT OUTER JOIN sys.database_principals AS DP2  
   ON DRM.member_principal_id = DP2.principal_id  
WHERE DP1.type = 'R'
ORDER BY DP1.name;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 카탈로그 뷰](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
[ALTER ROLE (Transact-sql-SQLL)](../../t-sql/statements/alter-role-transact-sql.md)      
[sys.server_role_members(Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
  


