---
title: 패키지 템플릿으로 패키지 저장 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- reusing packages
- templates [Integration Services]
ms.assetid: efe66cec-3933-4f6e-8d35-fe3d300de66c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 79652d50bb4df2bf80ec9f072e8828db9935368f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391190"
---
# <a name="save-a-package-as-a-package-template"></a>패키지 템플릿으로 패키지 저장
  이 항목에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 새 Integration Services 패키지를 만들 때 사용자 지정 패키지를 템플릿으로 지정하고 사용하는 방법에 대해 설명합니다. 기본적으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 새 패키지를 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 추가할 때 빈 패키지를 만드는 패키지 템플릿을 사용합니다. 이러한 기본 템플릿은 바꿀 수 없지만 새 템플릿을 추가할 수는 있습니다.  
  
 여러 개의 패키지를 템플릿으로 지정하여 사용할 수 있습니다. 사용자 지정 패키지를 템플릿으로 구현하려면 먼저 패키지를 만들어야 합니다.  
  
 사용자 지정 패키지를 템플릿으로 사용하여 패키지를 만들면 새 패키지에 템플릿과 동일한 이름 및 GUID가 지정됩니다. 패키지를 구분하려면 `Name` 속성 값을 업데이트하고 `ID` 속성에 대한 새 GUID를 생성해야 합니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 만들기](create-packages-in-sql-server-data-tools.md) 및 [패키지 속성 설정](set-package-properties.md)을 참조하세요.  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>사용자 지정 패키지를 패키지 템플릿으로 지정하려면  
  
1.  파일 시스템에서 템플릿으로 사용할 패키지를 찾습니다.  
  
2.  해당 패키지를 DataTransformationItems 폴더로 복사합니다. 기본적으로 이 폴더는 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject에 있습니다.  
  
3.  템플릿으로 사용할 각 패키지에 대해 1단계와 2단계를 반복합니다.  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>사용자 지정 패키지를 패키지 템플릿으로 사용하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 패키지를 만들려는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.  
  
3.  **새 항목 추가 -\<프로젝트 이름>** 대화 상자에서 템플릿으로 사용할 패키지를 클릭합니다.  
  
     템플릿 목록에 새 SSIS 패키지라는 기본 패키지 템플릿이 포함됩니다. 패키지 아이콘을 통해 패키지 템플릿으로 사용할 수 있는 템플릿을 식별할 수 있습니다.  
  
4.  **추가**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Data Tools에서 패키지 만들기](create-packages-in-sql-server-data-tools.md)   
 [Integration Services&#40;SSIS&#41; 패키지](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
