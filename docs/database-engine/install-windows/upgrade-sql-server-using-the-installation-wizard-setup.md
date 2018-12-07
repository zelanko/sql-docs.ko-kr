---
title: 설치 마법사를 사용하여 SQL Server 업그레이드(설치 프로그램) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- upgrading Database Engine
- Database Engine [SQL Server], upgrading
ms.assetid: cef118a5-a7ce-4bfa-8b9d-c81996284cfc
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 9ce14b9cbc983987072eb9433a20823c8721e3db
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533974"
---
# <a name="upgrade-sql-server-using-the-installation-wizard-setup"></a>설치 마법사를 사용하여 SQL Server 업그레이드(설치 프로그램)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 전체 업그레이드할 수 있는 단일 기능 트리를 제공합니다.  
  
>[!WARNING]  
>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하면 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 덮어쓰므로 컴퓨터에는 이 버전이 더 이상 존재하지 않게 됩니다. 
>
>그러므로 업그레이드 전에 이전 SQL Server 인스턴스와 연결된 SQL Server 데이터베이스 및 기타 개체를 백업하세요.  
  
> [!CAUTION]  
> 대부분의 프로덕션 환경과 일부 개발 환경에서는 현재 위치 업그레이드보다 새 설치 업그레이드 또는 롤링 업그레이드를 수행하는 것이 더 효율적입니다.  업그레이드 방법에 대한 자세한 내용은 다음을 참조하세요.
> * [데이터베이스 엔진 업그레이드 방법 선택](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)
> * [Data Quality Services 업그레이드](../../database-engine/install-windows/upgrade-data-quality-services.md)
> * [Integration Services 업그레이드](../../integration-services/install-windows/upgrade-integration-services.md)
> * [Master Data Services 업그레이드](../../database-engine/install-windows/upgrade-master-data-services.md)
> * [Reporting Services 업그레이드 및 마이그레이션](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)
> * [Analysis Services 업그레이드](../../database-engine/install-windows/upgrade-analysis-services.md)
> * [SharePoint용 파워 피벗 업그레이드](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)  
  
## <a name="prerequisites"></a>사전 요구 사항  
관리자로 설치 프로그램을 실행해야 합니다. 원격 공유에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있으며 로컬 관리자인 도메인 계정을 사용해야 합니다.  
  
> [!WARNING]  
>  업그레이드할 기능은 변경할 수 없으며, 업그레이드 작업 중에 기능을 추가할 수도 없습니다. 업그레이드 작업이 완료된 후 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]의 업그레이드된 인스턴스에 기능을 추가하는 방법에 대한 자세한 내용은 [SQL Server 인스턴스에 기능 추가&#40;설치 프로그램&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)를 참조하세요.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드하는 경우에는 [데이터베이스 엔진 업그레이드 계획 및 테스트](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md) 를 검토한 후에 다음 중 환경에 적합한 태스크를 수행합니다.  
  
-   필요할 때 복원할 수 있도록 업그레이드할 인스턴스의 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일을 백업합니다.  
  
-   업그레이드할 데이터베이스에서 적절한 DBCC(데이터베이스 콘솔 명령)를 실행하여 데이터베이스가 일관된 상태를 유지하도록 합니다.  
  
-   SQL Server 구성 요소 및 사용자 데이터베이스 업그레이드에 필요한 디스크 공간을 예측합니다. SQL Server 구성 요소에 필요한 디스크 공간은 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.  
  
-   기존 SQL Server 시스템 데이터베이스(master, model, msdb 및 tempdb)가 자동 증가하도록 구성되어 있는지 확인하고 하드 디스크 공간이 충분한지 확인합니다.  
  
-   master 데이터베이스에 모든 데이터베이스 서버에 대한 로그온 정보가 있는지 확인합니다. 시스템 로그온 정보는 master 데이터베이스에 있으므로 이는 데이터베이스 복원을 위해 중요합니다.  
  
-   업그레이드 프로세스에서는 업그레이드 중인 SQL Server 인스턴스의 서비스가 중지되었다가 시작되므로 모든 시작 저장 프로시저를 사용하지 않도록 설정합니다. 시작 시 처리되는 저장 프로시저로 인해 업그레이드 프로세스가 중단될 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 MSX/TSX 관계에 나열되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 업그레이드할 때는 마스터 서버를 업그레이드하기 전에 대상 서버를 업그레이드합니다. 대상 서버 전에 마스터 서버를 업그레이드하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 마스터 인스턴스에 연결할 수 없습니다.  
  
-   SQL Server를 사용하는 모든 서비스를 포함한 모든 응용 프로그램을 끝냅니다. 로컬 응용 프로그램이 업그레이드 중인 인스턴스에 연결되어 있으면 업그레이드가 실패할 수 있습니다.  
  
-   복제가 현재 상태인지 확인한 다음 복제를 중지합니다.   
    복제된 환경에서 롤링 업그레이드를 수행하기 위한 자세한 단계는 [복제된 데이터베이스 업그레이드](../../database-engine/install-windows/upgrade-replicated-databases.md)를 참조하세요.
  
## <a name="procedure"></a>절차  
  
### <a name="to-upgrade-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]로 업그레이드하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더로 이동한 다음 Setup.exe를 두 번 클릭합니다.  
  
2.  설치 마법사가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 시작합니다. 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 업그레이드하려면 왼쪽 탐색 영역에서 **설치**를 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 버전**에서 업그레이드**를 클릭합니다.  
  
3.  제품 키 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]무료 버전으로 업그레이드할지 아니면 제품의 프로덕션 버전에 대한 PID 키가 있는지를 나타내는 옵션을 클릭합니다. 자세한 내용은 [SQL Server 2016 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md) 및 [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하세요.  
  
4.  사용 조건 페이지에서 사용권 계약을 검토하고 동의하면 **동의함** 확인란을 선택한 다음 **다음**을 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다.  
  
5.  전역 규칙 창에서 규칙 오류가 없는 경우 설치 절차는 제품 업데이트 창으로 자동으로 진행됩니다.  
  
6.  다음에 Control Panel\All Control Panel Items\Windows Update\Change 설정에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 업데이트 확인란을 선택하지 않으면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 업데이트 페이지가 나타납니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 업데이트 페이지에서 확인란을 선택하면 Windows Update를 검색하는 경우 최신 업데이트를 포함하도록 컴퓨터 설정이 변경됩니다.  
  
7.  제품 업데이트 페이지에는 사용 가능한 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 업데이트가 표시됩니다. 업데이트를 포함하지 않으려면 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 업데이트 포함** 확인란의 선택을 취소합니다. 제품 업데이트가 검색되지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 이 페이지가 표시되지 않으며 **설치 파일 설치** 페이지로 자동으로 진행됩니다.  
  
8.  설치 파일 설치 페이지에는 설치 파일의 다운로드, 추출 및 설치 진행률이 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 대한 업데이트가 발견되고 이러한 업데이트가 포함되도록 지정된 경우 해당 업데이트도 함께 설치됩니다.  
  
9. 업그레이드 규칙 창에서 규칙 오류가 없는 경우 설치 절차는 인스턴스 선택 창으로 자동으로 진행됩니다.  
  
10. 인스턴스 선택 페이지에서 업그레이드할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정합니다. 관리 도구 및 공유 기능을 업그레이드하려면 **공유 기능만 업그레이드**를 선택합니다.  
  
11. 기능 선택 페이지에는 업그레이드할 기능이 미리 선택되어 있습니다. 기능 이름을 선택하면 오른쪽 창에 각 구성 요소 그룹에 대한 설명이 나타납니다.  
  
     선택한 기능의 필수 구성 요소가 오른쪽 창에 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서는 이미 설치되어 있지 않은 필수 구성 요소가 있는 경우 이 절차의 뒷부분에 설명된 설치 단계에서 이를 설치합니다.  
  
    > [!NOTE]  
    >  **인스턴스 선택** 페이지에서 **\<공유 기능만 업그레이드>** 를 선택하여 공유 기능을 업그레이드하도록 선택한 경우 [기능 선택] 페이지에서 모든 공유 기능이 미리 선택되어 있습니다. 모든 공유 구성 요소는 동시에 업그레이드됩니다.  
  
12. 인스턴스 구성 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 인스턴스 ID를 지정합니다.  
  
     **인스턴스 ID** - 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 기본 인스턴스의 경우 인스턴스 이름 및 인스턴스 ID는 MSSQLSERVER입니다. 기본값이 아닌 인스턴스 ID를 사용하려면 **인스턴스 ID** 입력란에 값을 제공합니다.  
  
     모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 팩 및 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 구성 요소에 적용됩니다.  
  
     **설치된 인스턴스** - 그리드에는 설치 프로그램이 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 표시됩니다. 컴퓨터에 기본 인스턴스가 이미 설치된 경우 명명된 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]인스턴스를 설치해야 합니다.  
  
13. 이 문서의 나머지 부분에 대한 워크플로는 설치에 대해 지정한 기능에 따라 달라집니다. 선택 항목에 따라 일부 페이지가 표시되지 않을 수도 있습니다.  
  
14. 서버 구성 - 서비스 계정 페이지에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 기본 서비스 계정이 표시됩니다. 이 페이지에 구성된 실제 서비스는 사용자가 업그레이드하려는 기능에 따라 달라집니다.  
  
     인증 및 로그인 정보는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 가져옵니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 동일한 로그인 계정을 할당하거나 각 서비스 계정을 따로 구성할 수 있습니다. 서비스 시작 유형을 자동 또는 수동으로 지정하거나 서비스의 해제 여부도 지정할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 는 서비스 계정을 개별적으로 구성하도록 권장합니다. 그러면 "서비스 시작" 태스크 완료에 필요한 최소한의 권한만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 부여됩니다. 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)를 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 서비스 계정에 대해 동일한 로그인 계정을 지정하려면 페이지 맨 아래에 있는 필드에 자격 증명을 제공합니다.  
  
     **보안 정보** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 정보 지정을 완료하면 **다음**을 클릭합니다.  
  
15. 전체 텍스트 검색 업그레이드 옵션 페이지에서 업그레이드하려는 데이터베이스의 업그레이드 옵션을 지정합니다. 자세한 내용은 [전체 텍스트 검색 업그레이드](https://msdn.microsoft.com/library/16c9376b-5fbb-4495-a429-06a2493849c9)를 참조하세요.  
  
16. 모든 규칙이 통과하면 기능 규칙 창이 자동으로 진행됩니다.  
  
17. 업그레이드 준비 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 계속하려면 **설치**를 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다.  
  
18. 설치 중에 진행률 페이지에서 제공하는 상태 정보를 통해 설치 진행률을 모니터링할 수 있습니다.  
  
19. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 완료 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다.  
  
20. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 설치 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
## <a name="next-steps"></a>Next Steps  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드한 후 다음 태스크를 완료하십시오.  
  
-   **서버 등록** - 업그레이드하면 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 등록 설정이 제거됩니다. 업그레이드한 후 서버를 다시 등록해야 합니다.  
  
-   **통계 업데이트** - 쿼리 성능을 최적화하려면 업그레이드 후에 모든 데이터베이스에 대한 통계를 업데이트하는 것이 좋습니다. **sp_updatestats** 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 있는 사용자 정의 테이블의 통계를 업데이트할 수 있습니다.  
  
-   **새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 구성** - 공격받을 수 있는 시스템의 노출 영역을 줄이려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 핵심 서비스와 기능을 선별적으로 설치하고 활성화합니다. 노출 영역 구성 도구에 대한 자세한 내용은 이 릴리스의 추가 정보 파일을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)   
 [이전 버전과의 호환성_삭제됨](https://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)  
  
  
