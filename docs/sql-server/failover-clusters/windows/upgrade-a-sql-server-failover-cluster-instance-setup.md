---
title: SQL Server 장애 조치(Failover) 클러스터 인스턴스 업그레이드(설치) | Microsoft 문서
ms.custom: ''
ms.date: 01/22/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
caps.latest.revision: 63
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35107b894f6c6887465553f13daf585083e4730e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>SQL Server 장애 조치(Failover) 클러스터 인스턴스 업그레이드(설치)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 UI를 사용하거나 명령 프롬프트에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 장애 조치(Failover) 클러스터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터로 업그레이드할 수 있습니다.  
  
 로컬로 설치하는 경우 관리자로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행해야 합니다. 원격 공유에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치하는 경우 원격 공유에 대한 읽기 권한이 있는 도메인 계정을 사용해야 합니다.  
  
 업그레이드하기 전에 [SQL Server 장애 조치(Failover) 클러스터 인스턴스 업그레이드](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)를 참조하세요.  
  
##  <a name="UpgradeSteps"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 업그레이드하려면  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 업그레이드하려면  
  
1.  업그레이드 중인 버전과 일치하는 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 미디어에서 루트 폴더에 있는 setup.exe를 두 번 클릭합니다. 필수 구성 요소가 설치되어 있지 않은 경우 해당 구성 요소를 설치하라는 메시지가 나타날 수 있습니다.  
  
2.  필수 구성 요소를 설치하고 나면 설치 마법사를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 센터가 시작됩니다. 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스를 업그레이드하려면 인스턴스를 선택합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 지원 파일이 필요한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램이 이를 설치합니다. 컴퓨터를 다시 시작하라는 메시지가 표시되면 컴퓨터를 다시 시작한 후 작업을 계속합니다.  
  
4.  시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 계속하려면 [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
5.  제품 키 페이지에서 기존 제품 버전에 맞는 새 버전의 PID 키를 입력합니다. 예를 들어 Enterprise 장애 조치(Failover) 클러스터를 업그레이드하려면 [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]용 PID 키를 입력해야 합니다. 계속하려면 **다음** 을 클릭합니다. 장애 조치(Failover) 클러스터 업그레이드에 사용하는 PID 키는 동일 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 내의 모든 장애 조치(Failover) 클러스터 노드에서 동일해야 합니다.  
  
6.  사용 조건 페이지에서 사용권 계약을 읽은 다음 사용 조건과 계약 조건에 동의하면 해당 확인란을 선택합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다. 계속하려면**다음**을 클릭합니다. 설치를 끝내려면 **취소**를 클릭합니다.  
  
7.  인스턴스 선택 페이지에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로 업그레이드할 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]인스턴스를 지정합니다. 계속하려면**다음**을 클릭합니다.  
  
8.  기능 선택 페이지에는 업그레이드할 기능이 미리 선택되어 있습니다. 기능 이름을 선택하면 오른쪽 창에 각 구성 요소 그룹에 대한 설명이 나타납니다. 업그레이드할 기능은 변경할 수 없으며, 업그레이드 작업 중에 기능을 추가할 수도 없습니다. 업그레이드 작업이 완료된 후 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 의 업그레이드된 인스턴스에 기능을 추가하려면 [SQL Server 2016 인스턴스에 기능 추가&#40;설치&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)를 참조하세요.  
  
     선택한 기능의 필수 구성 요소가 오른쪽 창에 표시됩니다. SQL Server 설치 프로그램에서는 이미 설치되어 있지 않은 필수 구성 요소가 있는 경우 이 절차의 뒷부분에 설명된 설치 단계에서 이를 설치합니다. 시간을 절약하려면 각 노드에서 이러한 필수 구성 요소를 미리 설치해야 합니다.  
  
9. 인스턴스 구성 페이지의 필드가 기존 인스턴스 정보로 자동으로 채워집니다. 필요에 따라 새 InstanceID 값을 지정할 수 있습니다.  
  
     **인스턴스 ID** - 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 기본 인스턴스의 경우 인스턴스 이름 및 인스턴스 ID는 MSSQLSERVER입니다. 기본이 아닌 인스턴스 ID를 사용하려면 **인스턴스 ID** 확인란을 선택하고 값을 입력합니다. 기본값을 재정의하는 경우, 모든 장애 조치 클러스터 노드에서 업그레이드할 인스턴스에 대해 동일한 인스턴스 ID를 지정해야 합니다. 업그레이드된 인스턴스에 대한 인스턴스 ID는 다수의 노드에서 일치해야 합니다.  
  
     **감지된 인스턴스 및 기능** - 설치 프로그램을 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 표 형식으로 표시됩니다. 계속하려면**다음**을 클릭합니다.  
  
10. 디스크 공간 요구 사항 페이지에서는 사용자가 지정한 기능에 필요한 디스크 공간을 계산한 후 설치 프로그램을 실행 중인 컴퓨터에서 사용 가능한 디스크 공간과 실제로 필요한 디스크 공간의 크기를 비교하여 보여 줍니다.  
  
11. 전체 텍스트 검색 업그레이드 페이지에서 업그레이드하려는 데이터베이스의 업그레이드 옵션을 지정합니다. 자세한 내용은 [전체 텍스트 검색 업그레이드 옵션](http://msdn.microsoft.com/library/16c9376b-5fbb-4495-a429-06a2493849c9)을 참조하세요.  
  
12. **오류 보고** 페이지에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 개선에 도움이 되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 보낼 정보를 지정할 수 있습니다. 오류 보고 옵션은 기본적으로 사용됩니다.  
  
13. 시스템 구성 검사기는 업그레이드 작업이 시작되기 전에 사용자가 지정한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능에 따라 사용자 컴퓨터 구성이 유효한지 검사하기 위한 하나 이상의 규칙 집합을 실행합니다.  
  
14. 클러스터 업그레이드 보고서 페이지에 장애 조치 클러스터 인스턴스의 노드 목록 및 각 노드에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 요소 관련 인스턴스 버전 정보가 표시됩니다. 여기에는 데이터베이스 스크립트 상태 및 복제 스크립트 상태가 나타나며, **다음**을 클릭하면 어떤 동작이 발생하는지에 대한 정보 메시지도 표시됩니다. 이미 업그레이드된 장애 조치 클러스터 노드 수 및 총 노드 수에 따라 **다음**을 클릭하면 나타나는 장애 조치 동작이 설치 프로그램에서 표시됩니다. 또한, 필수 구성 요소를 설치하지 않은 경우에는 불필요한 작동 중단 발생 가능성에 대해서도 경고합니다.  
  
15. 업그레이드 준비 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 계속하려면 **업그레이드**를 클릭합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다.  
  
16. 업그레이드 중에 진행률 페이지에서 제공하는 상태 정보를 통해 현재 노드에서의 업그레이드 진행률을 모니터링할 수 있습니다.  
  
17. 현재 노드의 업그레이드가 완료되면 클러스터 업그레이드 보고서 페이지에 모든 장애 조치 클러스터 노드, 각 장애 조치 클러스터 노드상의 기능, 해당 버전 정보 등이 표시됩니다. 표시된 버전 정보를 확인하고 계속해서 나머지 노드의 업그레이드를 진행합니다. 업그레이드된 노드로 장애 조치가 수행된 경우 이 정보도 상태 페이지에 나타납니다. Windows 클러스터 관리 도구에서 검토하여 확인할 수도 있습니다.  
  
18. 업그레이드가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 완료 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다.  
  
19. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 설치 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
20. 업그레이드 프로세스를 완료하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 있는 다른 모든 노드에서 이러한 단계를 반복합니다.  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터를 업그레이드하려면  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터로 업그레이드하려면(기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터가 다중 서브넷 클러스터가 아닌 경우)  
  
1.  클러스터를 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)](으)로 업그레이드하려면 위의 단계를 따릅니다.  
  
2.  AddNode 설치 동작을 사용하여 다른 서브넷에 있는 노드를 추가하고 **클러스터 네트워크 구성** 페이지에서 IP 주소 리소스 종속성을 OR로 설정합니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)을 참조하세요.  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>현재 V-LAN 확장을 사용하는 다중 서브넷 클러스터를 업그레이드하려면  
  
1.  클러스터를 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)](으)로 업그레이드하려면 위의 단계를 따릅니다.  
  
2.  네트워크 설정을 변경하여 원격 노드를 다른 서브넷으로 이동합니다.  
  
3.  Windows 장애 조치(Failover) 클러스터 관리 도구를 사용하여 새 서브넷에 대한 새 IP 주소를 추가하고 IP 주소 리소스 종속성을 OR로 설정합니다.  
  
## <a name="next-steps"></a>Next Steps  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]로 업그레이드한 후 다음 태스크를 완료하십시오.  
  
-   [데이터베이스 엔진 업그레이드 완료](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [새 SQL Server 2016 기능 활용](http://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 장애 조치(Failover) 클러스터 인스턴스 업그레이드](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)   
 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [SQL Server 2016 인스턴스에 기능 추가&#40;설치&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)  
  
  
