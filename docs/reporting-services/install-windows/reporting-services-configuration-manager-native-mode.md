---
title: Reporting Services 구성 관리자(기본 모드) | Microsoft Docs
ms.date: 09/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c6ea2a8ad189f5973b6fa3bb761be5c8596de761
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503634"
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Reporting Services 구성 관리자(기본 모드)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 설치를 구성할 수 있습니다. 파일 전용 설치 옵션을 사용하여 보고서 서버를 설치한 경우, 이를 사용할 수 있으려면 먼저 구성 관리자를 사용해서 서버를 구성해야 합니다. 기본 구성 설치 옵션을 사용하여 보고서 서버를 설치한 경우에는 구성 관리자를 사용하여 설치 중에 지정된 설정을 확인하거나 수정할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하면 로컬 또는 원격 보고서 서버 인스턴스를 구성할 수 있습니다.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 릴리스부터는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자가 SharePoint 모드 보고서 서버를 관리하도록 디자인되지 않았습니다. SharePoint 모드는 SharePoint 중앙 관리 및 PowerShell 스크립트를 사용하여 관리 및 구성됩니다.  
  
##  <a name="bkmk_scenarios"></a> Reporting Services 구성 관리자 사용 시나리오  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 수행할 수 있는 태스크는 다음과 같습니다.  
  
-   보고서 서버 서비스 계정 구성. 이 계정은 설치 중에 처음 구성되지만 암호를 업데이트하거나 다른 계정을 사용하려는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 수정할 수 있습니다.  
  
-   URL 만들기 및 구성. 보고서 서버와 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 은(는) URL을 통해 액세스되는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 애플리케이션입니다. 보고서 서버 URL을 사용하면 보고서 서버의 SOAP 엔드포인트에 액세스할 수 있으며 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] URL은 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 을(를) 여는 데 사용됩니다. 각 애플리케이션에 대해 URL을 한 개 또는 여러 개 구성할 수 있습니다.  
  
-   보고서 서버 데이터베이스 만들기 및 구성. 보고서 서버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 내부 스토리지로 사용하는 상태 비저장 서버입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 보고서 서버 데이터베이스에 대한 연결을 만들고 구성할 수 있습니다. 사용하려는 내용이 이미 포함되어 있는 기존 보고서 서버 데이터베이스를 선택할 수도 있습니다.  
  
-   기본 모드 스케일 아웃 배포를 구성합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 여러 개의 보고서 서버 인스턴스가 한 개의 공유 보고서 서버 데이터베이스를 사용하도록 허용하는 배포 토폴로지를 지원합니다. 보고서 서버 스케일 아웃 배포를 구현하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 각 보고서 서버를 공유 보고서 서버 데이터베이스에 연결해야 합니다.  
  
-   저장된 연결 문자열과 자격 증명을 암호화하는 데 사용되는 대칭 키 백업, 복원 또는 교체. 서비스 계정을 변경하거나 보고서 서버 데이터베이스를 다른 컴퓨터로 이동하는 경우 대칭 키 백업이 있어야 합니다.  
  
-   무인 실행 계정을 구성합니다. 이 계정은 예약된 작업이 수행되는 동안이나 사용자 자격 증명을 사용할 수 없는 경우 원격 연결에 사용됩니다.  
  
-   보고서 서버 전자 메일 구성 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 SMTP(Simple Mail Transport Protocol)를 통해 보고서 또는 보고서 처리 알림을 전자 사서함에 배달하는 메일 배달 확장 프로그램이 포함되어 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 네트워크에서 전자 메일 배달에 사용할 SMTP 서버나 게이트웨이를 지정할 수 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 보고서 서버 내용을 관리하거나 추가 기능을 활성화하거나 서버에 대한 액세스 권한을 부여할 수는 없습니다. 완전한 배포를 위해서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하여 추가 기능을 활성화하거나 기본값을 수정하고 웹 포털에서 서버에 대한 액세스 권한을 사용자에게 부여할 수 있도록 해야 합니다.

##  <a name="bkmk_requirements"></a> 요구 사항

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 버전별로 다릅니다. 이 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 함께 설치되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 구성할 수 없습니다. 같은 컴퓨터에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 이전 버전과 최신 버전이 함께 실행되고 있는 경우 각 버전과 함께 제공되는 Reporting Services 구성 관리자를 사용하여 각 인스턴스를 구성해야 합니다.  

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하려면 다음 사항을 충족해야 합니다.

- 구성하려는 보고서 서버를 호스팅하는 컴퓨터에 대한 로컬 시스템 관리자 권한이 있어야 합니다. 원격 컴퓨터를 구성하는 경우에는 해당 컴퓨터에 대한 로컬 시스템 관리자 권한도 있어야 합니다.

- 보고서 서버 데이터베이스를 호스팅하는 데 사용되는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에 데이터베이스를 만들 수 있는 사용 권한이 있어야 합니다.

- 구성하는 보고서 서버에 WMI(Windows Management Instrumentation) 서비스가 활성화되어 실행되고 있어야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 보고서 서버 WMI 공급자를 사용하여 로컬 및 원격 보고서 서버에 연결합니다. 원격 보고서 서버를 구성하는 경우에는 컴퓨터에서 원격 WMI 액세스를 허용해야 합니다. 자세한 내용은 [원격 관리를 위한 보고서 서버 구성](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)을 참조하세요.  

- 원격 보고서 서버 인스턴스에 연결하여 구성하기 전에 원격 WMI(Windows Management Instrumentation) 호출이 Windows 방화벽을 통과하도록 설정해야 합니다. 자세한 내용은 [온라인 설명서의](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) 원격 관리를 위한 보고서 서버 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.

Reporting Services 구성 관리자는 SQL Server Reporting Services를 설치할 때 자동으로 설치됩니다.

##  <a name="bkmk_start_configuration_manager"></a> Reporting Services 구성 관리자를 시작하려면

1.  사용자의 Microsoft Windows 버전에 적합한 방식으로 다음 단계를 사용합니다.

    - Windows 시작 화면에서 **Reporting** 을 입력하고 검색 결과에서 **Reporting Services 구성 관리자** 를 선택합니다.

    - **시작**을 클릭하고 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킵니다.

         [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이전 버전의 보고서 서버 인스턴스를 구성하려면 해당 버전의 프로그램 폴더를 엽니다. 예를 들어 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 대신 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] 을 가리켜서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 서버 구성 요소에 대한 구성 도구를 엽니다.

         **Reporting Services 구성 관리자**를 선택합니다.

2. 구성할 보고서 서버 인스턴스를 선택할 수 있도록 **Reporting Services 구성 연결** 대화 상자가 나타납니다. **연결**을 선택합니다.

3. **서버 이름**에 보고서 서버 인스턴스가 설치된 컴퓨터의 이름을 지정합니다. 기본적으로 로컬 컴퓨터의 이름이 표시되지만 원격 컴퓨터에 설치된 보고서 서버에 연결하려는 경우 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 입력할 수도 있습니다.

4. 원격 컴퓨터를 지정하는 경우 **찾기** 를 클릭하여 연결을 설정합니다.

5. **Report Server stance**에서 구성할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 선택합니다. 목록에 이 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보고서 서버 인스턴스만 표시됩니다. 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 구성할 수 없습니다.

6. **연결**을 선택합니다.

## <a name="next-steps"></a>다음 단계

[웹 포털](../../reporting-services/web-portal-ssrs-native-mode.md)   
[Reporting Services 도구](../../reporting-services/tools/reporting-services-tools.md)   
[보고서 서버 데이터베이스 연결 구성](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)   
[보고서 서버 구성 및 관리](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
