---
title: 처리 대화 상자 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.processdialog.f1
ms.assetid: c065248c-9001-4f0c-928f-9c59eccb618b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32411ff5b715e15fd52b832d8047d8382a603924
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070753"
---
# <a name="process-dialog-box-analysis-services---multidimensional-data"></a>처리 대화 상자(Analysis Services - 다차원 데이터)
  **및** 의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 처리 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체를 처리할 수 있습니다. 다음과 같은 방법으로 **에서** 처리 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 대화 상자를 표시할 수 있습니다.  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 솔루션 탐색기 **에서** 프로젝트, 큐브, 차원 또는 마이닝 구조를 마우스 오른쪽 단추로 클릭한 다음 **처리**를 선택합니다.  
  
-   모든 **큐브 디자이너** 페이지, 모든 **차원 디자이너**페이지 또는 **데이터 마이닝 모델 디자이너**의 **마이닝 구조** 및 **마이닝 모델** 페이지의 도구 모음에서 **처리**를 선택합니다.  
  
-   **데이터 마이닝 모델 디자이너** 의 **마이닝 모델** 페이지에서 마이닝 모델을 마우스 오른쪽 단추로 클릭한 다음 **마이닝 구조 및 모든 모델 처리** 또는 **모델 처리**를 선택합니다.  
  
 다음과 같은 방법으로 **SQL Server Management Studio** 에서 **처리** 대화 상자를 표시할 수 있습니다.  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체 탐색기 **에서** 데이터베이스, 큐브, 측정값 그룹, 파티션, 차원, 마이닝 구조 또는 마이닝 모델을 마우스 오른쪽 단추로 클릭한 다음 **처리**를 선택합니다.  
  
## <a name="options"></a>옵션  
 **개체 목록**  
 처리할 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체와 적용할 처리 옵션 및 설정을 선택합니다. 표에는 다음 열이 있습니다.  
  
 **개체 이름**  
 처리할 개체의 이름을 표시합니다. 이름 왼쪽에 있는 아이콘은 개체 유형을 나타냅니다.  
  
 **Type**  
 처리할 개체 유형을 표시합니다.  
  
 **처리 옵션**  
 선택한 개체에 대해 수행할 처리 유형을 선택합니다. 사용 가능한 처리 옵션에 대 한 자세한 내용은 [다차원 모델 개체 처리](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)를 참조 하세요.  
  
 **설정**  
 큐브, 측정값 그룹 또는 파티션에 대한 **처리 옵션** 에서 **증분 처리** 를 선택한 경우 **구성** 하이퍼링크가 표시됩니다. **구성** 을 클릭하여 **증분 업데이트** 대화 상자를 시작합니다. **증분 업데이트** 대화 상자에 대한 자세한 내용은 [증분 업데이트 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](incremental-update-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 **제거**  
 **개체 목록**에서 선택한 항목을 제거하려면 클릭합니다.  
  
 **영향 분석**  
 **영향 분석** 대화 상자를 열고 처리 태스크의 영향을 받게 될 개체를 표시하려면 클릭합니다. **영향 분석** 대화 상자에 대한 자세한 내용은 [영향 분석 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](impact-analysis-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.  
  
> [!NOTE]  
>   이 옵션은 **설정 변경** 대화 상자에서 **영향을 받는 개체 처리** 옵션을 선택한 경우 사용할 수 없습니다.  
  
 **설정 변경**  
 **설정 변경** 대화 상자를 열고 일괄 처리 설정, 쓰기 저장 설정 및 차원 키 오류 설정을 포함하여 선택한 개체의 처리를 제어하는 설정을 변경하려면 클릭합니다. **설정 변경** 대화 상자에 대한 자세한 내용은 [설정 변경 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](change-settings-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 **Run**  
 개체를 처리하려면 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [처리 진행률 대화 상자 &#40;Analysis Services 다차원 데이터&#41;](process-progress-dialog-box-analysis-services-multidimensional-data.md)  
  
  
