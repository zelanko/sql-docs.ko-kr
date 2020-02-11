---
title: sys. server_role_members (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_role_members
- sys.server_role_members_TSQL
- server_role_members_TSQL
- sys.server_role_members
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_role_members catalog view
ms.assetid: efa20414-2c6b-45a2-a7a9-60110a24da18
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11f39b29817716799ec693d6161135010c35a233
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68133032"
---
# <a name="sysserver_role_members-transact-sql"></a>sys.server_role_members(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  각 고정 및 사용자 정의 서버 역할의 각 멤버에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**role_principal_id**|**int**|역할의 서버 보안 주체 ID입니다.|  
|**member_principal_id**|**int**|멤버의 서버 보안 주체 ID입니다.|  
  
 서버 역할 멤버 자격을 추가 하거나 제거 하려면 [ALTER SERVER role &#40;transact-sql&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)문으로 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 로그인은 자체 서버 역할 멤버 자격을 볼 수 있으며 고정 서버 역할의 멤버 principal_id를 볼 수 있습니다. 모든 서버 역할 멤버 자격을 보려면 **서버 역할에 대 한 VIEW DEFINITION** 권한 또는 **securityadmin** 고정 서버 역할의 멤버 자격이 필요 합니다.  
  
 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 역할 및 해당 멤버의 이름과 ID를 반환합니다.  
  
```  
SELECT sys.server_role_members.role_principal_id, role.name AS RoleName,   
    sys.server_role_members.member_principal_id, member.name AS MemberName  
FROM sys.server_role_members  
JOIN sys.server_principals AS role  
    ON sys.server_role_members.role_principal_id = role.principal_id  
JOIN sys.server_principals AS member  
    ON sys.server_role_members.member_principal_id = member.principal_id;  
```  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 카탈로그 뷰](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
