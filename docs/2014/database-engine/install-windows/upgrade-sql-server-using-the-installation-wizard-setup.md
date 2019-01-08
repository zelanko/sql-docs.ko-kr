---
title: 업그레이드 하려면 SQL Server 2014 설치 마법사 (설치)를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- upgrading Database Engine
- Database Engine [SQL Server], upgrading
ms.assetid: cef118a5-a7ce-4bfa-8b9d-c81996284cfc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8330702d8c886cc9197dcd944878c3f794780205
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52536917"
---
# <a name="upgrade-to-sql-server-2014-using-the-installation-wizard-setup"></a>설치 마법사를 사용하여 SQL Server 2014로 업그레이드(설치 프로그램)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 여러 구성 요소를 업그레이드할 수 있는 단일 기능 트리를 제공합니다. 또한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 이전 버전과 함께 설치하거나 기존 데이터베이스 및 구성 설정을 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 마이그레이션하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스에 적용할 수 있습니다.  
  
 자세한 내용은 다음 항목을 참조하세요.  
  
-   [지원되는 버전 및 에디션 업그레이드](supported-version-and-edition-upgrades.md)  
  
-   [여러 버전 및 인스턴스의 SQL Server 작업](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
  
-   [SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
-   [명령 프롬프트에서 SQL Server 2014 설치](install-sql-server-from-the-command-prompt.md)  
  
-   [데이터베이스 복사 마법사 사용](../../relational-databases/databases/use-the-copy-database-wizard.md)  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 로 업그레이드하는 것은 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1을 실행하는 컴퓨터에서 지원되지 않습니다. Server Core 설치에 대 한 자세한 내용은 참조 하세요. [Server Core에 SQL Server 2014 설치](install-sql-server-on-server-core.md)합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있으며 로컬 관리자인 도메인 계정을 사용해야 합니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드하기 전에 다음 항목을 검토하십시오.  
  
-   [SQL Server 2014로 업그레이드](upgrade-sql-server.md)  
  
-   [SQL Server 2014 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [시스템 구성 검사기의 검사 매개 변수](check-parameters-for-the-system-configuration-checker.md)  
  
-   [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [SQL Server 데이터베이스 엔진의 이전 버전과의 호환성](../sql-server-database-engine-backward-compatibility.md)  
  
> [!WARNING]  
>  업그레이드할 기능은 변경할 수 없으며, 업그레이드 작업 중에 기능을 추가할 수도 없습니다. 업그레이드 된 인스턴스에 기능을 추가 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 작업이 완료 되 면 참조 [는 인스턴스에 SQL Server 2014의 기능 추가 &#40;설치&#41;](add-features-to-an-instance-of-sql-server-setup.md)합니다.  
  
## <a name="procedure"></a>프로시저  
  
#### <a name="to-upgrade-to-includesscurrentincludessscurrent-mdmd"></a>다음으로 업그레이드하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더로 이동한 다음 Setup.exe를 두 번 클릭합니다.  
  
2.  설치 마법사가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 시작합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기존 인스턴스에 업그레이드하려면 왼쪽 탐색 영역에서 **설치**를 클릭한 다음 **[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 업그레이드**를 클릭합니다.  
  
3.  제품 키 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]무료 버전으로 업그레이드할지 아니면 제품의 프로덕션 버전에 대한 PID 키가 있는지를 나타내는 옵션을 클릭합니다. 자세한 내용은 [버전 및 SQL Server 2014 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md) 하 고 [Supported Version and Edition Upgrades](supported-version-and-edition-upgrades.md)합니다.  
  
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
  
     **설치된 인스턴스** - 그리드에는 설치 프로그램이 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 표시됩니다. 컴퓨터에 기본 인스턴스가 이미 설치된 경우 명명된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스를 설치해야 합니다.  
  
13. 이 항목의 나머지 부분에 대한 워크플로는 설치에 대해 지정한 기능에 따라 달라집니다. 선택 항목에 따라 일부 페이지가 표시되지 않을 수도 있습니다.  
  
14. 서버 구성 - 서비스 계정 페이지에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 기본 서비스 계정이 표시됩니다. 이 페이지에 구성된 실제 서비스는 사용자가 업그레이드하려는 기능에 따라 달라집니다.  
  
     인증 및 로그인 정보는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 가져옵니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 동일한 로그인 계정을 할당하거나 각 서비스 계정을 따로 구성할 수 있습니다. 서비스 시작 유형을 자동 또는 수동으로 지정하거나 서비스의 해제 여부도 지정할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 는 서비스 계정을 개별적으로 구성하도록 권장합니다. 그러면 "서비스 시작" 태스크 완료에 필요한 최소한의 권한만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 부여됩니다. 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 서비스 계정에 대해 동일한 로그인 계정을 지정하려면 페이지 맨 아래에 있는 필드에 자격 증명을 제공합니다.  
  
     **보안 정보** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 로그인 정보 지정을 완료하면 **다음**을 클릭합니다.  
  
15. 전체 텍스트 검색 업그레이드 옵션 페이지에서 업그레이드하려는 데이터베이스의 업그레이드 옵션을 지정합니다. 자세한 내용은 [전체 텍스트 검색 업그레이드](../../sql-server/install/full-text-search-upgrade-options.md)를 참조하세요.  
  
16. 모든 규칙이 통과하면 기능 규칙 창이 자동으로 진행됩니다.  
  
17. 업그레이드 준비 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 계속하려면 **설치**를 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다.  
  
18. 설치 중에 진행률 페이지에서 제공하는 상태 정보를 통해 설치 진행률을 모니터링할 수 있습니다.  
  
19. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 완료 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다.  
  
20. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 설치 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](view-and-read-sql-server-setup-log-files.md)를 참조하세요.  
  
## <a name="next-steps"></a>다음 단계  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드한 후 다음 태스크를 완료하십시오.  
  
-   **서버 등록** - 업그레이드하면 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 등록 설정이 제거됩니다. 업그레이드한 후 서버를 다시 등록해야 합니다.  
  
-   **통계 업데이트** - 쿼리 성능을 최적화하려면 업그레이드 후에 모든 데이터베이스에 대한 통계를 업데이트하는 것이 좋습니다. `sp_updatestats` 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 있는 사용자 정의 테이블의 통계를 업데이트할 수 있습니다.  
  
-   **새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 구성** - 공격받을 수 있는 시스템의 노출 영역을 줄이려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 핵심 서비스와 기능을 선별적으로 설치하고 활성화합니다. 노출 영역 구성 도구에 대한 자세한 내용은 이 릴리스의 추가 정보 파일을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014로 업그레이드](upgrade-sql-server.md)   
 [이전 버전과의 호환성](../../getting-started/backward-compatibility.md)  
  
  
