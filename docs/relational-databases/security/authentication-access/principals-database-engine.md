---
title: "보안 주체(데이터베이스 엔진) | Microsoft Docs"
ms.custom: ""
ms.date: "01/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.roleproperties.selectroll.f1"
  - "sql13.swb.databaseuser.permissions.user.f1--May use common.permissions"
helpviewer_keywords: 
  - "인증서 [SQL Server], 보안 주체"
  - "역할 [SQL Server], 보안 주체"
  - "권한 [SQL Server], 보안 주체"
  - "##MS_SQLAuthenticatorCertificate##"
  - "보안 주체 [SQL Server]"
  - "##MS_SQLResourceSigningCertificate##"
  - "그룹 [SQL Server], 보안 주체"
  - "##MS_AgentSigningCertificate##"
  - "인증 [SQL Server], 보안 주체"
  - "스키마 [SQL Server], 보안 주체"
  - "보안 주체 [SQL Server], 보안 주체 정보"
  - "보안 [SQL Server], 보안 주체"
  - "사용자 [SQL Server], 보안 주체"
  - "##MS_SQLReplicationSigningCertificate##"
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
caps.latest.revision: 57
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# 보안 주체(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  *보안 주체* 는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스를 요청할 수 있는 엔터티입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 권한 부여 모델의 다른 구성 요소와 같이 보안 주체는 계층으로 정렬될 수 있습니다. 보안 주체의 영향 범위는 보안 주체의 정의 범위인 Windows, 서버 및 데이터베이스와 보안 주체가 분해 불가능하거나 컬렉션인지 여부에 따라 달라집니다. 분해 불가능한 보안 주체의 예로는 Windows 로그인을 들 수 있으며 Windows 그룹은 컬렉션인 보안 주체입니다. 모든 보안 주체에는 SID(보안 식별자)가 있습니다.  
  
 **Windows 수준의 보안 주체**  
  
-   Windows 도메인 로그인  
  
-   Windows 로컬 로그인  
  
 **SQL Server**-**수준의** **principals**  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인  
  
-   서버 역할  
  
 **데이터베이스 수준의 보안 주체**  
  
-   데이터베이스 사용자  
  
-   데이터베이스 역할  
  
-   응용 프로그램 역할  
  
## SQL Server sa 로그인  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sa 로그인은 서버 수준 보안 주체로서 인스턴스를 설치하면 기본적으로 생성됩니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터는 sa의 기본 데이터베이스가 master입니다. 이 동작은 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 변경되었습니다.  
  
## public 데이터베이스 역할  
 모든 데이터베이스 사용자는 public 데이터베이스 역할에 속합니다. 사용자에게 보안 개체에 대한 특정 사용 권한이 부여되지 않았거나 거부된 경우 사용자는 해당 보안 개체에 대해 public으로 부여된 사용 권한을 상속 받습니다.  
  
## INFORMATION_SCHEMA 및 sys  
 모든 데이터베이스에는 카탈로그 뷰에 사용자로 표시되는 두 엔터티인 INFORMATION_SCHEMA와 sys가 포함됩니다. 이러한 엔터티는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 필요합니다. 엔터티는 보안 주체가 아니며 수정 또는 삭제할 수 없습니다.  
  
## 인증서 기반 SQL Server 로그인  
 이름이 이중 해시 표시(##)로 묶인 서버 보안 주체는 내부 시스템 용도로만 사용됩니다. 다음 보안 주체는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 설치할 때 인증서에서 생성되며 삭제하면 안 됩니다.  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## guest 사용자  
 각 데이터베이스에는 **guest**가 포함되어 있습니다. **guest** 사용자에게 부여된 권한은 데이터베이스에 대한 액세스 권한이 있지만 데이터베이스에 사용자 계정이 없는 사용자가 상속합니다. **guest** 사용자는 삭제할 수 없지만 **CONNECT** 권한을 취소하여 해제할 수 있습니다. master 또는 tempdb가 아닌 임의의 데이터베이스 내에서 `REVOKE CONNECT FROM GUEST`를 실행하여 **CONNECT** 권한을 취소할 수 있습니다.  
  
## 클라이언트 및 데이터베이스 서버  
 정의에 따르면 클라이언트 및 데이터베이스 서버는 보안 주체이며 보안을 설정할 수 있습니다. 이러한 항목은 보안 네트워크 연결이 설정되기 전에 상호 인증될 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 클라이언트가 네트워크 인증 서비스와 상호 작용하는 방법을 정의하는 [Kerberos](http://go.microsoft.com/fwlink/?LinkId=100758) 인증 프로토콜을 지원합니다.  
  
## 관련 태스크  
 권한 시스템 디자인에 대한 정보는 [Getting Started with Database Engine Permissions](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)을(를) 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서 섹션에는 다음과 같은 항목이 포함되어 있습니다.  
  
-   [로그인, 사용자 및 스키마 관리 방법 도움말 항목](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [서버 수준 역할](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [데이터베이스 수준 역할](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [응용 프로그램 역할](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## 참고 항목  
 [SQL Server 보안 설정](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [서버 수준 역할](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [데이터베이스 수준 역할](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  