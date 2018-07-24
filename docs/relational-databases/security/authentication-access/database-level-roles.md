---
title: 데이터베이스 수준 역할 | Microsoft 문서
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.roleproperties.database.f1
- sql13.swb.roleproperties.object.f1
- SQL13.SWB.DBROLEPROPERTIES.GENERAL.F1
- sql13.swb.roleproperties.general.f1
helpviewer_keywords:
- db_denydatareader role
- users [SQL Server], database roles
- database-level roles [SQL Server]
- db_denydatawriter role
- roles [SQL Server], database
- principals [SQL Server], database-level
- db_backupoperator role
- credentials [SQL Server], roles
- db_accessadmin role
- schemas [SQL Server], roles
- permissions [SQL Server], roles
- database roles [SQL Server], listed
- db_datareader role
- db_ddladmin role
- db_datawriter role
- db_securityadmin role
- db_owner role
- database roles [SQL Server]
- fixed database roles [SQL Server]
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: 7f3fa5f6-6b50-43bb-9047-1544ade55e39
caps.latest.revision: 49
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 252ba405e8ad04b47581fcbbaca89cc7aee1eaf6
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106699"
---
# <a name="database-level-roles"></a>데이터베이스 수준 역할
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  데이터베이스에서 사용 권한을 쉽게 관리하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 다른 보안 주체를 그룹핑하는 보안 주체인 다양한 *역할* 을 제공합니다. 역할은 ***Windows 운영 체제의*** 그룹 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 과 같습니다. 데이터베이스 수준 역할은 데이터베이스 측 사용 권한 범위에 속합니다.  

데이터베이스 역할에 사용자를 추가하고 제거하려면 `ADD MEMBER` ALTER ROLE `DROP MEMBER` 문의 [및](../../../t-sql/statements/alter-role-transact-sql.md) 옵션을 사용합니다. [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] 에서는 이 `ALTER ROLE`사용을 지원하지 않습니다. 대신 기존의 [sp_addrolemember](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 및 [sp_droprolemember](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) 프로시저를 사용합니다.
  
 데이터베이스 수준 역할로는 데이터베이스에 미리 정의된 *고정 데이터베이스 역할* 과 사용자가 만들 수 있는 *사용자 정의 데이터베이스 역할* 의 두 가지 유형이 있습니다.  
  
 고정 데이터베이스 역할은 데이터베이스 수준에서 정의되며 각 데이터베이스에 존재합니다. **db_owner** 데이터베이스 역할의 멤버는 고정 데이터베이스 역할 멤버 자격을 관리할 수 있습니다. msdb 데이터베이스에는 몇 가지 특수한 용도의 데이터베이스 역할도 있습니다.  
  
 데이터베이스 계정과 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 역할을 데이터베이스 수준 역할에 추가할 수 있습니다. 고정 데이터베이스 역할의 각 멤버는 같은 역할에 다른 사용자를 추가할 수 있습니다.  
  
> [!TIP]  
>  사용자 정의 데이터베이스 역할을 고정 역할의 멤버로 추가하지 마세요. 이로 인해 원하지 않는 권한 상승이 설정될 수 있습니다.  

사용자 정의 데이터베이스 역할에 부여된 권한은 GRANT, DENY 및 REVOKE 문을 사용하여 사용자 지정할 수 있습니다. 자세한 내용은 [사용 권한(데이터베이스 엔진)](../../../relational-databases/security/permissions-database-engine.md)을 참조하세요.

모든 사용 권한 목록을 보려면 [데이터베이스 엔진 권한](https://aka.ms/sql-permissions-poster) 포스터를 참조하세요. (서버 수준 사용 권한은 데이터베이스 역할에 부여할 수 없습니다. 로그인 및 기타 서버 수준 보안 주체(예: 서버 역할)는 데이터베이스 역할에 추가할 수 없습니다. [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)]의 서버 수준 보안을 위해서는 대신 [서버 역할](../../../relational-databases/security/authentication-access/server-level-roles.md) 을 사용하세요. 서버 수준 사용 권한은 [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]에서 역할을 통해 부여할 수 없습니다.

## <a name="fixed-database-roles"></a>고정 데이터베이스 역할
  
 다음 표에서는 고정 데이터베이스 역할과 기능을 보여 줍니다. 이러한 역할은 모든 데이터베이스에 있습니다. **공용** 데이터베이스 역할을 제외하고 고정 데이터베이스 역할에 할당된 사용 권한은 변경할 수 없습니다.   
  
|고정 데이터베이스 역할 이름|설명|  
|-------------------------------|-----------------|  
|**db_owner**|**db_owner** 고정 데이터베이스 역할의 멤버는 데이터베이스에서 모든 구성 및 유지 관리 작업을 수행할 수 있고 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)]에서 데이터베이스를 삭제할 수도 있습니다. [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]에서 일부 유지 관리 작업은 서버 수준 권한이 필요하여 **db_owners**으로 수행할 수 없습니다.|  
|**db_securityadmin**|**db_securityadmin** 고정 데이터베이스 역할의 멤버는 역할 멤버 자격을 수정하고 사용 권한을 관리할 수 있습니다. 이 역할에 보안 주체를 추가하면 원하지 않는 권한 상승이 설정될 수 있습니다.|  
|**db_accessadmin**|**db_accessadmin** 고정 데이터베이스 역할의 멤버는 Windows 로그인, Windows 그룹 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인의 데이터베이스에 대한 액세스를 추가하거나 제거할 수 있습니다.|  
|**db_backupoperator**|**db_backupoperator** 고정 데이터베이스 역할의 멤버는 데이터베이스를 백업할 수 있습니다.|  
|**db_ddladmin**|**db_ddladmin** 고정 데이터베이스 역할의 멤버는 데이터베이스에서 모든 DDL(데이터 정의 언어) 명령을 실행할 수 있습니다.|  
|**db_datawriter**|**db_datawriter** 고정 데이터베이스 역할의 멤버는 모든 사용자 테이블에서 데이터를 추가, 삭제 또는 변경할 수 있습니다.|  
|**db_datareader**|**db_datareader** 고정 데이터베이스 역할의 멤버는 모든 사용자 테이블의 모든 데이터를 읽을 수 있습니다.|  
|**db_denydatawriter**|**db_denydatawriter** 고정 데이터베이스 역할의 멤버는 데이터베이스 내의 사용자 테이블에 있는 데이터를 추가, 수정 또는 삭제할 수 없습니다.|  
|**db_denydatareader**|**db_denydatareader** 고정 데이터베이스 역할의 멤버는 데이터베이스 내에 있는 사용자 테이블의 데이터를 읽을 수 없습니다.|  

고정 데이터베이스 역할에 할당된 권한은 변경할 수 없습니다. 다음 그림에서는 고정 데이터베이스 역할에 할당된 사용 권한을 보여 줍니다.

![fixed_database_role_permissions](../../../relational-databases/security/authentication-access/media/permissions-of-database-roles.png)

## <a name="special-roles-for-includesssdsmdincludessssds-mdmd-and-includesssdwmdincludessssdw-mdmd"></a>[!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]의 특수 역할

이러한 데이터베이스 역할은 가상 master 데이터베이스에만 존재합니다. 해당 권한은 master에서 수행된 작업으로 제한됩니다. master에서 데이터베이스 사용자만 이러한 역할에 추가할 수 있습니다. 이 역할에는 로그인을 추가할 수 없습니다. 하지만 로그인을 기반으로 사용자를 만들어 해당 사용자를 역할에 추가할 수는 있습니다. 마스터에서 포함된 데이터베이스 사용자도 역할에 추가할 수 있습니다.

|역할 이름|설명|  
|--------------------|-----------------|
**dbmanager** | 데이터베이스를 만들고 삭제할 수 있습니다. 데이터베이스를 만드는 dbmanager 역할의 멤버는 해당 데이터베이스 소유자가 되어 사용자가 dbo 사용자로 데이터베이스에 연결할 수 있게 합니다. dbo 사용자는 해당 데이터베이스에서 모든 데이터베이스 사용 권한을 가집니다. dbmanager 역할의 멤버는 소유하지 않은 데이터베이스에 액세스할 권한이 반드시 필요하지는 않습니다.
**loginmanager** | 가상 master 데이터베이스에서 로그인을 만들고 삭제할 수 있습니다.  

> [!NOTE]
> 서버 수준 보안 주체 및 Azure Active Directory 관리자(구성된 경우)는 역할 멤버가 아니더라도 [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)] 의 모든 권한이 있습니다. 자세한 내용은 [SQL Database 인증 및 권한 부여: 액세스 부여](https://azure.microsoft.com/documentation/articles/sql-database-manage-logins/)를 참조하세요. 
  
## <a name="msdb-roles"></a>msdb 역할  
 msdb 데이터베이스에는 다음 표에서 보여 주는 특수한 용도의 역할이 포함되어 있습니다.  
  
|msdb 역할 이름|설명|  
|--------------------|-----------------|  
|**db_ssisadmin**<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|이러한 데이터베이스 역할의 멤버는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]를 관리 및 사용할 수 있습니다. 이전 버전에서 업그레이드된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스에는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 대신 DTS(데이터 변환 서비스)를 사용하여 명명된 이전 버전의 역할이 포함될 수 있습니다. 자세한 내용은 [Integration Services 경로&#40;SSIS Service&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md)를 참조하세요.|  
|**dc_admin**<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|이러한 데이터베이스 역할의 멤버는 데이터 수집기를 관리 및 사용할 수 있습니다. 자세한 내용은 [Data Collection](../../../relational-databases/data-collection/data-collection.md)을 참조하세요.|  
|**PolicyAdministratorRole**|**db_ PolicyAdministratorRole** 데이터베이스 역할의 멤버는 정책 기반 관리 정책 및 조건의 모든 구성 및 유지 관리 작업을 수행할 수 있습니다. 자세한 내용은 [정책 기반 관리를 사용하여 서버 관리](../../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)를 참조하세요.|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|이러한 데이터베이스 역할의 멤버는 등록된 서버 그룹을 관리 및 사용할 수 있습니다.|  
|**dbm_monitor**|데이터베이스 미러링 모니터에서 첫 번째 데이터베이스를 등록하면 **msdb** 데이터베이스에서 만들어집니다. **dbm_monitor** 역할은 시스템 관리자가 사용자를 할당할 때까지 멤버를 가지지 않습니다.|  
  
> [!IMPORTANT]  
>  **db_ssisadmin** 및 **dc_admin** 역할의 멤버는 해당 권한을 sysadmin으로 승격할 수 있습니다. 이러한 권한 승격이 발생할 수 있는 것은 이러한 역할이 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지를 수정할 수 있고 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트의 sysadmin 보안 컨텍스트를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 패키지를 실행할 수 있기 때문입니다. 유지 관리 계획, 데이터 컬렉션 집합 및 기타 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지를 실행할 때 이러한 권한 상승이 발생하지 않도록 하려면 패키지를 실행하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 작업이 제한된 권한을 갖는 프록시 계정을 사용하도록 구성하거나 **db_ssisadmin** 및 **dc_admin** 역할에 **sysadmin** 멤버만 추가합니다.  

## <a name="working-with-r-services"></a>R Services 작업  

**적용 대상:** [!INCLUDE[ssSQLv14_md](../../../includes/sssqlv14-md.md)] 이상의 SQL Server   

R Services가 설치된 경우 추가 데이터베이스 역할을 패키지 관리에 사용할 수 있습니다. 자세한 내용은 [SQL Server에 대한 R 패키지 관리](../../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)를 참조하세요.

|역할 이름 |설명|  
|-------------|-----------------|
|**rpkgs-users** |사용자가 rpkgs-shared 역할의 멤버가 설치한 모든 공유 패키지를 사용하도록 허용합니다.|
|**rpkgs-private** |rpkgs-users 역할과 동일한 권한으로 공유 패키지에 액세스할 수 있습니다. 이 역할의 멤버는 비공개로 범위가 지정된 패키지를 설치, 제거 및 사용할 수도 있습니다.|
|**rpkgs-shared** |rpkgs-private 역할과 동일한 권한을 제공합니다. 이 역할의 멤버인 사용자는 공유 패키지를 설치하거나 제거할 수도 있습니다.|
  
## <a name="working-with-database-level-roles"></a>데이터베이스 수준 역할 작업  
 다음 표에서는 데이터베이스 수준 역할 작업을 위한 명령, 뷰 및 함수에 대해 설명합니다.  
  
|기능|형식|설명|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)|메타데이터|고정 데이터베이스 역할의 목록을 반환합니다.|  
|[sp_dbfixedrolepermission&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)|메타데이터|고정 데이터베이스 역할에 대한 사용 권한을 표시합니다.|  
|[sp_helprole&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)|메타데이터|현재 데이터베이스의 역할에 관한 정보를 반환합니다.|  
|[sp_helprolemember&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)|메타데이터|현재 데이터베이스에 있는 역할의 멤버에 관한 정보를 반환합니다.|  
|[sys.database_role_members&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)|메타데이터|각 데이터베이스 역할의 각 멤버에 대해 행을 반환합니다.|  
|[IS_MEMBER&#40;Transact-SQL&#41;](../../../t-sql/functions/is-member-transact-sql.md)|메타데이터|현재 사용자가 지정된 Microsoft Windows 그룹 또는 Microsoft SQL Server 데이터베이스 역할의 멤버인지 여부를 표시합니다.|  
|[CREATE ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-role-transact-sql.md)|Command|현재 데이터베이스에 새 데이터베이스 역할을 만듭니다.|  
|[ALTER ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md)|Command|데이터베이스 역할의 이름 또는 멤버 자격을 변경합니다.|  
|[DROP ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-role-transact-sql.md)|Command|데이터베이스에서 역할을 제거합니다.|  
|[sp_addrole&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)|Command|현재 데이터베이스에 새 데이터베이스 역할을 만듭니다.|  
|[sp_droprole&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)|Command|현재 데이터베이스에서 데이터베이스 역할을 제거합니다.|  
|[sp_addrolemember&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)|Command|현재 데이터베이스의 데이터베이스 역할에 데이터베이스 사용자, 데이터베이스 역할, Windows 로그인 또는 Windows 그룹을 추가합니다. [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] 를 제외한 모든 플랫폼에서 대신 `ALTER ROLE` 을 사용해야 합니다.|  
|[sp_droprolemember&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)|Command|현재 데이터베이스의 SQL Server 역할에서 보안 계정을 제거합니다. [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] 를 제외한 모든 플랫폼에서 대신 `ALTER ROLE` 을 사용해야 합니다.|
|[GRANT](../../../t-sql/statements/grant-transact-sql.md)| Permissions | 역할에 권한을 추가합니다.
|[DENY](../../../t-sql/statements/deny-transact-sql.md)| Permissions | 역할에 대한 권한을 거부합니다.
|[REVOKE](../../../t-sql/statements/revoke-transact-sql.md)| Permissions | 이전에 부여하거나 거부한 사용 권한을 제거합니다.
  
  
## <a name="public-database-role"></a>public 데이터베이스 역할  
 모든 데이터베이스 사용자는 **public** 데이터베이스 역할에 속합니다. 사용자에게 보안 개체에 대한 특정 사용 권한이 부여되지 않았거나 거부된 경우 사용자는 해당 보안 개체에 대해 **public** 으로 부여된 사용 권한을 상속 받습니다. 데이터베이스 사용자는 **공용** 역할에서 제거할 수 없습니다. 
  
## <a name="related-content"></a>관련 내용  
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
 [보안 저장 프로시저&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
 [보안 함수&#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)  
  
 [SQL Server 보안 설정](../../../relational-databases/security/securing-sql-server.md)  
  
 [sp_helprotect&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)  
  
  
