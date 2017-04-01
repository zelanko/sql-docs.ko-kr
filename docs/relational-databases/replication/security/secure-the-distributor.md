---
title: "배포자 보안 설정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "보안 [SQL Server 복제], 배포자"
  - "배포자 [SQL Server 복제], 보안"
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 배포자 보안 설정
  배포자에 연결하는 병합 에이전트에는 로그 판독기 에이전트, 스냅숏 에이전트, 큐 판독기 에이전트, 배포 에이전트 및 병합 에이전트가 있습니다. 필요한 최소 권한만 부여하는 원칙을 따르고 모든 암호 저장소를 보호하면서 이러한 에이전트에 적절한 로그인을 제공하는 것이 중요합니다.  
  
-   로그인 및 암호를 관리 하는 방법에 대 한 정보를 참조 하십시오. [복제의 관리 로그인 및 암호](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)합니다.  
  
-   각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
 역할을 이해 하는 로그인 및 암호를 적절 하 게 관리 하는 것 외에도 **repl_distributor** 원격 서버 링크 및 **distributor_admin** 계정.  
  
## 게시자에서 배포자로의 연결 보안  
 를 지원 하기 위해 필요한 통신 관리 저장된 프로시저가 배포자에서 게시자 및 업데이트 정보를 실행 하는 경우 복제가 자동으로 구성 된 원격 서버 **repl_distributor**합니다.  **repl_distributor** 원격 서버 항목이 여부에 관계 없이 배포 데이터베이스의 게시자 인스턴스 (로컬 배포자) 내에 포함 된 원격 내에 상주 하는 배포 데이터베이스에 통신에 사용 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 (원격 배포자).  
  
 배포 데이터베이스가 로컬 인스턴스에 포함되어 있는 경우 임의의 암호가 생성되고 자동으로 구성됩니다. 관리자는 게시자 및 배포자에 설치 하는 동안 공유 암호 구성 배포 데이터베이스를 원격 인스턴스에 있는 경우 이 암호는 다음 통과 하는 트래픽의 인증을 제공 하는 데 사용 됩니다는 **repl_distributor** 링크입니다.  
  
 배포자를 사용 하는 **repl_distributor** 저장 프로시저를 실행 하는 동안 원격 서버 항목 호출 하는 서버가 배포자에서 게시자로 구성 된, 게시자가 제공 하는 암호의 유효성을 검사 하 고 확인 합니다 저장된 프로시저는 복제 인지 유효성을 검사 합니다.  
  
 에 대해 구성 된 암호는 **repl_distributor** 설치 하는 동안 원격 서버 항목은 연결 된는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 **distributor_admin**, 를에 추가 되는 **sysadmin** 배포자에서 고정된 서버 역할입니다.  **distributor_admin** 로그인은 배포자에 연결할 때 복제 저장 프로시저에 사용 됩니다.  
  
> [!NOTE]  
>  에 대 한 암호를 변경 하지 마십시오는 **distributor_admin** 수동으로. 항상 사용 하는 **sp_changedistributor_password** 저장 프로시저를 또는 **배포자 속성** 또는 **복제 암호 업데이트** 대화 상자에 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], 이므로 암호를 로컬에 적용 된 게시 자동으로 변경 합니다.  
  
## 스냅숏 폴더 보안  
 스냅숏 공유에 병합 에이전트(병합 게시의 경우)나 배포 에이전트(스냅숏 또는 트랜잭션 복제의 경우)가 실행되는 계정에 대한 읽기 권한이 있고 스냅숏 에이전트가 실행되는 계정에 대한 쓰기 권한이 있는지 확인합니다. 스냅숏 폴더에 대 한 자세한 내용은 참조 [스냅숏 폴더 보안](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)합니다.  
  
## 참고 항목  
 [복제 보안 설정 보기 및 수정](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [데이터베이스 엔진 및 #40;에 암호화 연결 사용 SQL Server 구성 관리자 및 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [복제 보안을 위한 최선의 구현 방법](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [보안 및 보호 & #40입니다. 복제 및 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  