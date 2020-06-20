---
title: 설치 마법사에서 SQL Server 2014 설치 (설치 프로그램) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0561ff95fc5fbcfb6a9dc552580e14ff2a5d14f1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932728"
---
# <a name="install-sql-server-2014-from-the-installation-wizard-setup"></a>설치 마법사에서 SQL Server 2014 설치(설치 프로그램)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 마법사를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 새 인스턴스를 설치하는 절차를 단계별로 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 모든 구성 요소를 설치할 수 있는 단일 기능 트리를 제공하므로 구성 요소를 개별적으로 설치할 필요가 없습니다. 설치할 수 있는 다양 한 구성 요소에 대 한 자세한 내용은 [SQL Server 2014에 대 한 설치](installation-for-sql-server.md)를 참조 하세요.  구성 요소를 개별적으로 설치 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 2014 설치](install-sql-server.md)를 참조 하세요.  
  
 다음 추가 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 다른 방법을 설명합니다.  
  
-   [명령 프롬프트에서 SQL Server 2014을 설치](install-sql-server-from-the-command-prompt.md)합니다.  
  
-   [구성 파일을 사용하여 SQL Server 2014 설치](install-sql-server-using-a-configuration-file.md)  
  
-   [SysPrep을 사용하여 SQL Server 2014 설치](install-sql-server-using-sysprep.md)  
  
-   [설치&#41;&#40;SQL Server 장애 조치 (Failover) 클러스터를 새로 만듭니다 ](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md).  
  
-   [설치 마법사 &#40;설치&#41;를 사용 하 여 SQL Server 2014로 업그레이드 ](upgrade-sql-server-using-the-installation-wizard-setup.md)합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하기 전에 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)을 검토하세요.  
  
> [!NOTE]  
>  로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.  
  
### <a name="to-install-sscurrent"></a>다음을 설치하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더를 찾은 다음 Setup.exe를 두 번 클릭합니다.  
  
2.  설치 마법사가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 설치를 만들려면 왼쪽 탐색 영역에서 **설치**를 클릭한 다음 **새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭합니다.  
  
3.  제품 키 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 무료 버전을 설치할지 아니면 PID 키가 있는 제품의 프로덕션 버전을 설치할지를 나타내는 옵션을 선택합니다. 자세한 내용은 [SQL Server 2014의 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md)를 참조 하세요.  
  
     계속하려면 **다음**을 클릭합니다.  
  
4.  사용 조건 페이지에서 사용권 계약을 검토하고 동의하면 **동의함** 확인란을 선택한 다음 **다음**을 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 개선을 돕기 위해 기능 사용 옵션을 사용하도록 설정하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)]로 보고서를 보낼 수도 있습니다.  
  
5.  전역 규칙 창에서 규칙 오류가 없는 경우 설치 절차는 제품 업데이트 창으로 자동으로 진행됩니다.  
  
6.  다음에 Control Panel\All Control Panel Items\Windows Update\Change 설정에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 업데이트 확인란을 선택하지 않으면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 업데이트 페이지가 나타납니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 업데이트 페이지에서 확인란을 선택하면 Windows Update를 검색하는 경우 최신 업데이트를 포함하도록 컴퓨터 설정이 변경됩니다.  
  
7.  제품 업데이트 페이지에는 사용 가능한 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 업데이트가 표시됩니다. 제품 업데이트가 검색되지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 이 페이지가 표시되지 않으며 **설치 파일 설치** 페이지로 자동으로 진행됩니다.  
  
8.  설치 프로그램에서 설치 파일 설치 페이지에는 설치 파일의 다운로드, 추출 및 설치 진행률이 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 대한 업데이트가 발견되고 이러한 업데이트가 포함되도록 지정된 경우 해당 업데이트도 함께 설치됩니다.  
  
9. 설치 역할 페이지에서 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 설치**를 선택하고 **다음** 을 클릭하여 기능 선택 페이지를 계속 진행합니다.  
  
10. 기능 선택 페이지에서 설치할 구성 요소를 선택합니다. 기능 이름을 선택하면 **기능 설명** 창에 각 구성 요소 그룹에 대한 설명이 나타납니다. 확인란을 자유롭게 조합하여 선택할 수 있습니다. 자세한 내용은 [SQL Server 2014의 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md) 및 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조 하세요.  
  
     선택한 기능의 필수 구성 요소가 **선택한 기능의 필수 구성 요소** 창에 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서는 이미 설치되어 있지 않은 필수 구성 요소가 있는 경우 이 절차의 뒷부분에 설명된 설치 단계에서 이를 설치합니다.  
  
     또한 기능 선택 페이지 아래의 필드를 사용하여 공유 구성 요소의 사용자 지정 디렉터리를 지정할 수 있습니다. 공유 구성 요소의 설치 경로를 변경하려면 대화 상자의 맨 아래에 있는 필드에서 경로를 업데이트하거나 **찾아보기** 를 클릭하여 설치 디렉터리로 이동합니다. 기본 설치 경로는 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]입니다.  
  
     공유 구성 요소에 대해 절대 경로를 지정해야 합니다. 폴더는 압축하거나 암호화해서는 안 됩니다. 매핑된 드라이브는 지원되지 않습니다.  
  
     64비트 운영 체제에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하는 경우 다음 옵션이 표시됩니다.  
  
    1.  공유 기능 디렉터리  
  
    2.  공유 기능 디렉터리(x86)  
  
     위의 각 옵션에 대해 다른 경로를 지정해야 합니다.  
  
11. 모든 규칙이 통과하면 기능 규칙 창이 자동으로 진행됩니다.  
  
12. 인스턴스 구성 페이지에서 기본 인스턴스를 설치할지 명명된 인스턴스를 설치할지 지정합니다. 자세한 내용은 [Instance Configuration](../../sql-server/install/instance-configuration.md)을 참조하세요.  
  
     **인스턴스 id** -기본적으로 인스턴스 이름이 인스턴스 id로 사용 됩니다. 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 기본 인스턴스의 경우 인스턴스 이름 및 인스턴스 ID는 MSSQLSERVER입니다. 기본값이 아닌 인스턴스 ID를 사용하려면 **인스턴스 ID** 입력란에 다른 값을 지정합니다.  
  
    > [!NOTE]  
    >  일반적인 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]독립 실행형 인스턴스의 경우 기본 인스턴스인지 명명된 인스턴스인지에 관계없이 **인스턴스 ID**에 기본값을 사용합니다.  
  
     모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 팩 및 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 구성 요소에 적용됩니다.  
  
     **설치된 인스턴스** - 설치 프로그램을 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 표 형식으로 표시됩니다. 컴퓨터에 기본 인스턴스가 이미 설치된 경우 명명된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스를 설치해야 합니다.  
  
     설치의 나머지 부분에 대한 워크플로는 설치에 대해 지정한 기능에 따라 달라집니다. 선택 항목에 따라 일부 페이지가 표시되지 않을 수도 있습니다.  
  
13. 서버 구성 - 서비스 계정 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 로그인 계정을 지정합니다. 이 페이지에 구성된 실제 서비스는 사용자가 설치하도록 선택한 기능에 따라 달라집니다.  
  
     모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 동일한 로그인 계정을 할당하거나 각 서비스 계정을 따로 구성할 수 있습니다. 서비스 시작 유형을 자동 또는 수동으로 지정하거나 서비스의 해제 여부도 지정할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 서비스 계정을 개별적으로 구성하여 각 서비스에 대해 최소한의 권한만 제공할 것을 권장합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에서 태스크를 완료하는 데 필요한 최소한의 권한만 부여할 수 있습니다. 자세한 내용은 [서버 구성 - 서비스 계정](../../sql-server/install/server-configuration-service-accounts.md) 및 [Windows 서비스 계정 및 권한 구성](../configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 서비스 계정에 대해 동일한 로그온 계정을 지정하려면 페이지 맨 아래에 있는 필드에 자격 증명을 입력합니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     서버 구성 - 데이터 정렬 페이지를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 기본이 아닌 데이터 정렬을 지정합니다. 자세한 내용은 [서버 구성 - 데이터 정렬](../../sql-server/install/server-configuration-collation.md)을 참조하세요.  
  
14. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 – 서버 구성 페이지를 사용하여 다음을 지정합니다.  
  
    -   보안 모드 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 인증(Windows 인증 또는 혼합 모드 인증)을 선택합니다. 혼합 모드 인증을 선택할 경우 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자 계정에 강력한 암호를 제공해야 합니다.  
  
         디바이스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 성공적으로 연결되면 Windows 인증 및 혼합 모드에 모두 동일한 보안 메커니즘이 적용됩니다. 자세한 내용은 [Database Engine Configuration - Account Provisioning](../../sql-server/install/database-engine-configuration-account-provisioning.md)을 참조하세요.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 시스템 관리자를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하는 계정을 추가하려면 **현재 사용자 추가**를 클릭합니다. 시스템 관리자 목록에 계정을 추가하거나 목록의 계정을 제거하려면 **추가** 또는 **제거**를 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 관리자 권한을 가질 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.  
  
     [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 - 데이터 디렉터리 페이지를 사용하여 기본이 아닌 설치 디렉터리를 지정합니다. 기본 디렉터리에 설치하려면 **다음**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. 또한 드라이브의 루트 폴더나 마운트 지점에 데이터 디렉터리가 있게 SQL Server를 설치할 수 없습니다. 자세한 내용은 [탑재 된 볼륨에 대 한 SQL Server 지원](https://support.microsoft.com/kb/819546/en-us) 을 참조 하세요.  
  
     자세한 내용은 [데이터베이스 엔진 구성 - 데이터 디렉터리](../../sql-server/install/database-engine-configuration-data-directories.md)를 참조하세요.  
  
     [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 - FILESTREAM 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 FILESTREAM을 설정합니다. 자세한 내용은 [데이터베이스 엔진 구성 - Filestream](../../sql-server/install/database-engine-configuration-filestream.md)을 참조하세요.  
  
15. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 - 계정 프로비전 페이지를 사용하여 서버 모드와 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대해 관리자 권한을 갖는 사용자 또는 계정을 지정합니다. 서버 모드에 따라 해당 서버에서 사용되는 메모리 및 스토리지 하위 시스템이 결정됩니다. 각 솔루션 유형은 서로 다른 서버 모드로 실행됩니다. 서버에서 다차원 큐브 데이터베이스를 실행하려면 기본 옵션인 다차원 및 데이터 마이닝 서버 모드를 선택합니다. 관리자 권한의 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대해 시스템 관리자를 한 명 이상 지정해야 합니다. SQL Server 설치 프로그램을 실행하는 계정을 추가하려면 **현재 사용자 추가(Add Current User)** 를 클릭합니다. 시스템 관리자 목록에 계정을 추가하거나 목록의 계정을 제거하려면 **추가** 또는 **제거**를 클릭한 다음 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 관리자 권한을 가질 사용자, 그룹 또는 컴퓨터 목록을 편집합니다. 서버 모드 및 관리자 권한에 대한 자세한 내용은 [Analysis Services 구성 - 계정 프로비전](../../sql-server/install/analysis-services-configuration-account-provisioning.md)을 참조하세요.  
  
     목록 편집을 마쳤으면 **확인**을 클릭합니다. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록 구성을 완료했으면 **다음**을 클릭합니다.  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 - 데이터 디렉터리 페이지를 사용하여 기본이 아닌 설치 디렉터리를 지정합니다. 기본 디렉터리에 설치하려면 **다음**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. 또한 드라이브의 루트 폴더나 마운트 지점에 데이터 디렉터리가 있게 SQL Server를 설치할 수 없습니다. 자세한 내용은 [탑재 된 볼륨에 대 한 SQL Server 지원](https://support.microsoft.com/kb/819546/en-us) 을 참조 하세요.  
  
     자세한 내용은 [Analysis Services 구성 - 데이터 디렉터리](../../sql-server/install/analysis-services-configuration-data-directories.md)를 참조하세요.  
  
16. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 페이지를 사용하여 만들 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 유형을 지정할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 모드 및 사용 가능한 옵션에 대한 자세한 내용은 [Reporting Services 구성 옵션&#40;SSRS&#41;](../../sql-server/install/reporting-services-configuration-options-ssrs.md)을 참조하세요.  
  
     옵션을 선택한 후 **다음** 을 클릭하여 작업을 계속 진행합니다.  
  
17. Distributed Replay Controller 구성 페이지를 사용하여 Distributed Replay Controller 서비스에 대한 관리 권한을 부여할 사용자를 지정합니다. 관리 권한이 있는 사용자는 Distributed Replay Controller 서비스에 무제한으로 액세스할 수 있습니다.  
  
     Distributed Replay Controller 서비스에 대한 액세스 권한을 부여할 사용자를 추가하려면 **현재 사용자 추가** 단추를 클릭합니다. Distributed Replay Controller 서비스에 대한 액세스 권한을 추가하려면 **추가** 단추를 클릭합니다. Distributed Replay Controller 서비스에서 액세스 권한을 제거하려면 **제거** 단추를 클릭합니다.  
  
     계속하려면 **다음**을 클릭합니다.  
  
18. Distributed Replay Client 구성 페이지를 사용하여 Distributed Replay Client 서비스에 대한 관리 권한을 부여할 사용자를 지정합니다. 관리 권한이 있는 사용자는 Distributed Replay Client 서비스에 무제한으로 액세스할 수 있습니다.  
  
     **컨트롤러 이름** 은 선택적 매개 변수 이며 기본값은 \<*blank*> 입니다. 클라이언트 컴퓨터에서 Distributed Replay Client 서비스를 위해 통신할 컨트롤러의 이름을 입력합니다. 다음 사항에 유의하세요.  
  
    -   컨트롤러를 이미 설정한 경우 각 클라이언트를 구성할 때 컨트롤러의 이름을 입력합니다.  
  
    -   컨트롤러를 아직 설정하지 않은 경우에는 컨트롤러 이름을 비워 둡니다. 그러나 **클라이언트 구성** 파일에서 컨트롤러 이름을 수동으로 입력해야 합니다.  
  
     Distributed Replay 클라이언트 서비스의 **작업 디렉터리** 를 지정 합니다. 기본 작업 디렉터리는 \<*drive letter*> 파일 \ \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \DReplayClient\WorkingDir \\ 입니다.  
  
     Distributed Replay 클라이언트 서비스의 **결과 디렉터리** 를 지정 합니다. 기본 결과 디렉터리는 \<*drive letter*> 파일 \ 파일 \ \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \DReplayClient\ResultDir \\ 입니다.  
  
     계속하려면 **다음**을 클릭합니다.  
  
19. 설치 준비 완료 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 설치 프로그램의 이 페이지에서는 제품 업데이트 기능이 사용하도록 설정되었는지 여부와 최종 업데이트 버전이 표시됩니다.  
  
     계속하려면 **설치**를 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다.  
  
20. 설치 중에 설치 진행률 페이지에서 제공하는 상태 정보를 통해 설치 진행률을 모니터링할 수 있습니다.  
  
21. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 완료 페이지에 제공됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 과정을 완료하려면 **닫기**를 클릭합니다.  
  
22. 컴퓨터를 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](view-and-read-sql-server-setup-log-files.md)을 참조하세요.  
  
## <a name="next-steps"></a>다음 단계  
 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 구성합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 공격받을 수 있는 시스템의 노출 영역을 줄이기 위해 핵심 서비스와 기능을 선별적으로 설치하고 활성화합니다. 자세한 내용은 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 유효성 검사](validate-a-sql-server-installation.md)   
 [SQL Server 2014 설치 삭제](repair-a-failed-sql-server-installation.md)   
 [SQL Server 설치 로그 파일 보기 및 읽기](view-and-read-sql-server-setup-log-files.md)   
 [설치 마법사 &#40;사용 하 여 SQL Server 2014로 업그레이드&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Install SQL Server 2014 from the Command Prompt](install-sql-server-from-the-command-prompt.md)  
  
  
