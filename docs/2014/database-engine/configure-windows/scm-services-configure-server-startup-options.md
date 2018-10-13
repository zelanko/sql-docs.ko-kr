---
title: 서버 시작 옵션 구성(SQL Server 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], startup options
- SQL Server, startup options
- single-user mode [SQL Server], starting in
- startup options [SQL Server]
- SQL Server services, setting startup options
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 07fc15bf088cf48e0a1b9a30cd68d5c10254d345
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "49072108"
---
# <a name="configure-server-startup-options-sql-server-configuration-manager"></a>서버 시작 옵션 구성(SQL Server 구성 관리자)
  이 항목에서는 사용할 때마다 시작 옵션을 구성 하는 방법에 설명 합니다 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 시작 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. 시작 옵션 목록에 대한 자세한 내용은 [데이터베이스 엔진 서비스 시작 옵션](database-engine-service-startup-options.md)을 참조하세요.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
### <a name="limitations-and-restrictions"></a>제한 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 시작 매개 변수를 레지스트리에 씁니다. 이러한 매개 변수는 다음에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 시작할 때 적용됩니다.  
  
 클러스터의 활성 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 온라인 상태일 때 변경해야 하며, 이러한 변경 내용은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 다시 시작하면 적용됩니다. 다른 노드의 시작 옵션에 대한 레지스트리 업데이트는 다음 장애 조치(Failover) 시 수행됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 레지스트리에서 관련 항목을 변경할 수 있는 사용자만 서버 시작 옵션을 구성할 수 있습니다. 해당되는 사용자는 다음과 같습니다.  
  
-   로컬 Administrators 그룹의 멤버  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용되는 도메인 계정( [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 도메인 계정에서 실행하도록 구성된 경우)  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-configure-startup-options"></a>시작 옵션을 구성하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **SQL Server 서비스**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 최신 버전의 Windows에서 응용 프로그램으로 표시되지 않습니다.  
    >   
    >  -   **Windows 10**:  
    >          열려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager에는 **시작 페이지**, sqlservermanager12.msc (에 대 한 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 경우 12를 더 작은 수로 바꿉니다. SQLServerManager12.msc를 클릭 하면 Configuration Manager 열립니다. 구성 관리자를 시작 페이지나 작업 표시줄을 고정 하려면 SQLServerManager12.msc를 마우스 오른쪽 단추로 클릭 하 고 클릭 **파일 위치 열기**합니다. Windows 파일 탐색기에서 SQLServerManager12.msc를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 화면에 고정** 하거나 **작업 표시줄에 고정**합니다.  
    > -   **Windows 8**:  
    >          열려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager에서의 **검색** 참의 **앱**, 형식 **SQLServerManager\<버전 >.msc** 등`SQLServerManager12.msc`를 누릅니다 **Enter**합니다.  
  
2.  오른쪽 창에서 **SQL Server(***<instance_name>***)** 를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **시작 매개 변수** 탭의 **시작 매개 변수 지정** 상자에 매개 변수를 입력하고 **추가**를 클릭합니다.  
  
     예를 들어 단일 사용자 모드로 시작 하려면 입력 `-m` 에 **시작 매개 변수를 지정** 상자 하 고 클릭 **추가**합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 단일 사용자 모드로 다시 시작할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 중지합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 먼저 연결되므로 두 번째 사용자로 연결하지 못합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 다시 시작합니다.  
  
    > [!WARNING]  
    >  단일 사용자 모드를 사용 하 여 시작 매개 변수 상자에 작업을 완료 한 후 선택 합니다 `-m` 의 매개 변수를 **기존 매개 변수** 상자를 선택한 다음 클릭 **제거**합니다. 그런 후에 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 다시 시작하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 일반 다중 사용자 모드로 복원합니다.  
  
## <a name="see-also"></a>관련 항목  
 [단일 사용자 모드로 SQL Server 시작](start-sql-server-in-single-user-mode.md)   
 [시스템 관리자가 잠겨 있을 때 SQL Server에 연결](connect-to-sql-server-when-system-administrators-are-locked-out.md)   
 [SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
