---
title: SQL Server의 기존 인스턴스 제거(설치) | Microsoft 문서
ms.custom: ''
ms.date: 01/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- removing instances of SQL Server
- uninstalling instances of SQL Server
- removing SQL Server
- instances of SQL Server, uninstalling
- uninstalling SQL Server
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c4f9dc408f5b0cab4d568e8b63dfa3f61acdcd59
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126046"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>SQL Server의 기존 인스턴스 제거(설치)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 문서에서는 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 제거하는 방법에 대해 설명합니다. 이 문서의 단계를 수행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 설치할 수 있도록 시스템을 준비할 수도 있습니다.  
  
  >[!IMPORTANT]
  > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 제거하려면 서비스로 로그온할 수 있는 권한을 가진 로컬 관리자여야 합니다.  
  
 > [!NOTE]
 > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 제거하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 제공하는 노드 제거 기능을 사용하여 각 노드를 개별적으로 제거합니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제거하기 전에 다음의 중요 시나리오를 참고하십시오.  
  
-   필요한 최소한의 실제 메모리를 갖춘 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 제거하려면 먼저 페이지 파일 크기가 충분한지 확인해야 합니다. 페이지 파일 크기는 실제 메모리의 두 배여야 합니다. 가상 메모리가 부족하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 완전히 제거되지 않을 수도 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스가 여러 개인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 마지막 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스가 제거될 때 자동으로 제거됩니다.  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 모든 구성 요소를 제거하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제어판 **의** 프로그램 및 기능 **에서**Browser 구성 요소를 수동으로 제거해야 합니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을(를) 제거하면 설치 프로세스 중 추가된 tempdb 데이터 파일이 삭제됩니다. tempdb_mssql_*.ndf 이름 패턴의 파일이 시스템 데이터베이스 디렉터리에 있는 경우 삭제됩니다.  
  
### <a name="before-you-uninstall"></a>제거하기 전에  
  
1.  **데이터를 백업합니다.** 필수 단계는 아니지만 데이터베이스를 현재 상태대로 저장할 수 있습니다. 시스템 데이터베이스에 적용된 변경 사항을 저장할 수도 있습니다. 두 경우 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제거하기 전에 데이터를 백업해야 합니다. 또는 모든 데이터 및 로그 파일의 사본을 MSSQL 폴더 이외의 폴더에 저장해야 합니다. MSSQL 폴더는 제거 중에 삭제됩니다.  
  
     저장해야 하는 파일에는 다음 데이터베이스 파일이 포함됩니다.  
  
    -   Master.mdf  
  
    -   Mastlog.ldf  
  
    -   Model.mdf  
  
    -   Modellog.ldf  
  
    -   Msdbdata.mdf  
  
    -   Msdblog.ldf  
  
    -   Mssqlsystemresource.mdf  
  
    -   Mssqlsustemresource.ldf  
  
    -   Tempdb.mdf  
  
    -   Templog.ldf  
  
    -   ReportServer[$InstanceName] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 데이터베이스입니다.  
  
    -   ReportServer[$InstanceName]TempDB [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 임시 데이터베이스입니다.  
  
2.  **로컬 보안 그룹을 삭제합니다.** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제거하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에 대한 로컬 보안 그룹을 삭제합니다.  
  
3.  **모든** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **서비스 를 중지합니다.** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 제거하기 전에 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 중지하는 것이 좋습니다. 활성 연결로 인해 제거 작업이 실패할 수 있습니다.  
  
4.  **적합한 권한을 가진 계정을 사용합니다.** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 또는 동등한 권한을 가진 계정을 사용하여 서버에 로그온합니다. 예를 들어 로컬 Administrators 그룹의 멤버 계정을 사용하여 서버에 로그온할 수 있습니다.  
  
### <a name="to-uninstall-an-instance-of-includessnoversionincludesssnoversion-mdmd"></a>기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  제거 프로세스를 시작하려면 **제어판** , **프로그램 및 기능**으로 차례로 이동합니다.  
  
2.  **SQL Server 2016**을 마우스 오른쪽 단추로 클릭하고 **제거**를 선택합니다. **제거**를 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 시작합니다.  
  
     컴퓨터 구성을 확인하기 위해 설치 지원 규칙이 실행됩니다. 계속하려면 **다음**을 클릭합니다.  
  
3.  인스턴스 선택 페이지에서 드롭다운 상자를 사용하여 제거할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 기능 및 관리 도구만 제거하는 옵션을 지정합니다. 계속하려면 **다음**을 클릭합니다.  
  
4.  기능 선택 페이지에서 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 제거할 기능을 지정합니다.  
  
     작업을 성공적으로 완료할 수 있는지 확인하기 위해 제거 규칙이 실행됩니다.  
  
5.  **제거 준비** 페이지에서 제거할 구성 요소 및 기능 목록을 검토합니다. **제거** 를 클릭하여 제거를 시작합니다.  
  
6.  마지막 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 제거한 직후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로그램 및 기능 **의 프로그램 목록에**와 연결된 다른 프로그램이 계속 표시됩니다. 그러나 **프로그램 및 기능**을 닫은 후 다음에 **프로그램 및 기능**을 열면 프로그램 목록이 새로 고쳐져서 실제로 설치된 프로그램만 표시됩니다.  
  
### <a name="if-the-uninstallation-fails"></a>제거에 실패하는 경우  
  
1.  제거 프로세스가 성공적으로 완료되지 않은 경우 제거 실패 원인이 된 문제를 해결하십시오. 다음 문서는 제거 실패의 원인을 파악하는 데 도움이 될 수 있습니다.  
  
    -   [설치 로그 파일에서 SQL Server 2008 설치 문제를 확인하는 방법](https://support.microsoft.com/kb/955396/en-us)  
  
    -   [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
2.  제거 실패 원인을 해결할 수 없는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 고객 지원 센터에 문의할 수 있습니다. 중요 파일을 의도하지 않게 삭제한 경우와 같은 때는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 설치하기 전에 운영 체제를 다시 설치해야 할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
