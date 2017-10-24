---
title: "Analysis Services (SSDT) 프로젝트에 대 한 XML 보기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- projects [Analysis Services], viewing XML
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6633f8da10ad176ee86e9bbc61d42b638795a4a2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Analysis Services 프로젝트에 대한 XML 보기(SSDT)
  프로젝트 모드로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 사용하는 경우 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 프로젝트 폴더 내의 각 개체에 대해 XML 정의를 만듭니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]내에서 각 개체에 대한 XML 파일의 내용을 볼 수 있습니다. XML 파일을 직접 편집할 수도 있지만 이러한 변경 내용으로 인해 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 XML을 읽지 못할 수도 있으므로 이 방법은 일반적으로 권장되지 않습니다.  
  
> [!NOTE]  
>  전체 프로젝트에 대한 xml 코드는 볼 수 없지만 각 개체에 대한 파일이 개별적으로 존재하기 때문에 각 개체의 코드를 볼 수 있습니다. 코드에서 프로젝트를 빌드하고 ASSL을 확인 하는 전체 프로젝트에 대해 코드를 볼 수 있는 유일한 방법은 \<프로젝트 이름 >.asdatabase 파일입니다.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>개체에 대한 XML 코드를 보려면  
  
1.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 개체를 마우스 오른쪽 단추로 클릭한 다음 **코드 보기**를 클릭합니다.  
  
     개체에 대한 XML 코드가 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 프로젝트 빌드&#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
  

