---
title: "Analysis Services SQL Server Management Studio에서 스크립트 프로젝트 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [Analysis Services]
- scripts [Analysis Services], projects
- projects [Analysis Services], Analysis Server Scripts project
- projects [Analysis Services], creating
- Analysis Server Scripts project
- items [Analysis Services]
ms.assetid: c4f5a06b-e2e4-4660-a3a8-6fd356742c02
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2b8652fbb1028fa58f06d7ff165b02dc8f5fdc02
ms.sourcegitcommit: 3206a31870f8febab7d1718fa59fe0590d4d45db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="analysis-services-scripts-project-in-sql-server-management-studio"></a>SQL Server Management Studio의 Analysis Services 스크립트 프로젝트
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 분석 서버 스크립트 프로젝트를 만들어 개발, 관리 및 원본 제어를 위해 관련 스크립트를 그룹화할 수 있습니다. 현재 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 솔루션이 로드되어 있지 않은 경우 새 분석 서버 스크립트 프로젝트를 만들면 자동으로 새 솔루션이 생성됩니다. 그렇지 않은 경우 새 분석 서버 스크립트 프로젝트를 기존 솔루션에 추가하거나 새 솔루션에 만들 수 있습니다.  
  
 다음 기본 단계를 수행하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 분석 서버 스크립트 프로젝트를 만들 수 있습니다.  
  
1.  파일 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.  
  
     **분석 서버 스크립트** 프로젝트 템플릿을 선택한 다음 새 프로젝트의 이름과 위치를 지정합니다.  
  
2.  **연결** 을 마우스 오른쪽 단추로 클릭하여 솔루션 탐색기에 있는 Analysis Server 스크립트 프로젝트의 연결 폴더에 새 연결을 만듭니다.  
  
     이 폴더는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결 문자열을 포함하며 분석 서버 스크립트 프로젝트에 포함된 스크립트를 이에 대해 실행할 수 있습니다. 하나의 분석 서버 스크립트 프로젝트에 대해 여러 연결을 설정할 수 있으며 이러한 연결 중 프로젝트에 포함된 스크립트를 실행할 연결을 실행 시 선택할 수 있습니다.  
  
3.  **쿼리** 를 마우스 오른쪽 단추로 클릭하여 솔루션 탐색기에 있는 Analysis Server 스크립트 프로젝트의 스크립트 폴더에 MDX(Multidimensional Expressions), DMX(Data Mining Extensions) 및 XMLA(XML for Analysis) 스크립트를 만듭니다.
  
4.  프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **기존 항목** 을 선택하여 프로젝트에 대한 메모를 포함하는 텍스트 파일과 같은 기타 파일을 솔루션 탐색기에 있는 Analysis Server 스크립트 프로젝트의 **기타** 폴더에 추가합니다. 이러한 파일은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 무시됩니다.  
  
## <a name="file-types"></a>파일 유형  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 솔루션은 솔루션에 포함시킨 프로젝트에 따라 그리고 해당 솔루션의 각 프로젝트에 포함시킨 항목에 따라 여러 파일 형식을 포함할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 솔루션 파일 유형에 대한 자세한 내용은 [솔루션 및 프로젝트 관리 파일](http://msdn.microsoft.com/library/e19d2859-0b97-4727-ac27-c4c226d86b2f)을 참조하세요. 일반적으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 솔루션의 각 프로젝트에 대한 파일은 솔루션 폴더에 저장되며 각 프로젝트에 대해 별도의 폴더에 저장됩니다.  
  
 분석 서버 스크립트 프로젝트에 대한 프로젝트 폴더는 다음 표에 나열된 파일 유형을 포함할 수 있습니다.  
  
|파일 유형|Description|  
|---------------|-----------------|  
|분석 서버 스크립트 프로젝트 정의 파일(.ssmsasproj)|프로젝트에 포함된 파일을 표시할 폴더를 나타내는 정보를 비롯하여 솔루션 탐색기에 표시되는 폴더에 대한 메타데이터를 포함합니다.<br /><br /> 또한 프로젝트 정의 파일은 연결을 프로젝트에 포함된 스크립트 파일과 연결하는 메타데이터를 비롯하여 프로젝트에 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결에 대한 메타데이터를 포함합니다.|  
|DMX 스크립트 파일(.dmx)|프로젝트에 포함된 DMX 스크립트를 포함합니다.|  
|MDX 스크립트 파일(.mdx)|프로젝트에 포함된 MDX 스크립트를 포함합니다.|  
|XMLA 스크립트 파일(.xmla)|프로젝트에 포함된 XMLA 스크립트를 포함합니다.|  
  
## <a name="analysis-services-templates"></a>Analysis Services 템플릿  
 새 MDX, DMX 또는 XMLA 스크립트를 분석 서버 스크립트 프로젝트에 추가하는 경우 템플릿 탐색기를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 템플릿을 찾을 수 있습니다. 이러한 템플릿은 지정한 동작을 수행하는 방법을 보여 주는 미리 정의된 스크립트 또는 문의 모음입니다. 템플릿 탐색기는 **보기** 메뉴에서 사용할 수 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssEW](../../includes/ssew-md.md)]에 대한 템플릿을 포함합니다. 자세한 내용은 [Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SSDT&#40;SQL Server Data Tools&#41;를 사용하여 다차원 모델 만들기](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [다차원 식 &#40; Mdx&#41; 참조](../../mdx/multidimensional-expressions-mdx-reference.md)   
 [Data Mining Extensions &#40; DMX &#41; 참조](../../dmx/data-mining-extensions-dmx-reference.md)   
 [Analysis Services Scripting Language&#40;XMLA용 ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [스크립팅 언어 &#40; analysis Services ASSL XMLA &#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
  
