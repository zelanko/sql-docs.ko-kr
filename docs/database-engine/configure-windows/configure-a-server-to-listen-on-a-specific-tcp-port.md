---
title: "특정 TCP 포트에서 수신 대기하도록 서버 구성 | Microsoft Docs"
ms.custom: 
ms.date: 04/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- fixed port
- static ports
- ports [SQL Server], assigning numbers
- assigning port numbers
- dynamic ports [SQL Server]
- TCP/IP [SQL Server], port numbers
ms.assetid: 2276a5ed-ae3f-4855-96d8-f5bf01890640
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: daec5ed8b8ea3aece68c5bcde3522e8e3f9de9f4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="configure-a-server-to-listen-on-a-specific-tcp-port"></a>특정 TCP 포트에서 수신 대기하도록 서버 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 SQL Server 구성 관리자를 사용하여 특정 고정 포트에서 수신할 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스를 구성하는 방법에 대해 설명합니다. 설정된 경우 기본 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스는 TCP 포트 1433에서 수신합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 의 명명된 인스턴스는 [동적 포트](https://msdn.microsoft.com/library/dd981060)로 구성됩니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 시작되면 해당 인스턴스가 사용 가능한 포트를 선택함을 의미합니다. 방화벽을 통해 명명된 인스턴스에 연결할 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 특정 포트에서 수신하도록 구성하면 방화벽에서 해당 포트를 열 수 있습니다.  

1433 포트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 알려진 표준이므로 일부 조직에서는 보안을 강화하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 포트 번호를 변경해야 한다고 명시하고 있습니다. 이는 일부 환경에서 유용할 수 있습니다. 그러나 TCP/IP 아키텍처에서는 [포트 스캐너](https://wikipedia.org/wiki/Port_scanner)에서 열린 포트를 쿼리할 수 있으므로 포트 번호를 변경하는 것은 강력한 보안 수단으로 간주되지 않습니다.

 기본 Windows 방화벽 설정 방법과 데이터베이스 엔진, Analysis Services, Reporting Services 및 Integration Services에 영향을 주는 TCP 포트에 대한 설명은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
> [!TIP]  
>  포트 번호를 선택할 때 특정 응용 프로그램에 할당된 포트 번호 목록을 보려면 [http://www.iana.org/assignments/port-numbers](http://www.iana.org/assignments/port-numbers) 를 참조하세요. 할당되지 않은 포트 번호를 선택합니다. 자세한 내용은 [TCP/IP에 대한 기본 동적 포트 범위는 Windows Vista 및 Windows Server 2008에서 변경](http://support.microsoft.com/kb/929851)을 참조하세요.  
  
> [!WARNING]  
>  다시 시작할 때 데이터베이스 엔진은 새 포트에서 수신을 시작합니다. 그러나 데이터베이스 엔진이 사용하지 않을 수 있는 경우에도 구성을 변경하는 즉시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 브라우저 서비스가 레지스트리를 모니터링하고 새 포트 번호를 보고합니다. 데이터베이스 엔진을 다시 시작하여 일관성을 확인하고 연결 실패를 방지합니다.  
  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-assign-a-tcpip-port-number-to-the-sql-server-database-engine"></a>SQL Server 데이터베이스 엔진에 TCP/IP 포트 번호를 할당하려면  
  
1.  SQL Server 구성 관리자의 콘솔 창에서 **SQL Server 네트워크 구성**, **\<인스턴스 이름>에 대한 프로토콜**을 차례로 펼친 다음 **TCP/IP**를 두 번 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 여는 동안 문제가 발생하는 경우 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 참조하세요.  
  
2.  **TCP/IP 속성** 대화 상자의 **IP 주소** 탭에 여러 개의 IP 주소가 **IP1**, **IP2**의 형식으로 **IPAll**까지 표시됩니다. 이러한 주소에는 루프백 어댑터의 IP 주소인 127.0.0.1이 포함됩니다. 컴퓨터의 각 IP 주소에 대한 추가 IP 주소가 나타납니다. (IP 버전 4 및 IP 버전 6 주소가 모두 표시됩니다.) 각 주소를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭하여 구성할 IP 주소를 확인합니다.  
  
3.  **TCP 동적 포트** 대화 상자에 **0**이 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 동적 포트에서 수신한다는 표시이므로 0을 삭제합니다.  
  
     ![TCP_ports](../../database-engine/configure-windows/media/tcp-ports.png "TCP_ports")  
  
4.  **IP***n* **속성** 영역 상자의 **TCP 포트** 상자에서 이 IP 주소가 수신 대기할 포트 번호를 입력한 다음 **확인**을 클릭합니다.  
  
5.  콘솔 창에서 **SQL Server 서비스**를 클릭합니다.  
  
6.  세부 정보 창에서 **SQL Server(**\<인스턴스 이름>**)**를 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지하고 다시 시작합니다.  
  
## <a name="connecting"></a>Connecting  
특정 포트에서 수신하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성한 후에 특정 포트를 통해 클라이언트 응용 프로그램과 연결하는 세 가지 방법은 다음과 같습니다.  
  
-   서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 실행하여 이름을 기준으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다.  
-   클라이언트에서 별칭을 만들어 포트 번호를 지정합니다.  
-   클라이언트가 사용자 지정 연결 문자열을 사용하여 연결하도록 프로그래밍합니다.  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트에서 사용할 서버 별칭 만들기 또는 삭제&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [SQL Server Browser 서비스](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
