---
title: 기존 인스턴스 제거
description: 이 문서에서는 SQL Server 독립 실행형 인스턴스를 제거하는 방법을 설명합니다. 이렇게 하면 SQL Server를 다시 설치할 수 있도록 시스템을 준비할 수도 있습니다.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
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
author: cawrites
ms.author: chadam
ms.openlocfilehash: 16522114fb7e02517ec7385b6b7c73aa90b4b6b0
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96127489"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>SQL Server의 기존 인스턴스 제거(설치)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  이 문서에서는 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 제거하는 방법에 대해 설명합니다. 이 문서의 단계를 수행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 설치할 수 있도록 시스템을 준비할 수도 있습니다.  
  
 > [!NOTE]
 > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 제거하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 제공하는 노드 제거 기능을 사용하여 각 노드를 개별적으로 제거합니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)를 참조하세요.  

## <a name="considerations"></a>고려 사항

- SQL Server를 제거하려면 서비스로 로그온할 수 있는 권한을 가진 로컬 관리자여야 합니다. 
- 컴퓨터에 *최소* 요구 실제 메모리 양이 있는 경우 페이지 파일의 크기를 실제 메모리 용량의 2배까지 늘립니다. 가상 메모리가 부족하면 SQL Server가 완전히 제거되지 않을 수도 있습니다. 
- SQL Server 인스턴스가 여러 개 있는 시스템에서는 SQL Server의 마지막 인스턴스가 제거된 후에만 SQL Server 브라우저 서비스가 제거됩니다. SQL Server Browser 서비스는 **제어판** 의 **프로그램 및 기능** 에서 수동으로 제거할 수 있습니다. 
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을(를) 제거하면 설치 프로세스 중 추가된 tempdb 데이터 파일이 삭제됩니다. tempdb_mssql_*.ndf 이름 패턴의 파일이 시스템 데이터베이스 디렉터리에 있는 경우 삭제됩니다. 
  

  
## <a name="prepare"></a>준비  
  
1.  **데이터를 백업합니다.** 시스템 데이터베이스를 비롯한 모든 데이터베이스의 [전체 백업](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)을 만들거나 .mdf 및 .ldf 파일을 별도의 위치에 수동으로 복사합니다. **마스터** 데이터베이스는 로그인과 스키마 같은 서버에 대한 모든 시스템 수준 정보를 포함합니다. **msdb** 데이터베이스는 SQL Server 에이전트 작업, 백업 기록 및 유지 관리 계획과 같은 작업 정보를 포함합니다. 시스템 데이터베이스에 관한 자세한 내용은 [시스템 데이터베이스](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)를 참조하세요. 
  
    저장해야 하는 파일에는 다음 데이터베이스 파일이 포함됩니다.  

    * master.mdf
    * msdbdata.mdf
    * Tempdb.mdf
    * mastlog.ldf
    * msdblog.ldf
    * Templog.ldf
    * model.mdf
    * Mssqlsystemresource.mdf
    * ReportServer[$InstanceName]
    * modellog.ldf
    * Mssqlsustemresource.ldf
    * ReportServer[$InstanceName]TempDB

    > [!NOTE]
    > ReportServer 데이터베이스는 SQL Server Reporting Service에 포함되어 있습니다.   

 
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **서비스를** **모두 중지합니다.** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 제거하기 전에 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 중지하는 것이 좋습니다. 활성 연결로 인해 제거 작업이 실패할 수 있습니다.  
  
1.  **적합한 권한을 가진 계정을 사용합니다.** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 또는 동등한 권한을 가진 계정을 사용하여 서버에 로그온합니다. 예를 들어 로컬 Administrators 그룹의 멤버 계정을 사용하여 서버에 로그온할 수 있습니다.  
  
## <a name="uninstall"></a>제거 

# <a name="windows-10--2016-"></a>[Windows 10/2016+](#tab/Windows10)

Windows 10, Windows Server 2016, Windows Server 2019 이상에서 SQL Server를 제거하려면 다음 단계를 수행합니다. 

1. 제거 프로세스를 시작하려면 시작 메뉴에서 **설정** 으로 이동한 다음 **앱** 을 선택합니다. 
1. 검색 상자에서 `sql`을 검색합니다. 
1. **Microsoft SQL Server (버전) (비트)** 를 선택합니다. 예들 들어 `Microsoft SQL Server 2017 (64-bit)`입니다.
1. **제거** 를 선택합니다.
 
    ![SQL Server 제거](media/uninstall-an-existing-instance-of-sql-server-setup/uninstall-sql-server-windows-10.png)

1. SQL Server 대화 상자에서 **제거** 를 선택하여 Microsoft SQL Server 설치 마법사를 시작합니다. 

    ![SQL Server 제거](media/uninstall-an-existing-instance-of-sql-server-setup/remove-sql-2017.png)
  
1.  인스턴스 **선택** 페이지에서 드롭다운 상자를 사용하여 제거할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 기능 및 관리 도구만 제거하는 옵션을 지정합니다. 계속하려면 **다음** 을 선택합니다.  
  
1.  **기능 선택** 페이지에서 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 제거할 기능을 지정합니다.  
  
1.  **제거 준비** 페이지에서 제거할 구성 요소 및 기능 목록을 검토합니다. **제거** 를 클릭하여 제거를 시작합니다.  
 
1. **앱 및 기능** 창을 새로 고쳐서 SQL Server 인스턴스가 성공적으로 제거되었는지 확인하고 여전히 존재하는 SQL Server 구성 요소가 있는지 확인합니다. 그렇게 선택한 경우 이 창에서도 이러한 구성 요소를 제거합니다. 

# <a name="windows-2008---2012-r2"></a>[Windows 2008 - 2012 R2](#tab/windows2012)

Windows Server 2008, Windows Server 2012 및 Windows 2012 R2에서 SQL Server를 제거하려면 다음 단계를 수행합니다. 

1. 제거 프로세스를 시작하려면 **제어판** 으로 이동한 다음 **프로그램 및 기능** 을 선택합니다.
1. **Microsoft SQL Server (버전) (비트)** 를 마우스 오른쪽 단추로 클릭하고 **제거** 를 선택합니다. 예들 들어 `Microsoft SQL Server 2012 (64-bit)`입니다.  
  
    ![SQL Server 제거](media/uninstall-an-existing-instance-of-sql-server-setup/uninstall-sql-server-windows-2012.png)

1. SQL Server 대화 상자에서 **제거** 를 선택하여 Microsoft SQL Server 설치 마법사를 시작합니다. 

    ![SQL Server 제거](media/uninstall-an-existing-instance-of-sql-server-setup/remove-sql-2012.png)
  
1.  인스턴스 **선택** 페이지에서 드롭다운 상자를 사용하여 제거할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 기능 및 관리 도구만 제거하는 옵션을 지정합니다. 계속하려면 **다음** 을 선택합니다.  
  
1.  **기능 선택** 페이지에서 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 제거할 기능을 지정합니다.  
  
1.  **제거 준비** 페이지에서 제거할 구성 요소 및 기능 목록을 검토합니다. **제거** 를 클릭하여 제거를 시작합니다.  
 
1. **프로그램 및 기능** 창을 새로 고쳐서 SQL Server 인스턴스가 성공적으로 제거되었는지 확인하고 여전히 존재하는 SQL Server 구성 요소가 있는지 확인합니다. 그렇게 선택한 경우 이 창에서도 이러한 구성 요소를 제거합니다. 

---

  
## <a name="in-the-event-of-failure"></a>오류가 발생한 경우  

제거 프로세스가 실패하면 [SQL Server 설치 로그 파일](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 검토하여 근본 원인을 확인하세요. 

기술 자료 문서 [설치 로그 파일에서 SQL Server 설치 문제를 파악하는 방법](https://support.microsoft.com/kb/955396/en-us)은 조사에 도움이 될 수 있습니다. SQL Server 2008에 관한 내용이지만 설명된 방법은 모든 버전의 SQL Server에 적용됩니다. 

  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
