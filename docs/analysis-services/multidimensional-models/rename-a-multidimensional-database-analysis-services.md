---
title: "(Analysis Services) 다차원 데이터베이스 이름 바꾸기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: renaming databases
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6c56fc4d10e29e377b1b55330ec3badce57723f6
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="rename-a-multidimensional-database-analysis-services"></a>다차원 데이터베이스 이름 바꾸기(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]이름을 변경 하는 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 연결 하는 방법에 따라 달라 집니다는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스입니다. 기존 데이터베이스의 이름을 변경하려면 온라인 모드로 연결해야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 개체를 인스턴스화할 데이터베이스의 이름을 변경하려면 프로젝트 모드에서 연결해야 합니다.  
  
### <a name="to-change-the-database-name-in-online-mode"></a>온라인 모드에서 데이터베이스 이름을 변경하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 직접 연결합니다.  
  
2.  솔루션 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **데이터베이스 편집**을 클릭합니다.  
  
3.  **데이터베이스 이름** 입력란에서 데이터베이스 이름을 변경합니다.  
  
4.  도구 모음에서 **저장** 또는 **모두 저장** 을 클릭하거나 **파일** 메뉴에서 **선택한 항목 저장** 또는 **모두 저장** 을 클릭하거나 **데이터베이스 디자이너** 를 닫고 메시지가 표시되면 **저장** 을 클릭합니다.  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 데이터베이스 이름이 업데이트되고 솔루션 탐색기의 데이터베이스 개체가 새로 고쳐집니다.  
  
### <a name="to-change-the-database-name-in-project-mode"></a>프로젝트 모드에서 데이터베이스 이름을 변경하려면  
  
1.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **속성 페이지** 대화 상자의 **구성 속성** 섹션에서 **배포** 를 클릭합니다.  
  
4.  **데이터베이스** 속성을 새 데이터베이스 이름으로 변경합니다.  
  
     다음에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 배포하면 새 데이터베이스 이름으로 배포됩니다. 이 데이터베이스가 이미 있으면 덮어씁니다.  
  
### <a name="to-change-the-database-name-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 데이터베이스 이름을 변경하려면  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 마우스 오른쪽 단추로 클릭하고 Name 속성을 편집합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [다차원 데이터베이스 속성 &#40; 설정 합니다. Analysis Services &#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)   
 [Analysis Services 프로젝트 속성 구성&#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [Analysis Services 프로젝트 배포&#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
