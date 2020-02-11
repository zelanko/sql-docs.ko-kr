---
title: Analysis Services 프로젝트에 대 한 XML 보기 (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], viewing XML
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f4826be0fd38118e94921f63e02882935132a4d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072474"
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Analysis Services 프로젝트에 대한 XML 보기(SSDT)
  프로젝트 모드로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 사용하는 경우 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 프로젝트 폴더 내의 각 개체에 대해 XML 정의를 만듭니다. 
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]내에서 각 개체에 대한 XML 파일의 내용을 볼 수 있습니다. XML 파일을 직접 편집할 수도 있지만 이러한 변경 내용으로 인해 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 XML을 읽지 못할 수도 있으므로 이 방법은 일반적으로 권장되지 않습니다.  
  
> [!NOTE]  
>  전체 프로젝트에 대한 xml 코드는 볼 수 없지만 각 개체에 대한 파일이 개별적으로 존재하기 때문에 각 개체의 코드를 볼 수 있습니다. 전체 프로젝트에 대 한 코드를 볼 수 있는 유일한 방법은 프로젝트를 빌드하고 \<프로젝트 이름>. asdatabase 데이터베이스 파일에서 해당 코드를 확인 하는 것입니다.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>개체에 대한 XML 코드를 보려면  
  
1.  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 개체를 마우스 오른쪽 단추로 클릭한 다음 **코드 보기**를 클릭합니다.  
  
     개체에 대한 XML 코드가 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSDT &#40;Analysis Services 프로젝트 빌드&#41;](build-analysis-services-projects-ssdt.md)  
  
  
