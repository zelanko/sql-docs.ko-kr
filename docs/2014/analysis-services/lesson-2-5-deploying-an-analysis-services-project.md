---
title: 배포 된 Analysis Services 프로젝트 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5d98bab3-3577-4143-b737-5196444a36ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7f04f586511140b9e21c8eca80ec19b43fa90eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729389"
---
# <a name="deploying-an-analysis-services-project"></a>Analysis Services 프로젝트 배포
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 프로젝트의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 있는 개체에 대한 큐브 및 차원 데이터를 보려면 지정한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 이 프로젝트를 배포한 다음 큐브와 큐브 차원을 처리해야 합니다. *프로젝트를* 배포 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 정의된 개체가 만들어집니다. *인스턴스의 개체를* 처리 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 하면 데이터가 기본 데이터 원본에서 큐브 개체로 복사됩니다. 자세한 내용은 [Analysis Services 프로젝트 배포&#40;SSDT&#41;](multidimensional-models/deploy-analysis-services-projects-ssdt.md) 및 [Analysis Services 프로젝트 속성 구성&#40;SSDT&#41;](multidimensional-models/configure-analysis-services-project-properties-ssdt.md)을 참조하세요.  
  
 개발 프로세스의 이 시점에서는 일반적으로 개발 서버의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 큐브를 배포합니다. 비즈니스 인텔리전스 프로젝트 개발이 완료되면 일반적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개발 마법사를 사용하여 개발 서버의 프로젝트를 프로덕션 서버에 배포합니다. 자세한 내용은 [다차원 모델 솔루션 배포](multidimensional-models/multidimensional-model-solution-deployment.md) 및 [배포 마법사를 사용하여 모델 솔루션 배포](multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)를 참조하세요.  
  
 다음 태스크에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 프로젝트의 배포 속성을 검토한 다음 프로젝트를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 로컬 인스턴스에 배포하는 방법에 대해 설명합니다.  
  
### <a name="to-deploy-the-analysis-services-project"></a>Analysis Services 프로젝트를 배포하려면  
  
1.  솔루션 탐색기에서 **Analysis Services Tutorial** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
     **Analysis Services Tutorial 속성 페이지** 대화 상자가 나타나고 활성(개발) 구성의 속성이 표시됩니다. 각각 서로 다른 속성을 포함한 여러 구성을 정의할 수 있습니다. 예를 들어 개발자는 같은 프로젝트를 서로 다른 개발 컴퓨터에 데이터베이스 이름이나 처리 속성과 같은 서로 다른 배포 속성을 사용하여 배포하도록 구성할 수 있습니다. **Output Path** 속성 값이 표시됩니다. 이 속성은 프로젝트가 빌드될 때 프로젝트의 XMLA 배포 스크립트를 저장할 위치를 지정합니다. 이러한 스크립트는 프로젝트의 개체를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 배포하는 데 사용됩니다.  
  
2.  왼쪽 창의 **구성 속성** 노드에서 **배포**를 클릭합니다.  
  
     프로젝트의 배포 속성을 검토합니다. 기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트 템플릿을 통해 모든 프로젝트를 로컬 컴퓨터의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 기본 인스턴스에 증분식으로 배포하며 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트와 같은 이름으로 데이터베이스를 만들고 기본 처리 옵션을 사용하여 배포 후에 개체를 처리하도록 해당 프로젝트를 구성합니다. 자세한 내용은 [Analysis Services 프로젝트 속성 구성&#40;SSDT&#41;](multidimensional-models/configure-analysis-services-project-properties-ssdt.md)을 참조하세요.  
  
    > [!NOTE]  
    >  프로젝트의 명명된 된 인스턴스를 배포 하려는 경우 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 컴퓨터의 로컬 또는 원격 서버의 인스턴스에 변경 합니다 **Server** 와 같은 속성을 적절 한 인스턴스 이름 \<  *ServerName**>\\<** InstanceName * * >* 합니다.  
  
3.  **확인**을 클릭합니다.  
  
4.  솔루션 탐색기에서 **Analysis Services Tutorial** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **배포**를 클릭합니다. 기다려야 할 수도 있습니다.  
  
    > [!NOTE]  
    >  배포 중에 오류가 발생하는 경우 SQL Server Management Studio를 사용하여 데이터베이스 사용 권한을 확인하십시오. 데이터 원본 연결에 대해 지정한 계정에는 SQL Server 인스턴스에서 로그인이 있어야 합니다. 로그인을 두 번 클릭하면 사용자 매핑 속성을 볼 수 있습니다. 계정에는 **AdventureWorksDW2012** 데이터베이스에 대한 db_datareader 사용 권한이 있어야 합니다.  
  
     [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 프로젝트를 빌드한 다음 배포 스크립트를 사용하여 지정된 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 배포합니다. 두 창에 배포 진행률이 표시 됩니다: 합니다 **출력** 창 및 **배포 진행률-Analysis Services Tutorial** 창입니다.  
  
     필요한 경우 **보기** 메뉴에서 **출력** 을 클릭하여 출력 창을 엽니다. **출력** 창에는 전체적인 배포 진행률이 표시됩니다. 합니다 **배포 진행률-Analysis Services Tutorial** 창에는 배포 진행 단계가 자세히 표시 됩니다. 자세한 내용은 [Analysis Services 프로젝트 빌드&#40;SSDT&#41;](multidimensional-models/build-analysis-services-projects-ssdt.md) 및 [Analysis Services 프로젝트 배포&#40;SSDT&#41;](multidimensional-models/deploy-analysis-services-projects-ssdt.md)를 참조하세요.  
  
5.  내용을 검토 합니다 **출력** 창 및 **배포 진행률-Analysis Services Tutorial** 창 큐브에 작성 된 확인, 배포 및 처리가 오류 없이 합니다.  
  
6.  **배포 진행률 - Analysis Services Tutorial** 창을 숨기려면 창 도구 모음에서 **자동 숨기기** 아이콘(압정 모양)을 클릭합니다.  
  
7.  **출력** 창을 숨기려면 창 도구 모음에서 **자동 숨기기** 아이콘을 클릭합니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 로컬 인스턴스에 배포한 다음 배포된 큐브를 처리했습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [큐브 찾아보기](lesson-2-6-browsing-the-cube.md)  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 프로젝트 & #40; 배포 SSDT & #41;](multidimensional-models/deploy-analysis-services-projects-ssdt.md)   
 [Analysis Services 프로젝트 속성 구성&#40;SSDT&#41;](multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  
