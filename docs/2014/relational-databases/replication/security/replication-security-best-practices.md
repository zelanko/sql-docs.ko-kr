---
title: 복제 보안을 위한 최선의 구현 방법 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], best practices
- security [SQL Server replication], between domains
- authentication [SQL Server replication]
- Internet [SQL Server replication], security
ms.assetid: 1ab2635d-0992-4c99-b17d-041d02ec9a7c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: db577e8f3d248945db67610404ad4093d46a0430
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066573"
---
# <a name="replication-security-best-practices"></a>복제 보안을 위한 최선의 구현 방법
  단일 도메인의 인트라넷에서부터 트러스트되지 않은 도메인 간이나 인터넷을 통해 데이터에 액세스하는 애플리케이션에 이르기까지의 분산 환경에서 복제는 데이터를 이동합니다. 따라서 이러한 다양한 환경에서 복제 연결의 보안을 유지하는 최선의 방법을 이해하는 것이 중요합니다.  
  
 다음 정보는 모든 환경에서의 복제와 관련이 있습니다.  
  
-   VPN(가상 프라이빗 네트워크), SSL(Secure Sockets Layer) 또는 IPSEC(IP 보안)과 같은 산업 표준 방법을 사용하여 복제 토폴로지의 컴퓨터 간 연결을 암호화합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요. VPN 및 SSL을 사용하여 인터넷에서 데이터를 복제하는 방법은 [Securing Replication Over the Internet](securing-replication-over-the-internet.md)을 참조하십시오.  
  
     SSL을 사용하여 복제 토폴로지에서 컴퓨터 간의 연결 보안을 유지하는 경우 각 복제 에이전트의 **-EncryptionLevel** 매개 변수 값을 **1** 또는 **2** 로 지정합니다(값 **2** 가 권장됨). 값 **1** 을 지정하면 암호화가 사용되지만 에이전트에서 SSL 서버 인증서가 신뢰할 수 있는 발급자에 의해 서명된 것인지 확인하지는 않습니다. 값 **2** 를 지정하면 인증서가 확인됩니다. 에이전트 프로필 및 명령줄에서 에이전트 매개 변수를 지정할 수 있습니다. 자세한 내용은 다음을 참조하세요.  
  
    -   [복제 에이전트 프로필 작업](../agents/replication-agent-profiles.md)  
  
    -   [복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정&#40;SQL Server Management Studio&#41;](../agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)  
  
-   각 복제 에이전트를 서로 다른 Windows 계정으로 실행하고 모든 복제 에이전트 연결에 Windows 인증을 사용합니다. 계정 지정에 대한 자세한 내용은 [복제의 로그인 및 암호 관리](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)를 참조하세요.  
  
-   각 에이전트에 필요한 사용 권한만 부여합니다. 자세한 내용은 [Replication Agent Security Model](replication-agent-security-model.md)의 "에이전트에 필요한 사용 권한" 섹션을 참조하십시오.  
  
-   모든 병합 에이전트 및 배포 에이전트 계정이 PAL(게시 액세스 목록)에 있는지 확인합니다. 자세한 내용은 [게시자 보안 설정](secure-the-publisher.md)을 참조하세요.  
  
-   PAL의 각 계정에 복제 태스크를 수행하는 데 필요한 사용 권한만 허용하여 최소 권한의 원칙을 따릅니다. 복제에 필요하지 않은 고정 서버 역할에 로그인을 추가하지 마십시오.  
  
-   스냅샷 공유에서 모든 병합 에이전트와 배포 에이전트의 읽기 권한을 허용하도록 구성합니다. 매개 변수가 있는 필터를 포함한 게시에 대한 스냅샷의 경우 각 폴더에서 해당 병합 에이전트 계정에만 액세스를 허용하도록 구성해야 합니다.  
  
-   스냅샷 공유에서 스냅샷 에이전트의 쓰기 권한을 허용하도록 구성합니다.  
  
-   끌어오기 구독을 사용하는 경우 스냅샷 폴더에 로컬 경로가 아닌 네트워크 공유를 사용합니다.  
  
 복제 토폴로지에 동일한 도메인에 있지 않거나 서로 트러스트 관계가 구축되지 않은 도메인에 있는 컴퓨터가 포함되어 있으면 에이전트 연결에 대해 Windows 인증이나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용할 수 있습니다. 도메인에 대한 자세한 내용은 Windows 설명서를 참조하십시오. 최상의 권장 보안 방법은 Windows 인증을 사용하는 것입니다.  
  
-   Windows 인증을 사용하려면  
  
    -   각 에이전트에 대한 로컬 Windows 계정(도메인 계정 아님)을 해당 노드에 추가합니다. 각 노드에서 동일한 이름과 암호를 사용합니다. 예를 들어 밀어넣기 구독의 배포 에이전트는 배포자에서 실행되며 배포자와 구독자에 연결합니다. 배포 에이전트에 대한 Windows 계정은 배포자와 구독자에 추가해야 합니다.  
  
    -   지정된 에이전트(예: 구독에 대한 배포 에이전트)가 각 컴퓨터에서 동일한 계정으로 실행되는지 확인합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하려면  
  
    -   각 에이전트에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 계정을 해당 노드에 추가합니다. 각 노드에서 동일한 계정 이름과 암호를 사용합니다. 예를 들어 밀어넣기 구독의 배포 에이전트는 배포자에서 실행되며 배포자와 구독자에 연결합니다. 배포 에이전트에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 계정은 배포자와 구독자에 추가해야 합니다.  
  
    -   지정된 에이전트(예: 구독에 대한 배포 에이전트)가 각 컴퓨터에서 동일한 계정으로 연결하는지 확인합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증이 필요한 환경에서는 UNC 스냅샷 공유에 액세스할 수 없는 경우가 많습니다. 예를 들어 방화벽에서 액세스를 차단할 수 있습니다. 이 경우 FTP(파일 전송 프로토콜)를 통해 스냅샷을 구독자에게 전송할 수 있습니다. 자세한 내용은 [FTP를 통해 스냅샷 전송](../transfer-snapshots-through-ftp.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [인터넷을 통한 복제](../replication-over-the-internet.md)   
 [구독자 보안 설정](secure-the-subscriber.md)   
 [배포자 보안 설정](secure-the-distributor.md)   
 [게시자 보안 설정](secure-the-publisher.md)   
 [SQL Server 복제 보안](view-and-modify-replication-security-settings.md)  
  
  
