---
title: "네트워크 프로토콜 및 네트워크 라이브러리 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- protocols [SQL Server]
- configuration options [SQL Server], protocols
- network libraries [SQL Server]
- protocols [SQL Server], about network protocols
- pipes [SQL Server]
- network protocols [SQL Server]
- default SQL Server configurations
- library [SQL Server]
- network protocols [SQL Server], about network protocols
- configuration options [SQL Server], libraries
ms.assetid: 8cd437f6-9af1-44ce-9cb0-4d10c83da9ce
caps.latest.revision: 50
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aac8ea2ddd6582529952398f3896f548d8117078
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="network-protocols-and-network-libraries"></a>네트워크 프로토콜 및 네트워크 라이브러리
  서버는 한 번에 여러 네트워크 프로토콜을 수신하거나 모니터링할 수 있습니다. 이때 각각의 프로토콜을 구성해야 합니다. 특정 프로토콜을 구성하지 않으면 서버가 해당 프로토콜에서 수신할 수 없습니다. 설치 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 프로토콜 구성을 변경할 수 있습니다.  
  
## <a name="default-sql-server-network-configuration"></a>기본 SQL Server 네트워크 구성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기본 인스턴스는 TCP/IP 포트 1433 및 명명된 파이프 \\\\.\pipe\sql\query에 대해 구성됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명명된 인스턴스는 포트 번호가 운영 체제에서 할당되는 TCP 동적 포트로 구성됩니다.  
  
 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결이 특정 포트 주소를 통과하도록 구성된 방화벽 서버를 통과해야 하는 경우와 같이 동적 포트 주소를 사용할 수 없는 경우에는 할당되지 않은 포트 번호를 선택합니다. 포트 번호 할당은 Internet Assigned Numbers Authority에서 관리하며 이 목록은 [http://www.iana.org](http://go.microsoft.com/fwlink/?LinkId=48844)에서 볼 수 있습니다.  
  
 보안을 향상시키기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치될 때 네트워크 연결이 부분적으로만 설정됩니다. 설치가 완료된 후 네트워크 프로토콜을 설정, 해제 및 구성하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 구성 영역을 사용합니다.  
  
## <a name="server-message-block-protocol"></a>서버 메시지 블록 프로토콜  
 경계 네트워크에 연결된 서버는 SMB(서버 메시지 블록)를 포함해 불필요한 모든 프로토콜을 비활성화해야 합니다. 웹 서버 및 DNS(Domain Name System) 서버에는 SMB가 필요 없습니다. 이 프로토콜은 사용자 목록 노출 위협에 대비하여 비활성화되어야 합니다.  
  
> [!WARNING]  
>  서버 메시지 블록을 사용하지 않도록 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Windows 클러스터 서비스가 원격 파일 공유에 액세스할 수 없습니다. 다음 중 하나를 수행하거나 계획 중인 경우 SMB를 사용하지 않도록 설정하지 마세요.  
>   
>  -   Windows 클러스터 노드 및 파일 공유 주 쿼럼 모드 사용  
> -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 SMB 파일 공유를 데이터 디렉터리로 지정  
> -   SMB 파일 공유에 데이터베이스 파일 만들기  
  
#### <a name="to-disable-smb"></a>SMB를 비활성화하려면  
  
1.  **시작** 메뉴에서 **설정**을 가리킨 다음 **네트워크 및 전화 접속 연결**을 클릭합니다.  
  
     인터넷 연결을 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
2.  **Microsoft 네트워크용 클라이언트** 확인란을 선택한 다음 **제거**를 클릭합니다.  
  
3.  제거 단계를 따릅니다.  
  
4.  **Microsoft 네트워크용 파일 및 프린터 공유**를 선택한 다음 **제거**를 클릭합니다.  
  
5.  제거 단계를 따릅니다.  
  
#### <a name="to-disable-smb-on-servers-accessible-from-the-internet"></a>인터넷에서 액세스 가능한 서버의 SMB를 비활성화하려면  
  
-   로컬 영역 연결 속성에서 **인터넷 프로토콜(TCP/IP) 속성** 대화 상자를 사용하여 **Microsoft 네트워크용 파일 및 프린터 공유** 및 **Microsoft 네트워크용 클라이언트**를 제거합니다.  
  
## <a name="endpoints"></a>끝점  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결에 대한 새로운 개념이 도입되었습니다. 즉, 연결이 서버 끝에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]*끝점*으로 표시됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 끝점에 대해 사용 권한을 부여, 취소 및 거부할 수 있습니다. 기본적으로 모든 사용자는 sysadmin 그룹의 멤버나 끝점 소유자에 의해 사용 권한이 거부 또는 취소되지 않은 한 끝점에 액세스할 권한이 있습니다. GRANT, REVOKE 및 DENY ENDPOINT 구문에는 관리자가 끝점의 카탈로그 뷰에서 가져와야 하는 끝점 ID가 사용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서는 지원되는 모든 네트워크 프로토콜뿐만 아니라 관리자 전용 연결에 대해서도 [!INCLUDE[tsql](../../includes/tsql-md.md)] 끝점을 만듭니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 설치 프로그램에서 만드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 끝점은 다음과 같습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 로컬 컴퓨터  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 명명된 파이프  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 기본 TCP  
  
 끝점에 대한 자세한 내용은 [여러 TCP 포트에서 수신하도록 데이터베이스 엔진 구성](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md) 및 [끝점 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 구성에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 다음 항목을 참조하십시오.  
  
-   [서버 네트워크 구성](../../database-engine/configure-windows/server-network-configuration.md)  
  
## <a name="see-also"></a>참고 항목  
 [노출 영역 구성](../../relational-databases/security/surface-area-configuration.md)   
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)  
  
  
