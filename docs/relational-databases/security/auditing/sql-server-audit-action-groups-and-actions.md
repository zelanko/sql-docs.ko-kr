---
title: SQL Server 감사 동작 그룹 및 동작 | Microsoft 문서
ms.custom: ''
ms.date: 10/19/2016
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- audit
helpviewer_keywords:
- audit actions [SQL Server]
- audits [SQL Server], groups
- server-level audit actions [SQL Server]
- SQL Server Audit
- audit-level audit actions [SQL Server]
- database-level audit actions [SQL Server]
- audit action groups [SQL Server]
- audits [SQL Server], actions
ms.assetid: b7422911-7524-4bcd-9ab9-e460d5897b3d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: cf6fe9b80bbbb270b75faaa0d1f34a0685ad18c7
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036778"
---
# <a name="sql-server-audit-action-groups-and-actions"></a>SQL Server 감사 동작 그룹 및 동작
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit 기능을 통해 서버 수준 및 데이터베이스 수준의 이벤트 그룹과 개별 이벤트를 감사할 수 있습니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit는 0개 이상의 감사 동작 항목으로 구성되어 있습니다. 이러한 감사 동작 항목은 동작 그룹(예: Server_Object_Change_Group) 또는 개별 동작(예: 테이블에 대한 SELECT 작업)일 수 있습니다.  
  
> [!NOTE]  
>  Server_Object_Change_Group에는 모든 서버 개체(데이터베이스 또는 끝점)에 대한 CREATE, ALTER 및 DROP이 포함됩니다.  
  
 감사의 동작 범주는 다음과 같습니다.  
  
-   서버 수준. 관리 변경 내용 및 로그온/로그오프 작업과 같은 서버 작업이 이에 해당됩니다.  
  
-   데이터베이스 수준. DML(데이터 조작 언어) 및 DDL(데이터 정의 언어) 작업이 이에 해당됩니다.  
  
-   감사 수준. 감사 프로세스의 동작이 이에 해당됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit 구성 요소에서 수행되는 일부 동작은 기본적으로 특정 감사에서 감사됩니다. 이 경우 부모 개체에서 이벤트가 발생한 것이므로 감사 이벤트가 자동으로 발생합니다.  
  
 기본적으로 감사되는 동작은 다음과 같습니다.  
  
-   서버 감사 상태 변경(상태를 ON 또는 OFF로 설정)  
  
 다음 이벤트는 기본적으로 감사되지 않습니다.  
  
-   CREATE SERVER AUDIT SPECIFICATION  
  
-   ALTER SERVER AUDIT SPECIFICATION  
  
-   DROP SERVER AUDIT SPECIFICATION  
  
-   CREATE DATABASE AUDIT SPECIFICATION  
  
-   ALTER DATABASE AUDIT SPECIFICATION  
  
-   DROP DATABASE AUDIT SPECIFICATION  
  
 모든 감사는 처음 만들어진 상태에서는 비활성화되어 있습니다.  
  
## <a name="server-level-audit-action-groups"></a>서버 수준 감사 동작 그룹  
 서버 수준 감사 동작 그룹은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 보안 감사 이벤트 클래스와 유사한 동작입니다. 자세한 내용은 [SQL Server Event Class Reference](../../../relational-databases/event-classes/sql-server-event-class-reference.md)를 참조하세요.  
  
 다음 표에서는 서버 수준 감사 동작 그룹에 대해 설명하며 해당하는 경우 동일한 SQL Server 이벤트 클래스를 제공합니다.  
  
|동작 그룹 이름|설명|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|응용 프로그램 역할의 암호가 변경될 때마다 발생하는 이벤트입니다. [Audit App Role Change Password Event Class](../../../relational-databases/event-classes/audit-app-role-change-password-event-class.md)와 동일합니다.|  
|AUDIT_CHANGE_GROUP|모든 감사가 생성, 수정 또는 삭제되거나 모든 감사 사양이 생성, 수정 또는 삭제될 때마다 발생하는 이벤트입니다. 감사에 대한 모든 변경 내용은 자체적으로 감사됩니다. [Audit Change Audit Event Class](../../../relational-databases/event-classes/audit-change-audit-event-class.md)와 동일합니다.|  
|BACKUP_RESTORE_GROUP|백업 또는 복원 명령이 실행될 때마다 발생하는 이벤트입니다. [감사 백업 및 이벤트 클래스 복원](../../../relational-databases/event-classes/audit-backup-and-restore-event-class.md)과 동일합니다.|  
|BROKER_LOGIN_GROUP|Service Broker 전송 보안과 연관된 감사 메시지를 보고하기 위해 발생하는 이벤트입니다. [Audit Broker Login Event Class](../../../relational-databases/event-classes/audit-broker-login-event-class.md)와 동일합니다.|  
|DATABASE_CHANGE_GROUP|데이터베이스가 생성, 변경 또는 삭제되면 발생하면 발생하는 이벤트입니다. 이 이벤트는 모든 데이터베이스가 생성, 변경 또는 삭제될 때마다 발생합니다. [Audit Database Management Event Class](../../../relational-databases/event-classes/audit-database-management-event-class.md)와 동일합니다.|  
|DATABASE_LOGOUT_GROUP|포함된 데이터베이스 사용자가 데이터베이스에서 로그아웃하면 발생하는 이벤트입니다. Audit Database Logout 이벤트 클래스와 동일합니다.|  
|DATABASE_MIRRORING_LOGIN_GROUP|데이터베이스 미러링 전송 보안과 연관된 감사 메시지를 보고하기 위해 발생하는 이벤트입니다. [Audit Database Mirroring Login Event Class](../../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md)와 동일합니다.|  
|DATABASE_OBJECT_ACCESS_GROUP|메시지 유형, 어셈블리, 계약과 같은 데이터베이스 개체에 액세스할 때마다 발생하는 이벤트입니다. 이 이벤트는 모든 데이터베이스의 모든 액세스에 대해 발생합니다. 참고: 이로 인해 다량의 감사 레코드가 생성될 수 있습니다.<br /><br /> [Audit Database Object Access Event Class](../../../relational-databases/event-classes/audit-database-object-access-event-class.md)와 동일합니다.|  
|DATABASE_OBJECT_CHANGE_GROUP|스키마와 같은 데이터베이스 개체에 대해 CREATE, ALTER 또는 DROP 문이 실행되면 발생하는 이벤트입니다. 이 이벤트는 모든 데이터베이스 개체가 생성, 변경 또는 삭제될 때마다 발생합니다. 참고: 이로 인해 다량의 감사 레코드가 생성될 수 있습니다.<br /><br /> [Audit Database Object Management Event Class](../../../relational-databases/event-classes/audit-database-object-management-event-class.md)와 동일합니다.|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|데이터베이스 범위 내에서 개체에 대한 소유자가 변경되면 발생하는 이벤트입니다. 이 이벤트는 모든 서버 데이터베이스의 모든 개체 소유권 변경에 대해 발생합니다. [Audit Database Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md)와 동일합니다.|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|어셈블리 및 스키마와 같은 데이터베이스 개체에 대해 GRANT, REVOKE 또는 DENY가 실행되면 발생하는 이벤트입니다. 모든 서버 데이터베이스의 모든 개체 사용 권한 변경에 대해 발생하는 이벤트입니다. [Audit Database Object GDR Event Class](../../../relational-databases/event-classes/audit-database-object-gdr-event-class.md)와 동일합니다.|  
|DATABASE_OPERATION_GROUP|쿼리 알림 구독 또는 검사점 설정과 같은 데이터베이스 작업이 수행되면 발생하는 이벤트입니다. 이 이벤트는 모든 데이터베이스의 모든 데이터베이스 작업에 대해 발생합니다. [Audit Database Operation Event Class](../../../relational-databases/event-classes/audit-database-operation-event-class.md)와 동일합니다.|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|ALTER AUTHORIZATION 문을 사용하여 데이터베이스 소유자를 변경하고 변경 작업에 필요한 권한을 확인하면 발생하는 이벤트입니다. 이 이벤트는 모든 서버 데이터베이스의 모든 데이터베이스 소유권 변경에 대해 발생합니다. [Audit Change Database Owner Event Class](../../../relational-databases/event-classes/audit-change-database-owner-event-class.md)와 동일합니다.|  
|DATABASE_PERMISSION_CHANGE_GROUP|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 모든 보안 주체가 문 사용 권한에 대해 GRANT, REVOKE 또는 DENY를 실행할 때마다 발생하는 이벤트입니다. 이는 데이터베이스 사용 권한 부여와 같은 데이터베이스 전용 이벤트에 해당합니다.<br /><br /> 모든 서버 데이터베이스의 모든 데이터베이스 사용 권한 변경(GDR)에 대해 발생하는 이벤트입니다. [Audit Database Scope GDR Event Class](../../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md)와 동일합니다.|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|사용자 같은 보안 주체가 데이터베이스에서 생성, 변경 또는 삭제되면 발생하는 이벤트입니다. [Audit Database Principal Management Event Class](../../../relational-databases/event-classes/audit-database-principal-management-event-class.md)와 동일합니다. 또한 더 이상 사용되지 않는 sp_grantdbaccess, sp_revokedbaccess, sp_addPrincipal 및 sp_dropPrincipal 저장 프로시저에 대해 발생하는 Audit Add DB Principal 이벤트 클래스와 동일합니다.<br /><br /> sp_addrole 및 sp_droprole 저장 프로시저를 사용하여 데이터베이스 역할을 추가 또는 제거할 때마다 발생하는 이벤트입니다. 이 이벤트는 모든 데이터베이스에서 모든 데이터베이스 보안 주체가 생성, 변경 또는 삭제될 때마다 발생합니다. [Audit Add Role 이벤트 클래스](../../../relational-databases/event-classes/audit-add-role-event-class.md)와 동일합니다.|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|데이터베이스 범위 내에 EXECUTE AS \<principal> 또는 SETPRINCIPAL과 같은 가장 작업이 있으면 발생하는 이벤트입니다. 모든 데이터베이스에서 가장이 수행되면 발생하는 이벤트입니다. [Audit Database Principal Impersonation Event Class](../../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md)와 동일합니다.|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|데이터베이스 역할에서 로그인이 추가 또는 제거될 때마다 발생하는 이벤트입니다. 이 이벤트 클래스는 sp_addrolemember, sp_changegroup 및 sp_droprolemember 저장 프로시저에 대해 발생하며 모든 데이터베이스의 모든 데이터베이스 역할 멤버 변경에 대해 발생합니다. [Audit Add Member to DB Role 이벤트 클래스](../../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md)와 동일합니다.|  
|DBCC_GROUP|보안 주체가 모든 DBCC 명령을 실행할 때마다 발생하는 이벤트입니다. [Audit DBCC Event Class](../../../relational-databases/event-classes/audit-dbcc-event-class.md)와 동일합니다.|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|보안 주체가 포함된 데이터베이스 로그온을 시도했으나 실패했음을 나타냅니다. 이 클래스의 이벤트는 연결 풀에서 다시 사용된 연결 또는 새 연결에 의해 발생합니다. [Audit Login Failed Event Class](../../../relational-databases/event-classes/audit-login-failed-event-class.md)와 동일합니다.|  
|FAILED_LOGIN_GROUP|보안 주체의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대한 로그인 시도가 실패했음을 나타냅니다. 이 클래스의 이벤트는 연결 풀에서 다시 사용된 연결 또는 새 연결에 의해 발생합니다. [Audit Login Failed Event Class](../../../relational-databases/event-classes/audit-login-failed-event-class.md)와 동일합니다.|  
|FULLTEXT_GROUP|전체 텍스트 이벤트가 발생했음을 나타냅니다. [Audit Fulltext Event Class](../../../relational-databases/event-classes/audit-fulltext-event-class.md)와 동일합니다.|  
|LOGIN_CHANGE_PASSWORD_GROUP|ALTER LOGIN 문 또는 sp_password 저장 프로시저를 통해 로그인 암호가 변경될 때마다 발생하는 이벤트입니다. [Audit Login Change Password Event Class](../../../relational-databases/event-classes/audit-login-change-password-event-class.md)와 동일합니다.|  
|LOGOUT_GROUP|보안 주체가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 로그아웃했음을 나타냅니다. 이 클래스의 이벤트는 연결 풀에서 다시 사용된 연결 또는 새 연결에 의해 발생합니다. [Audit Logout Event Class](../../../relational-databases/event-classes/audit-logout-event-class.md)와 동일합니다.|  
|SCHEMA_OBJECT_ACCESS_GROUP|스키마에서 개체 사용 권한이 사용될 때마다 발생하는 이벤트입니다. [Audit Schema Object Access Event Class](../../../relational-databases/event-classes/audit-schema-object-access-event-class.md)와 동일합니다.|  
|SCHEMA_OBJECT_CHANGE_GROUP|스키마에 대해 CREATE, ALTER 또는 DROP 작업이 수행되면 발생하는 이벤트입니다. [Audit Schema Object Management Event Class](../../../relational-databases/event-classes/audit-schema-object-management-event-class.md)와 동일합니다.<br /><br /> 스키마 개체에 대해 발생하는 이벤트입니다. [Audit Object Derived Permission Event Class](../../../relational-databases/event-classes/audit-object-derived-permission-event-class.md)와 동일합니다.<br /><br /> 모든 데이터베이스의 모든 스키마가 변경될 때마다 발생하는 이벤트입니다. [Audit Statement Permission Event Class](../../../relational-databases/event-classes/audit-statement-permission-event-class.md)와 동일합니다.|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|스키마 개체(예: 테이블, 프로시저, 함수) 소유자 변경 권한을 확인하거나 ALTER AUTHORIZATION 문을 사용하여 개체에 소유자를 할당하면 발생하는 이벤트입니다. 이 이벤트는 모든 서버 데이터베이스의 모든 스키마 소유권 변경에 대해 발생합니다. [Audit Schema Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md)와 동일합니다.|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|스키마 개체에 대해 권한 부여, 거부 또는 취소 작업이 수행될 때마다 발생하는 이벤트입니다. [Audit Schema Object GDR Event Class](../../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md)와 동일합니다.|  
|SERVER_OBJECT_CHANGE_GROUP|서버 개체에 대해 CREATE, ALTER 또는 DROP 작업이 수행되면 발생하는 이벤트입니다. [Audit Server Object Management Event Class](../../../relational-databases/event-classes/audit-server-object-management-event-class.md)와 동일합니다.|  
|SERVER_OBJECT_OWNERSHIP_CHANGE_GROUP|서버 범위의 개체에 대한 소유자가 변경되면 발생하는 이벤트입니다. [Audit Server Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-server-object-take-ownership-event-class.md)와 동일합니다.|  
|SERVER_OBJECT_PERMISSION_CHANGE_GROUP|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 모든 보안 주체가 서버 개체 사용 권한에 대해 GRANT, REVOKE 또는 DENY를 실행할 때마다 발생하는 이벤트입니다. [Audit Server Object GDR Event Class](../../../relational-databases/event-classes/audit-server-object-gdr-event-class.md)와 동일합니다.|  
|SERVER_OPERATION_GROUP|설정, 리소스, 외부 액세스, 권한 부여 변경 등의 보안 감사 작업이 사용되면 발생하는 이벤트입니다. [Audit Server Operation Event Class](../../../relational-databases/event-classes/audit-server-operation-event-class.md)와 동일합니다.|  
|SERVER_PERMISSION_CHANGE_GROUP|서버 범위의 사용 권한(예: 로그인 생성)에 대해 GRANT, REVOKE 또는 DENY가 실행되면 발생하는 이벤트입니다. [Audit Server Scope GDR Event Class](../../../relational-databases/event-classes/audit-server-scope-gdr-event-class.md)와 동일합니다.|  
|SERVER_PRINCIPAL_CHANGE_GROUP|서버 보안 주체가 생성, 변경 또는 삭제되면 발생하는 이벤트입니다. [Audit Server Principal Management Event Class](../../../relational-databases/event-classes/audit-server-principal-management-event-class.md)와 동일합니다.<br /><br /> 보안 주체가 sp_defaultdb 또는 sp_defaultlanguage 저장 프로시저나 ALTER LOGIN 문을 실행하면 발생하는 이벤트입니다. [Audit Addlogin Event Class](../../../relational-databases/event-classes/audit-addlogin-event-class.md)와 동일합니다.<br /><br /> sp_addlogin 및 sp_droplogin 저장 프로시저에 대해 발생하는 이벤트입니다. 또한 [Audit Login Change Property Event Class](../../../relational-databases/event-classes/audit-login-change-property-event-class.md)와 동일합니다.<br /><br /> sp_grantlogin 또는 sp_revokelogin 저장 프로시저에 대해 발생하는 이벤트입니다. [Audit Login GDR Event Class](../../../relational-databases/event-classes/audit-login-gdr-event-class.md)와 동일합니다.|  
|SERVER_PRINCIPAL_IMPERSONATION_GROUP|서버 범위 내에 EXECUTE AS \<login>과 같은 가장이 있으면 발생하는 이벤트입니다. [Audit Server Principal Impersonation Event Class](../../../relational-databases/event-classes/audit-server-principal-impersonation-event-class.md)와 동일합니다.|  
|SERVER_ROLE_MEMBER_CHANGE_GROUP|고정 서버 역할에서 로그인이 추가 또는 제거될 때마다 발생하는 이벤트입니다. 이 이벤트는 sp_addsrvrolemember 및 sp_dropsrvrolemember 저장 프로시저에 대해 발생합니다. [Audit Add Login to Server Role 이벤트 클래스](../../../relational-databases/event-classes/audit-add-login-to-server-role-event-class.md)와 동일합니다.|  
|SERVER_STATE_CHANGE_GROUP|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 상태가 수정되면 발생하는 이벤트입니다. [Audit Server Starts and Stops Event Class](../../../relational-databases/event-classes/audit-server-starts-and-stops-event-class.md)와 동일합니다.|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|보안 주체가 포함된 데이터베이스에 성공적으로 로그인했음을 나타냅니다. Audit Successful Database Authentication 이벤트 클래스와 동일합니다.|  
|SUCCESSFUL_LOGIN_GROUP|보안 주체가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 성공적으로 로그인했음을 나타냅니다. 이 클래스의 이벤트는 연결 풀에서 다시 사용된 연결 또는 새 연결에 의해 발생합니다. [Audit Login Event Class](../../../relational-databases/event-classes/audit-login-event-class.md)와 동일합니다.|  
|TRACE_CHANGE_GROUP|ALTER TRACE 권한을 확인하는 모든 문에 대해 발생하는 이벤트입니다. [Audit Server Alter Trace Event Class](../../../relational-databases/event-classes/audit-server-alter-trace-event-class.md)와 동일합니다.|  
|TRANSACTION_GROUP|이 이벤트는 이러한 문에 대한 명시적 호출 및 암시적 트랜잭션 작업의 BEGIN TRANSACTION, ROLLBACK TRANSACTION 및 COMMIT TRANSACTION 작업에 대해 발생합니다. 또한 이 이벤트는 트랜잭션 롤백에 의한 개별 문의 UNDO 작업에 대해서도 발생합니다.|  
|USER_CHANGE_PASSWORD_GROUP|ALTER USER 문을 사용하여 포함된 데이터베이스 사용자의 암호를 변경할 때마다 발생하는 이벤트입니다.|  
|USER_DEFINED_AUDIT_GROUP|이 그룹은 [sp_audit_write&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md)를 사용하여 발생하는 이벤트를 모니터링합니다. 일반적으로 트리거 또는 저장 프로시저는 중요한 이벤트를 감사할 수 있도록 **sp_audit_write** 호출을 포함합니다.|  
  
### <a name="considerations"></a>고려 사항  
 서버 수준 동작 그룹은 전체 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 동작을 포함합니다. 예를 들어 서버 감사 사양에 적절한 동작 그룹이 추가되면 모든 데이터베이스의 모든 스키마 개체 액세스 검사가 기록됩니다. 데이터베이스 감사 사양에서는 해당 데이터베이스의 스키마 개체 액세스만 기록됩니다.  
  
 서버 수준 동작은 데이터베이스 수준 동작에 대한 자세한 필터링을 허용하지 않습니다. 자세한 동작 필터링을 구현하려면 데이터베이스 수준 감사(예: Employee 그룹에서 로그인에 사용할 Customers 테이블 SELECT 동작에 대한 감사)가 필요합니다. 시스템 뷰와 같은 서버 범위 개체는 사용자 데이터베이스 감사 사양에 포함하지 마십시오.  
  
## <a name="database-level-audit-action-groups"></a>데이터베이스 수준 감사 동작 그룹  
 데이터베이스 수준 감사 동작 그룹은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 보안 감사 이벤트 클래스와 유사한 동작입니다. 이벤트 클래스에 대한 자세한 내용은 [SQL Server Event Class Reference](../../../relational-databases/event-classes/sql-server-event-class-reference.md)를 참조하십시오.  
  
 다음 표에서는 데이터베이스 수준 감사 동작 그룹에 대해 설명하며 해당하는 경우 동일한 SQL Server 이벤트 클래스를 제공합니다.  
  
|동작 그룹 이름|설명|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|응용 프로그램 역할의 암호가 변경될 때마다 발생하는 이벤트입니다. [Audit App Role Change Password Event Class](../../../relational-databases/event-classes/audit-app-role-change-password-event-class.md)와 동일합니다.|  
|AUDIT_CHANGE_GROUP|모든 감사가 생성, 수정 또는 삭제되거나 모든 감사 사양이 생성, 수정 또는 삭제될 때마다 발생하는 이벤트입니다. 감사에 대한 모든 변경 내용은 자체적으로 감사됩니다. [Audit Change Audit Event Class](../../../relational-databases/event-classes/audit-change-audit-event-class.md)와 동일합니다.|  
|BACKUP_RESTORE_GROUP|백업 또는 복원 명령이 실행될 때마다 발생하는 이벤트입니다. [감사 백업 및 이벤트 클래스 복원](../../../relational-databases/event-classes/audit-backup-and-restore-event-class.md)과 동일합니다.|  
|DATABASE_CHANGE_GROUP|데이터베이스가 생성, 변경 또는 삭제되면 발생하면 발생하는 이벤트입니다. [Audit Database Management Event Class](../../../relational-databases/event-classes/audit-database-management-event-class.md)와 동일합니다.|  
|DATABASE_LOGOUT_GROUP|포함된 데이터베이스 사용자가 데이터베이스에서 로그아웃하면 발생하는 이벤트입니다. [감사 백업 및 이벤트 클래스 복원](../../../relational-databases/event-classes/audit-backup-and-restore-event-class.md)과 동일합니다.|  
|DATABASE_OBJECT_ACCESS_GROUP|인증서 및 비대칭 키와 같은 데이터베이스 개체에 액세스할 때마다 발생하는 이벤트입니다. [Audit Database Object Access Event Class](../../../relational-databases/event-classes/audit-database-object-access-event-class.md)와 동일합니다.|  
|DATABASE_OBJECT_CHANGE_GROUP|스키마와 같은 데이터베이스 개체에 대해 CREATE, ALTER 또는 DROP 문이 실행되면 발생하는 이벤트입니다. [Audit Database Object Management Event Class](../../../relational-databases/event-classes/audit-database-object-management-event-class.md)와 동일합니다.|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|데이터베이스 범위 내에서 개체에 대한 소유자가 변경되면 발생하는 이벤트입니다. [Audit Database Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md)와 동일합니다.|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|어셈블리 및 스키마와 같은 데이터베이스 개체에 대해 GRANT, REVOKE 또는 DENY가 실행되면 발생하는 이벤트입니다. [Audit Database Object GDR Event Class](../../../relational-databases/event-classes/audit-database-object-gdr-event-class.md)와 동일합니다.|  
|DATABASE_OPERATION_GROUP|쿼리 알림 구독 또는 검사점 설정과 같은 데이터베이스 작업이 수행되면 발생하는 이벤트입니다. [Audit Database Operation Event Class](../../../relational-databases/event-classes/audit-database-operation-event-class.md)와 동일합니다.|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|ALTER AUTHORIZATION 문을 사용하여 데이터베이스 소유자를 변경하고 변경 작업에 필요한 권한을 확인하면 발생하는 이벤트입니다. [Audit Change Database Owner Event Class](../../../relational-databases/event-classes/audit-change-database-owner-event-class.md)와 동일합니다.|  
|DATABASE_PERMISSION_CHANGE_GROUP|데이터베이스 사용 권한 부여와 같은 데이터베이스 전용 이벤트에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 모든 사용자가 문 사용 권한에 대해 GRANT, REVOKE 또는 DENY를 실행할 때마다 발생하는 이벤트입니다. [Audit Database Scope GDR Event Class](../../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md)와 동일합니다.|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|사용자 같은 보안 주체가 데이터베이스에서 생성, 변경 또는 삭제되면 발생하는 이벤트입니다. [Audit Database Principal Management Event Class](../../../relational-databases/event-classes/audit-database-principal-management-event-class.md)와 동일합니다. 또한 더 이상 사용되지 않는 sp_grantdbaccess, sp_revokedbaccess, sp_adduser 및 sp_dropuser 저장 프로시저에 대해 발생하는 [Audit Add DB User 이벤트 클래스](../../../relational-databases/event-classes/audit-add-db-user-event-class.md)와 동일합니다.<br /><br /> 이 이벤트는 더 이상 사용되지 않는 sp_addrole 및 sp_droprole 저장 프로시저를 사용하여 데이터베이스 역할을 추가 또는 제거할 때마다 발생합니다. [Audit Add Role Event Class](../../../relational-databases/event-classes/audit-add-role-event-class.md)와 동일합니다.|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|데이터베이스 범위 내에 EXECUTE AS \<user>와 같은 가장이 있으면 발생하는 이벤트입니다. [Audit Database Principal Impersonation Event Class](../../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md)와 동일합니다.|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|데이터베이스 역할에서 로그인이 추가 또는 제거될 때마다 발생하는 이벤트입니다. 이 이벤트 클래스는 sp_addrolemember, sp_changegroup 및 sp_droprolemember 저장 프로시저에서 사용됩니다. [Audit Add Member to DB Role 이벤트 클래스](../../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md)와 동일합니다.|  
|DBCC_GROUP|보안 주체가 모든 DBCC 명령을 실행할 때마다 발생하는 이벤트입니다. [Audit DBCC Event Class](../../../relational-databases/event-classes/audit-dbcc-event-class.md)와 동일합니다.|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|보안 주체가 포함된 데이터베이스 로그온을 시도했으나 실패했음을 나타냅니다. 이 클래스의 이벤트는 연결 풀에서 다시 사용된 연결 또는 새 연결에 의해 발생합니다. 발생합니다.|  
|SCHEMA_OBJECT_ACCESS_GROUP|스키마에서 개체 사용 권한이 사용될 때마다 발생하는 이벤트입니다. [Audit Schema Object Access Event Class](../../../relational-databases/event-classes/audit-schema-object-access-event-class.md)와 동일합니다.|  
|SCHEMA_OBJECT_CHANGE_GROUP|스키마에 대해 CREATE, ALTER 또는 DROP 작업이 수행되면 발생하는 이벤트입니다. [Audit Schema Object Management Event Class](../../../relational-databases/event-classes/audit-schema-object-management-event-class.md)와 동일합니다.<br /><br /> 스키마 개체에 대해 발생하는 이벤트입니다. [Audit Object Derived Permission Event Class](../../../relational-databases/event-classes/audit-object-derived-permission-event-class.md)와 동일합니다. 또한 [Audit Statement Permission Event Class](../../../relational-databases/event-classes/audit-statement-permission-event-class.md)와 동일합니다.|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|스키마 개체(예: 테이블, 프로시저, 함수) 소유자 변경 권한을 확인하거나 ALTER AUTHORIZATION 문을 사용하여 개체에 소유자를 할당하면 발생하는 이벤트입니다. [Audit Schema Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md)와 동일합니다.|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|스키마 개체에 대해 권한 부여, 거부 또는 취소 작업이 실행될 때마다 발생하는 이벤트입니다. [Audit Schema Object GDR Event Class](../../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md)와 동일합니다.|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|보안 주체가 포함된 데이터베이스에 성공적으로 로그인했음을 나타냅니다. Audit Successful Database Authentication 이벤트 클래스와 동일합니다.|  
|USER_CHANGE_PASSWORD_GROUP|ALTER USER 문을 사용하여 포함된 데이터베이스 사용자의 암호를 변경할 때마다 발생하는 이벤트입니다.|  
|USER_DEFINED_AUDIT_GROUP|이 그룹은 [sp_audit_write&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md)를 사용하여 발생하는 이벤트를 모니터링합니다.|  
  
## <a name="database-level-audit-actions"></a>데이터베이스 수준 감사 동작  
 데이터베이스 수준 동작은 데이터베이스 스키마 및 스키마 개체(예: 테이블, 뷰, 저장 프로시저, 함수, 확장 저장 프로시저, 큐, 동의어)에 대한 특정 동작을 직접 감사할 수 있습니다. 유형, XML 스키마 컬렉션, 데이터베이스 및 스키마는 감사되지 않습니다. 스키마 개체 감사는 스키마 및 데이터베이스에 구성될 수 있습니다. 이 경우 지정된 스키마 또는 데이터베이스에 포함된 모든 스키마 개체의 이벤트가 감사됩니다. 다음 표에서는 데이터베이스 수준 감사 동작에 대해 설명합니다.  
  
|작업|설명|  
|------------|-----------------|  
|SELECT|SELECT를 실행할 때마다 발생하는 이벤트입니다.|  
|UPDATE|UPDATE를 실행할 때마다 발생하는 이벤트입니다.|  
|INSERT|INSERT를 실행할 때마다 발생하는 이벤트입니다.|  
|Delete|DELETE를 실행할 때마다 발생하는 이벤트입니다.|  
|CREATE 문을 실행하기 전에|EXECUTE를 실행할 때마다 발생하는 이벤트입니다.|  
|RECEIVE|RECEIVE를 실행할 때마다 발생하는 이벤트입니다.|  
|REFERENCES|REFERENCES 사용 권한을 확인할 때마다 발생하는 이벤트입니다.|  
  
### <a name="considerations"></a>고려 사항  
*  데이터베이스 수준 감사 동작은 열에 적용되지 않습니다.  
  
*  쿼리 프로세서에서 쿼리를 매개 변수화하면 쿼리의 열 값 대신 해당 매개 변수가 감사 이벤트 로그에 나타납니다. 
 
*  RPC 문이 기록되지 않았습니다. 
  
## <a name="audit-level-audit-action-groups"></a>감사 수준 감사 동작 그룹  
 감사 프로세스의 동작을 감사할 수도 있습니다. 이는 서버 범위 또는 데이터베이스 범위일 수 있습니다. 데이터베이스 범위에서는 데이터베이스 감사 사양에 대해서만 발생합니다. 다음 표에서는 감사 수준 감사 동작 그룹에 대해 설명합니다.  
  
|동작 그룹 이름|설명|  
|-----------------------|-----------------|  
|AUDIT_ CHANGE_GROUP|다음 명령 중 하나를 실행할 때마다 발생하는 이벤트입니다.<br /><br /> CREATE SERVER AUDIT<br /><br /> ALTER SERVER AUDIT<br /><br /> DROP SERVER AUDIT<br /><br /> CREATE SERVER AUDIT SPECIFICATION<br /><br /> ALTER SERVER AUDIT SPECIFICATION<br /><br /> DROP SERVER AUDIT SPECIFICATION<br /><br /> CREATE DATABASE AUDIT SPECIFICATION<br /><br /> ALTER DATABASE AUDIT SPECIFICATION<br /><br /> DROP DATABASE AUDIT SPECIFICATION|  
  
## <a name="related-content"></a>관련 내용  
 [서버 감사 및 서버 감사 사양 만들기](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
 [서버 감사 및 데이터베이스 감사 사양 만들기](../../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)  
  
 [CREATE SERVER AUDIT&#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md)  
  
 [ALTER SERVER AUDIT&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-transact-sql.md)  
  
 [DROP SERVER AUDIT&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-transact-sql.md)  
  
 [CREATE SERVER AUDIT SPECIFICATION&#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)  
  
 [ALTER SERVER AUDIT SPECIFICATION&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-specification-transact-sql.md)  
  
 [DROP SERVER AUDIT SPECIFICATION&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-specification-transact-sql.md)  
  
 [CREATE DATABASE AUDIT SPECIFICATION&#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)  
  
 [ALTER DATABASE AUDIT SPECIFICATION&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-audit-specification-transact-sql.md)  
  
 [DROP DATABASE AUDIT SPECIFICATION&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-audit-specification-transact-sql.md)  
  
 [ALTER AUTHORIZATION&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-authorization-transact-sql.md)  
  
 [sys.fn_get_audit_file&#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)  
  
 [sys.server_audits&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)  
  
 [sys.server_file_audits&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)  
  
 [sys.server_audit_specifications&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)  
  
 [sys.server_audit_specification_details&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)  
  
 [sys.database_audit_specifications&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)  
  
 [sys.database_audit_specification_details&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)  
  
 [sys.dm_server_audit_status&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)  
  
 [sys.dm_audit_actions&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)  
  
 [sys.dm_audit_class_type_map&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)  
  
  
