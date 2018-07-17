---
title: 서버 수준 역할 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.Security.NT_AUTHORITY.SYSTEM
- sql13.Security.BUILTIN.administrators
helpviewer_keywords:
- roles [SQL Server], server-level
- principals [SQL Server], server-level
- CONTROL SERVER permission
- fixed server roles [SQL Server]
- credentials [SQL Server], roles
- sysadmin fixed server role
- server-level roles [SQL Server]
- authentication [SQL Server], roles
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
caps.latest.revision: 52
author: CarlRabeler
ms.author: carlraba
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b8e51950aace311b2e4a1a1bbc9e4591e87a9cb2
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36942569"
---
# <a name="server-level-roles"></a>서버 수준 역할
[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md](../../../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 서버에 대한 사용 권한을 쉽게 관리할 수 있도록 서버 수준 역할을 제공합니다. 서버 역할은 다른 보안 주체를 그룹화하는 보안 주체입니다. 서버 수준 역할은 서버 측 사용 권한 범위에 속합니다. *역할* 은 Windows 운영 체제의 *그룹* 과 같습니다.  
  
 고정 서버 역할은 편리성 및 이전 버전과의 호환성을 위해 제공됩니다. 가능하면 보다 구체적인 사용 권한을 할당하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 제공하는 고정 서버 역할은 9개입니다. 고정 서버 역할(**공용** 제외)에 부여된 사용 권한은 변경할 수 없습니다. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터는 사용자 정의 서버 역할을 만들어 여기에 서버 수준 사용 권한을 추가할 수 있습니다.  
  
 서버 수준 보안 주체([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인, Windows 계정 및 Windows 그룹)를 서버 수준 역할에 추가할 수 있습니다. 고정 서버 역할의 각 멤버는 같은 역할에 다른 로그인을 추가할 수 있습니다. 사용자 정의 서버 역할의 멤버는 이 역할에 다른 서버 보안 주체를 추가할 수 없습니다.  
>  [!NOTE]
>  SQL Database 또는 SQL Data Warehouse에서는 서버 수준 사용 권한을 사용할 수 없습니다. SQL Database에 대한 자세한 내용은 [데이터베이스 액세스 제어 및 권한 부여](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)를 참조하세요.
  
## <a name="fixed-server-level-roles"></a>고정 서버 수준 역할  
 다음 표에서는 고정 서버 수준 역할과 해당 기능을 보여 줍니다.  
  
|고정 서버 수준 역할|설명|  
|------------------------------|-----------------|  
|**sysadmin**|**sysadmin** 고정 서버 역할의 멤버는 서버에서 모든 작업을 수행할 수 있습니다.|  
|**serveradmin**|**serveradmin** 고정 서버 역할의 멤버는 서버 차원의 구성 옵션을 변경하고 서버를 종료할 수 있습니다.|  
|**securityadmin**|**securityadmin** 고정 서버 역할의 멤버는 로그인 및 해당 속성을 관리합니다. 서버 수준 사용 권한을 `GRANT`, `DENY` 및 `REVOKE`할 수 있습니다. 데이터베이스에 액세스할 수 있는 데이터베이스 수준 사용 권한도 `GRANT`, `DENY` 및 `REVOKE`할 수 있습니다. 또한 이 역할의 멤버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로그인 암호를 다시 설정할 수 있습니다.<br /><br /> **중요:** 보안 관리자는 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에 대한 액세스 권한을 부여하고 사용자 권한을 구성할 수 있으므로 대부분의 서버 사용 권한을 할당할 수 있습니다. **securityadmin** 역할은 **sysadmin** 역할과 동일하게 처리되어야 합니다.|  
|**processadmin**|**processadmin** 고정 서버 역할의 멤버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스에서 실행 중인 프로세스를 종료할 수 있습니다.|  
|**setupadmin**|**setupadmin** 고정 서버 역할의 멤버는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용하여 연결된 서버를 추가하거나 제거할 수 있습니다. ([!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]를 사용할 때 **sysadmin** 멤버 자격이 필요합니다.)|  
|**bulkadmin**|**bulkadmin** 고정 서버 역할의 멤버는 `BULK INSERT` 문을 실행할 수 있습니다.|  
|**diskadmin**|**diskadmin** 고정 서버 역할은 디스크 파일을 관리하는 데 사용됩니다.|  
|**dbcreator**|**dbcreator** 고정 서버 역할의 멤버는 데이터베이스를 생성, 변경, 삭제, 복원할 수 있습니다.|  
|**public**|모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인은 **public** 서버 역할에 속합니다. 서버 보안 주체에게 보안 개체에 대한 특정 사용 권한이 부여되지 않았거나 거부된 경우 사용자는 해당 개체에 대해 public으로 부여된 사용 권한을 상속 받습니다. 모든 사용자가 개체를 사용할 수 있도록 하려는 경우에만 개체에 public 권한을 할당해야 합니다. public의 멤버 자격은 변경할 수 없습니다.<br /><br /> **참고:** **public**은 다른 역할과 다른 방식으로 구현되며 public 고정 서버 역할에서 사용 권한이 부여, 거부 또는 취소될 수 있습니다.|  
  
## <a name="permissions-of-fixed-server-roles"></a>고정 서버 역할에 대한 사용 권한  
 각 고정 서버 역할에는 관련된 특정 사용 권한이 있습니다. 다음 그림에서는 서버 역할에 할당된 사용 권한을 보여 줍니다.   
![fixed_server_role_permissions](../../../relational-databases/security/authentication-access/media/permissions-of-server-roles.png)   
  
> [!IMPORTANT]  
>  **CONTROL SERVER** 권한은 **sysadmin** 고정 서버 역할과 유사하지만 동일하지는 않습니다. 권한이 역할 멤버 자격을 의미하지 않으며 역할 멤버 자격이 있다고 해서 사용 권한이 부여되는 것도 아닙니다. 예를 들어 **CONTROL SERVER**가 **sysadmin** 고정 서버 역할의 멤버 자격을 의미하지는 않습니다. 그러나 때로 역할과 해당 권한 간에 가장하는 것이 가능할 수 있습니다. 대부분의 **DBCC** 명령 및 많은 시스템 절차를 수행하려면 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다. **sysadmin** 멤버 자격이 필요한 171개의 시스템 저장 프로시저 목록의 경우 Andreas Wolter가 작성한 [CONTROL SERVER vs. sysadmin/sa: permissions, system procedures, DBCC, automatic schema creation and privilege escalation - caveats](http://www.insidesql.org/blogs/andreaswolter/2013/08/control-server-vs-sysadmin-sa-permissions-privilege-escalation-caveats)(제어 서버 및 sysadmin/sa: 사용 권한, 시스템 프로시저, DBCC, 자동 스키마 생성 및 권한 에스컬레이션 - 주의할 사항) 블로그 게시물을 참조하세요.  
  
## <a name="server-level-permissions"></a>서버 수준 사용 권한  
 사용자 정의 서버 역할에는 서버 수준 사용 권한만 추가할 수 있습니다. 서버 수준 사용 권한을 나열하려면 다음 문을 실행하세요. 서버 수준 사용 권한은 다음과 같습니다.  
  
```  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 사용 권한에 대한 자세한 내용은 [사용 권한&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/permissions-database-engine.md) 및 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)를 참조하세요.  
  
## <a name="working-with-server-level-roles"></a>서버 수준 역할 작업  
 다음 표에서는 서버 수준 역할을 통해 사용할 수 있는 명령, 뷰 및 함수를 보여 줍니다.  
  
|기능|형식|설명|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)|메타데이터|서버 수준 역할의 목록을 반환합니다.|  
|[sp_helpsrvrolemember&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)|메타데이터|서버 수준 역할의 멤버에 대한 정보를 반환합니다.|  
|[sp_srvrolepermission&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)|메타데이터|서버 수준 역할의 사용 권한을 표시합니다.|  
|[IS_SRVROLEMEMBER&#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|메타데이터|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인이 지정된 서버 수준 역할의 멤버인지 여부를 나타냅니다.|  
|[sys.server_role_members&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)|메타데이터|각 서버 수준 역할의 각 멤버에 대해 행을 반환합니다.|  
|[sp_addsrvrolemember&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)|Command|서버 수준 역할의 멤버로서 로그인을 추가합니다. 사용되지 않습니다. 대신 [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md) 을 사용하세요.|  
|[sp_dropsrvrolemember&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)|Command|서버 수준 역할에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인이나 Windows 사용자 또는 그룹을 제거합니다. 사용되지 않습니다. 대신 [ALTER SERVER ROLE](../../../t-sql/statements/alter-server-role-transact-sql.md) 을 사용하세요.|  
|[CREATE SERVER ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-role-transact-sql.md)|Command|사용자 정의 서버 역할을 만듭니다.|  
|[ALTER SERVER ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md)|Command|서버 역할의 멤버 자격을 변경하거나 사용자 정의 서버 역할의 이름을 변경합니다.|  
|[DROP SERVER ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-role-transact-sql.md)|Command|사용자 정의 서버 역할을 제거합니다.|  
|[IS_SRVROLEMEMBER&#40;Transact-SQL&#41;](../../../t-sql/functions/is-srvrolemember-transact-sql.md)|함수|서버 역할의 멤버 자격을 결정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 수준 역할](../../../relational-databases/security/authentication-access/database-level-roles.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)   
 [SQL Server 보안 설정](../../../relational-databases/security/securing-sql-server.md)   
 [GRANT 서버 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [REVOKE 서버 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [DENY 서버 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [서버 역할 만들기](../../../relational-databases/security/authentication-access/create-a-server-role.md)  
  
  
