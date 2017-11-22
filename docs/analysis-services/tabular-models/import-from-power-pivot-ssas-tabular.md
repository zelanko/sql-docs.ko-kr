---
title: "Power Pivot (SSAS 테이블 형식)에서 가져오기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.importfromppt.f1
ms.assetid: ac1a6a79-bda3-4122-a717-8b1e2f77da02
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ddea709433a76faae800615c0a974ad14d153c8c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="import-from-power-pivot-ssas-tabular"></a>파워 피벗에서 가져오기(SSAS 테이블 형식)
  이 항목에서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에서 가져오기 프로젝트 템플릿을 사용하여 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]통합 문서에서 메타데이터와 데이터를 가져와서 새로운 테이블 형식 모델 프로젝트를 만드는 방법에 대해 설명합니다.  
  
## <a name="create-a-new-tabular-model-from-a-power-pivot-for-excel-file"></a>Power Pivot for Excel 파일에서 새 테이블 형식 모델 만들기  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에서 가져와서 새로운 테이블 형식 모델 프로젝트를 만드는 경우 통합 문서의 구조를 정의하는 메타데이터를 사용하여 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 테이블 형식 모델 프로젝트의 구조를 만들고 정의합니다. 테이블, 열, 측정값 및 관계와 같은 개체는 그대로 유지되며 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 표시되는 것과 같이 테이블 형식 모델 프로젝트에 표시됩니다. .xlsx 통합 문서 파일은 변경되지 않습니다.  
  
> [!NOTE]  
>  테이블 형식 모델은 연결된 테이블을 지원하지 않습니다. 연결된 테이블이 포함된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에서 가져오는 경우 연결된 테이블 데이터는 복사하여 붙여넣은 데이터로 처리되며 Model.bim 파일에 저장됩니다. 복사하여 붙여넣은 테이블의 속성을 볼 때 **원본 데이터** 속성은 비활성화되고 **테이블** 메뉴의 **테이블 속성** 대화 상자도 비활성화됩니다.  
>   
>  모델에 포함된 데이터에 추가할 수 있는 행은 최대 10,000개로 제한됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에서 모델을 가져오는 경우 “데이터가 잘렸습니다. 붙여넣은 테이블은 10,000개가 넘는 행을 포함할 수 없습니다.” 오류가 표시되면 포함된 데이터를 다른 데이터 원본(예: SQL Server의 테이블)으로 이동하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 모델을 수정한 다음 모델을 다시 가져와야 합니다.  
  
 작업 영역 데이터베이스가 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 와 동일한 컴퓨터(로컬)의 Analysis Services 인스턴스에 있는지, 아니면 원격 Analysis Services 인스턴스에 있는지에 따라 특별히 고려해야 할 사항이 있습니다.  
  
 작업 영역 데이터베이스가 Analysis Services의 로컬 인스턴스에 있는 경우 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에서 메타데이터와 데이터를 모두 가져올 수 있습니다. 메타데이터는 통합 문서에서 복사되고 테이블 형식 모델 프로젝트를 만드는 데 사용됩니다. 그런 다음 데이터가 통합 문서에서 복사되고 프로젝트의 작업 영역 데이터베이스에 저장됩니다(복사/붙여넣은 데이터는 제외되며 이러한 데이터는 Model.bim 파일에 저장됨).  
  
 작업 영역 데이터베이스가 원격 Analysis Services 인스턴스에 있는 경우 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 통합 문서에서 데이터를 가져올 수 없습니다. 통합 문서 메타데이터를 여전히 가져올 수 있지만 이렇게 하면 스크립트가 원격 Analysis Services 인스턴스에서 실행됩니다. 신뢰할 수 있는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에서만 메타데이터를 가져와야 합니다. 데이터 원본 연결에 정의된 원본에서 데이터를 가져와야 합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서의 복사하여 붙여넣은 테이블 데이터와 연결된 테이블 데이터를 복사하여 테이블 형식 모델 프로젝트에 붙여넣어야 합니다.  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-power-pivot-for-excel-file"></a>PowerPivot for Excel 파일에서 새 테이블 형식 모델 프로젝트를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 **파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.  
  
2.  **새 프로젝트** 대화 상자의 **설치된 템플릿**에서 **비즈니스 인텔리전스**를 클릭한 다음 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에서 가져오기**를 클릭합니다.  
  
3.  **이름**에 프로젝트의 이름을 입력하고 위치 및 솔루션 이름을 지정한 다음 **확인**을 클릭합니다.  
  
4.  **열기** 대화 상자에서 가져올 모델 메타데이터 및 데이터가 포함된 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 파일을 선택한 다음 **열기**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [작업 영역 데이터베이스&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)   
 [복사 및 붙여넣기 데이터 &#40; SSAS 테이블 형식 &#41;](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md)  
  
  
