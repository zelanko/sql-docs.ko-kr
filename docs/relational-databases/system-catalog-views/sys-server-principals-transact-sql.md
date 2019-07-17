---
title: sys.server_principals (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_principals
- sys.server_principals_TSQL
- sys.server_principals
- server_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_principals catalog view
ms.assetid: c5dbe0d8-a1c8-4dc4-b9b1-22af20effd37
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 408ad309ade858c800b79ee83993fda4fe78467a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133094"
---
# <a name="sysserverprincipals-transact-sql"></a>sys.server_principals(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  각 서버 수준 보안 주체에 대한 행이 포함되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|보안 주체의 이름입니다. 서버 내에서 고유합니다.|  
|**principal_id**|**int**|보안 주체의 ID 번호입니다. 서버 내에서 고유합니다.|  
|**sid**|**varbinary(85)**|보안 주체의 SID(보안 ID)입니다. Windows 보안 주체의 경우 Windows SID와 일치합니다.|  
|**type**|**char(1)**|보안 주체 유형입니다.<br /><br /> S = SQL 로그인<br /><br /> U = Windows 로그인<br /><br /> G = Windows 그룹<br /><br /> R = 서버 역할<br /><br /> C = 인증서에 매핑된 로그인<br /><br /> K = 비대칭 키에 매핑된 로그인|  
|**type_desc**|**nvarchar(60)**|보안 주체 유형에 대한 설명입니다.<br /><br /> SQL_LOGIN<br /><br /> WINDOWS_LOGIN<br /><br /> WINDOWS_GROUP<br /><br /> SERVER_ROLE<br /><br /> CERTIFICATE_MAPPED_LOGIN<br /><br /> ASYMMETRIC_KEY_MAPPED_LOGIN|  
|**is_disabled**|**int**|1 = 로그인을 사용할 수 없습니다.|  
|**create_date**|**datetime**|보안 주체가 생성된 시간입니다.|  
|**modify_date**|**datetime**|보안 주체 정의가 마지막으로 수정된 시간입니다.|  
|**default_database_name**|**sysname**|이 보안 주체에 대한 기본 데이터베이스입니다.|  
|**default_language_name**|**sysname**|이 보안 주체에 대한 기본 언어입니다.|  
|**credential_id**|**int**|이 보안 주체와 연결된 자격 증명의 ID입니다. 이 보안 주체와 연결된 자격 증명이 없는 경우 credential_id는 NULL이 됩니다.|  
|**owning_principal_id**|**int**|합니다 **principal_id** 서버 역할의 소유자입니다. 보안 주체가 서버 역할이 아닌 경우 NULL입니다.|  
|**is_fixed_role**|**bit**|보안 주체가 고정된 사용 권한 가진 기본 제공 서버 역할 중 하나 이면 1을 반환 합니다. 자세한 내용은 [서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md)을 참조하세요.|  
  
## <a name="permissions"></a>사용 권한  
 모든 로그인은 자신의 로그인 이름, 시스템 로그인 및 고정 서버 역할을 볼 수 있습니다. 다른 로그인을 보려면 로그인할 때 ALTER ANY LOGIN 또는 사용 권한이 필요합니다. 사용자 정의 서버 역할을 보려면 ANY SERVER ROLE 또는 역할의 멤버 자격이 필요합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 쿼리는 서버 보안 주체에 대해 명시적으로 부여되거나 거부된 사용 권한을 나열합니다.  
  
> [!IMPORTANT]  
>  (Public)이 아닌 고정된 서버 역할의 사용 권한을 sys.server_permissions에 나타나지 않습니다. 따라서 서버 보안 주체가 여기에 나열되지 않은 추가 사용 권한을 가질 수 있습니다.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pe.state_desc, pe.permission_name   
FROM sys.server_principals AS pr   
JOIN sys.server_permissions AS pe   
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
## <a name="see-also"></a>관련 항목  
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
  
  
