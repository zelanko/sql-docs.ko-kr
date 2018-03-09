---
title: "보안 주체(데이터베이스 엔진) | Microsoft 문서"
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.roleproperties.selectroll.f1
- sql13.swb.databaseuser.permissions.user.f1--May use common.permissions
helpviewer_keywords:
- certificates [SQL Server], principals
- roles [SQL Server], principals
- permissions [SQL Server], principals
- '##MS_SQLAuthenticatorCertificate##'
- principals [SQL Server]
- '##MS_SQLResourceSigningCertificate##'
- groups [SQL Server], principals
- '##MS_AgentSigningCertificate##'
- authentication [SQL Server], principals
- schemas [SQL Server], principals
- principals [SQL Server], about principals
- security [SQL Server], principals
- users [SQL Server], principals
- '##MS_SQLReplicationSigningCertificate##'
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ab67ccf5240ad3797bf744b56e615a92fa95d9bd
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="principals-database-engine"></a>보안 주체(데이터베이스 엔진)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  *보안 주체* 는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스를 요청할 수 있는 엔터티입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 권한 부여 모델의 다른 구성 요소와 같이 보안 주체는 계층으로 정렬될 수 있습니다. 보안 주체의 영향 범위는 보안 주체의 정의 범위인 Windows, 서버 및 데이터베이스와 보안 주체가 분해 불가능하거나 컬렉션인지 여부에 따라 달라집니다. 분해 불가능한 보안 주체의 예로는 Windows 로그인을 들 수 있으며 Windows 그룹은 컬렉션인 보안 주체입니다. 모든 보안 주체에는 SID(보안 식별자)가 있습니다. 이 항목은 모든 버전의 SQL Server에 적용되지만 SQL Database 또는 SQL Data Warehouse의 서버 수준 보안 주체에는 몇 가지 제한 사항이 있습니다. 
  
## <a name="sql-server-level-principals"></a>SQL Server 수준의 보안 주체  
  
-  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 로그인   
-  Windows 사용자에 대한 Windows 인증 로그인  
-  Windows 그룹에 대한 Windows 인증 로그인   
-  AD 사용자에 대한 Azure Active Directory 인증 로그인
-  AD 그룹에 대한 Azure Active Directory 인증 로그인
-  서버 역할  
  
 ## <a name="database-level-principals"></a>데이터베이스 수준의 보안 주체  
  
-   데이터베이스 사용자(사용자 유형은 11가지입니다. 자세한 내용은 [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.) 
-   데이터베이스 역할  
-   응용 프로그램 역할  
  
## <a name="sa-login"></a>sa 로그인  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `sa` 로그인은 서버 수준의 보안 주체로서, 인스턴스를 설치하면 기본적으로 생성됩니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터는 sa의 기본 데이터베이스가 master입니다. 이 동작은 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 변경되었습니다. `sa` 로그인은 `sysadmin` 고정 데이터베이스 역할의 멤버입니다. `sa` 로그인에는 서버에 대한 모든 권한이 부여되며 제한할 수 없습니다. `sa` 로그인은 삭제할 수 없지만 아무도 사용할 수 없도록 해제할 수는 있습니다.

## <a name="dbo-user-and-dbo-schema"></a>dbo 사용자 및 dbo 스키마

`dbo` 사용자는 각 데이터베이스에서 특수한 사용자 계정입니다. 모든 SQL Server 관리자, `sysadmin` 고정 서버 역할의 멤버, `sa` 로그인 및 데이터베이스의 소유자는 데이터베이스를 `dbo` 사용자로 시작합니다. `dbo` 사용자에게는 데이터베이스에 대한 모든 권한이 부여되며 제한하거나 삭제할 수 없습니다. `dbo`는 데이터베이스 소유자를 나타내지만 `dbo` 사용자 계정은 `db_owner` 고정 데이터베이스 역할과 동일하지 않고 `db_owner` 고정 데이터베이스 역할은 데이터베이스 소유자로 기록되는 사용자 계정과 동일하지 않습니다.     
`dbo` 사용자는 `dbo` 스키마를 소유합니다. `dbo` 스키마는 일부 다른 스키마를 지정하지 않는 한 모든 사용자에 대한 기본 스키마입니다.  `dbo` 스키마는 삭제할 수 없습니다.
  
## <a name="public-server-role-and-database-role"></a>public 서버 역할 및 데이터베이스 역할  
모든 로그인은 `public` 고정 서버 역할에 속하고 모든 데이터베이스 사용자는 `public` 데이터베이스 역할에 속합니다. 로그인이나 사용자에게 보안 개체에 대한 특정 사용 권한이 부여되지 않았거나 거부된 경우 로그인이나 사용자는 해당 보안 개체에 대해 public으로 부여된 사용 권한을 상속받습니다. `public` 고정 서버 역할 및 `public` 고정 데이터베이스 역할은 삭제할 수 없습니다. 그러나 `public` 역할로부터 사용 권한을 취소할 수 있습니다. 기본적으로 `public` 역할에 할당되는 사용 권한은 많습니다. 대부분의 이러한 사용 권한은 모든 사용자가 수행할 수 있어야 하는 작업의 유형인 데이터베이스의 일상적인 작업에 필요합니다. public 로그인 또는 사용자로부터 사용 권한을 취소하면 모든 로그인/사용자에 영향을 미치므로 주의해야 합니다. deny 문은 개인에 대한 모든 grant 문을 재정의하기 때문에 일반적으로 public에 대한 사용 권한은 거부하면 안 됩니다. 
  
## <a name="informationschema-and-sys-users-and-schemas"></a>INFORMATION_SCHEMA 및 sys 사용자와 스키마 
 모든 데이터베이스에는 카탈로그 뷰에 사용자로 표시되는 두 엔터티인 `INFORMATION_SCHEMA`와 `sys`가 포함됩니다. 이러한 엔터티는 데이터베이스 엔진 내부에서 사용하는 데 필요하며, 수정하거나 삭제할 수 없습니다.  
  
## <a name="certificate-based-sql-server-logins"></a>인증서 기반 SQL Server 로그인  
 이름이 이중 해시 표시(##)로 묶인 서버 보안 주체는 내부 시스템 용도로만 사용됩니다. 다음 보안 주체는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치할 때 인증서에서 생성되며 삭제하면 안 됩니다.  
  
-   \##MS_SQLResourceSigningCertificate##    
-   \##MS_SQLReplicationSigningCertificate##    
-   \##MS_SQLAuthenticatorCertificate##    
-   \##MS_AgentSigningCertificate##   
-   \##MS_PolicyEventProcessingLogin##   
-   \##MS_PolicySigningCertificate##   
-   \##MS_PolicyTsqlExecutionLogin##   
 
 이러한 사용자 계정은 Microsoft에 발급된 인증서에 기반하므로 관리자에 의해 변경될 수 있는 암호를 갖지 않습니다.
  
## <a name="the-guest-user"></a>guest 사용자  
 각 데이터베이스에는 `guest`에서 변경되었습니다. `guest` 사용자에게 부여된 권한은 데이터베이스에 대한 액세스 권한이 있지만 데이터베이스에 사용자 계정이 없는 사용자가 상속합니다. `guest` 사용자는 삭제할 수 없지만 CONNECT 권한을 취소하여 해제할 수 있습니다. CONNECT 권한은 `master` 또는 `tempdb`가 아닌 임의의 데이터베이스 내에서 `REVOKE CONNECT FROM GUEST;`를 실행하여 취소할 수 있습니다.  
  
  
## <a name="related-tasks"></a>관련 태스크  
 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서 섹션에는 다음과 같은 항목이 포함되어 있습니다.  
  
-   [로그인, 사용자 및 스키마 관리 방법 도움말 항목](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [서버 수준 역할](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [데이터베이스 수준 역할](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [응용 프로그램 역할](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 보안 설정](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [서버 수준 역할](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [데이터베이스 수준 역할](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  
