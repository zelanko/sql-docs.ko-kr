---
title: Integration Services 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, upgrading
- SSIS, upgrading
- SQL Server Integration Services, upgrading
- upgrading Integration Services
ms.assetid: 04f9863c-ba0b-47c5-af91-f2d41b078a23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b6abc8e9e025bc24b4f456b58e0e9625e66b4b71
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "49072027"
---
# <a name="upgrade-integration-services"></a>Integration Services 업그레이드
  [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 또는 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]가 현재 컴퓨터에 설치되어 있으면 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]로 업그레이드할 수 있습니다.  
  
 이전 버전의 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 중 하나가 설치된 컴퓨터에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 로 업그레이드하면 이전 버전과 함께 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 가 설치됩니다.  
  
 함께 설치하면 여러 버전의 dtexec 유틸리티가 설치됩니다. 올바른 버전의 유틸리티가 실행되도록 하려면 명령 프롬프트에서 전체 경로(\<drive>:\Program Files\Microsoft SQL Server\\<version\>\DTS\Binn)를 입력하는 방식으로 유틸리티를 실행합니다. dtexec에 대한 자세한 내용은 [dtexec Utility](../packages/dtexec-utility.md)를 참조하십시오.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하면 기본적으로 Users 그룹의 모든 사용자에게 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 액세스 권한이 부여되었지만 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 설치하면 사용자에게 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 액세스 권한이 부여되지 않습니다. 이 서비스에는 기본적으로 보안이 적용됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 설치한 후 DCOM 구성 도구(Dcomcnfg.exe)를 실행하여 특정 사용자에게 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 액세스 권한을 부여해야 합니다. 자세한 내용은 [Grant Permissions to Integration Services Service](../grant-permissions-to-integration-services-service.md)을(를) 참조하세요.  
  
## <a name="before-upgrading-integration-services"></a>Integration Services를 업그레이드하기 전에  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하기 전에 먼저 업그레이드 관리자를 실행하는 것이 좋습니다. 업그레이드 관리자는 기존 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 사용되는 새로운 패키지 형식으로 마이그레이션하는 경우 발생할 수 있는 문제를 보고합니다. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
> [!NOTE]  
>  마이그레이션 또는 실행 Data Transformation Services (dts)도 지원 되지 않습니다 현재 릴리스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]합니다. 다음 DTS 기능이 더 이상 사용되지 않습니다.  
>   
>  -   DTS 런타임  
> -   DTS API  
> -   DTS 패키지를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
> -   다음 DTS 패키지 유지 관리 지원: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
> -   DTS 2000 패키지 실행 태스크  
> -   DTS 패키지의 업그레이드 관리자 검색입니다.  
>   
>  지원 되지 않는 다른 기능에 대 한 정보를 참조 하세요 [SQL Server 2014에서는 Integration Services 기능 지원 되지 않는](../discontinued-integration-services-functionality-in-sql-server-2014.md)합니다.  
  
## <a name="upgrading-integration-services"></a>Integration Services 업그레이드  
 다음 방법 중 하나를 사용하여 업그레이드할 수 있습니다.  
  
-   실행할 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 옵션을 선택 하 고 **SQL Server 2005, SQL Server 2008 또는 SQL Server 2008 R2에서 업그레이드**, 또는 **[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]** 합니다.  
  
-   실행 **setup.exe** 명령 프롬프트에서 지정 된 `/ACTION=upgrade` 옵션입니다. 자세한 내용은 섹션을 참조 하세요. "용 설치 스크립트 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)],"의 [명령 프롬프트에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)합니다.  
  
 다음 동작은 업그레이드를 사용하여 수행할 수 없습니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 기존 설치 다시 구성  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32비트에서 64비트 버전으로 전환, 또는 64비트 버전에서 32비트 버전으로 전환  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 한 언어 버전에서 다른 언어 버전으로 전환  
  
 업그레이드할 때 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 와 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 모두 업그레이드하거나 [!INCLUDE[ssDE](../../includes/ssde-md.md)]만 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]만 업그레이드할 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]만 업그레이드하는 경우 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 또는 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]는 계속 작동하지만 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]의 기능은 사용할 수 없습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]만 업그레이드하는 경우 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 의 모든 기능이 작동하지만 [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)] 인스턴스를 다른 컴퓨터에서 사용할 수 있는 경우가 아니면 패키지를 파일 시스템에만 저장할 수 있습니다.  
  
## <a name="upgrading-both-integration-services-and-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>Integration Services와 데이터베이스 엔진 모두 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 이 섹션에서는 다음 조건에 해당하는 업그레이드를 수행할 때 나타나는 결과에 대해 설명합니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 모두 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하는 경우  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 같은 컴퓨터에 있는 경우  
  
### <a name="what-the-upgrade-process-does"></a>업그레이드 프로세스에서 수행하는 태스크  
 업그레이드 프로세스에서는 다음 태스크를 수행합니다.  
  
-   [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 파일, 서비스 및 도구([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 및 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)])를 설치합니다. 한 컴퓨터에 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 인스턴스가 여러 개 있을 경우 아무 인스턴스나 처음으로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드할 때 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 파일, 서비스 및 도구가 설치됩니다.  
  
-   인스턴스를 업그레이드 합니다 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전입니다.  
  
-   데이터를 이동 합니다 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 또는 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 시스템 테이블을 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 다음과 같은 시스템 테이블:  
  
    -   msdb.dbo.sysdtspackages90 시스템 테이블에서 msdb.dbo.sysssispackages 시스템 테이블로 패키지를 변경하지 않고 이동합니다.  
  
        > [!NOTE]  
        >  데이터를 다른 시스템 테이블로 이동하지만 패키지를 새 형식으로 마이그레이션하지는 않습니다.  
  
    -   msdb.sysdtsfolders90 시스템 테이블에서 msdb.sysssisfolders 시스템 테이블로 폴더 메타데이터를 이동합니다.  
  
    -   msdb.sysdtslog90 시스템 테이블에서 msdb.sysssislog 시스템 테이블로 로그 데이터를 이동합니다.  
  
-   데이터를 새 msdb.sysssis\* 테이블로 이동한 후 msdb.sysdts*90 시스템 테이블 및 이 시스템 테이블에 액세스하는 데 사용되는 저장 프로시저를 제거합니다. 그러나 업그레이드하면 sysdtslog90 테이블은 똑같이 sysdtslog90이라는 이름을 가진 뷰로 대체됩니다. 이 새 sysdtslog90 뷰에는 새 msdb.sysssislog 시스템 테이블이 표시됩니다. 이를 통해 로그 테이블 기반의 보고서가 중단 없이 계속 실행됩니다.  
  
-   패키지에 대한 액세스를 제어하기 위해 세 가지 새로운 고정 데이터베이스 수준 역할인 db_ssisadmin, db_ssisltduser 및 db_ssisoperator를 만듭니다. db_dtsadmin, db_dtsltduser 및 db_dtsoperator의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 역할은 제거되지 않고 해당하는 새 역할의 멤버가 됩니다.  
  
-   경우는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소 (즉, 파일 시스템 위치를 관리 하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스) 아래의 기본 위치인 **\SQL Server\90**를 **\SQL Server\100**, 또는 **\SQL Server\110** 패키지만 아래의 새 기본 위치로 이동 **SERVER\120**합니다.  
  
-   업그레이드된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인스턴스를 가리키도록 [!INCLUDE[ssDE](../../includes/ssde-md.md)]서비스 구성 파일을 업데이트합니다.  
  
### <a name="what-the-upgrade-process-does-not-do"></a>업그레이드 프로세스에서 수행하지 않는 태스크  
 업그레이드 프로세스에서는 다음 태스크를 수행하지 않습니다.  
  
-   **않습니다** 제거 합니다 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 또는 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 서비스입니다.  
  
-   기존 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 사용되는 새 패키지 형식으로 마이그레이션하지 않습니다. 패키지를 마이그레이션하는 방법은 [Integration Services 패키지 업그레이드](upgrade-integration-services-packages.md)를 참조하세요.  
  
-   서비스 구성 파일에 추가된 기본 위치가 아닌 파일 시스템 위치에서 패키지를 이동하지 않습니다. 이전에 서비스 구성 파일을 편집하여 파일 시스템 폴더를 추가한 경우 이러한 폴더에 저장된 패키지는 새 위치로 이동되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 **dtexec** 유틸리티(dtexec.exe)를 직접 호출하는 작업 단계는 **dtexec** 유틸리티에 대한 파일 시스템 경로를 업데이트하지 않습니다. 이러한 작업 단계는 수동으로 편집하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dtexec **유틸리티에 대한** 위치를 지정하도록 파일 시스템 경로를 업데이트해야 합니다.  
  
### <a name="what-you-can-do-after-upgrading"></a>업그레이드한 후 수행할 수 있는 태스크  
 업그레이드 프로세스가 완료되면 다음 태스크를 수행할 수 있습니다.  
  
-   패키지를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 실행합니다.  
  
-   사용 하 여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 관리할 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인스턴스에 저장 된 패키지를 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 인스턴스를 서비스에서 관리하는 위치 목록에 추가하려면 서비스 구성 파일을 수정해야 합니다.  
  
    > [!NOTE]  
    >  이전 버전의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 서비스에 연결할 수 없습니다.  
  
-   packageformat 열의 값을 확인하여 msdb.dbo.sysssispackages 시스템 테이블에서 패키지 버전을 식별합니다. 테이블에는 각 패키지의 버전을 식별하는 packageformat 열이 있습니다. packageformat 열 값이 2이면 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 패키지를, 3이면 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 패키지를 나타냅니다. 패키지를 새 패키지 형식으로 마이그레이션할 때까지 packageformat 열 값은 변경되지 않습니다.  
  
-   사용할 수 없습니다는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 도구를 디자인, 실행 또는 관리할 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 도구에는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사, 그리고 패키지 실행 유틸리티(dtexecui.exe)가 포함되어 있습니다. 업그레이드 프로세스를 제거 하지 않습니다 합니다 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]도구입니다. 그러나 업그레이드된 서버에서 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 또는 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 패키지에 대한 작업을 수행하는 데 이러한 도구를 계속 사용할 수는 없습니다.  
  
-   기본적으로 업그레이드 설치의 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지 실행과 관련된 이벤트를 애플리케이션 이벤트 로그에 로깅하도록 구성됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 데이터 수집기 기능을 사용하는 경우 이 설정으로 인해 이벤트 로그 항목이 너무 많이 생성될 수 있습니다. 로깅되는 이벤트에는 EventID 12288, "패키지가 시작되었습니다" 및 EventID 12289, "패키지가 성공적으로 완료되었습니다"가 포함됩니다. 이러한 이벤트가 애플리케이션 이벤트 로그에 로깅되지 않도록 하려면 편집을 위해 레지스트리를 엽니다. 그런 다음 레지스트리에서 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS 노드를 찾고 LogPackageExecutionToEventLog 설정의 DWORD 값을 1에서 0으로 변경합니다.  
  
## <a name="upgrading-only-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>데이터베이스 엔진만 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 이 섹션에서는 다음 조건에 해당하는 업그레이드를 수행할 때 나타나는 결과에 대해 설명합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스만 업그레이드하는 경우. 즉, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스가 되지만 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인스턴스 및 클라이언트 도구는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에 속하는 경우입니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 한 컴퓨터에 있고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 클라이언트 도구가 다른 컴퓨터에 있는 경우  
  
### <a name="what-you-can-do-after-upgrading"></a>업그레이드한 후 수행할 수 있는 태스크  
 업그레이드된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 패키지를 저장하는 시스템 테이블은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 사용되는 시스템 테이블과 다릅니다. 따라서 합니다 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 버전의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 및 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 업그레이드 된 인스턴스의 시스템 테이블에서 패키지를 검색할 수 없습니다는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]합니다. 이러한 패키지는 검색할 수 없으므로 이에 대해 수행할 수 있는 작업은 다음과 같이 제한됩니다.  
  
-   다른 컴퓨터에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 도구인 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 및 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 사용하여 업그레이드된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 패키지를 로드하거나 관리할 수 없습니다.  
  
    > [!NOTE]  
    >  업그레이드된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 패키지가 아직 새 패키지 형식으로 마이그레이션되지 않은 경우에도 이러한 패키지는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 도구로 검색할 수 없습니다. 따라서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 도구에서 이러한 패키지를 사용할 수 없습니다.  
  
-   사용할 수 없습니다 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 또는 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 업그레이드 된 인스턴스에서 msdb에 저장 된 패키지를 실행 하려면 다른 컴퓨터는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 컴퓨터의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 에이전트 작업을 사용하여 업그레이드된 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 인스턴스에 저장된 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 패키지를 실행할 수 없습니다.  
  
## <a name="external-resources"></a>외부 리소스  
 blogs.msdn.com의 블로그 항목 - [기존 사용자 지정 SSIS 확장 프로그램 및 애플리케이션을 Denali에서 사용되도록 설정](http://go.microsoft.com/fwlink/?LinkId=238157)  
  
  
