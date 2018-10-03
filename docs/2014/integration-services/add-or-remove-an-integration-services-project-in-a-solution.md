---
title: 추가 하거나 솔루션에서 Integration Services 프로젝트 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- Integration Services projects, adding
- SQL Server Integration Services projects, adding
- SSIS projects, adding
- projects [Integration Services], adding
ms.assetid: f01f6475-b63c-41dc-82ac-b62162b3adf7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 75e3727bcfc28ac60819c09068db4ae54711b72f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050111"
---
# <a name="add-or-remove-an-integration-services-project-in-a-solution"></a>솔루션에서 Integration Services 프로젝트 추가 또는 제거
  다음 절차에서는 솔루션에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 추가 또는 제거하는 방법에 대해 설명합니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 솔루션을 볼 수 있는 경우에만 해당 솔루션에 프로젝트를 추가하거나 솔루션에서 프로젝트를 제거할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]에서 **솔루션 항상 표시** 옵션을 선택한 경우 솔루션이 하나의 프로젝트만 포함하는 경우에도 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 해당 솔루션이 표시됩니다. 그렇지 않은 경우 솔루션은 두 개 이상의 프로젝트를 포함하는 경우에만 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에 표시됩니다. 추가 프로젝트는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 프로젝트이거나 다른 형식의 프로젝트일 수 있습니다.  
  
## <a name="adding-an-integration-services-project"></a>Integration Services 프로젝트 추가  
 프로젝트를 추가할 때 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 새로운 빈 프로젝트를 만들도록 하거나 다른 솔루션용으로 이미 만든 프로젝트를 추가할 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 솔루션을 볼 수 있는 경우에만 해당 솔루션에 프로젝트를 추가할 수 있습니다.  
  
#### <a name="to-add-a-new-integration-services-project-to-a-solution"></a>솔루션에 새 Integration Services 프로젝트를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 새 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 추가하려는 솔루션을 열고 다음 중 하나를 수행하십시오.  
  
    -   솔루션을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 후 **새 프로젝트**를 클릭합니다.  
  
    -   **파일** 메뉴에서 **추가**를 가리키고 **새 프로젝트**를 클릭합니다.  
  
2.  **새 프로젝트 추가** 대화 상자의 **템플릿** 창에서 **Integration Services 프로젝트** 를 클릭합니다.  
  
3.  선택적으로 프로젝트 이름과 위치를 편집합니다.  
  
4.  **확인**을 클릭합니다.  
  
#### <a name="to-add-an-existing-integration-services-project-to-a-solution"></a>솔루션에 기존 Integration Services 프로젝트를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 기존 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 추가하려는 솔루션을 열고 다음 중 하나를 수행합니다.  
  
    -   솔루션을 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 후 **기존 프로젝트**를 클릭합니다.  
  
    -   **파일** 메뉴에서 **추가**를 클릭한 후 **기존 프로젝트**를 클릭합니다.  
  
2.  **기존 프로젝트 추가** 대화 상자에서 추가할 프로젝트를 찾은 다음 **열기**를 클릭합니다.  
  
3.  **솔루션 탐색기**의 솔루션 폴더에 프로젝트가 추가됩니다.  
  
## <a name="removing-an-integration-services-project"></a>Integration Services 프로젝트 제거  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 솔루션을 볼 수 있는 경우에만 해당 솔루션에서 프로젝트를 제거할 수 있습니다. 솔루션이 표시되면 한 프로젝트를 제외한 나머지 프로젝트를 모두 제거할 수 있습니다. 프로젝트가 한 개만 남으면 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에 더 이상 해당 솔루션 폴더가 표시되지 않으므로 마지막 프로젝트를 제거할 수 없습니다.  
  
#### <a name="to-remove-an-integration-services-project-from-a-solution"></a>솔루션에서 Integration Services 프로젝트를 제거하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 제거하려는 솔루션을 엽니다.  
  
2.  솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **프로젝트 언로드**를 클릭합니다.  
  
3.  **확인** 을 클릭하여 제거를 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services &#40;SSIS&#41; 프로젝트](integration-services-ssis-projects-and-solutions.md)   
 [새 Integration Services 프로젝트 만들기](../../2014/integration-services/create-a-new-integration-services-project.md)  
  
  
