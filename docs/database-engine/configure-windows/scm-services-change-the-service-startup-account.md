---
title: SCM 서비스 - 서비스 시작 계정 변경 | Microsoft Docs
description: SQL Server 및 대부분의 SQL Server 서비스에서 사용하는 서비스 계정을 변경하는 방법을 알아봅니다. 서비스 계정 변경에 대한 제한 사항을 확인합니다.
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server services, startup account changes
- startup accounts [SQL Server]
- changing startup accounts for services
ms.assetid: d721c796-0397-46a7-901b-1a9a3c3fb385
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ac1e58ba681857b6548bf067f91cde5163a8583b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651514"
---
# <a name="scm-services---change-the-service-startup-account"></a>SCM 서비스 - 서비스 시작 계정 변경
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 토픽에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 시작 옵션을 변경하고 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 사용하는 서비스 계정을 변경하는 방법을 설명합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]또는 PowerShell을 사용합니다. 적절한 서비스 계정을 선택하는 방법에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 서비스 시작 계정을 변경한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스( [!INCLUDE[ssDE](../../includes/ssde-md.md)])를 다시 시작해야만 변경 내용이 적용됩니다. 서비스를 다시 시작하면 서비스가 성공적으로 다시 시작될 때까지 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 모든 데이터베이스를 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 서비스 시작 계정을 변경해야 하는 경우 정기적으로 예약된 유지 관리 중 또는 일상적인 작업을 방해하지 않고 데이터베이스를 오프라인 상태로 만들 수 있을 때 이 작업을 수행해야 합니다.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   클러스터형 서버  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 사용하는 서비스 계정을 변경하는 작업은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터의 액티브 노드에서 수행해야 합니다.  
  
     Windows Server 2008에서 실행 중인 경우(도메인 그룹을 사용하는 기본 구성이 아닌 다른 구성인 경우) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 사용하는 서비스 계정을 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 중지하여 리소스 그룹을 오프라인 상태로 만들어야 합니다.  
  
-   [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 에서 Express 이외 버전으로 SKU 업그레이드  
  
     [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 네트워크 서비스를 사용하도록 구성되지만 이는 비활성화됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 할당된 계정을 변경할 수 있지만 서비스를 설정하거나 시작할 수는 없습니다. SKU를 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 에서 Express 이외 버전으로 업그레이드하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동으로 활성화되지 않지만 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 서비스 시작 모드를 수동 또는 자동으로 변경하면 활성화할 수 있습니다.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-change-the-sql-server-service-startup-account"></a>SQL Server 서비스 시작 계정을 변경하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 최신 버전의 Windows에서 애플리케이션으로 표시되지 않습니다.  
    >   
    >  -   **Windows 10**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 열려면 **시작 페이지**에 SQLServerManager13.msc를 입력합니다( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 경우). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 경우 13을 더 작은 수로 바꿉니다. SQLServerManager13.msc를 클릭하면 구성 관리자가 열립니다. 구성 관리자를 시작 페이지나 작업 표시줄에 고정하려면 SQLServerManager13.msc를 마우스 오른쪽 단추로 클릭한 다음 **파일 위치 열기**를 클릭합니다. Windows 파일 탐색기에서 SQLServerManager13.msc를 마우스 오른쪽 단추로 클릭하고 **시작 화면에 고정** 또는 **작업 표시줄에 고정**을 클릭합니다.  
    > -   **Windows 8**:  
    >          [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 열려면 **검색** 참의 **앱**에 **SQLServerManager\<version>.msc**(예: **SQLServerManager13.msc**)를 입력한 다음 **Enter** 키를 누릅니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **SQL Server 서비스**를 클릭합니다.  
  
3.  세부 정보 창에서 서비스 시작 계정을 변경할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **SQL Server \<**_instancename_**> 속성** 대화 상자에서 **로그온** 탭을 클릭하고 **다음 계정으로 로그온** 계정 유형을 선택합니다.  
  
5.  새 서비스 시작 계정을 선택한 다음 **확인**을 클릭합니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작할지 여부를 확인하는 메시지 상자가 표시됩니다.  
  
6.  **예**를 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [WMI를 구성하여 SQL Server 도구에 서버 상태 표시](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
