---
title: 데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], firewall systems
- firewall systems, [Database Engine]
- security [SQL Server], firewalls
ms.assetid: 0093b43c-c6b5-4574-9b30-3a0e91e1a1f9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6e0eafd8a8eb1d9d73f71ab069dc8bf0795a87bc
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640054"
---
# <a name="configure-a-windows-firewall-for-database-engine-access"></a>데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성
  이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 데이터베이스 엔진 액세스에 대한 Windows 방화벽을 구성하는 방법에 대해 설명합니다. 방화벽 시스템은 컴퓨터 리소스에 대한 무단 액세스를 방지합니다. 방화벽을 통해 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 액세스하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행하는 컴퓨터에서 액세스를 허용하도록 방화벽을 구성해야 합니다.  
  
 기본 Windows 방화벽 설정 방법과 [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services 및 Integration Services에 영향을 주는 TCP 포트에 대한 설명은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요. 사용할 수 있는 방화벽 시스템은 여러 가지가 있습니다. 사용 중인 시스템에 해당하는 설명은 방화벽 설명서를 참조하세요.  
  
 액세스를 허용하는 주요 단계는 다음과 같습니다.  
  
1.  특정 TCP/IP 포트를 사용하도록 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 구성합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 기본 인스턴스에서는 포트 1433을 사용하지만 이 포트는 변경할 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 사용하는 포트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 나열됩니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 인스턴스, [!INCLUDE[ssEW](../../includes/ssew-md.md)] 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 명명된 인스턴스에서는 동적 포트를 사용합니다. 특정 포트를 사용하도록 이러한 인스턴스를 구성하려면 [특정 TCP 포트로 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](configure-a-server-to-listen-on-a-specific-tcp-port.md)을 참조하세요.  
  
2.  권한 있는 사용자 또는 컴퓨터에 해당 포트에 대한 액세스를 허용하도록 방화벽을 구성합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 사용하면 사용자가 포트 번호를 몰라도 포트 1433에서 수신하지 않는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser를 사용하려면 UDP 포트 1434를 열어야 합니다. 가장 안전한 환경으로 승격하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 중지하고 해당 포트 번호를 사용하여 연결하도록 클라이언트를 구성합니다.  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows에서는 포트 1433을 닫아 인터넷 컴퓨터가 사용자 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 없도록 하는 Windows 방화벽을 사용합니다. 포트 1433을 다시 열 때까지 TCP/IP를 사용하여 기본 인스턴스에 연결할 수 없습니다. Windows 방화벽 구성을 위한 기본적인 단계는 다음 절차에서 볼 수 있습니다. 자세한 내용은 Windows 설명서를 참조하십시오.  
  
 고정 포트에서 수신하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성하고 포트를 여는 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 파일(Sqlservr.exe)을 차단된 프로그램의 예외로 표시할 수 있습니다. 동적 포트를 계속 사용하려는 경우 이 방법을 사용합니다. 이렇게 하면 하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에만 액세스할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **데이터베이스 엔진 액세스에 대한 Windows 방화벽을 구성하려면:**  
  
     [SQL Server 구성 관리자](#SSMSProcedure)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
 방화벽의 포트를 열면 서버가 악의적인 공격에 노출될 수 있습니다. 포트를 열기 전에 방화벽 시스템을 잘 이해해야 합니다. 자세한 내용은 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)를 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
 Windows Vista, Windows 7 및 Windows Server 2008에 적용됩니다.  
  
 다음 절차에서는 고급 보안이 설정된 Windows 방화벽 MMC(Microsoft Management Console) 스냅인을 사용하여 Windows 방화벽을 구성합니다. 고급 보안이 설정된 Windows 방화벽은 현재 프로필만 구성할 수 있습니다. 고급 보안이 포함된 Windows 방화벽에 대한 자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access"></a>Windows 방화벽에서 TCP 액세스용 포트를 열려면  
  
1.  **시작** 메뉴에서 **실행**을 클릭한 다음 **WF.msc**를 입력하고 **확인**을 클릭합니다.  
  
2.  **고급 보안이 포함된 Windows 방화벽**의 왼쪽 창에서 **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음 작업 창에서 **새 규칙** 을 클릭합니다.  
  
3.  **규칙 유형** 대화 상자에서 **포트**를 선택한 다음 **다음**을 클릭합니다.  
  
4.  **프로토콜 및 포트** 대화 상자에서 **TCP**를 선택합니다. 선택 **특정 로컬 포트**, 인스턴스의 포트 번호를 입력 하 고는 [!INCLUDE[ssDE](../../includes/ssde-md.md)], 같은 `1433` 기본 인스턴스에 대 한 합니다. **다음**을 클릭합니다.  
  
5.  **동작** 대화 상자에서 **연결 허용**을 선택한 다음 **다음**을 클릭합니다.  
  
6.  **프로필** 대화 상자에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결할 때의 컴퓨터 연결 환경을 설명하는 프로필을 선택한 다음 **다음**을 클릭합니다.  
  
7.  **이름** 대화 상자에 이 규칙의 이름 및 설명을 입력한 다음 **마침**을 클릭합니다.  
  
#### <a name="to-open-access-to-sql-server-when-using-dynamic-ports"></a>동적 포트 사용 시 SQL Server에 대한 액세스를 열려면  
  
1.  **시작** 메뉴에서 **실행**을 클릭한 다음 **WF.msc**를 입력하고 **확인**을 클릭합니다.  
  
2.  **고급 보안이 포함된 Windows 방화벽**의 왼쪽 창에서 **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음 작업 창에서 **새 규칙** 을 클릭합니다.  
  
3.  **규칙 유형** 대화 상자에서 **프로그램**을 선택한 다음 **다음**을 클릭합니다.  
  
4.  **프로그램** 대화 상자에서 **다음 프로그램 경로**를 선택합니다. **찾아보기**를 클릭하여 방화벽을 통해 액세스할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 찾은 다음 **열기**를 클릭합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 **C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn\Sqlservr.exe**합니다. **다음**을 클릭합니다.  
  
5.  **동작** 대화 상자에서 **연결 허용**을 선택한 다음 **다음**을 클릭합니다.  
  
6.  **프로필** 대화 상자에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결할 때의 컴퓨터 연결 환경을 설명하는 프로필을 선택한 다음 **다음**을 클릭합니다.  
  
7.  **이름** 대화 상자에 이 규칙의 이름 및 설명을 입력한 다음 **마침**을 클릭합니다.  
  
  
