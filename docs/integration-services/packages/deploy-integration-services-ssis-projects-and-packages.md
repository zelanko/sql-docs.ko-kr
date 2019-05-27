---
title: Integration Services(SSIS) 프로젝트 및 패키지 배포 | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.bids.converttolegacydeployment.f1
- sql13.ssis.deploymentwizard.f1
- sql13.ssis.ssms.isenvprop.permissions.f1
- sql13.ssis.ssms.isenvprop.general.f1
- sql13.ssis.ssms.iscreateenv.f1
- sql13.ssis.ssms.isenvprop.variables.f1
- sql13.ssis.migrationwizard.f1
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c0759d5da7af3cfd50ff32b500050b90affa70c5
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65720050"
---
# <a name="deploy-integration-services-ssis-projects-and-packages"></a>Integration Services(SSIS) 프로젝트 및 패키지 배포

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 프로젝트 배포 모델 및 레거시 패키지 배포 모델의 두 가지 배포 모델을 지원합니다. 프로젝트 배포 모델을 사용하면 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다.  
  
레거시 패키지 배포 모델에 대한 자세한 내용은 [레거시 패키지 배포&#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)를 참조하세요.  
  
> [!NOTE]  
>  프로젝트 배포 모델은 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]에서 소개했습니다. 이 배포 모델을 사용하여 전체 프로젝트를 배포하지 않고 하나 이상의 패키지를 배포할 수 없습니다. [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)]은 전체 프로젝트를 배포하지 않고 하나 이상의 패키지를 배포할 수 있는 패키지 배포 모델을 소개했습니다.  

> [!NOTE]
> 이 문서에서는 SSIS 패키지를 일반적으로 배포하는 방법 및 온-프레미스에서 패키지를 배포하는 방법을 설명합니다. 또한 다음 플랫폼으로 SSIS 패키지를 배포할 수도 있습니다.
> - **Microsoft Azure 클라우드** 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.
> - **Linux** 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.

## <a name="compare-project-deployment-model-and-legacy-package-deployment-model"></a>프로젝트 배포 모델과 레거시 패키지 배포 모델 비교  
 프로젝트에 대해 선택한 배포 모델 유형에 따라 해당 프로젝트에 사용할 수 있는 배포 및 관리 옵션이 달라집니다. 다음 표에서는 프로젝트 배포 모델을 사용하는 경우와 패키지 배포 모델을 사용하는 경우의 차이점과 유사점을 보여 줍니다.  
  
|프로젝트 배포 모델을 사용하는 경우|레거시 패키지 배포 모델을 사용하는 경우|  
|---------------------------------------------|----------------------------------------------------|  
|프로젝트가 배포 단위입니다.|패키지가 배포 단위입니다.|  
|패키지 속성에 값을 할당하는 데 매개 변수가 사용됩니다.|패키지 속성에 값을 할당하는 데 구성이 사용됩니다.|  
|패키지 및 매개 변수를 포함하는 프로젝트가 프로젝트 배포 파일(.ispac 확장명)에 기본 제공됩니다.|패키지(.dtsx 확장명) 및 구성(.dtsConfig 확장명)이 파일 시스템에 개별적으로 저장됩니다.|  
|패키지와 매개 변수를 포함하는 프로젝트가 SQL Server 인스턴스의 SSISDB 카탈로그에 배포됩니다.|패키지 및 구성이 다른 컴퓨터의 파일 시스템에 복사됩니다. SQL Server 인스턴스의 MSDB 데이터베이스에 패키지를 저장할 수도 있습니다.|  
|데이터베이스 엔진에서 CLR 통합이 필요합니다.|데이터베이스 엔진에서 CLR 통합이 필요하지 않습니다.|  
|환경 관련 매개 변수 값이 환경 변수에 저장됩니다.|환경 관련 구성 값이 구성 파일에 저장됩니다.|  
|카탈로그에 있는 프로젝트 및 패키지를 실행하기 전에 서버에서 유효성을 검사할 수 있습니다. SQL Server Management Studio, 저장 프로시저 또는 관리 코드를 사용하여 유효성 검사를 수행할 수 있습니다.|패키지를 실행하기 바로 전에 유효성을 검사합니다. 또한 dtExec 또는 관리 코드를 사용하여 패키지의 유효성을 검사할 수도 있습니다.|  
|데이터베이스 엔진에서 실행을 시작하는 방식으로 패키지를 실행합니다. 실행을 시작하기 전에 실행에 프로젝트 식별자, 명시적 매개 변수 값(옵션) 및 환경 참조(옵션)를 할당합니다.<br /><br /> 또한 **dtExec**를 사용하여 패키지를 실행할 수도 있습니다.|패키지는 **dtExec** 및 **DTExecUI** 실행 유틸리티를 사용하여 실행됩니다. 해당 구성이 명령 프롬프트 인수(옵션)로 식별됩니다.|  
|실행 시 패키지에 의해 생성된 이벤트가 자동으로 캡처되고 카탈로그에 저장됩니다. Transact-SQL 뷰를 사용하여 이러한 이벤트를 쿼리할 수 있습니다.|실행 시 패키지에 의해 생성된 이벤트가 자동으로 캡처되지 않습니다. 이벤트를 캡처하려면 로그 공급자를 패키지에 추가해야 합니다.|  
|패키지가 별도의 Windows 프로세스에서 실행됩니다.|패키지가 별도의 Windows 프로세스에서 실행됩니다.|  
|SQL Server 에이전트를 사용하여 패키지 실행을 예약합니다.|SQL Server 에이전트를 사용하여 패키지 실행을 예약합니다.|  
  
 프로젝트 배포 모델은 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]에서 소개했습니다. 이 모델을 사용하는 경우 전체 프로젝트를 배포하지 않고 하나 이상의 패키지를 배포할 수 없습니다. [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)] 은 전체 프로젝트를 배포하지 않고 기존 프로젝트나 새 프로젝트에 하나 이상의 패키지를 배포할 수 있는 증분 패키지 배포 기능을 소개했습니다.   
  
## <a name="features-of-project-deployment-model"></a>프로젝트 배포 모델의 기능  
 다음 표에서는 프로젝트 배포 모델에만 배포되는 프로젝트에 사용할 수 있는 기능을 나열합니다.  
  
|기능|설명|  
|-------------|-----------------|  
|매개 변수|매개 변수는 패키지에서 사용할 데이터를 지정합니다. 패키지 매개 변수 및 프로젝트 매개 변수를 사용하여 각각 패키지 수준 또는 프로젝트 수준으로 매개 변수 범위를 지정할 수 있습니다. 매개 변수를 식 또는 태스크에서 사용할 수 있습니다. 프로젝트가 카탈로그에 배포되면 각 매개 변수의 리터럴 값을 할당하거나 디자인 타임에 할당된 기본값을 사용할 수 있습니다. 리터럴 값 대신 환경 변수를 참조할 수도 있습니다. 환경 변수 값은 패키지 실행 시 확인됩니다.|  
|환경|환경은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에서 참조할 수 있는 변수의 컨테이너입니다. 각 프로젝트는 환경 참조를 여러 개 가질 수 있지만 단일 패키지 실행 인스턴스는 단일 환경의 변수만 참조할 수 있습니다. 환경을 사용하여 패키지에 할당할 값을 구성할 수 있습니다. 예를 들어 "Dev", "test" 및 "Production"이라는 환경이 있을 수 있습니다.|  
|환경 변수|환경 변수는 패키지 실행 시 매개 변수에 할당할 수 있는 리터럴 값을 정의합니다. 환경 변수를 사용하려면 실행 인스턴스를 구성할 때 매개 변수가 있는 환경에 해당하는 프로젝트에 환경 참조를 만들고, 환경 변수 이름에 매개 변수 값을 할당하고, 해당 환경 참조를 지정합니다.|  
|SSISDB 카탈로그|모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체는 SSISDB 카탈로그라는 데이터베이스의 SQL Server 인스턴스에 저장되고 관리됩니다. 카탈로그를 통해 폴더를 사용하여 프로젝트 및 환경을 구성할 수 있습니다. 각 SQL Server 인스턴스는 카탈로그를 하나만 가질 수 있습니다. 각 카탈로그는 0개 이상의 폴더를 가질 수 있습니다. 각 폴더는 0개 이상의 프로젝트 및 0개 이상의 환경을 가질 수 있습니다. 카탈로그의 폴더를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체에 대한 사용 권한의 경계로 사용할 수도 있습니다.|  
|카탈로그 저장 프로시저 및 뷰|많은 수의 저장 프로시저 및 뷰를 사용하여 카탈로그의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체를 관리할 수 있습니다. 예를 들어 매개 변수 및 환경 변수에 값을 지정하고, 실행을 생성 및 시작하고, 카탈로그 작업을 모니터링할 수 있습니다. 실행이 시작되기 전에 패키지에서 사용될 값을 정확히 확인할 수도 있습니다.|  
  
## <a name="project-deployment"></a>프로젝트 배포  
 프로젝트 배포 모델의 중앙에는 프로젝트 배포 파일(.ispac extension)이 있습니다. 프로젝트 배포 파일은 프로젝트의 패키지 및 매개 변수에 대한 중요 정보만 포함하는 자체 포함된 배포 단위입니다. 프로젝트 배포 파일은 Integration Services 프로젝트 파일(.dtproj 확장명)에 포함된 모든 정보 중 일부만 캡처합니다. 예를 들어 메모를 작성하는 데 사용하는 추가 텍스트 파일은 프로젝트 배포 파일에 저장되지 않으므로 카탈로그에 배포되지 않습니다.  

## <a name="permissions-required-to-deploy-ssis-projects-and-packages"></a>SSIS 프로젝트 및 패키지를 배포하는 데 필요한 권한

기본값에서 SSIS 서비스 계정을 변경하는 경우, 패키지를 성공적으로 배포하려면 먼저 기본이 아닌 서비스 계정에 추가 권한을 부여해야 할 수 있습니다. 기본이 아닌 서비스 계정에 필요한 사용 권한이 없으면 다음과 같은 오류 메시지가 표시될 수 있습니다.

*사용자 정의 루틴 또는 집계 "deploy_project_internal"을 실행하는 동안 .NET Framework 오류가 발생했습니다. System.ComponentModel.Win32Exception: 클라이언트에 필수 권한이 없습니다.*

이 오류는 일반적으로 DCOM 권한 누락으로 인해 발생합니다. 오류를 해결하려면 다음 작업을 수행합니다.

1.  **구성 요소 서비스** 콘솔을 엽니다(또는 Dcomcnfg.exe 실행).
2.  **구성 요소 서비스** 콘솔에서 **구성 요소 서비스** > **컴퓨터** > **내 컴퓨터** > **DCOM 구성**을 차례로 확장합니다.
3.  목록에서 사용 중인 SQL Server의 버전으로 **Microsoft SQL Server Integration Services xx.0**을 찾습니다. 예를 들어, SQL Server 2016은 버전 13입니다.
4.  마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
5.  **SQL Server Integration Services 13.0 속성** 대화 상자에서 **보안** 탭을 선택합니다.
6.  시작, 활성화, 액세스 및 구성의 세 가지 권한 집합 각각에 대해 **사용자 지정**을 선택한 후 **편집**을 선택하여 **권한** 대화 상자를 엽니다.
7.  **권한** 대화 상자에서 기본이 아닌 서비스 계정을 추가하고 필요에 따라 **허용** 권한을 부여합니다. 일반적으로 계정에는 **로컬 시작** 및 **로컬 활성화** 사용 권한이 있습니다.
8.  **확인**을 두 번 클릭한 후 **구성 요소 서비스** 콘솔을 닫습니다.

이 섹션에 설명된 오류 및 SSIS 서비스 계정에 필요한 사용 권한에 대한 자세한 내용은 다음 블로그 게시물을 참조하세요.  
[System.ComponentModel.Win32Exception: SSIS 프로젝트를 배포하는 동안 클라이언트가 필요한 권한을 가지고 있지 않습니다.](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2013/08/20/system-componentmodel-win32exception-a-required-privilege-is-not-held-by-the-client-while-deploying-ssis-project/)

## <a name="deploy-projects-to-integration-services-server"></a>Deploy Projects to Integration Services Server
  현재 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서는 환경을 사용하여 패키지를 관리하고, 패키지를 실행하고, 패키지에 대한 런타임 값을 구성할 수 있습니다.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서와 마찬가지로 현재 릴리스에서도 SQL Server 인스턴스에 패키지를 배포하고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 실행 및 관리할 수 있습니다. 패키지 배포 모델을 사용합니다. 자세한 내용은 [레거시 패키지 배포&#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포하려면 다음 태스크를 완료합니다.  
  
1.  아직 없는 경우 SSISDB 카탈로그를 만듭니다. 자세한 내용은 [SSIS 카탈로그](../../integration-services/catalog/ssis-catalog.md)를 참조하세요.  
  
2.  **Integration Services 프로젝트 변환 마법사** 를 실행하여 프로젝트를 프로젝트 배포 모델로 변환합니다. 자세한 내용은 아래 지침을 참조하세요. [프로젝트 배포 모델로 프로젝트를 변환하려면](#convert)  
  
    -   [!INCLUDE[ssISversion12](../../includes/ssisversion12-md.md)] 이상에서 프로젝트를 만든 경우 기본적으로 해당 프로젝트는 프로젝트 배포 모델을 사용합니다.  
  
    -   이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 프로젝트를 만든 경우 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 프로젝트 파일을 연 후 프로젝트 배포 모델로 프로젝트를 변환합니다.  
  
        > [!NOTE]  
        >  프로젝트에 하나 이상의 데이터 원본이 포함된 경우 프로젝트 변환이 완료되면 데이터 원본이 제거됩니다. 프로젝트의 패키지에서 공유할 수 있는 데이터 원본에 대한 연결을 만들려면 프로젝트 수준에서 연결 관리자를 추가합니다. 자세한 내용은 [패키지에서 연결 관리자 추가, 삭제 또는 공유](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)을 참조하세요.  
  
         **Integration Services 프로젝트 변환 마법사** 를 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 에서 실행하는지 아니면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 실행하는지에 따라 수행되는 변환 태스크가 다릅니다.  
  
        -   마법사를 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 실행하면 프로젝트에 포함된 패키지가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 2005, 2008 또는 2008 R2에서 현재 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 사용되는 형식으로 변환됩니다. 원래 프로젝트 파일(.dtproj)과 패키지 파일(.dtsx)이 업그레이드됩니다.  
  
        -   마법사를 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 실행하면 마법사는 프로젝트에 포함된 패키지 및 구성에서 프로젝트 배포 파일(.ispac)을 생성합니다. 원래 패키지 파일(.dtsx)은 업그레이드되지 않습니다.  
  
             마법사의 **대상 선택** 페이지에서 기존 파일을 선택하거나 새 파일을 만들 수 있습니다.  
  
             프로젝트 변환 시 패키지 파일을 업그레이드하려면 **Integration Services 프로젝트 변환 마법사** 를 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 실행합니다. 프로젝트 변환과 별도로 패키지 파일을 업그레이드하려면 **에서** Integration Services 프로젝트 변환 마법사 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 실행한 다음 **SSIS 패키지 업그레이드 마법사**를 실행합니다. 패키지 파일을 개별적으로 업그레이드한 경우에는 변경 내용을 저장해야 합니다. 그러지 않으면 프로젝트 배포 모델로 프로젝트를 변환할 때 저장되지 않은 패키지 변경 내용이 변환되지 않습니다.  
  
     패키지 업그레이드에 대한 자세한 내용은 [Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages.md) 및 [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)를 참조하세요.  
  
3.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포합니다. 자세한 내용은 아래 지침을 참조하세요. [Integration Services 서버에 프로젝트를 배포하려면](#deploy) 지침을 참조하세요.  
  
4.  (선택 사항) 배포한 프로젝트에 대한 환경을 만듭니다. 
  
###  <a name="convert"></a> 프로젝트 배포 모델로 프로젝트를 변환하려면  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 프로젝트를 열고 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **프로젝트 배포 모델로 변환**을 클릭합니다.  
  
     -또는-  
  
     [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 개체 탐색기에서 **프로젝트** 노드를 마우스 오른쪽 단추로 클릭하고 **패키지 가져오기**를 선택합니다.  
  
2.  마법사를 완료합니다.
  
###  <a name="deploy"></a> Integration Services 서버에 프로젝트를 배포하려면  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 프로젝트를 연 다음 **프로젝트** 메뉴에서 **배포** 를 선택하여 **Integration Services 배포 마법사**를 시작합니다.  
  
     -또는-  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] > **SSISDB** 노드를 확장하고 배포할 프로젝트의 프로젝트 폴더를 찾습니다. **프로젝트** 폴더를 마우스 오른쪽 단추로 클릭하고 **프로젝트 배포**를 클릭합니다.  
  
     -또는-  
  
     명령 프롬프트의 **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn** 에서 **isdeploymentwizard.exe**를 실행합니다. 64비트 컴퓨터의 **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn**에는 도구의 32비트 버전도 있습니다.  
  
2.  **원본 선택** 페이지에서 **프로젝트 배포 파일** 을 클릭하여 프로젝트 배포 파일을 선택합니다.  
  
     -또는-  
  
     **Integration Services 카탈로그** 를 클릭하여 SSISDB 카탈로그에 이미 배포된 프로젝트를 선택합니다.  
  
3.  마법사를 완료합니다. 

## <a name="deploy-packages-to-integration-services-server"></a>Integration Services 서버에 패키지 배포
  [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)] 에 도입된 증분 패키지 배포 기능을 사용하면 전체 프로젝트를 배포하지 않고 기존 프로젝트나 새 프로젝트에 하나 이상의 패키지를 배포할 수 있습니다.  
  
###  <a name="DeployWizard"></a> Integration Services 배포 마법사를 사용하여 패키지 배포  
  
1.  명령 프롬프트의 **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn** 에서 **isdeploymentwizard.exe**를 실행합니다. 64비트 컴퓨터의 **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn**에는 도구의 32비트 버전도 있습니다.  
  
2.  **원본 선택** 페이지에서 **패키지 배포 모델**로 전환합니다. 그런 다음 원본 패키지가 포함된 폴더를 선택하고 패키지를 구성합니다.  
  
3.  마법사를 완료합니다. [Package Deployment Model](#PackageModel)에서 설명하는 나머지 단계를 수행합니다.  
  
###  <a name="SSMS"></a> SQL Server Management Studio를 사용하여 패키지 배포  
  
1.  SQL Server Management Studio의 개체 탐색기에서 **Integration Services 카탈로그** > **SSISDB** 노드를 확장합니다.  
  
2.  **프로젝트** 폴더를 마우스 오른쪽 단추로 클릭하고 **프로젝트 배포**를 클릭합니다.  
  
3.  **소개** 페이지가 표시되면 **다음** 을 클릭하여 계속합니다.  
  
4.  **원본 선택** 페이지에서 **패키지 배포 모델**로 전환합니다. 그런 다음 원본 패키지가 포함된 폴더를 선택하고 패키지를 구성합니다.  
  
5.  마법사를 완료합니다. [Package Deployment Model](#PackageModel)에서 설명하는 나머지 단계를 수행합니다.  
  
###  <a name="SSDT"></a> SQL Server Data Tools(Visual Studio)를 사용하여 패키지 배포  
  
1.  Visual Studio에서 Integration Services 프로젝트를 연 상태로 배포할 패키지를 하나 이상 선택합니다.  
  
2.  마우스 오른쪽 단추를 클릭하고 **패키지 배포**를 선택합니다. 선택한 패키지가 원본 패키지로 구성된 상태로 배포 마법사가 열립니다.  
  
3.  마법사를 완료합니다. [Package Deployment Model](#PackageModel)에서 설명하는 나머지 단계를 수행합니다.  
  
###  <a name="StoredProcedure"></a> deploy_packages 저장 프로시저를 사용하여 패키지 배포  
 **[catalog].[deploy_packages]** 저장 프로시저를 사용하여 SSIS 카탈로그에 SSIS 패키지를 하나 이상 배포할 수 있습니다. 다음 코드 예제에서는 이 저장 프로시저를 사용하여 SSIS 서버에 패키지를 배포하는 방법을 보여 줍니다. 자세한 내용은 [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md)를 참조하세요.  
  
```cs
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
###  <a name="MOMApi"></a> 관리 개체 모델 API를 사용하여 패키지 배포  
 다음 코드 예제에서는 관리 개체 모델 API를 사용하여 서버에 패키지를 배포하는 방법을 보여 줍니다.  
  
```cs 
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```

## <a name="convert-to-package-deployment-model-dialog-box"></a>패키지 배포 모델로 변환 대화 상자
  **패키지 배포 모델로 변환** 명령을 사용하면 프로젝트 및 프로젝트의 각 패키지에서 해당 모델과의 호환성을 검사한 후 패키지를 패키지 배포 모델로 변환할 수 있습니다. 패키지에 매개 변수와 같이 프로젝트 배포 모델에 고유한 기능이 사용된 경우 패키지를 변환할 수 없습니다.  
  
### <a name="task-list"></a>작업 목록  
 패키지를 패키지 배포 모델로 변환하려면 두 단계가 필요합니다.  
  
1.  **프로젝트** 메뉴에서 **패키지 배포 모델로 변환** 명령을 선택하면 이 모델에 대한 프로젝트 및 각 패키지의 호환성이 검사됩니다. 결과는 **결과** 테이블에 표시됩니다.  
  
     프로젝트 또는 패키지가 호환성 테스트를 실패한 경우 **결과** 열에서 **실패** 를 클릭하여 자세한 내용을 확인합니다. **보고서 저장** 을 클릭하여 이 정보의 복사본을 텍스트 파일로 저장합니다.  
  
2.  프로젝트 및 모든 패키지가 호환성 테스트를 성공하면 **확인** 을 클릭하여 패키지를 변환합니다.  
  
> **참고:** 프로젝트를 프로젝트 배포 모델로 변환하려면 **Integration Services 프로젝트 변환 마법사**를 사용합니다. 자세한 내용은 [Integration Services Project Conversion Wizard](deploy-integration-services-ssis-projects-and-packages.md)을 참조하세요.  

## <a name="integration-services-deployment-wizard"></a>Integration Services 배포 마법사
  **Integration Services 배포 마법사** 는 아래의 두 가지 배포 모델을 지원합니다.
   - 프로젝트 배포 모델
   - 패키지 배포 모델 
   
 **프로젝트 배포 모델** 을 사용하면 SSIS(SQL Server Integration Services) 프로젝트를 를 하나의 단위로 SSIS 카탈로그에 배포할 수 있습니다.
 
 **패키지 배포 모델** 을 사용하면 전체 프로젝트를 배포할 필요 없이 SSIS 카탈로그로 업데이트한 패키지를 배포할 수 있습니다. 
 
 > **참고:** Integration Services 배포 마법사의 기본 배포는 프로젝트 배포 모델입니다.  
  
### <a name="launch-the-wizard"></a>마법사 시작
다음과 같이 마법사를 시작합니다.

 - Windows Search에서 **"SQL Server 배포 마법사"** 를 입력합니다. 

**OR**

 - SQL Server 설치 폴더에서 실행 파일 **ISDeploymentWizard.exe**를 검색합니다(예: "C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn". 
 
 > **참고:** **소개** 페이지에서 **다음** 을 클릭하여 **원본 선택** 페이지로 전환합니다. 
 
 이 페이지의 설정은 각 배포 모델에서 서로 다릅니다. 이 페이지에서 선택한 모델에 따라 [Project Deployment Model](#ProjectModel) 섹션의 단계 또는 [Package Deployment Model](#PackageModel) 섹션의 단계를 따릅니다.  
  
###  <a name="ProjectModel"></a> Project Deployment Model  
  
#### <a name="select-source"></a>원본 선택  
 만든 프로젝트 배포 파일을 배포하려면 **프로젝트 배포 파일** 을 선택하고 .ispac 파일에 대한 경로를 입력합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트를 배포하려면 **Integration Services 카탈로그**를 선택한 후 서버 이름과 카탈로그에 있는 프로젝트 경로를 입력합니다. **다음** 을 클릭하여 **대상 선택** 페이지를 표시합니다.  
  
#### <a name="select-destination"></a>대상 선택  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에서 프로젝트에 대한 대상 폴더를 선택하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 입력하거나 서버 목록에서 **찾아보기** 를 클릭하여 선택합니다. SSISDB에 프로젝트 경로를 입력하거나 **찾아보기** 를 클릭하여 선택합니다. **다음** 을 클릭하여 **검토** 페이지를 표시합니다.  
  
#### <a name="review-and-deploy"></a>검토(및 배포)  
 이 페이지를 사용하면 선택한 설정을 검토할 수 있습니다. **이전**을 클릭하거나 왼쪽 창의 단계 중 하나를 클릭하여 선택 항목을 변경할 수 있습니다. **배포** 를 클릭해 배포 프로세스를 시작합니다.  
  
#### <a name="results"></a>결과  
 배포 프로세스가 완료되면 **결과** 페이지가 표시되어야 합니다. 이 페이지는 각 동작의 성공 또는 실패 여부를 표시합니다. 작업이 실패하면 **결과** 열에서 **실패** 를 클릭하여 해당 오류에 대한 설명을 표시합니다. 결과를 XML 파일로 저장하려면 **보고서 저장...** 을 클릭하거나 **닫기**를 클릭해 마법사를 종료합니다.
  
###  <a name="PackageModel"></a> Package Deployment Model  
  
#### <a name="select-source"></a>원본 선택  
 **Integration Services 배포 마법사** 의 **원본 선택** 페이지는 **배포 모델** 에서 **패키지 배포**옵션을 선택할 때 패키지 배포 모델별 설정을 보여줍니다.  
  
 원본 패키지를 선택하려면 **찾아보기...** 단추를 클릭하여 패키지가 포함된 **폴더**를 선택하거나 **패키지 폴더 경로** 텍스트 상자에 폴더 경로를 입력하고 페이지 아래쪽에 있는 **새로 고침** 단추를 클릭합니다. 이제 목록 상자의 지정된 폴더에 모든 패키지가 표시됩니다. 기본적으로 모든 패키지가 선택되어 있습니다. 첫 번째 열에 있는 **확인란** 을 클릭해 서버로 배포할 패키지를 선택합니다.  
  
 **상태** 및 **메시지** 열을 참조하여 패키지 상태를 확인합니다. 상태가 **준비** 또는 **경고**로 설정된 경우 배포 마법사는 배포 프로세스를 차단하지 않습니다. 반면, 상태가 **오류**로 설정된 경우 마법사는 선택한 패키지의 배포를 더 이상 진행하지 않습니다. 자세한 경고/오류 메시지를 보려면 **메시지** 열에 있는 링크를 클릭합니다.  
  
 중요한 데이터 또는 패키지 데이터가 암호로 암호화된 경우 **암호** 열에 암호를 입력한 후 **새로 고침** 단추를 클릭해 암호가 맞는지 확인합니다. 암호가 맞는 경우 상태가 **준비** 로 변경되고 경고 메시지가 사라집니다. 여러 패키지의 암호가 동일한 경우 동일한 암호화 암호가 있는 패키지들을 선택한 후 **암호** 텍스트 상자에 암호를 입력한 후 **적용** 단추를 클릭합니다. 암호는 선택한 패키지에 적용됩니다.  
  
 선택한 일부 패키지가 **오류**로 설정되지 않은 경우 **다음** 단추가 활성화되어 패키지 배포 프로세스를 계속 진행할 수 있습니다.  
  
#### <a name="select-destination"></a>대상 선택  
 패키지 소스를 선택한 후 **다음** 단추를 클릭해 **대상 선택** 페이지로 전환합니다. 패키지는 SSIS 카탈로그(SSISDB)에 프로젝트로 배포되어야 합니다. 따라서 대상 프로젝트가 SSIS 카탈로그에 이미 있는지 확인한 후 패키지를 배포하십시오. 그렇지 않으면 빈 프로젝트를 만듭니다. **대상 선택** 페이지에서 **서버 이름** 텍스트 상자에 서버 이름을 입력하거나 **찾아보기...** 단추를 클릭해 서버 인스턴스를 선택합니다. 그런 다음, **경로** 옆에 있는 **찾아보기...** 단추를 클릭하여 대상 프로젝트를 지정합니다. 프로젝트가 없는 경우 **새 프로젝트...** 를 클릭하여 대상 프로젝트로 빈 프로젝트를 만듭니다. 프로젝트는 **반드시** 폴더 아래에 생성되어야 합니다.  
  
#### <a name="review-and-deploy"></a>검토 및 배포  
 **대상 선택** 페이지에서 **다음** 을 클릭해 **Integration Services 배포 마법사** 의 **검토**페이지로 전환합니다. 검토 페이지에서 배포 작업에 대한 요약 보고서를 검토합니다. 검토한 후, **배포** 단추를 클릭해 배포 작업을 수행합니다.  
  
#### <a name="results"></a>결과  
 배포가 완료되면 **결과** 페이지가 표시되어야 합니다. **결과** 페이지에서 배포 프로세스의 각 단계 결과를 검토합니다. **결과** 페이지에서 **보고서 저장** 을 클릭해 배포 보고서를 저장하거나 **닫기** 를 클릭해 마법사를 종료합니다.  

## <a name="create-and-map-a-server-environment"></a>서버 환경 만들기 및 매핑
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포한 프로젝트에 포함된 패키지의 런타임 값을 지정하기 위한 서버 환경을 만듭니다. 그런 다음 특정 패키지, 진입점 패키지 또는 지정된 프로젝트의 모든 패키지에 대한 매개 변수에 환경 변수를 매핑할 수 있습니다. 진입점 패키지는 일반적으로 자식 패키지를 실행하는 부모 패키지입니다.  
  
> [!IMPORTANT]  
>  지정된 실행의 경우 패키지는 단일 서버 환경에 포함된 값만으로 실행할 수 있습니다.  
  
 서버 환경, 환경 참조 및 환경 변수 목록에 대한 뷰를 쿼리할 수 있습니다. 저장 프로시저를 호출하여 환경, 환경 참조 및 환경 변수를 추가, 삭제 및 수정할 수도 있습니다. 자세한 내용은 **SSIS Catalog** 의 [서버 환경, 서버 변수 및 서버 환경 참조](../../integration-services/catalog/ssis-catalog.md)섹션을 참조하십시오.  
  
### <a name="to-create-and-use-a-server-environment"></a>서버 환경을 만들고 사용하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 개체 탐색기에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그> **SSISDB** 노드를 확장하고 환경을 만들 프로젝트의 **환경** 폴더를 찾습니다.  
  
2.  **환경** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **환경 만들기**를 클릭합니다.  
  
3.  환경의 이름을 입력하고 선택적으로 설명을 입력한 다음 **확인**을 클릭합니다.  
  
4.  새 환경을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **변수** 페이지에서 다음을 수행하여 변수를 추가합니다.  
  
    1.  변수의 **유형** 을 선택합니다. 변수 이름은 변수에 매핑할 프로젝트 매개 변수의 이름과 일치하지 **않아도** 됩니다.  
  
    2.  변수에 대한 선택적 **설명** 을 입력합니다.  
  
    3.  환경 변수의 **값** 을 입력합니다.  
  
         환경 변수 이름에 대한 규칙은 **SSIS Catalog** 의 [환경 변수](../../integration-services/catalog/ssis-catalog.md)섹션을 참조하십시오.  
  
    4.  **중요** 확인란을 선택하거나 선택을 취소하여 변수에 중요한 값이 포함되어 있는지 여부를 나타냅니다.  
  
         **중요**를 선택하면 변수 값이 **값** 필드에 표시되지 않습니다.  
  
         중요한 값은 SSISDB 카탈로그에서 암호화됩니다. 암호화에 대한 자세한 내용은 [SSIS Catalog](../../integration-services/catalog/ssis-catalog.md)를 참조하십시오.  
  
6.  **사용 권한** 페이지에서 다음을 수행하여 선택한 사용자 및 역할에 대해 사용 권한을 허용하거나 거부합니다.  
  
    1.  **찾아보기**를 클릭한 다음 **모든 보안 주체 찾아보기** 대화 상자에서 하나 이상의 사용자 및 역할을 선택합니다.  
  
    2.  **로그인 또는 역할** 영역에서 사용 권한을 허용하거나 거부할 사용자 또는 역할을 선택합니다.  
  
    3.  **명시적** 영역에서 각 사용 권한 옆의 **허용** 또는 **거부** 를 클릭합니다.  
  
7.  환경을 스크립팅하려면 **스크립트**를 클릭합니다. 기본적으로 스크립트는 새 쿼리 편집기 창에 표시됩니다.  
  
    > [!TIP]  
    >  변수를 추가하는 등 환경 속성을 하나 이상 변경한 후에 **환경 속성** 대화 상자에서 **확인**을 클릭하기 전에 **스크립트**를 클릭해야 합니다. 그렇지 않으면 스크립트가 생성되지 않습니다.  
  
8.  변경 내용을 환경 속성에 저장하려면 **확인** 을 클릭합니다.  
  
9. 개체 탐색기의 **SSISDB** 노드에서 **프로젝트** 폴더를 확장하고 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **구성**을 클릭합니다.  
  
10. **참조** 페이지에서 **추가** 를 클릭하여 환경을 추가한 다음 **확인** 을 클릭하여 참조를 환경에 저장합니다.  
  
11. 프로젝트를 다시 마우스 오른쪽 단추로 클릭한 다음 **구성**을 클릭합니다.  
  
12. 디자인 타임 시 패키지에 추가한 매개 변수 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 프로젝트 배포 모델로 변환할 때 생성된 매개 변수에 환경 변수를 매핑하려면 다음을 수행합니다.  
  
    1.  **매개 변수** 페이지의 **매개 변수** 탭에서 **값** 필드 옆에 있는 찾아보기 단추를 클릭합니다.  
  
    2.  **환경 변수 사용**을 클릭한 다음 만든 환경 변수를 선택합니다.  
  
13. 환경 변수를 연결 관리자 속성에 매핑하려면 다음을 수행합니다. 연결 관리자 속성에 대한 매개 변수가 SSIS 서버에 자동으로 생성됩니다.  
  
    1.  **매개 변수** 페이지의 **연결 관리자** 탭에서 **값** 필드 옆에 있는 찾아보기 단추를 클릭합니다.  
  
    2.  **환경 변수 사용**을 클릭한 다음 만든 환경 변수를 선택합니다.  
  
14. **확인** 을 두 번 클릭하여 변경 내용을 저장합니다.  

## <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>저장 프로시저를 사용하여 SSIS 패키지 배포 및 실행
  프로젝트 배포 모델을 사용하도록 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 구성하면 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 카탈로그의 저장 프로시저를 사용하여 프로젝트를 배포하고 패키지를 실행할 수 있습니다. 프로젝트 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)를 참조하십시오.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용하여 프로젝트를 배포하고 패키지를 실행할 수도 있습니다. 자세한 내용은 **참고 항목** 섹션의 항목을 참조하십시오.  
  
> [!TIP]
>  다음을 수행하여 아래 절차에 나열된 저장 프로시저에 대한 Transact-SQL 문을 쉽게 생성할 수 있습니다. 단, catalog.deploy_project는 예외입니다.  
> 
>  1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **Integration Services 카탈로그** 노드를 확장하고 실행할 패키지로 이동합니다.  
> 2.  패키지를 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다.  
> 3.  필요에 따라 **고급** 탭에서 로깅 수준 등의 옵션을 설정하거나 매개 변수 값과 연결 관리자 속성을 설정합니다.  
> 
>      로깅 수준에 대한 자세한 내용은 [SSIS 서버에서 패키지 실행에 대한 로깅 설정](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)을 참조하십시오.  
> 4.  **확인** 을 클릭하여 패키지를 실행하기 전에 **스크립트**를 클릭합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쿼리 편집기 창에 Transact-SQL이 나타납니다.  
  
### <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>저장 프로시저를 사용하여 패키지를 배포하고 실행하려면  
  
1.  [catalog.deploy_project&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)를 호출하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 대한 패키지를 포함하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 배포합니다.  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 배포 파일의 이진 콘텐츠를 검색하려면 *@project_stream* 매개 변수에 대해 SELECT 문을 OPENROWSET 함수 및 BULK 행 집합 공급자와 함께 사용합니다. BULK 행 집합 공급자를 사용하여 파일에서 데이터를 읽을 수 있습니다. BULK 행 집합 공급자에 대한 SINGLE_BLOB 인수는 데이터 파일의 내용을 varbinary(max) 형식의 단일 행, 단일 열 행 집합으로 반환합니다. 자세한 내용은 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)을 참조하세요.  
  
     다음 예에서는 SSISPackages_ProjectDeployment 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버의 SSIS Packages 폴더에 배포합니다. 프로젝트 파일(SSISPackage_ProjectDeployment.ispac)에서 이진 데이터를 읽어서 varbinary(max) 형식의 *@ProjectBinary* 매개 변수에 저장합니다. *@ProjectBinary* 매개 변수 값이 *@project_stream* 매개 변수에 할당됩니다.  
  
    ```sql
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)을 호출하여 프로젝트 실행 인스턴스를 만들고 필요에 따라 [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)를 호출하여 런타임 매개 변수 값을 설정합니다.  
  
     다음 예에서는 catalog.create_execution이 SSISPackage_ProjectDeployment 프로젝트에 포함된 package.dtsx에 대한 실행 인스턴스를 만듭니다. 프로젝트는 SSIS Packages 폴더에 있습니다. 저장 프로시저에서 반환된 execution_id가 catalog.set_execution_parameter_value 호출에 사용됩니다. 이 두 번째 저장 프로시저는 LOGGING_LEVEL 매개 변수를 3(자세한 로깅)으로 설정하고 Parameter1이라는 패키지 매개 변수의 값을 1로 설정합니다.  
  
     LOGGING_LEVEL과 같은 매개 변수의 object_type 값은 50입니다. 패키지 매개 변수의 object_type 값은 30입니다.  
  
    ```sql
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)을 호출하여 패키지를 실행합니다.  
  
     다음 예에서는 패키지 실행 시작을 위해 catalog.start_execution 호출이 Transact-SQL에 추가됩니다. catalog.create_execution 저장 프로시저에서 반환된 execution_id가 사용됩니다.  
  
    ```sql
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
### <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>저장 프로시저를 사용하여 서버 간에 프로젝트를 배포하려면  
 [catalog.get_project&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md) 및 [catalog.deploy_project&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md) 저장 프로시저를 사용하여 서버 간에 프로젝트를 배포할 수 있습니다.  
  
 저장 프로시저를 실행하기 전에 다음을 수행해야 합니다.  
  
-   연결된 서버 개체를 만듭니다. 자세한 내용은 [연결된 서버 만들기&#40;SQL Server 데이터베이스 엔진&#41;](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)를 참조하세요.  
  
     **연결된 서버 속성** 대화 상자의 **서버 옵션** 페이지에서 **RPC** 와 **RPC 내보내기** 를 **True**로 설정합니다. **RPC에 대한 분산 트랜잭션 승격 설정** 도 **False**로 설정합니다.  
  
-   개체 탐색기의 **연결된 서버** 에서 **공급자** 노드를 확장하고 공급자를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭하여 연결된 서버에 대해 선택된 공급자에 동적 매개 변수를 사용하도록 설정합니다. **동적 매개 변수** 옆에서 **사용**을 선택합니다.  
  
-   DTC(Distributed Transaction Coordinator)가 두 서버에서 모두 시작되었는지 확인합니다.  
  
 catalog.get_project를 호출하여 프로젝트에 대한 이진값을 반환하고 catalog.deploy_project를 호출합니다. catalog.get_project에서 반환된 값이 varbinary(max) 형식의 테이블 변수에 삽입됩니다. 연결된 서버에서는 varbinary(max) 형식의 결과를 반환할 수 없습니다.  
  
 다음 예에서는 catalog.get_project가 연결된 서버의 SSISPackages 프로젝트에 대한 이진값을 반환합니다. catalog.deploy_project가 로컬 서버의 DestFolder 폴더에 프로젝트를 배포합니다.  
  
```sql
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  

## <a name="integration-services-project-conversion-wizard"></a>Integration Services 프로젝트 변환 마법사
  **Integration Services 프로젝트 변환 마법사** 는 프로젝트를 프로젝트 배포 모델로 변환합니다.  
  
> [!NOTE]  
>  프로젝트에 하나 이상의 데이터 원본이 포함된 경우 프로젝트 변환이 완료되면 데이터 원본이 제거됩니다. 프로젝트의 패키지에서 공유할 수 있는 데이터 원본에 대한 연결을 만들려면 프로젝트 수준에서 연결 관리자를 추가합니다. 자세한 내용은 [패키지에서 연결 관리자 추가, 삭제 또는 공유](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)을 참조하세요.  
  
 **수행 작업**  
  
-   [Integration Services 프로젝트 변환 마법사 열기](#open_dialog)  
  
-   [패키지 찾기 페이지에서 옵션 설정](#locate)  
  
-   [패키지 선택 페이지에서 옵션 설정](#selectPackages)  
  
-   [대상 선택 페이지에서 옵션 설정](#destination)  
  
-   [프로젝트 속성 지정 페이지에서 옵션 설정](#projectProperties)  
  
-   [패키지 실행 태스크 업데이트 페이지에서 옵션 설정](#executePackage)  
  
-   [구성 선택 페이지에서 옵션 설정](#configurations)  
  
-   [매개 변수 만들기 페이지에서 옵션 설정](#createParameters)  
  
-   [매개 변수 구성 페이지에서 옵션 설정](#configureParameters)  
  
-   [검토 페이지에서 옵션 설정](#review)  
  
-   [변환 수행에서 옵션 설정](#conversion)  
  
###  <a name="open_dialog"></a> Integration Services 프로젝트 변환 마법사 열기  
 다음 중 하나를 수행하여 **Integration Services 프로젝트 변환** 마법사를 엽니다.  
  
-   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 프로젝트를 열고 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **프로젝트 배포 모델로 변환**을 클릭합니다.  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 개체 탐색기에서 **프로젝트** 노드를 마우스 오른쪽 단추로 클릭하고 **패키지 가져오기**를 선택합니다.  
  
 **Integration Services 프로젝트 변환 마법사** 를 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 에서 실행하는지 아니면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 실행하는지에 따라 수행되는 변환 태스크가 다릅니다.   
  
###  <a name="locate"></a> 패키지 찾기 페이지에서 옵션 설정  
  
> [!NOTE]  
>  **패키지 찾기** 페이지는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 마법사를 실행할 때만 사용할 수 있습니다.  
  
 **원본** 드롭다운 목록에서 **파일 시스템** 을 선택하면 페이지에 다음 옵션이 표시됩니다. 패키지가 파일 시스템에 있으면 이 옵션을 선택합니다.  
  
 **Folder**  
 패키지 경로를 입력하거나 **찾아보기**를 클릭하여 패키지로 이동합니다.  
  
 **원본** 드롭다운 목록에서 **SSIS 패키지 저장소**를 선택하면 페이지에 다음 옵션이 표시됩니다. 패키지 저장소에 대한 자세한 내용은 [패키지 관리&#40;SSIS 서비스&#41;](../../integration-services/service/package-management-ssis-service.md)를 참조하세요.  
  
 **Server**  
 서버 이름을 입력하거나 서버를 선택합니다.  
  
 **Folder**  
 패키지 경로를 입력하거나 **찾아보기**를 클릭하여 패키지로 이동합니다.  
  
 **원본** 드롭다운 목록에서 **Microsoft SQL Server** 를 선택하면 페이지에 다음 옵션이 표시됩니다. 패키지가 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 있으면 이 옵션을 선택합니다.  
  
 **Server**  
 서버 이름을 입력하거나 서버를 선택합니다.  
  
 **Windows 인증 사용**  
 Microsoft Windows 인증 모드에서는 사용자가 Windows 사용자 계정을 통해 연결할 수 있습니다. Windows 인증을 사용하면 사용자 이름 또는 암호를 제공할 필요가 없습니다.  
  
 **SQL Server 인증 사용**  
 사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정이 설정되었는지와 지정한 암호가 이전에 기록한 암호와 일치하는지를 확인하여 연결을 인증합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 로그인 계정이 설정되어 있지 않으면 인증이 실패하고 오류 메시지가 나타납니다.  
  
 **User name**  
 SQL Server 인증을 사용할 경우 사용자 이름을 지정합니다.  
  
 **암호**  
 SQL Server 인증을 사용할 경우 암호를 제공합니다.  
  
 **Folder**  
 패키지 경로를 입력하거나 **찾아보기**를 클릭하여 패키지로 이동합니다.  
  
###  <a name="selectPackages"></a> 패키지 선택 페이지에서 옵션 설정  
 **패키지 이름**  
 패키지 파일을 나열합니다.  
  
 **상태**  
 패키지를 프로젝트 배포 모델로 변환할 준비가 되었는지를 나타냅니다.  
  
 **메시지**  
 패키지와 연결된 메시지를 표시합니다.  
  
 **암호**  
 패키지와 연결된 암호를 표시합니다. 암호 텍스트는 숨겨져 있습니다.  
  
 **선택 항목에 적용**  
 **암호** 입력란의 암호를 선택한 패키지에 적용하려면 클릭합니다.  
  
 **새로 고침**  
 패키지 목록을 새로 고칩니다.  
  
###  <a name="destination"></a> 대상 선택 페이지에서 옵션 설정  
 이 페이지에서 새 프로젝트 배포 파일(.ispac)의 이름과 경로를 지정하거나 기존 파일을 선택합니다.  
  
> [!NOTE]  
>  **대상 선택** 페이지는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 마법사를 실행할 때만 사용할 수 있습니다.  
  
 **출력 경로**  
 배포 파일에 대한 경로를 입력하거나 **찾아보기**를 클릭하여 해당 파일로 이동합니다.  
  
 **프로젝트 이름**  
 프로젝트 이름을 입력합니다.  
  
 **보호 수준**  
 보호 수준을 선택합니다. 자세한 내용은 [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)을 참조하세요.  
  
 **프로젝트 설명**  
 프로젝트에 대한 선택적 설명을 입력합니다.  
  
###  <a name="projectProperties"></a> 프로젝트 속성 지정 페이지에서 옵션 설정  
  
> [!NOTE]  
>  **프로젝트 속성 지정** 페이지는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 마법사를 실행할 때만 사용할 수 있습니다.  
  
 **프로젝트 이름**  
 프로젝트 이름을 나열합니다.  
  
 **보호 수준**  
 프로젝트에 포함된 패키지에 대한 보호 수준을 선택합니다. 보호 수준에 대한 자세한 내용은 [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)를 참조하십시오.  
  
 **프로젝트 설명**  
 선택적인 프로젝트 설명을 입력합니다.  
  
###  <a name="executePackage"></a> 패키지 실행 태스크 업데이트 페이지에서 옵션 설정  
 프로젝트 기반 참조를 사용할 수 있도록 패키지 실행 태스크 업데이트가 패키지에 포함되었습니다. 자세한 내용은 [Execute Package Task Editor](../../integration-services/control-flow/execute-package-task-editor.md)을 참조하세요.  
  
 **부모 패키지**  
 패키지 실행 태스크를 사용하여 자식 패키지를 실행하는 패키지의 이름을 나열합니다.  
  
 **태스크 이름**  
 패키지 실행 태스크의 이름을 나열합니다.  
  
 **원래 참조**  
 자식 패키지의 현재 경로를 나열합니다.  
  
 **참조 할당**  
 프로젝트에 저장된 자식 패키지를 선택합니다.  
  
###  <a name="configurations"></a> 구성 선택 페이지에서 옵션 설정  
 매개 변수로 대체하려고 하는 패키지 구성을 선택합니다.  
  
 **패키지**  
 패키지 파일을 나열합니다.  
  
 **형식**  
 XML 구성과 같은 구성 유형을 나열합니다.  
  
 **구성 문자열**  
 구성 파일의 경로를 나열합니다.  
  
 **상태**  
 구성에 대한 상태 메시지를 표시합니다. 전체 메시지 텍스트를 보려면 메시지를 클릭합니다.  
  
 **구성 추가**  
 다른 프로젝트에 포함된 패키지 구성을 매개 변수로 바꾸려는 사용 가능한 구성 목록에 추가합니다. 파일 시스템 또는 SQL Server에 저장된 구성을 선택할 수 있습니다.  
  
 **새로 고침**  
 구성 목록을 새로 고치려면 클릭합니다.  
  
 **변환 후 구성을 모든 패키지에서 제거**  
 이 옵션을 선택하여 프로젝트에서 모든 구성을 제거하는 것이 좋습니다.  
  
 이 옵션을 선택하지 않으면 매개 변수로 바꾸려고 선택한 구성만 제거됩니다.  
  
###  <a name="createParameters"></a> 매개 변수 만들기 페이지에서 옵션 설정  
 각 구성 속성에 대한 매개 변수 이름과 범위를 선택합니다.  
  
 **패키지**  
 패키지 파일을 나열합니다.  
  
 **매개 변수 이름**  
 매개 변수 이름을 나열합니다.  
  
 **범위**  
 패키지 또는 프로젝트 중에서 매개 변수 범위를 선택합니다.  
  
###  <a name="configureParameters"></a> 매개 변수 구성 페이지에서 옵션 설정  
 **이름**  
 매개 변수 이름을 나열합니다.  
  
 **범위**  
 매개 변수의 범위를 나열합니다.  
  
 **Value**  
 매개 변수 값을 나열합니다.  
  
 매개 변수 속성을 구성하려면 값 필드 옆에 있는 줄임표 단추를 클릭합니다.  
  
 **매개 변수 정보 설정** 대화 상자에서 매개 변수 값을 편집할 수 있습니다. 패키지를 실행할 때 매개 변수 값을 제공해야 하는지 여부를 지정할 수도 있습니다.  
  
 매개 변수 옆에 있는 찾아보기 단추를 클릭하여 **에서** 구성 **대화 상자의** 매개 변수 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]페이지에 있는 값을 수정할 수 있습니다. **매개 변수 값 설정** 대화 상자가 표시됩니다.  
  
 **매개 변수 정보 설정** 대화 상자에는 매개 변수 값의 데이터 형식 및 매개 변수의 원본도 나열됩니다.  
  
###  <a name="review"></a> 검토 페이지에서 옵션 설정  
 **검토** 페이지를 사용하여 프로젝트 변환을 위해 선택한 옵션을 확인합니다.  
  
 **이전**  
 옵션을 변경하려면 클릭합니다.  
  
 **변환**  
 프로젝트를 프로젝트 배포 모델로 변환하려면 클릭합니다.  
  
###  <a name="conversion"></a> 변환 수행에서 옵션 설정  
 변환 수행 페이지에는 프로젝트 변환 상태가 표시됩니다.  
  
 **동작**  
 특정 변환 단계를 나열합니다.  
  
 **결과**  
 각 변환 단계의 상태를 나열합니다. 자세한 내용을 보려면 상태 메시지를 클릭하십시오.  
  
 프로젝트 변환은 프로젝트가 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에 저장될 때까지 저장되지 않습니다.  
  
 **보고서 저장**  
 프로젝트 변환 요약을 .xml 파일로 저장하려면 클릭합니다.  
