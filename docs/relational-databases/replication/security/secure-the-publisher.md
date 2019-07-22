---
title: 게시자 보안 설정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- Publishers [SQL Server replication], security
- publications [SQL Server replication], security
ms.assetid: 4513a18d-dd6e-407a-b009-49dc9432ec7e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3784135455a29d3d1662793d743d9d788e64b5f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095642"
---
# <a name="secure-the-publisher"></a>게시자 보안 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  게시자에 연결하는 복제 에이전트는 다음과 같습니다.  
  
-   로그 판독기 에이전트  
  
-   스냅샷 에이전트  
  
-   큐 판독기 에이전트  
  
-   병합 에이전트  
  
 이러한 에이전트에 적절한 로그인을 제공하고 필요한 최소 권한만 부여하는 원칙을 따르며 모든 암호 스토리지를 보호하는 것이 좋습니다. 각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
 로그인과 암호를 적절하게 관리하는 것 외에도 PAL(게시 액세스 목록)의 역할을 이해해야 합니다. PAL은 게시자에서 데이터베이스에 대한 임의 액세스를 제한하면서 로그인에 게시 데이터에 대한 액세스 권한을 설정하는 데 사용됩니다.  
  
## <a name="publication-access-list"></a>게시 액세스 목록  
 PAL은 게시자의 게시 보안을 유지하는 기본 메커니즘입니다. PAL 기능은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 액세스 제어 목록과 유사하게 작동합니다. 게시를 만들면 복제에서 게시에 대한 PAL을 만듭니다. 게시에 대한 액세스 권한이 부여된 로그인 및 그룹 목록을 포함하도록 PAL을 구성할 수 있습니다. 에이전트가 게시자나 배포자에 연결한 다음 게시에 대한 액세스를 요청하면 PAL의 인증 정보가 에이전트에서 제공한 게시자 로그인과 비교됩니다. 이 프로세스는 클라이언트 도구가 게시자에서 직접 수정 작업을 수행하는 데 게시자 및 배포자 로그인을 사용하지 못하도록 방지하여 게시자에 대한 보안을 강화합니다.  
  
> [!NOTE]  
>  복제는 각 게시의 게시자에 PAL 멤버 자격을 적용할 역할을 만듭니다. 역할 이름은 병합 복제의 경우 **Msmerge_**_\<PublicationID&gt;_ 형식으로 지정되고 트랜잭션 및 스냅샷 복제의 경우 **MSReplPAL_**_\<PublicationDatabaseID&gt;_**_**_\<PublicationID&gt;_ 형식으로 지정됩니다.  
  
 기본적으로 PAL에는 게시 생성 시의 **sysadmin** 고정 서버 역할의 멤버와 게시를 만드는 데 사용된 로그인이 포함됩니다. 기본적으로 게시 데이터베이스에서 **sysadmin** 고정 서버 역할이나 **db_owner** 고정 데이터베이스 역할의 멤버인 모든 로그인은 PAL에 명시적으로 추가하지 않아도 게시를 구독할 수 있습니다.  
  
 PAL을 사용하는 경우에는 다음 지침을 유의하십시오.  
  
-   PAL에 로그인을 추가하려면 먼저 게시 데이터베이스의 데이터베이스 사용자와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인을 연결해야 합니다.  
  
-   PAL의 로그인에 복제 태스크 수행에 필요한 권한만 허용하는 최소 권한 원칙을 따릅니다. 복제 시 필요 없는 고정 데이터베이스 역할이나 서버 역할에 로그인을 추가하지 마십시오. 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) 및 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)을 참조하십시오.  
  
-   원격 배포자를 사용할 경우 PAL의 계정을 게시자와 배포자에서 모두 사용할 수 있어야 합니다. 이 계정은 두 서버 모두에 정의된 도메인 계정이나 로컬 계정이어야 합니다. 또한 두 로그인과 연결된 암호는 같아야 합니다.  
  
-   PAL에 Windows 계정이 포함되어 있고 도메인에서 Active Directory를 사용할 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 실행하는 계정에 Active Directory에서 읽을 수 있는 권한이 있어야 합니다. Windows 계정에 문제가 발생하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 실행하는 계정에 충분한 사용 권한이 있는지 확인합니다. 자세한 내용은 Windows 설명서를 참조하십시오.  
  
 PAL을 관리하려면 [게시 액세스 목록에서 로그인 관리](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)를 참조하세요.  
  
## <a name="snapshot-agent"></a>스냅샷 에이전트  
 각 게시에 하나의 스냅샷 에이전트가 있습니다. 자세한 내용은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
## <a name="ftp-snapshot-delivery"></a>FTP 스냅샷 배달  
 UNC 공유가 아닌 FTP 공유를 통해서만 스냅샷을 사용할 수 있도록 지정한 경우 FTP 액세스를 구성할 때 로그인과 암호를 지정해야 합니다. 자세한 내용은 [FTP를 통해 스냅샷 배달](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)을 참조하세요.  
  
## <a name="log-reader-agent"></a>로그 판독기 에이전트  
 트랜잭션 복제에 대해 게시된 각 데이터베이스에 하나의 로그 판독기 에이전트가 있습니다. 자세한 내용은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
## <a name="queue-reader-agent"></a>큐 판독기 에이전트  
 지정된 배포자와 관련된 모든 게시자와 게시(지연 업데이트 구독 허용)에 하나의 큐 판독기 에이전트가 있습니다. 자세한 내용은 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [복제 보안 설정 보기 및 수정](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
