---
title: "SQL Server 장애 조치(Failover) 클러스터에서 노드 추가 또는 제거(설치) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "노드 추가"
  - "노드 [장애 조치(Failover) 클러스터링], 제거"
  - "노드 [장애 조치(Failover) 클러스터링], 추가"
  - "장애 조치(failover) 클러스터링 [SQL Server], 노드"
  - "노드 삭제"
  - "클러스터 유지 관리 [SQL Server]"
  - "노드 제거"
ms.assetid: fe20dca9-a4c1-4d32-813d-42f1782dfdd3
caps.latest.revision: 49
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 49
---
# SQL Server 장애 조치(Failover) 클러스터에서 노드 추가 또는 제거(설치)
  이 절차에 따라 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스에서 노드를 관리할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터를 업데이트하거나 제거하려면 장애 조치 클러스터의 모든 노드에 서비스로 로그인할 수 있는 권한을 가진 로컬 관리자여야 합니다. 로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.  
  
 기존의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 노드를 추가하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스에 추가할 노드에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행해야 합니다. 액티브 노드에서 설치 프로그램을 실행해서는 안 됩니다.  
  
 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에서 노드를 제거하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스에서 제거할 노드에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행해야 합니다.  
  
 노드를 추가하거나 제거하는 절차 단계를 보려면 다음 작업 중 하나를 선택합니다.  
  
-   [기존 SQL Server 장애 조치(Failover) 클러스터에 노드 추가](#Add)  
  
-   [기존 SQL Server 장애 조치(Failover) 클러스터에서 노드 제거](#Remove)  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 위치에 대한 운영 체제 드라이브 문자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 추가된 모든 노드와 일치해야 합니다.  
  
##  <a name="Add"></a> 노드 추가  
  
#### 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 노드를 추가하려면  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더로 이동한 다음 Setup.exe를 두 번 클릭합니다.  
  
2.  설치 마법사가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 센터를 시작합니다. 기존 장애 조치(failover) 클러스터 인스턴스에 노드를 추가하려면 왼쪽 창에서 **설치**를 클릭합니다. 그런 다음 **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터에 노드 추가**를 선택합니다.  
  
3.  시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
4.  지역화된 운영 체제에서 설치하고 있고 설치 미디어에 영어와 해당 운영 체제 언어에 대한 언어 팩이 둘 다 있는 경우 언어 선택 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 언어를 지정할 수 있습니다. 언어 간 호환성 지원 및 설치 고려 사항에 대한 자세한 내용은 [SQL Server의 로컬 언어 버전](../../../sql-server/install/local-language-versions-in-sql-server.md)을 참조하세요.  
  
     계속하려면 **다음**을 클릭합니다.  
  
5.  제품 키 페이지에서 제품의 프로덕션 버전에 대한 PID 키를 지정합니다. 이 설치에 입력하는 제품 키는 액티브 노드에 설치된 것과 동일한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전에 대한 제품 키여야 합니다.  
  
6.  사용 조건 페이지에서 사용권 계약을 읽은 다음 동의함 확인란을 선택합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다. 계속하려면 **다음**을 클릭합니다. 설치를 끝내려면 **취소**를 클릭합니다.  
  
7.  시스템 구성 검사기는 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. 검사가 완료되면 **다음** 을 클릭하여 작업을 계속 진행합니다.  
  
8.  클러스터 노드 구성 페이지에서 드롭다운 상자를 사용하여 이 설치 작업 중에 수정할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스의 이름을 지정합니다.  
  
9. 서버 구성 - 서비스 계정 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 계정을 지정합니다. 이 페이지에 구성된 실제 서비스는 사용자가 설치하도록 선택한 기능에 따라 달라집니다. 장애 조치(Failover) 클러스터 설치의 경우 계정 이름 및 시작 유형 정보는 액티브 노드에 대해 지정된 설정에 따라 이 페이지에 미리 채워집니다. 암호는 각 계정별로 지정해야 합니다. 자세한 내용은 [서버 구성 - 서비스 계정](../Topic/Server%20Configuration%20-%20Service%20Accounts.md) 및 [Windows 서비스 계정 및 권한 구성](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
     **보안 정보** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 정보 지정을 완료하면 **다음**을 클릭합니다.  
  
10. 보고 페이지에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 개선에 도움이 되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 보낼 정보를 지정할 수 있습니다. 오류 보고 옵션은 기본적으로 사용됩니다.  
  
11. 시스템 구성 검사기는 사용자가 지정한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능에 따라 사용자 컴퓨터 구성의 유효성을 검사하기 위해 하나 이상의 규칙 집합을 실행합니다.  
  
12. 노드 추가 준비 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다.  
  
13. 노드 추가 진행률 페이지에서 제공하는 상태 정보를 통해 설치 진행률을 모니터링할 수 있습니다.  
  
14. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 완료 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다.  
  
15. 컴퓨터를 다시 시작합니다. 설치가 완료되면 설치 마법사에 표시되는 메시지를 꼭 읽으십시오. 설치 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
##  <a name="Remove"></a> 노드 제거  
  
#### 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에서 노드를 제거하려면  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더로 이동한 다음 Setup.exe를 두 번 클릭합니다.  
  
2.  설치 마법사가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 센터를 시작합니다. 기존 장애 조치(failover) 클러스터 인스턴스에서 노드를 제거하려면 왼쪽 창에서 **유지 관리**를 클릭한 다음 **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터에서 노드 제거**를 선택합니다.  
  
3.  시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
4.  설치 지원 파일 페이지에서 설치를 클릭하면 시스템 구성 검사기는 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. 검사가 완료되면 **다음** 을 클릭하여 작업을 계속 진행합니다.  
  
5.  클러스터 노드 구성 페이지에서 드롭다운 상자를 사용하여 이 설치 작업 중에 수정할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스의 이름을 지정합니다. 제거할 노드가 **이 노드의 이름** 필드에 표시됩니다.  
  
6.  노드 제거 준비 페이지에는 설치 중에 지정된 옵션이 트리 뷰로 표시됩니다. 계속하려면 **제거**를 클릭합니다.  
  
7.  제거 작업 중에 노드 제거 진행률 페이지에서 상태를 보여 줍니다.  
  
8.  노드 제거 작업 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 완료 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 노드 제거 작업을 완료하려면 **닫기**를 클릭합니다. 설치 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
## 참고 항목  
 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  