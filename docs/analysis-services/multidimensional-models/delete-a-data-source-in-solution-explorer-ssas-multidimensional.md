---
title: 솔루션 탐색기 (SSAS 다차원)에서 데이터 원본을 삭제 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 51510891524b77ee0a2edaa33f024c538dcd4b81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043978"
---
# <a name="delete-a-data-source-in-solution-explorer-ssas-multidimensional"></a>솔루션 탐색기에서 데이터 원본 삭제(SSAS 다차원)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  데이터 원본 개체를 삭제하여 Analysis Services 다차원 모델 프로젝트에서 해당 개체를 영구적으로 제거할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 데이터 원본은 데이터 원본 뷰의 생성 기반을 제공하며 데이터 원본 뷰는 다시 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트나 데이터베이스의 차원, 큐브 및 마이닝 구조를 정의하는 데 사용됩니다. 따라서 데이터 원본을 삭제하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 다른 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체가 무효화될 수 있습니다. 항상 개체를 삭제하기 전에 제공되는 종속 개체의 목록을 검토해야 합니다.  
  
> [!IMPORTANT]  
>  다른 개체가 종속된 데이터 원본은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 온라인 모드로 열린 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 데이터베이스에서 삭제할 수 없습니다. 데이터 원본을 삭제하기 전에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에서 해당 데이터 원본에 종속된 모든 개체를 삭제해야 합니다. 온라인 모드에 대한 자세한 내용은 [Connect in Online Mode to an Analysis Services Database](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)을 참조하십시오.  
  
### <a name="to-delete-a-data-source"></a>데이터 원본을 삭제하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 데이터 원본을 삭제할 데이터베이스에 연결하거나 프로젝트를 엽니다.  
  
2.  **솔루션 탐색기**에서 **데이터 원본** 폴더를 확장합니다.  
  
3.  데이터 원본을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다. **개체 삭제**  대화 상자가 나타나고, 데이터 원본을 삭제하는 경우 무효화될 개체가 표시됩니다. **확인** 을 클릭하여 데이터 원본을 삭제하기 전에 이 목록을 신중하게 검토합니다.  
  
4.  프로젝트를 저장합니다.  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 데이터 원본을 삭제한 후 수정된 프로젝트를 저장해야 합니다. 그렇지 않으면 프로젝트에서 삭제된 데이터 원본을 로드할 때 삭제된 데이터 원본의 기본 XML 파일이 없으므로 다음에 프로젝트를 열 때 오류가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델의 데이터 원본](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [지원되는 데이터 원본&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
