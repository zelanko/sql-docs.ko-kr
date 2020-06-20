---
title: Integration Services 설치 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bd3c15610065c4c26da0476d50cac9bd4bd1dacc
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966283"
---
# <a name="install-integration-services"></a>Integration Services 설치
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 비롯한 구성 요소 중 일부 또는 전체를 설치하는 한 개의 설치 프로그램을 제공합니다. 설치 프로그램을 통해 한 개의 컴퓨터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소와 함께 설치하거나 단독으로 설치할 수 있습니다.  
  
 이 항목에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치하기 전에 알아야 할 중요한 고려 사항에 대해 중점적으로 설명합니다. 이 항목의 정보를 통해 설치 옵션을 평가하여 성공적인 설치를 위한 항목을 선택할 수 있습니다.  
  
 이 항목에서는 설치 프로그램 시작, 설치 마법사 사용 또는 명령줄에서 설치 프로그램 실행에 대한 지침을 다루지 않습니다. 설치 프로그램을 시작 하 고 설치할 구성 요소를 선택 하는 방법에 대 한 단계별 지침은 [SQL Server 2014의 빠른 시작 설치](../../getting-started/quick-start-installation-of-sql-server-2014.md)를 참조 하세요. 을 설치 하는 명령줄 옵션에 대 한 자세한 내용은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [명령 프롬프트에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 참조 하세요.  
  
## <a name="preparing-to-install-integration-services"></a>Integration Services 설치 준비  
 를 설치 하기 전에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 다음 요구 사항을 검토 합니다.  
  
-   [SQL Server 2014 설치에 대한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [시스템 구성 검사기의 검사 매개 변수](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)  
  
-   [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
## <a name="selecting-an-integration-services-configuration"></a>Integration Services 구성 선택  
 다음과 같은 구성으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 수 있습니다.  
  
-   이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 없는 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 수 있습니다.  
  
-   [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 및 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 의 기존 인스턴스와 함께 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]를 설치할 수 있습니다.  
  
     이전 버전의 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 중 하나가 이미 설치된 컴퓨터에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 로 업그레이드하면 이전 버전과 함께 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 가 설치됩니다.  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]업그레이드에 대한 자세한 내용은 [Integration Services 업그레이드](upgrade-integration-services.md)를 참조하세요. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]이전 버전과의 호환성에 대한 자세한 내용은 [Integration Services의 이전 버전과의 호환성](../integration-services-backward-compatibility.md)을 참조하세요.  
  
## <a name="installing-integration-services"></a>Integration Services 설치  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 설치 요구 사항을 검토한 결과 컴퓨터가 이러한 요구 사항을 만족하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 준비가 된 것입니다.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하면 기본적으로 Users 그룹의 모든 사용자에게 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 액세스 권한이 부여되었지만 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 설치하면 사용자에게 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 액세스 권한이 부여되지 않습니다. 이 서비스에는 기본적으로 보안이 적용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치 된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자는 Dcomcnfg.exe (DCOM 구성 도구)를 실행 하 여 특정 사용자에 게 **SQL Server Integration Services 12.0**에 대 한 액세스 권한을 부여 해야 합니다.  
>   
>  사용 권한을 부여하는 방법에 대한 자세한 내용은 [Grant Permissions to Integration Services Service](../grant-permissions-to-integration-services-service.md)를 참조하십시오.  
  
 설치 마법사를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치하는 경우 구성 요소와 옵션을 지정하는 일련의 페이지가 표시됩니다. 선택 하는 옵션은 선택 권장 사항을 사용 하 여 설치에 영향을 미치는 설치 마법사의 페이지는 다음과 같습니다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   **기능 선택**  
  
     **Integration Services** 를 선택하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 설치되고 디자인 환경 외부에서 패키지가 실행됩니다.  
  
     패키지 개발과 관리를 위한 도구 및 설명서와 함께 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 전체 설치하려면 **Integration Services** 와 다음 **공유 기능**을 선택합니다.  
  
    -   **SQL Server Data Tools** 를 선택합니다.  
  
    -   패키지 관리를 위한**를 설치하려면** 관리 도구 - 전체 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 선택합니다.  
  
    -   **프로그래밍을 위한 관리되는 어셈블리를 설치하려면** 클라이언트 도구 SDK [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 선택합니다.  
  
     또한 많은 데이터 웨어하우징 솔루션에는,, 등의 추가 구성 요소를 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    > [!NOTE]  
    >  설치 마법사의 **기능 선택** 페이지에서 선택하여 설치할 수 있는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소의 일부분만 설치합니다. 이러한 구성 요소는 특정 태스크에 유용하지만 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 기능은 제한됩니다. 예를 들어 **데이터베이스 엔진 서비스** 옵션을 선택하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가져오기 및 내보내기 마법사에 필요한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소가 설치됩니다. **SQL Server Data Tools** 옵션을 선택하면 패키지 디자인에 필요한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소는 설치되지만 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 설치되지 않으므로 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]외부에서 패키지를 실행할 수 없습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 전체 설치하려면 **기능 선택** 페이지에서 **Integration Services** 를 선택해야 합니다.  
  
     **64 비트 컴퓨터에 설치** 64 비트 컴퓨터에서 **Integration Services** 를 선택 하면 64 비트 런타임 및 도구만 설치 됩니다. 패키지를 32비트 모드로 실행해야 하는 경우 32비트 런타임 및 도구를 설치하는 추가 옵션도 선택해야 합니다.  
  
    -   64 비트 컴퓨터에서 x86 운영 체제를 실행 하는 경우 **SQL Server Data Tools** 또는 **관리 도구-전체**를 선택 합니다.  
  
    -   64 비트 컴퓨터에서 운영 체제를 실행 하는 경우 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] **관리 도구-전체**를 선택 합니다.  
  
     **ETL용 전용 서버 설치** ETL(추출, 변환 및 로드) 프로세스에 전용 서버를 사용하려면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 를 설치할 때 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 로컬 인스턴스를 설치하는 것이 좋습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 일반적으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 패키지를 저장하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 패키지를 예약합니다. ETL 서버에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스가 없는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스가 있는 서버에서 패키지를 예약 또는 실행해야 합니다. 이는 패키지가 ETL 서버에서 실행되지 않고 해당 패키지가 시작된 서버에서 실행됨을 의미합니다. 따라서 전용 ETL 서버의 리소스는 의도대로 사용되지 않습니다. 또한 다른 서버의 리소스가 실행 중인 ETL 프로세스에 의해 소모될 수 있습니다.  
  
-   **인스턴스 구성**  
  
     **인스턴스 구성** 페이지에서 선택할 수 있는 항목은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 영향을 미치지 않습니다.  
  
     컴퓨터에는 하나의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 인스턴스만 설치할 수 있습니다. 컴퓨터 이름을 사용하여 서비스에 연결하십시오.  
  
     기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 **와 동시에 설치되는 데이터베이스 엔진 인스턴스의** msdb [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]데이터베이스에 저장된 패키지를 관리하도록 구성됩니다. 데이터베이스 인스턴스가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]와 동시에 설치되지 않는 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 **의 로컬 기본 인스턴스에 있는** msdb [!INCLUDE[ssDE](../../includes/ssde-md.md)]데이터베이스에 저장된 패키지를 관리하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 명명된 인스턴스나 원격 인스턴스 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 여러 인스턴스에 저장된 패키지를 관리하려면 구성 파일을 수정해야 합니다. 이 구성 파일을 수정하는 방법은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](../service/integration-services-service-ssis-service.md)을 참조하세요.  
  
-   **서버 구성**  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버 구성 **페이지의** 서비스 계정 **탭에서** 서비스에 대한 설정을 검토합니다.  
  
     Windows 7 또는 Windows Server 2008 r 2가 설치 된 경우이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 NT Services\MsDtsServer120 가상 계정에서 실행 되도록 등록 되며 **시작 유형은** **자동**입니다.  가상 계정에 대한 암호는 입력할 필요가 없습니다. Microsoft Vista 또는 Windows Server 2008이 설치되어 있으면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 기본 제공 네트워크 서비스 계정에서 실행되도록 등록되며 **시작 유형** 은 **자동**입니다. 기본 제공 네트워크 서비스 계정에 대한 암호는 입력할 필요가 없습니다.  
  
 기본적으로 새로 설치하는 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지 실행과 관련된 이벤트를 애플리케이션 이벤트 로그에 기록하지 않도록 구성됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 데이터 수집기 기능을 사용하는 경우 이 설정은 이벤트 로그 항목이 너무 많이 생성되지 않도록 방지합니다. 기록되지 않는 이벤트는 EventID 12288, "패키지가 시작되었습니다" 및 EventID 12289, "패키지가 성공적으로 완료되었습니다"입니다. 이러한 이벤트를 애플리케이션 이벤트 로그에 기록하려면 편집을 위해 레지스트리를 엽니다. 그런 다음 레지스트리에서 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS 노드를 찾고 LogPackageExecutionToEventLog 설정의 DWORD 값을 0에서 1로 변경합니다.  
  
## <a name="understanding-the-integration-services-service"></a>Integration Services 서비스 이해  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 설치합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 기능 선택 **페이지에서** Integration Services **옵션을 선택하면** 서비스가 설치됩니다. **서버 구성** 페이지의 기본 설정을 적용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 활성화되며 이 경우 **시작 유형** 은 **자동**입니다.  
  
 컴퓨터에는 하나의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 인스턴스만 설치할 수 있습니다. 서비스는 특정 데이터베이스 엔진 인스턴스에 국한되지 않습니다. 서비스가 실행 중인 컴퓨터의 이름을 사용하여 서비스에 연결하십시오.  
  
## <a name="installing-integration-services-on-64-bit-computers"></a>64비트 컴퓨터에 Integration Services 설치  
  
### <a name="integration-services-features-installed-on-64-bit-computers"></a>64비트 컴퓨터에 설치되는 Integration Services 기능  
 설치 프로그램에서는 사용자가 선택한 설치 옵션에 따라 다양한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 기능을 설치합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 설치를 선택하면 사용 가능한 모든 64비트 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 기능 및 도구가 설치됩니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 디자인 타임 기능이 필요한 경우 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]도 설치해야 합니다.  
  
-   특정 패키지를 32비트 모드로 실행하기 위해 32비트 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임 및 도구가 필요한 경우 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]도 설치해야 합니다.  
  
 64비트 기능은 **Program Files** 디렉터리에 설치되며 32비트 기능은 **Program Files (x86)** 디렉터리에 별도로 설치됩니다. 이 동작은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 한정되지 않습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지용 32비트 개발 환경인 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 64비트 운영 체제에서 지원되지 않으며 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 서버에 설치되지도 않습니다.  
  
  
