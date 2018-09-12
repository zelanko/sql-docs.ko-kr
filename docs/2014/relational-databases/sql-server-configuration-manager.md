---
title: SQL Server 구성 관리자 | Microsoft 문서
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], managing
- network protocols [SQL Server], managing
- Client Network Utility
- accounts [SQL Server]
- SQL Server Configuration Manager
- Server Network Utility
- accounts [SQL Server], services
- services [SQL Server], managing
- tools [SQL Server], SQL Server Configuration Manager
- configuration manager [SQL Server]
ms.assetid: e6beaea4-164c-4078-95ae-b9e28b0aefe8
caps.latest.revision: 43
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: af29597b57e0268b87dae428905d981c3d7b4737
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814929"
---
# <a name="sql-server-configuration-manager"></a>SQL Server 구성 관리자
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]와 연관된 서비스를 관리하고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 사용되는 네트워크 프로토콜을 구성하며 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 클라이언트 컴퓨터에서 네트워크 연결 구성을 관리하기 위한 도구입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자는 시작 메뉴에서 사용할 수 있거나 다른 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console 표시에 추가할 수 있는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console 스냅인입니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (mmc.exe) 열려면 Windows System32 폴더의 SQLServerManager10.msc 파일을 사용 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager입니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자 및 SQL Server Management Studio는 WMI(Window Management Instrumentation)를 사용하여 일부 서버 설정을 확인 및 변경합니다. WMI는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구에 의해 요청된 레지스트리 작업을 관리하는 API 호출과 상호 작용하고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자 스냅인 구성 요소의 선택된 SQL 서비스에 대한 향상된 제어 및 조작을 제공하기 위한 통합된 방법을 제공합니다. WMI와 관련된 사용 권한을 구성하는 방법에 대한 자세한 내용은 [WMI를 구성하여 SQL Server 도구에 서버 상태 표시](../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자는 최신 버전의 Windows에서 응용 프로그램으로 표시되지 않습니다.  
>   
>  -   **Windows 10**:  
>          열려는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager에는 **시작 페이지**, sqlservermanager12.msc (에 대 한 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]). 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 12를 더 적은 수로 바꿉니다. SQLServerManager12.msc를 클릭 하면 Configuration Manager 열립니다. 구성 관리자를 시작 페이지나 작업 표시줄을 고정 하려면 SQLServerManager12.msc를 마우스 오른쪽 단추로 클릭 하 고 클릭 **파일 위치 열기**합니다. Windows 파일 탐색기에서 SQLServerManager12.msc를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 화면에 고정** 하거나 **작업 표시줄에 고정**합니다.  
> -   **Windows 8**:  
>          열려는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager에서의 **검색** 참의 **앱**, 형식 **SQLServerManager\<버전 >.msc** 등`SQLServerManager12.msc`를 누릅니다 **Enter**합니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 다른 컴퓨터에서 서비스를 시작, 중지, 일시 중지, 재개 또는 구성하려면 [다른 컴퓨터에 연결&#40;SQL Server 구성 관리자&#41;](../database-engine/configure-windows/scm-services-connect-to-another-computer.md)을 참조하세요.  
  
## <a name="managing-services"></a>서비스 관리  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 서비스를 시작, 일시 중지, 재개 또는 중지하거나 서비스 속성을 확인하거나 서비스 속성을 변경할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 시작 매개 변수를 통해 [!INCLUDE[ssDE](../includes/ssde-md.md)]을 시작할 수 있습니다.  자세한 내용은 [서버 시작 옵션 구성&#40;SQL Server 구성 관리자&#41;](../database-engine/configure-windows/scm-services-configure-server-startup-options.md)을 참조하세요.  
  
## <a name="changing-the-accounts-used-by-the-services"></a>서비스에 사용되는 계정 변경  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스를 관리합니다.  
  
> [!IMPORTANT]  
>  항상 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자와 같은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 서비스에 사용되는 계정을 변경하거나 계정의 암호를 변경할 수 있습니다. 계정 이름을 변경하는 것 외에도 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자는 새 계정이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설정을 읽을 수 있도록 Windows 레지스트리에서 사용 권한을 설정하는 등의 추가 구성을 수행합니다. Windows 서비스 제어 관리자와 같은 다른 도구는 계정 이름을 변경할 수 있지만 연관된 설정은 변경할 수 없습니다. 서비스는 레지스트리의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 부분에 액세스할 수 없는 경우 제대로 시작되지 않을 수 있습니다.  
  
 또한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자, SMO 또는 WMI를 사용하여 변경한 암호는 서비스를 다시 시작할 필요 없이 즉시 적용된다는 이점이 있습니다.  
  
## <a name="manage-server--client-network-protocols"></a>서버 및 클라이언트 네트워크 프로토콜 관리  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용하면 서버 및 클라이언트 네트워크 프로토콜과 연결 옵션을 구성할 수 있습니다. 올바른 프로토콜을 설정한 후에는 일반적으로 서버 네트워크 연결을 변경할 필요가 없습니다. 그러나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 특정 네트워크 프로토콜, 포트 또는 파이프를 수신 대기하도록 서버 연결을 다시 구성해야 할 경우에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용할 수 있습니다. 프로토콜을 사용하도록 설정하는 방법에 대한 자세한 내용은 [서버 네트워크 프로토콜 설정 또는 해제](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)를 참조하세요. 방화벽을 통해 프로토콜에 대한 액세스를 사용하도록 설정하는 방법에 대한 자세한 내용은 [SQL Server 액세스를 허용 하도록 Windows 방화벽 구성](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용하면 프로토콜 암호화를 강제하거나 별칭 속성을 확인하거나 프로토콜을 설정/해제하는 기능을 비롯하여 서버 및 클라이언트 네트워크 프로토콜을 관리할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용하면 별칭을 작성 또는 제거하거나 프로토콜이 사용되는 순서를 변경하거나 다음을 비롯한 서버 별칭의 속성을 볼 수 있습니다.  
  
-   서버 별칭 - 클라이언트가 연결되는 컴퓨터에 사용되는 서버 별칭입니다.  
  
-   프로토콜 - 구성 항목에 사용되는 네트워크 프로토콜입니다.  
  
-   연결 매개 변수 - 네트워크 프로토콜 구성을 위한 연결 주소와 연관된 매개 변수입니다.  
  
 서비스를 시작 및 중지하는 등의 일부 동작에 클러스터 관리자를 사용해야 하지만 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 장애 조치(failover) 클러스터 인스턴스에 대한 정보를 볼 수도 있습니다.  
  
### <a name="available-network-protocols"></a>사용 가능한 네트워크 프로토콜  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 공유 메모리, TCP/IP 및 명명된 파이프 프로토콜을 지원합니다. 네트워크 프로토콜을 선택하는 방법은 [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md)을 참조하세요. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 VIA, Banyan VINES SPP(Sequenced Packet Protocol), 멀티프로토콜, AppleTalk 또는 NWLink IPX/SPX 네트워크 프로토콜이 지원되지 않습니다. 이전에 이러한 프로토콜을 사용하여 연결된 클라이언트는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 연결하기 위해 다른 프로토콜을 선택해야 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 WinSock 프록시를 구성할 수 없습니다. WinSock 프록시를 구성하려면 ISA 서버 설명서를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [서비스 관리 방법 도움말 항목&#40;SQL Server 구성 관리자&#41;](../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
 [SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
 [SQL Server 인스턴스를 자동으로 시작하도록 설정&#40;SQL Server 구성 관리자&#41;](../database-engine/configure-windows/scm-services-set-an-instance-to-start-automatically.md)  
  
 [SQL Server 인스턴스의 자동 시작 방지&#40;SQL Server 구성 관리자&#41;](../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)  
  
  
