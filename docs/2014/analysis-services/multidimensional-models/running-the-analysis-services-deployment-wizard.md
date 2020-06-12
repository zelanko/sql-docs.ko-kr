---
title: Analysis Services 배포 마법사 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, running
ms.assetid: 3a38d489-4625-4878-bd18-c6f903be33df
author: minewiskan
ms.author: owend
ms.openlocfilehash: 03e142f00192e04d5b17bc2041563cea06199c8b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545725"
---
# <a name="running-the-analysis-services-deployment-wizard"></a>Analysis Services 배포 마법사 실행
  배포 마법사를 사용 하 여 프로젝트를 배포 하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다음과 같은 방법으로 마법사를 실행할 수 있습니다.  
  
-   **대화형으로**[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 대화형으로 실행하면 사용자 입력에 따라 변경되는 입력 파일을 기반으로 XML 배포 스크립트가 생성됩니다. 모든 사용자 수정 내용은 배포 스크립트에만 적용됩니다. 마법사가 입력 파일을 수정하지는 않습니다. 입력 파일에 대한 자세한 내용은 [배포 스크립트를 만드는 데 사용하는 입력 파일 이해](deployment-script-files-input-used-to-create-deployment-script.md)를 참조하세요.  
  
-   **명령 프롬프트에서** 명령 프롬프트에서 실행 되는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사는 마법사를 실행 하는 데 사용 하는 스위치에 따라 XMLA (XML for Analysis) 배포 스크립트를 생성 합니다. 이 경우 마법사가 사용자 입력이 필요한 메시지를 표시하고 해당 입력 내용을 기반으로 입력 파일을 수정하거나 현재 입력 파일을 그대로 사용하여 자동 무인 배포를 실행하거나 나중에 사용할 수 있는 배포 스크립트를 만들 수 있습니다.  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>대화형으로 Analysis Services 배포 마법사 실행  
 대화형으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 실행하면 마법사가 입력 파일의 값을 읽고 사용자에게 이 정보를 표시합니다. 배포 대상, 구성 설정, 배포 옵션 및 연결 문자열 암호 등의 입력 값을 수정 하거나 그대로 둘 수 있습니다. 사용자가 변경한 입력 값은 XMLA 배포 스크립트 생성 시 사용됩니다. 그러나 마법사가 입력 파일의 값을 변경하지는 않습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사가 입력 값을 수정하게 하려면 명령 프롬프트에서 마법사를 실행하고 응답 파일 모드로 실행되도록 마법사를 설정합니다.  
  
 입력 값을 검토한 다음 필요에 맞게 변경하면 XMLA 배포 스크립트가 생성됩니다. 이 배포 스크립트를 대상 서버에서 바로 실행하거나 나중에 사용하도록 저장할 수 있습니다.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>대화형으로 Analysis Services 배포 마법사를 실행하려면  
  
-   **시작**메뉴에서 **모든 프로그램**, **Microsoft SQL Server**, **Analysis Services**를 차례로 가리키고 **배포 마법사**를 클릭합니다.  
  
     또는  
  
-   프로젝트의 **프로젝트 폴더에서** . n e t [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 파일을 두 번 클릭 합니다. *\<project name>*  
  
    > [!NOTE]  
    >  Asdatabase 파일을 찾을 수 없는 경우 *\<project name>* 검색을 사용 하 여 * asdatabase를 지정 합니다.  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>명령 프롬프트에서 Analysis Services 배포 마법사 실행  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 명령 프롬프트에서도 실행할 수 있습니다. 명령 프롬프트에서 마법사를 실행하는 경우 .asdatabase 파일의 전체 경로를 제공하고 다음 모드 중 하나로 마법사를 실행합니다.  
  
 **응답 파일 모드**  
 응답 파일 모드에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]프로젝트를 작성할 때 기본적으로 생성된 입력 파일을 대화형으로 수정할 수 있습니다. 이렇게 수정한 입력 파일은 XMLA 배포 스크립트 생성 전에 저장됩니다. 수정한 입력 파일은 다음에 마법사를 실행할 때 새 시작 지점이 됩니다.  
  
 응답 파일 모드에서 마법사를 실행 하려면 **/a** 스위치를 사용 합니다.  
  
 **자동 모드**  
 자동 모드에서는 입력 파일에 있는 정보를 기반으로 자동 무인 배포가 실행됩니다.  
  
 자동 모드에서 마법사를 실행 하려면 **/s** 스위치를 사용 합니다. 자동 모드로 마법사를 실행하는 경우 메시지가 콘솔이나 로그 파일(제공된 경우)에 출력됩니다.  
  
 **출력 모드**  
 출력 모드에서는 입력 파일을 기반으로 나중에 실행할 XMLA 배포 스크립트가 생성됩니다.  
  
 출력 모드에서 마법사를 실행 하려면 **/o** 스위치를 사용 하 고 출력 파일 이름을 제공 합니다.  
  
 이러한 명령줄 스위치에 대한 자세한 내용은 [배포 유틸리티를 사용하여 모델 솔루션 배포](deploy-model-solutions-with-the-deployment-utility.md)를 참조하세요.  
  
 다음 절차에서는 명령 프롬프트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 실행하는 방법을 설명합니다.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>명령 프롬프트에서 Analysis Services 배포 마법사를 실행하려면  
  
1.  명령 프롬프트를 열고 C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE 폴더로 이동합니다.  
  
2.  **Microsoft.AnalysisServices.Deployment.exe** 를 입력하고 뒤에 마법사를 실행하려는 모드에 해당하는 스위치를 추가합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 배포 스크립트 이해](understanding-the-analysis-services-deployment-script.md)   
 [배포 마법사를 사용하여 모델 솔루션 배포](deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
