---
title: 차원 처리 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimensionprocessingdest.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8ca91bb8788d44c8a5a51d84e3d56b7a2b05d95e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827360"
---
# <a name="dimension-processing-destination"></a>차원 처리 대상
  차원 처리 대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 차원을 로드하고 처리합니다. 차원에 대한 자세한 내용은 [차원&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 차원 처리 대상에는 다음 기능이 포함됩니다.  
  
-   증분, 전체 또는 업데이트 처리를 수행하기 위한 옵션  
  
-   차원 처리 중에 오류를 무시하거나 지정된 오류 개수 이후에 프로세스가 중지되는지 여부를 지정하기 위한 오류 구성  
  
-   입력 열을 차원 테이블의 열로 매핑  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 처리하는 방법에 대한 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>차원 처리 대상 구성  
 차원 처리 대상은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 연결하거나 대상에서 처리되는 차원이 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
 이 대상은 하나의 입력을 갖습니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **차원 처리 대상 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [차원 처리 대상 편집기&#40;연결 관리자 페이지&#41;](../dimension-processing-destination-editor-connection-manager-page.md)  
  
-   [차원 처리 대상 편집기&#40;매핑 페이지&#41;](../dimension-processing-destination-editor-mappings-page.md)  
  
-   [차원 처리 대상 편집기&#40;고급 페이지&#41;](../dimension-processing-destination-editor-advanced-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [공용 속성](../common-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 흐름](data-flow.md)   
 [Integration Services 변환](transformations/integration-services-transformations.md)  
  
  
