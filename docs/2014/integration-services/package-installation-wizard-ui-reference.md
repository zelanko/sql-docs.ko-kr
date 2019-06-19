---
title: 패키지 설치 마법사 UI 참조 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.deploymentwizard.confirminstallation.f1
- sql12.dts.deploymentwizard.deploydtspackages.f1
- sql12.dts.deploymentwizard.selectinstfolder.f1
- sql12.dts.deploymentwizard.specifytargetsqlserver.f1
- sql12.dts.deploymentwizard.welcome.f1
- sql12.dts.deploymentwizard.finish.f1
- sql12.dts.deploymentwizard.configurepackages.f1
- sql12.dts.deploymentwizard.packagevalidation.f1
helpviewer_keywords:
- Package Installer Wizard
ms.assetid: 6fca44d9-5001-4644-bcf3-c2d10a674b97
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f907127ff9863b696843a7d17e8df9950cd99c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056833"
---
# <a name="package-installation-wizard-ui-reference"></a>패키지 설치 마법사 UI 참조
  **패키지 설치 마법사** 를 사용하여 프로젝트에 포함된 패키지 및 기타 파일과 모든 패키지 종속 파일을 포함한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 배포할 수 있습니다.  
  
 패키지를 배포하기 전에 구성을 만들어 패키지와 함께 배포할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 구성을 사용하여 런타임 시 패키지와 패키지 개체의 속성을 동적으로 업데이트합니다. 예를 들어 연결 문자열이 포함된 속성에 값을 매핑하는 구성을 제공하여 OLE DB 연결의 연결 문자열을 런타임 시 동적으로 설정할 수 있습니다.  
  
 패키지 설치 마법사는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 작성하고 배포 유틸리티를 만든 후에만 실행할 수 있습니다. 자세한 내용은 [Deploy Packages by Using the Deployment Utility](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)를 참조하세요.  
  
 다음 섹션에서는 마법사의 페이지에 대해 설명합니다.  
  
## <a name="welcome-to-the-package-installation-wizard-page"></a>패키지 설치 마법사 시작 페이지  
 **패키지 설치 마법사** 를 사용하여 패키지 배포 유틸리티를 만든 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 배포할 수 있습니다.  
  
 **이 시작 페이지를 다시 표시 안 함**  
 마법사를 다시 실행할 때 시작 페이지를 건너뛰려면 선택합니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
## <a name="configure-packages-page"></a>패키지 구성 페이지  
 **패키지 구성** 페이지를 사용하여 패키지 구성을 편집할 수 있습니다.  
  
### <a name="options"></a>변수  
 **구성 파일**  
 목록에서 파일을 선택하여 구성 파일의 내용을 편집합니다.  
  
 **관련 항목:** [패키지 구성 만들기](../../2014/integration-services/create-package-configurations.md)  
  
 **경로**  
 구성할 속성의 경로를 봅니다.  
  
 **형식**  
 속성의 데이터 형식을 봅니다.  
  
 **Value**  
 구성의 값을 지정합니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
## <a name="confirm-installation-page"></a>설치 페이지 확인  
 **설치 확인** 페이지를 사용하여 패키지 설치를 시작하고, 상태를 보고, 지정한 프로젝트의 파일을 설치할 때 마법사에서 사용할 정보를 볼 수 있습니다.  
  
 **다음**  
 패키지와 종속 파일을 설치하고 설치가 완료되면 마법사의 다음 페이지로 이동합니다.  
  
 **상태**  
 패키지 설치 진행률을 표시합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 이동합니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
## <a name="deploy-ssis-packages-page"></a>SSIS 패키지 배포 페이지  
 **SSIS 패키지 배포** 페이지를 사용하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지 및 해당 종속성을 설치할 위치를 지정할 수 있습니다.  
  
### <a name="options"></a>변수  
 **파일 시스템 배포**  
 파일 시스템에서 지정한 폴더에 패키지 및 종속성을 배포합니다.  
  
 **SQL Server 배포**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 패키지 및 종속성을 배포합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가 서버 간에 패키지를 공유하는 경우 이 옵션을 사용합니다. 모든 패키지 종속성은 파일 시스템에서 지정한 폴더에 설치됩니다.  
  
 **설치 후 패키지 유효성 검사**  
 설치 후 패키지 유효성 검사 여부를 나타냅니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
## <a name="packages-validation-page"></a>패키지 유효성 검사 페이지  
 **패키지 유효성 검사** 페이지를 사용하여 패키지 유효성 검사의 진행률 및 결과를 볼 수 있습니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
## <a name="select-installation-folder-page"></a>설치 폴더 선택 페이지  
 **설치 폴더 선택** 페이지를 사용하여 패키지 및 패키지의 종속성을 설치할 파일 시스템 폴더를 지정할 수 있습니다.  
  
### <a name="options"></a>변수  
 **Folder**  
 패키지 및 해당 패키지의 종속성을 복사할 경로 및 폴더를 지정합니다.  
  
 **찾아보기**  
 **폴더 찾아보기** 대화 상자를 사용하여 대상 폴더를 찾습니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
## <a name="specify-target-sql-server-page"></a>대상 SQL Server 지정 페이지  
 **대상 SQL Server 지정** 페이지를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 패키지를 배포할 수 있는 옵션을 지정할 수 있습니다.  
  
### <a name="options"></a>변수  
 **서버 이름**  
 패키지를 배포할 서버의 이름을 지정합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하여 서버에 로그온하도록 할지 여부를 지정합니다. 보안을 강화하려면 Windows 인증을 사용하는 것이 좋습니다.  
  
 **SQL Server 인증 사용**  
 패키지에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 로그온하도록 할지 여부를 지정합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
 **사용자 이름**  
 사용자 이름을 지정합니다.  
  
 **암호**  
 암호를 지정합니다.  
  
 **패키지 경로**  
 논리적 폴더의 이름을 지정하거나 "/"를 입력하여 기본 폴더를 사용합니다.  
  
 **SSIS 패키지** 대화 상자에서 폴더를 선택하려면 찾아보기(...)를 클릭합니다. 그러나 이 대화 상자에서는 기본 폴더를 선택할 수 없습니다. 기본 폴더를 사용하려면 입력란에 "/"를 입력해야 합니다.  
  
> [!NOTE]  
>  유효한 패키지 경로를 입력하지 않으면 "인수 중 하나가 올바르지 않습니다"라는 오류 메시지가 나타납니다.  
  
 **암호화에 서버 스토리지 사용**  
 패키지를 보호하기 위해 [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 보안 기능을 사용하려면 선택합니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
## <a name="finish-the-package-installation-page"></a>패키지 설치 마침 페이지  
 **패키지 설치 마법사 마침** 페이지를 사용하여 패키지 설치 결과에 대한 요약을 볼 수 있습니다. 이 페이지에서는 배포된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트의 이름, 설치한 패키지, 구성 파일 및 설치 위치와 같은 세부 정보를 제공합니다.  
  
 **마침**  
 **마침**을 클릭하여 마법사를 종료합니다.  
  
## <a name="see-also"></a>관련 항목  
 [배포 패키지 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
