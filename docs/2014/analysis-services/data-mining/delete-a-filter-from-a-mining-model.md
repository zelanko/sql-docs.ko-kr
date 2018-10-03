---
title: 마이닝 모델에서 필터를 삭제 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- filters [Analysis Services]
ms.assetid: 91220b21-adbc-49a9-b200-8bf0a724eff1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 02bf9026d14f759b5e5931b132faae3ee0fec1a2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082943"
---
# <a name="delete-a-filter-from-a-mining-model"></a>마이닝 모델에서 필터 삭제
  마이닝 모델에 대한 필터를 정의할 때 데이터 원본 뷰에서 데이터의 하위 집합에 대한 모델을 만들 수 있습니다. 필터는 원래 데이터의 하위 집합에 대한 모델의 정확도를 테스트하는 데에도 유용합니다.  
  
 그러나 전체 사례 집합을 다시 보려면 필터를 삭제해야 합니다. 이 절차에서는 필터에서 조건을 제거하거나 필터를 완전히 삭제하는 방법에 대해 설명합니다.  
  
### <a name="to-delete-a-condition-from-a-filter-on-a-mining-model"></a>마이닝 모델의 필터에서 조건을 삭제하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 솔루션 탐색기에서 필터링할 마이닝 모델이 포함된 마이닝 구조를 클릭합니다.  
  
2.  **마이닝 모델** 탭을 클릭합니다.  
  
3.  모델을 선택하고 마우스 오른쪽 단추를 클릭하여 바로 가기 메뉴를 엽니다.  
  
     -또는-  
  
     모델을 선택합니다. **마이닝 모델** 메뉴에서 **모델 필터 설정**을 선택합니다.  
  
4.  **모델 필터** 대화 상자에서 삭제할 조건이 포함된 표의 행을 마우스 오른쪽 단추로 클릭합니다.  
  
5.  **삭제**를 선택합니다.  
  
### <a name="to-clear-the-filter-on-a-mining-model-in-the-filter-editor-dialog-box"></a>필터 편집기 대화 상자에서 마이닝 모델의 필터를 지우려면  
  
-   **필터 편집기** 대화 상자에서 표의 아무 행이나 마우스 오른쪽 단추로 클릭하고 **모두 삭제**를 선택합니다.  
  
## <a name="working-with-model-filters-using-the-properties-window"></a>속성 창을 사용하여 모델 필터 작업  
 전체 필터를 삭제하는 경우에는 필터 편집기 대화 상자를 열지 않아도 됩니다. 만든 필터 조건에서 사용할 수는 `Filter` 마이닝 모델의 속성입니다.  
  
> [!NOTE]  
>  마이닝 모델의 속성은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서는 볼 수 있지만 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 볼 수 없습니다.  
  
#### <a name="to-clear-the-filter-on-a-mining-model-in-solution-explorer"></a>솔루션 탐색기에서 마이닝 모델의 필터를 지우려면  
  
1.  솔루션 탐색기에서 필터가 포함된 마이닝 모델을 클릭합니다.  
  
2.  에 **속성** 창의 필터 텍스트를 마우스 오른쪽 단추로 클릭 합니다 `Filter` 속성을 선택한 **모두 선택**합니다.  
  
3.  백스페이스 또는 Delete 키를 누릅니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델에서 사례 데이터로 드릴스루](drill-through-to-case-data-from-a-mining-model.md)   
 [마이닝 모델 태스크 및 방법](mining-model-tasks-and-how-tos.md)   
 [마이닝 모델에 대 한 필터 &#40;Analysis Services-데이터 마이닝&#41;](mining-models-analysis-services-data-mining.md)  
  
  
