---
title: "Integration Services 서버에 프로젝트 배포 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e9402f4-4d50-49ff-820d-65a77829c4a5
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Integration Services 서버에 프로젝트 배포
  현재 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서는 환경을 사용하여 패키지를 관리하고, 패키지를 실행하고, 패키지에 대한 런타임 값을 구성할 수 있습니다.  
  
 환경에 대한 자세한 내용은 [서버 환경 만들기 및 매핑](../../integration-services/packages/create-and-map-a-server-environment.md)을 참조하세요.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서와 마찬가지로 현재 릴리스에서도 SQL Server 인스턴스에 패키지를 배포하고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 실행 및 관리할 수 있습니다. 패키지 배포 모델을 사용합니다. 자세한 내용은 [레거시 패키지 배포&#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포하려면 다음 태스크를 완료합니다.  
  
1.  SSISDB 카탈로그를 만듭니다(아직 없는 경우). 자세한 내용은 [SSIS 카탈로그 만들기](../../integration-services/service/create-the-ssis-catalog.md)를 참조하세요.  
  
2.  **Integration Services 프로젝트 변환 마법사** 를 실행하여 프로젝트를 프로젝트 배포 모델로 변환합니다. 자세한 내용은 아래의 [프로젝트 배포 모델로 프로젝트를 변환하려면](#convert)지침을 참조하세요.  
  
    -   [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]에서 프로젝트를 만든 경우 기본적으로 해당 프로젝트는 프로젝트 배포 모델을 사용합니다.  
  
    -   이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 프로젝트를 만든 경우 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 프로젝트 파일을 연 후 프로젝트 배포 모델로 프로젝트를 변환합니다.  
  
        > [!NOTE]  
        >  프로젝트에 하나 이상의 데이터 원본이 포함된 경우 프로젝트 변환이 완료되면 데이터 원본이 제거됩니다. 프로젝트의 패키지에서 공유할 수 있는 데이터 원본에 대한 연결을 만들려면 프로젝트 수준에서 연결 관리자를 추가합니다. 자세한 내용은 [Add, Delete, or Share a Connection Manager in a Package](../Topic/Add,%20Delete,%20or%20Share%20a%20Connection%20Manager%20in%20a%20Package.md)을 참조하세요.  
  
         **Integration Services 프로젝트 변환 마법사** 를 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 에서 실행하는지 아니면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 실행하는지에 따라 수행되는 변환 태스크가 다릅니다.  
  
        -   마법사를 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 실행하면 프로젝트에 포함된 패키지가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 2005, 2008 또는 2008 R2에서 현재 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 사용되는 형식으로 변환됩니다. 원래 프로젝트 파일(.dtproj)과 패키지 파일(.dtsx)이 업그레이드됩니다.  
  
        -   마법사를 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 실행하면 마법사는 프로젝트에 포함된 패키지 및 구성에서 프로젝트 배포 파일(.ispac)을 생성합니다. 원래 패키지 파일(.dtsx)은 업그레이드되지 않습니다.  
  
             마법사의 **대상 선택** 페이지에서 기존 파일을 선택하거나 새 파일을 만들 수 있습니다.  
  
             프로젝트 변환 시 패키지 파일을 업그레이드하려면 **Integration Services 프로젝트 변환 마법사** 를 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 실행합니다. 프로젝트 변환과 별도로 패키지 파일을 업그레이드하려면 **에서** Integration Services 프로젝트 변환 마법사 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 실행한 다음 **SSIS 패키지 업그레이드 마법사**를 실행합니다. 패키지 파일을 개별적으로 업그레이드한 경우에는 변경 내용을 저장해야 합니다. 그러지 않으면 프로젝트 배포 모델로 프로젝트를 변환할 때 저장되지 않은 패키지 변경 내용이 변환되지 않습니다.  
  
     패키지 업그레이드에 대한 자세한 내용은 [Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages.md) 및 [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)를 참조하세요.  
  
3.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포합니다. 자세한 내용은 아래의 [Integration Services 서버에 프로젝트를 배포하려면](#deploy) 지침을 참조하세요.  
  
4.  (선택 사항) 배포한 프로젝트에 대한 환경을 만듭니다. 자세한 내용은 [서버 환경 만들기 및 매핑](../../integration-services/packages/create-and-map-a-server-environment.md)을 참조하세요.  
  
##  <a name="convert"></a> 프로젝트 배포 모델로 프로젝트를 변환하려면  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 프로젝트를 열고 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **프로젝트 배포 모델로 변환**을 클릭합니다.  
  
     -또는-  
  
     [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 개체 탐색기에서 **프로젝트** 노드를 마우스 오른쪽 단추로 클릭하고 **패키지 가져오기**를 선택합니다.  
  
2.  마법사를 완료합니다. 자세한 내용은 [Integration Services Project Conversion Wizard](../../integration-services/packages/integration-services-project-conversion-wizard.md)을 참조하세요.  
  
##  <a name="deploy"></a> Integration Services 서버에 프로젝트를 배포하려면  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 프로젝트를 연 다음 **프로젝트** 메뉴에서 **배포** 를 선택하여 **Integration Services 배포 마법사**를 시작합니다.  
  
     -또는-  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] > **SSISDB** 노드를 확장하고 배포할 프로젝트의 프로젝트 폴더를 찾습니다. **프로젝트** 폴더를 마우스 오른쪽 단추로 클릭하고 **프로젝트 배포**를 클릭합니다.  
  
     -또는-  
  
     명령 프롬프트의 **%ProgramFiles%\Microsoft SQL Server\110\DTS\Binn**에서 **isdeploymentwizard.exe**를 실행합니다. 64비트 컴퓨터의 **%ProgramFiles(x86)%\Microsoft SQL Server\100\DTS\Binn**에는 도구의 32비트 버전도 있습니다.  
  
2.  **원본 선택** 페이지에서 **프로젝트 배포 파일** 을 클릭하여 프로젝트 배포 파일을 선택합니다.  
  
     -또는-  
  
     **Integration Services 카탈로그** 를 클릭하여 SSISDB 카탈로그에 이미 배포된 프로젝트를 선택합니다.  
  
3.  마법사를 완료합니다. 자세한 내용은 [Integration Services Deployment Wizard](../../integration-services/packages/integration-services-deployment-wizard.md)을 참조하세요.  
  
  