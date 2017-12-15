---
title: "데이터베이스 엔진 서비스 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- SQL Server Configuration Manager, accessing
- Database Engine [SQL Server], services
- managing services [SQL Server], about service management
- services [SQL Server]
- SQL Server Agent service, managing
- SQL Server services, about SQL Server service
- MSSQLServer
- server configuration [SQL Server]
- managing services [SQL Server]
- SQL Server Agent service
- services [SQL Server], managing
- administering SQL Server, services
- SQL Server services
ms.assetid: aa732e43-53ba-4eea-bb9b-089da0766fc1
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 77501642cb7f3cf7067d8ea51bcb5a7beed9eaa0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="manage-the-database-engine-services"></a>데이터베이스 엔진 서비스 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 운영 체제에서 서비스로 실행됩니다. 서비스는 시스템 백그라운드에서 실행되는 일종의 응용 프로그램입니다. 서비스는 일반적으로 웹 지원, 이벤트 로깅 또는 파일 지원 등 운영 체제의 중요한 기능을 제공합니다. 서비스는 컴퓨터 바탕 화면에 사용자 인터페이스를 표시하지 않고 실행할 수 있습니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 및 여러 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소가 서비스로 실행됩니다. 이러한 서비스는 일반적으로 운영 체제를 시작할 때 함께 시작되지만 설치 시 지정된 설정에 따라 달라질 수 있으며 일부 서비스는 기본적으로 시작되지 않습니다. 이 섹션에서는 다양한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 관리에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 로그인하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 시작, 중지, 일시 중지, 재개 및 다시 시작하는 방법에 대해 알아야 합니다. 로그인한 후에 서버 관리 또는 데이터베이스 쿼리와 같은 태스크를 수행할 수 있습니다.  
  
## <a name="using-the-sql-server-service"></a>SQL Server 서비스 사용  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스를 시작하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 시작됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 시작한 후 사용자는 서버에 새 연결을 만들 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스는 로컬 또는 원격에서 서비스로 시작 및 중지될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 기본 인스턴스인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)로, 명명된 인스턴스인 경우 MSSQL$*\<instancename>*으로 참조됩니다.  
  
## <a name="using-sql-server-configuration-manager"></a>SQL Server 구성 관리자 사용  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하면 다양한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 중지, 시작 또는 일시 중지할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서비스를 관리할 수 없습니다.  
  
 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 선택한 서비스의 속성을 볼 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 MMC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console) 스냅인이며 MMC 및 스냅인 작동 방법은 Windows 도움말을 참조하세요.  
  
 **SQL Server 구성 관리자에 액세스하려면**  
  
-   **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
 **Windows 8을 사용하여 SQL Server 구성 관리자에 액세스하려면**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 Windows 8.0을 실행할 때 응용 프로그램으로 표시되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 열려면 **앱** 의 **검색**창에서 **SQLServerManager12.msc** ( [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우), **SQLServerManager11.msc** ( [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 경우) 또는 **SQLServerManager10.msc** ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]의 경우)를 입력한 다음 **Enter**키를 누릅니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|||  
|-|-|  
|[서비스 관리를 위한 보안 요구 사항](../../database-engine/configure-windows/security-requirements-for-managing-services.md)|[SQL Server 인스턴스의 자동 시작 방지&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)|  
|[Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)|[SQL Server의 서비스 시작 계정 변경&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-change-the-service-startup-account.md)|  
|[네트워크에서 또는 네트워크 없이 SQL Server 실행](../../database-engine/configure-windows/run-sql-server-with-or-without-a-network.md)|[서버 시작 옵션 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)|  
|[SQL Server Browser 서비스&#40;데이터베이스 엔진 및 SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)|[SQL Server에서 사용하는 계정의 암호 변경&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-change-the-password-of-the-accounts-used.md)|  
|[데이터베이스 엔진 서비스 시작 옵션](../../database-engine/configure-windows/database-engine-service-startup-options.md)|[SQL Server 오류 로그 구성](../../database-engine/configure-windows/scm-services-configure-sql-server-error-logs.md)|  
|[데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)|[서버 인증 모드 변경](../../database-engine/configure-windows/change-server-authentication-mode.md)|  
|[단일 사용자 모드로 SQL Server 시작](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)|[SQL 기록기 서비스](../../database-engine/configure-windows/sql-writer-service.md)|  
|[최소 구성으로 SQL Server 시작](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)|[종료 메시지 브로드캐스트&#40;명령 프롬프트&#41;](../../database-engine/configure-windows/broadcast-a-shutdown-message-command-prompt.md)|  
|[다른 컴퓨터에 연결&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)|[SQL Server 인스턴스에 로그인&#40;명령 프롬프트&#41;](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)|  
|[SQL Server 인스턴스를 자동으로 시작하도록 설정&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-set-an-instance-to-start-automatically.md)|[데이터베이스 엔진 액세스에 대한 파일 시스템 사용 권한 구성](../../database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md)|  
  
## <a name="related-content"></a>관련 내용  
 [SQL Server 에이전트 구성](http://msdn.microsoft.com/library/2e361a62-9e92-4fcd-80d7-d6960f127900)  
  
 [SQL Server로 로그인](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
  
