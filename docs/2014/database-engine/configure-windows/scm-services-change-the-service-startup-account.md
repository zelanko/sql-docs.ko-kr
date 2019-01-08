---
title: SQL Server (SQL Server 구성 관리자)에 대 한 서비스 시작 계정 변경 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server services, startup account changes
- startup accounts [SQL Server]
- changing startup accounts for services
ms.assetid: d721c796-0397-46a7-901b-1a9a3c3fb385
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a2a830ad4d6fa87cd754910baf8be53216086cab
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52641254"
---
# <a name="change-the-service-startup-account-for-sql-server-sql-server-configuration-manager"></a>SQL Server의 서비스 시작 계정 변경(SQL Server 구성 관리자)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 시작 옵션을 변경하고 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 사용하는 서비스 계정을 변경하는 방법에 대해 설명합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]또는 PowerShell을 사용합니다. 적절한 서비스 계정을 선택하는 방법에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 서비스 시작 계정을 변경한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스( [!INCLUDE[ssDE](../../includes/ssde-md.md)])를 다시 시작해야만 변경 내용이 적용됩니다. 서비스를 다시 시작하면 서비스가 성공적으로 다시 시작될 때까지 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 모든 데이터베이스를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 서비스 시작 계정을 변경해야 하는 경우 정기적으로 예약된 유지 관리 중 또는 일상적인 작업을 방해하지 않고 데이터베이스를 오프라인 상태로 만들 수 있을 때 이 작업을 수행해야 합니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   클러스터형 서버  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 사용하는 서비스 계정을 변경하는 작업은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터의 액티브 노드에서 수행해야 합니다.  
  
     Windows Server 2008에서 실행 중인 경우(도메인 그룹을 사용하는 기본 구성이 아닌 다른 구성인 경우) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 사용하는 서비스 계정을 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 중지하여 리소스 그룹을 오프라인 상태로 만들어야 합니다.  
  
-   [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 에서 Express 이외 버전으로 SKU 업그레이드  
  
     [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 네트워크 서비스를 사용하도록 구성되지만 이는 비활성화됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 할당된 계정을 변경할 수 있지만 서비스를 설정하거나 시작할 수는 없습니다. SKU를 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 에서 Express 이외 버전으로 업그레이드하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동으로 활성화되지 않지만 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 서비스 시작 모드를 수동 또는 자동으로 변경하면 활성화할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-change-the-sql-server-service-startup-account"></a>SQL Server 서비스 시작 계정을 변경하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 최신 버전의 Windows에서 애플리케이션으로 표시되지 않습니다.  
    >   
    >  -   **Windows 10**:  
    >          열려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager에는 **시작 페이지**, sqlservermanager12.msc (에 대 한 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 경우 12를 더 작은 수로 바꿉니다. SQLServerManager12.msc를 클릭 하면 Configuration Manager 열립니다. 구성 관리자를 시작 페이지나 작업 표시줄을 고정 하려면 SQLServerManager12.msc를 마우스 오른쪽 단추로 클릭 하 고 클릭 **파일 위치 열기**합니다. Windows 파일 탐색기에서 SQLServerManager12.msc를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 화면에 고정** 하거나 **작업 표시줄에 고정**합니다.  
    > -   **Windows 8**:  
    >          열려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager에서의 **검색** 참의 **앱**, 형식 **SQLServerManager\<버전 >.msc** 등`SQLServerManager12.msc`를 누릅니다 **Enter**합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **SQL Server 서비스**를 클릭합니다.  
  
3.  세부 정보 창에서 서비스 시작 계정을 변경할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **SQL Server \<***instancename***> 속성** 대화 상자에서 **로그온** 탭을 클릭하고 **다음 계정으로 로그온** 계정 유형을 선택합니다.  
  
5.  새 서비스 시작 계정을 선택한 다음 **확인**을 클릭합니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작할지 여부를 확인하는 메시지 상자가 표시됩니다.  
  
6.  **예**를 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](start-stop-pause-resume-restart-sql-server-services.md)   
 [WMI를 구성하여 SQL Server 도구에 서버 상태 표시](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
