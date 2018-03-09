---
title: "배포자 보안 설정 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [SQL Server replication], Distributors
- Distributors [SQL Server replication], security
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69919214ba8fae9f6158466482f5b08201ad8afd
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="secure-the-distributor"></a>배포자 보안 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 배포자에 연결하는 병합 에이전트에는 로그 판독기 에이전트, 스냅숏 에이전트, 큐 판독기 에이전트, 배포 에이전트 및 병합 에이전트가 있습니다. 필요한 최소 권한만 부여하는 원칙을 따르고 모든 암호 저장소를 보호하면서 이러한 에이전트에 적절한 로그인을 제공하는 것이 중요합니다.  
  
-   로그인 및 암호 관리에 대한 자세한 내용은 [복제의 로그인 및 암호 관리](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)를 참조하세요.  
  
-   각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
 적절한 로그인 및 암호 관리를 비롯하여 **repl_distributor** 원격 서버 링크 및 **distributor_admin** 계정의 역할도 이해해야 합니다.  
  
## <a name="securing-the-connection-from-the-publisher-to-the-distributor"></a>게시자에서 배포자로의 연결 보안  
 관리 저장 프로시저가 게시자에서 실행되고 배포자에서 정보를 업데이트할 때 필요한 통신을 지원하기 위해 복제는 자동으로 **repl_distributor**원격 서버를 구성합니다. **repl_distributor** 원격 서버 항목은 배포 데이터베이스가 게시자 인스턴스(로컬 배포자) 내에 포함되어 있는지 또는 원격 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스(원격 배포자) 내에 상주하는지 여부에 관계없이 배포 데이터베이스에 대한 통신에 사용됩니다.  
  
 배포 데이터베이스가 로컬 인스턴스에 포함되어 있는 경우 임의의 암호가 생성되고 자동으로 구성됩니다. 배포 데이터베이스가 원격 인스턴스에 있는 경우 관리자는 게시자 및 배포자를 설치하는 동안 공유 암호를 구성합니다. 그런 다음 이 암호는 **repl_distributor** 링크를 통과하는 트래픽의 인증을 제공하는 데 사용됩니다.  
  
 배포자는 **repl_distributor** 원격 서버 항목을 사용하여 호출하는 서버가 배포자에서 게시자로 구성되었는지 확인하고 게시자가 제공한 암호의 유효성을 검사하며 실행 중에 저장 프로시저가 복제 저장 프로시저인지를 확인합니다.  
  
 설치하는 동안 **repl_distributor** 원격 서버 항목에 대해 구성된 암호는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인인 **distributor_admin**과 연결되어 있으며 이 로그인은 배포자에서 **sysadmin** 고정 서버 역할에 추가됩니다. **distributor_admin** 로그인은 복제 저장 프로시저가 배포자에 연결할 때 사용합니다.  
  
> [!NOTE]  
>  **distributor_admin** 에 대한 암호를 수동으로 변경하지 마십시오. 암호를 변경할 때는 항상 **sp_changedistributor_password** 저장 프로시저 또는 **의** 배포자 속성 **이나** 복제 암호 업데이트 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]대화 상자를 사용하십시오. 그러면 암호 변경 내용이 로컬 게시에 자동으로 적용됩니다.  
  
## <a name="snapshot-folder-security"></a>스냅숏 폴더 보안  
 스냅숏 공유에 병합 에이전트(병합 게시의 경우)나 배포 에이전트(스냅숏 또는 트랜잭션 복제의 경우)가 실행되는 계정에 대한 읽기 권한이 있고 스냅숏 에이전트가 실행되는 계정에 대한 쓰기 권한이 있는지 확인합니다. 스냅숏 폴더에 대한 자세한 내용은 [스냅숏 폴더 보안 설정](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [복제 보안 설정 보기 및 수정](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [보안 및 보호&#40;복제&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
