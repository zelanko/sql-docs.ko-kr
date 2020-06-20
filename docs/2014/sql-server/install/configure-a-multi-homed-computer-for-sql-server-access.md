---
title: SQL Server 액세스를 허용하도록 다중 홈 컴퓨터 구성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], multi-homed computer
- multi-homed computer [SQL Server] configuring ports
- firewall systems [Database Engine], multi-homed computer
ms.assetid: ba369e5b-7d1f-4544-b7f1-9b098a1e75bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 97ba04b8d41c3e5ca4927abb53cf27cfa3013fcd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036987"
---
# <a name="configure-a-multi-homed-computer-for-sql-server-access"></a>SQL Server 액세스를 허용하도록 다중 홈 컴퓨터 구성
  한 서버에서 두 개 이상의 네트워크 또는 네트워크 서브넷으로의 연결을 제공해야 할 경우 다중 홈 컴퓨터를 사용하는 것이 일반적인 시나리오입니다. 이 컴퓨터는 경계 네트워크(DMZ(완충 영역) 또는 스크린된 서브넷이라고도 함)에 있는 경우가 많습니다. 이 항목에서는 다중 홈 환경에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 네트워크 연결을 제공하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 고급 보안이 포함된 Windows 방화벽을 구성하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  다중 홈 컴퓨터는 여러 개의 네트워크 어댑터를 가지고 있거나, 하나의 네트워크 어댑터에 여러 IP 주소를 사용할 수 있도록 구성되어 있습니다. 이중 홈 컴퓨터는 두 개의 네트워크 어댑터를 가지고 있거나, 하나의 네트워크 어댑터에 두 개의 IP 주소를 사용할 수 있도록 구성되어 있습니다.  
  
 이 항목의 내용을 이해하려면 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)항목에 설명되어 있는 내용에 대해 잘 알고 있어야 합니다. 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 방화벽과 함께 사용하는 방법에 대한 기본 정보를 제공합니다.  
  
 **이 예는 다음과 같은 가정을 전제로 합니다.**  
  
-   컴퓨터에 두 개의 네트워크 어댑터가 설치되어 있으며, 하나 또는 두 개 모두 무선일 수 있습니다. 한 네트워크 어댑터의 IP 주소를 사용하고 루프백 IP 주소(127.0.0.1)를 두 번째 네트워크 어댑터로 사용하여 두 개의 네트워크 어댑터를 시뮬레이션할 수 있습니다.  
  
-   간단히 하기 위해 이 예에서는 IPv4 주소를 사용합니다. IPv6 주소를 사용하여 동일한 절차를 수행할 수 있습니다.  
  
    > [!NOTE]  
    >  IPv4 주소는 옥텟이라고 하는 일련의 네 개 숫자로 구성됩니다. 각 숫자는 255 이하이며 점으로 구분됩니다(예: 127.0.0.1). IPv6 주소는 8개의 16진수가 각각 콜론으로 구분되어 있습니다(예: fe80:4898:23:3:49a6:f5c1:2452:b994).  
  
-   방화벽 규칙에서 1433 포트 등과 같은 특정 포트를 통한 액세스를 허용할 수 있습니다. 또는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 프로그램(sqlservr.exe)에 대한 액세스를 허용할 수 있습니다. 둘 중 한 방법이 더 좋은 것은 아닙니다. 경계 네트워크에 있는 서버는 인트라넷에 있는 서버보다 공격으로부터 더 취약하기 때문에 이 항목에서는 포트를 보다 세부적으로 제어하여 열고자 하는 포트를 개별적으로 선택하기로 합니다. 따라서 이 항목에서는 고정 포트에서 수신하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용하는 포트에 대한 자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
-   이 예에서는 TCP 포트 1433을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 대한 액세스를 구성합니다. 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에서 사용하는 다른 포트는 포트를 구성하는 일반적인 절차를 사용하여 구성할 수 있습니다.  
  
 **이 예에서는 다음과 같은 일반 절차를 사용합니다.**  
  
-   컴퓨터의 IP 주소를 확인합니다.  
  
-   특정 TCP 포트에서 수신하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성합니다.  
  
-   고급 보안이 포함된 Windows 방화벽을 구성합니다.  
  
## <a name="optional-procedures"></a>선택적 절차  
 컴퓨터에서 사용할 수 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하고 있는 IP 주소를 알고 있으면 이 절차를 건너뛸 수 있습니다.  
  
#### <a name="to-determine-the-ip-addresses-available-on-the-computer"></a>컴퓨터에서 사용할 수 있는 IP 주소를 확인하려면  
  
1.  가 설치 된 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **시작**, **실행**을 차례로 클릭 하 고를 입력 한 다음을 입력 `cmd` [!INCLUDE[clickOK](../../includes/clickok-md.md)] 합니다.  
  
2.  명령 프롬프트 창에 `ipconfig,`을 입력한 다음 Enter 키를 누르면 해당 컴퓨터에서 사용할 수 있는 IP 주소가 나열됩니다.  
  
    > [!NOTE]  
    >  **ipconfig** 명령은 끊긴 연결까지 포함하여 사용 가능한 많은 연결을 나열하는 경우가 있습니다. **ipconfig** 명령을 사용하여 IPv4와 IPv6 주소 모두를 확인할 수 있습니다.  
  
3.  사용 중인 IPv4 주소와 IPv6 주소를 기록해 둡니다. 임시 주소, 서브넷 마스크 및 기본 게이트웨이 등과 같은 기타 정보는 TCP/IP 네트워크를 구성할 때 중요한 정보입니다. 그러나 이 예에서는 이 정보를 사용하지 않습니다.  
  
#### <a name="to-determine-the-ip-addresses-and-ports-used-by-ssnoversion"></a>사용하는 IP 주소와 포트를 확인하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  **시작**을 클릭하고 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 선택한 다음 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자**를 클릭합니다.  
  
2.  ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager**의 콘솔 창에서 ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 구성**, **에 대 한 \<instance name> 프로토콜 **을 차례로 확장 한 다음 **tcp/ip**를 두 번 클릭 합니다.  
  
3.  **TCP/IP 속성** 대화 상자의 **IP 주소** 탭에 여러 개의 IP 주소가 **IP1**, **IP2**의 형식으로 **IPAll**까지 표시됩니다. 이러한 주소에는 루프백 어댑터의 IP 주소인 127.0.0.1이 포함됩니다. 컴퓨터에 구성된 각 IP 주소에 대한 추가 IP 주소가 나타납니다.  
  
4.  IP 주소의 경우 **TCP 동적 포트** 대화 상자에 **0**이 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 동적 포트에서 수신하고 있음을 나타냅니다. 이 예에서는 컴퓨터를 다시 시작할 때 변경될 수 있는 동적 포트 대신 고정 포트를 사용합니다. 따라서 **TCP 동적 포트** 대화 상자에 **0**이 있으면 0을 삭제합니다.  
  
5.  구성할 각 IP 주소에 대해 나열된 TCP 포트를 기록해 둡니다. 이 예에서는 두 IP 주소 모두 기본 포트 1433에서 수신한다고 가정합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 특정 포트를 사용하지 못하게 하려면 **프로토콜** 탭에서 **모두 수신** 값을 **아니요**로 변경한 후 **IP 주소** 탭에서 사용하지 않으려는 IP 주소에 대해 **활성** 값을 **아니요** 로 변경합니다.  
  
## <a name="configuring-windows-firewall-with-advanced-security"></a>고급 보안이 포함된 Windows 방화벽 구성  
 컴퓨터에서 사용하는 IP 주소와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용하는 포트를 확인했으면 방화벽 규칙을 만들어 특정 IP 주소에 이 규칙을 적용하도록 구성할 수 있습니다.  
  
#### <a name="to-create-a-firewall-rule"></a>방화벽 규칙을 만들려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치된 컴퓨터에서 관리자로 로그온합니다.  
  
2.  **시작**, **실행**을 차례로 클릭 하 `wf.msc` 고를 입력 한 다음 **확인**을 클릭 합니다.  
  
3.  **사용자 계정 컨트롤** 대화 상자에서 **계속** 을 클릭하여 고급 보안이 포함된 Windows 방화벽 스냅인을 관리자 자격 증명으로 엽니다.  
  
4.  **개요** 페이지에서 Windows 방화벽이 사용되고 있는지 확인합니다.  
  
5.  왼쪽 창에서 **인바운드 규칙**을 클릭합니다.  
  
6.  **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 후 **새 규칙** 을 클릭하여 **새 인바운드 규칙 마법사**를 엽니다.  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로그램에 대한 규칙을 만들 수 있습니다. 그러나 이 예에서는 고정 포트를 사용하므로 **포트**를 선택하고 **다음**을 클릭합니다.  
  
8.  **프로토콜 및 포트** 페이지에서 **TCP**를 선택합니다.  
  
9. **지정된 로컬 포트**를 선택합니다. 포트 번호를 쉼표로 구분하여 입력한 후 **다음**을 클릭합니다. 이 예에서는 기본 포트를 구성하므로 `1433`을 입력합니다.  
  
10. **동작** 페이지에서 옵션을 검토합니다. 이 예에서는 방화벽을 사용하여 보안 연결을 적용하지 않습니다. 따라서 **연결 허용**을 클릭한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  환경에 따라 보안 연결이 필요할 수 있습니다. 보안 연결 옵션 중 하나를 선택할 경우 인증서와 **암호화 적용** 옵션을.구성해야 합니다. 보안 연결에 대한 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md) 및 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
11. **프로필** 페이지에서 규칙에 대해 하나 이상의 프로필을 선택합니다. 방화벽 프로필에 대해 잘 모를 경우 방화벽 프로그램에서 **프로필에 대해 자세히 알아봅니다** 링크를 클릭합니다.  
  
    -   컴퓨터가 서버이고 도메인에 연결되었을 때만 사용할 수 있을 경우 **도메인**을 선택하고 **다음**을 클릭합니다.  
  
    -   컴퓨터가 모바일 컴퓨터(랩톱)일 경우 여러 네트워크에 연결할 때 여러 개의 프로필을 사용할 것입니다. 모바일 컴퓨터의 경우 서로 다른 프로필을 위한 여러 개의 액세스 기능을 구성해야 합니다. 예를 들어, 컴퓨터에서 도메인 프로필을 사용할 경우 액세스를 허용하고, 공개 프로필을 사용할 경우에는 액세스를 금지할 수 있습니다.  
  
12. **이름** 페이지에 규칙의 이름과 설명을 입력한 후 **마침**을 클릭합니다.  
  
13. 이 절차를 반복하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용할 각 IP 주소에 대한 규칙을 만듭니다.  
  
 하나 이상의 규칙을 만든 후 다음 단계를 수행하여 컴퓨터의 각 IP 주소에서 규칙을 사용하도록 구성합니다.  
  
#### <a name="to-configure-the-firewall-rule-for-a-specific-ip-addresses"></a>특성 IP 주소에 대한 방화벽 규칙을 구성하려면  
  
1.  **고급 보안이 포함된 Windows 방화벽** 의 **인바운드 규칙**페이지에서 방금 만든 규칙을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **규칙 속성** 대화 상자에서 **범위** 탭을 선택합니다.  
  
3.  **로컬 IP 주소** 영역에서 **다음 IP 주소**를 선택한 다음 **추가**를 클릭합니다.  
  
4.  **IP 주소** 대화 상자에서 **다음 IP 주소 또는 서브넷**을 선택한 다음 구성하려는 IP 주소 중 하나를 입력합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  **원격 IP 주소** 영역에서 **다음 IP 주소**를 선택한 다음 **추가**를 클릭합니다.  
  
7.  **IP 주소** 대화 상자를 사용하여 컴퓨터의 선택된 IP 주소에 대한 연결을 구성합니다. 지정한 IP 주소, IP 주소 범위, 전체 서브넷 또는 특정 컴퓨터의 연결을 활성화할 수 있습니다. 이 옵션을 올바르게 구성하려면 네트워크에 대해 잘 알고 있어야 합니다. 네트워크에 대한 자세한 내용은 네트워크 관리자를 참조하십시오.  
  
8.  **IP 주소** 대화 상자를 닫으려면 **확인**을 클릭합니다. 그런 다음 **확인** 을 클릭하여 **규칙 속성** 대화 상자를 닫습니다.  
  
9. 다중 홈 컴퓨터의 IP 주소를 구성하려면 다른 IP 주소와 다른 규칙을 사용하여 이 절차를 반복합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Browser 서비스&#40;데이터베이스 엔진 및 SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [프록시 서버를 통해 SQL Server에 연결&#40;SQL Server 구성 관리자&#41;](../../relational-databases/sql-server-configuration-manager.md)  
  
  
