---
title: Security Audit 이벤트 범주 - Profiler
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [SQL Server], Security Audit event category
- SQL Server event classes, Security Audit event category
ms.assetid: e64f7695-2f23-4adb-b83d-52f147cc1a2f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f07afead7d74b358c0220dc7ed22dbf31ebbf11a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74056053"
---
# <a name="security-audit-event-category-sql-server-profiler"></a>Security Audit 이벤트 범주(SQL Server Profiler)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Security Audit** 이벤트 범주에는 보안 감사 이벤트가 포함됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[Audit Add DB User 이벤트 클래스](../../relational-databases/event-classes/audit-add-db-user-event-class.md)|데이터베이스에서 로그인이 데이터베이스 사용자로 추가되거나 제거되었음을 나타냅니다.|  
|[Audit Add Login to Server Role 이벤트 클래스](../../relational-databases/event-classes/audit-add-login-to-server-role-event-class.md)|고정 서버 역할에서 로그인이 추가되거나 제거되었음을 나타냅니다.|  
|[Audit Add Member to DB Role 이벤트 클래스](../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md)|역할에서 로그인이 추가되거나 제거되었음을 나타냅니다.|  
|[Audit Add Role 이벤트 클래스](../../relational-databases/event-classes/audit-add-role-event-class.md)|데이터베이스에서 데이터베이스 역할이 추가되거나 제거되었음을 나타냅니다.|  
|[Audit Addlogin 이벤트 클래스](../../relational-databases/event-classes/audit-addlogin-event-class.md)|로그인이 추가되거나 제거되었음을 나타냅니다.|  
|[Audit App Role Change Password 이벤트 클래스](../../relational-databases/event-classes/audit-app-role-change-password-event-class.md)|애플리케이션 역할의 암호가 변경되었음을 나타냅니다.|  
|[감사 백업 및 이벤트 클래스 복원](../../relational-databases/event-classes/audit-backup-and-restore-event-class.md)|백업 문 또는 복원 문이 실행되었음을 나타냅니다.|  
|[Audit Broker Conversation 이벤트 클래스](../../relational-databases/event-classes/audit-broker-conversation-event-class.md)|Service Broker 대화 보안과 연관된 감사 메시지를 보고합니다.|  
|[Audit Broker Login 이벤트 클래스](../../relational-databases/event-classes/audit-broker-login-event-class.md)|Service Broker 전송 보안과 연관된 감사 메시지를 보고합니다.|  
|[Audit Change Audit 이벤트 클래스](../../relational-databases/event-classes/audit-change-audit-event-class.md)|감사 추적이 수정되었음을 나타냅니다.|  
|[Audit Change Database Owner 이벤트 클래스](../../relational-databases/event-classes/audit-change-database-owner-event-class.md)|데이터베이스 소유자를 변경할 권한이 확인되었음을 나타냅니다.|  
|[Audit Database Management 이벤트 클래스](../../relational-databases/event-classes/audit-database-management-event-class.md)|데이터베이스가 생성, 변경 또는 삭제되었음을 나타냅니다.|  
|[Audit Database Mirroring Login 이벤트 클래스](../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md)|데이터베이스 미러링 전송 보안과 연관된 감사 메시지를 보고합니다.|  
|[Audit Database Object Access 이벤트 클래스](../../relational-databases/event-classes/audit-database-object-access-event-class.md)|스키마와 같은 데이터베이스 개체가 액세스되었음을 나타냅니다.|  
|[Audit Database Object GDR 이벤트 클래스](../../relational-databases/event-classes/audit-database-object-gdr-event-class.md)|데이터베이스 개체에 대한 GDR 이벤트가 발생했음을 나타냅니다.|  
|[Audit Database Object Management 이벤트 클래스](../../relational-databases/event-classes/audit-database-object-management-event-class.md)|데이터베이스 개체에 대해 CREATE, ALTER 또는 DROP 문이 실행되었음을 나타냅니다.|  
|[Audit Database Object Take Ownership 이벤트 클래스](../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md)|데이터베이스 범위에서 개체의 소유자가 변경되었음을 나타냅니다.|  
|[Audit Database Operation 이벤트 클래스](../../relational-databases/event-classes/audit-database-operation-event-class.md)|검사점 또는 구독 쿼리 알림과 같은 여러 작업이 발생했음을 나타냅니다.|  
|[Audit Database Principal Impersonation 이벤트 클래스](../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md)|데이터베이스 범위에서 가장이 발생했음을 나타냅니다.|  
|[Audit Database Principal Management 이벤트 클래스](../../relational-databases/event-classes/audit-database-principal-management-event-class.md)|데이터베이스에서 보안 주체가 생성, 변경 또는 삭제되었음을 나타냅니다.|  
|[Audit Database Scope GDR 이벤트 클래스](../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자에 의해 문 사용 권한에 대한 GRANT, REVOKE 또는 DENY 명령이 실행되었음을 나타냅니다.|  
|[Audit DBCC 이벤트 클래스](../../relational-databases/event-classes/audit-dbcc-event-class.md)|DBCC 명령이 실행되었음을 나타냅니다.|  
|[Audit Fulltext 이벤트 클래스](../../relational-databases/event-classes/audit-fulltext-event-class.md)|전체 텍스트 이벤트가 발생했음을 나타냅니다.|  
|[Audit Login Change Password 이벤트 클래스](../../relational-databases/event-classes/audit-login-change-password-event-class.md)|사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 암호를 변경했음을 나타냅니다.|  
|[Audit Login Change Property 이벤트 클래스](../../relational-databases/event-classes/audit-login-change-property-event-class.md)|**sp_defaultdb**, **sp_defaultlanguage**또는 ALTER LOGIN을 사용하여 로그인 속성을 수정했음을 나타냅니다.|  
|[Audit Login 이벤트 클래스](../../relational-databases/event-classes/audit-login-event-class.md)|사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 성공적으로 로그인했음을 나타냅니다.|  
|[Audit Login Failed 이벤트 클래스](../../relational-databases/event-classes/audit-login-failed-event-class.md)|사용자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 로그인 시도가 실패했음을 나타냅니다.|  
|[Audit Login GDR 이벤트 클래스](../../relational-databases/event-classes/audit-login-gdr-event-class.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 로그인 권한이 추가 또는 제거되었음을 나타냅니다.|  
|[Audit Logout 이벤트 클래스](../../relational-databases/event-classes/audit-logout-event-class.md)|사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 로그아웃되었음을 나타냅니다.|  
|[Audit Object Derived Permission 이벤트 클래스](../../relational-databases/event-classes/audit-object-derived-permission-event-class.md)|개체 대해 CREATE, ALTER 또는 DROP 명령이 실행되었음을 나타냅니다.|  
|[Audit Schema Object Access 이벤트 클래스](../../relational-databases/event-classes/audit-schema-object-access-event-class.md)|개체 사용 권한(SELECT 등)이 사용되었음을 나타냅니다.|  
|[Audit Schema Object GDR 이벤트 클래스](../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자에 의해 스키마 개체 사용 권한에 대한 GRANT, REVOKE 또는 DENY 명령이 실행되었음을 나타냅니다.|  
|[Audit Schema Object Management 이벤트 클래스](../../relational-databases/event-classes/audit-schema-object-management-event-class.md)|서버 개체가 생성, 변경 또는 삭제되었음을 나타냅니다.|  
|[Audit Schema Object Take Ownership 이벤트 클래스](../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md)|스키마 개체 소유자를 변경할 권한이 확인되었음을 나타냅니다.|  
|[Audit Server Alter Trace 이벤트 클래스](../../relational-databases/event-classes/audit-server-alter-trace-event-class.md)|ALTER TRACE 권한이 확인되었음을 나타냅니다.|  
|[Audit Server Object GDR 이벤트 클래스](../../relational-databases/event-classes/audit-server-object-gdr-event-class.md)|스키마 개체에 대한 GDR 이벤트가 발생했음을 나타냅니다.|  
|[Audit Server Object Management 이벤트 클래스](../../relational-databases/event-classes/audit-server-object-management-event-class.md)|서버 개체에 대해 CREATE, ALTER 또는 DROP 이벤트가 발생했음을 나타냅니다.|  
|[Audit Server Object Take Ownership 이벤트 클래스](../../relational-databases/event-classes/audit-server-object-take-ownership-event-class.md)|서버 개체 소유자가 변경되었음을 나타냅니다.|  
|[Audit Server Operation 이벤트 클래스](../../relational-databases/event-classes/audit-server-operation-event-class.md)|서버에서 감사 작업이 발생했음을 나타냅니다.|  
|[Audit Server Principal Impersonation 이벤트 클래스](../../relational-databases/event-classes/audit-server-principal-impersonation-event-class.md)|서버 범위에서 가장이 발생했음을 나타냅니다.|  
|[Audit Server Principal Management 이벤트 클래스](../../relational-databases/event-classes/audit-server-principal-management-event-class.md)|서버 보안 주체에 대해 CREATE, ALTER 또는 DROP이 발생했음을 나타냅니다.|  
|[Audit Server Scope GDR 이벤트 클래스](../../relational-databases/event-classes/audit-server-scope-gdr-event-class.md)|서버 사용 권한에 대해 GDR 이벤트가 발생했음을 나타냅니다.|  
|[Audit Server Starts and Stops 이벤트 클래스](../../relational-databases/event-classes/audit-server-starts-and-stops-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 상태가 수정되었음을 나타냅니다.|  
|[Audit Statement Permission 이벤트 클래스](../../relational-databases/event-classes/audit-statement-permission-event-class.md)|문 사용 권한이 사용되었음을 나타냅니다.|  
  
## <a name="related-content"></a>관련 내용  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
