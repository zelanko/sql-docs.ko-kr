---
title: 마이닝 모델에서 열의 불연속화 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- mining structures [Analysis Services], how-to topics
- discretized columns [data mining]
- bucketing problems [Analysis Services]
ms.assetid: 3c49862b-595d-4fa4-b890-e2e1bde1d74f
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af80e187acceb9565e939dbb3699c98b827cf648
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202173"
---
# <a name="change-the-discretization-of-a-column-in-a-mining-model"></a>마이닝 모델에서 열의 분할 변경
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 특정 시나리오에서 값을 자동으로 불연속화합니다. 즉, 숫자 열의 데이터가 범주화됩니다. 예를 들어 데이터에 연속 숫자 데이터가 포함되고 있고 의사 결정 트리 모델을 만드는 경우 데이터의 배포에 따라 연속 데이터의 각 열이 자동으로 범주화됩니다. 데이터가 불연속화되는 방법을 제어하려면 모델에서 데이터가 사용되는 방법을 제어하는 마이닝 구조 열의 속성을 변경해야 합니다.  
  
 마이닝 모델의 속성을 설정하는 방법에 대한 일반적인 내용은 [마이닝 모델 열](mining-model-columns.md)을 참조하세요.  
  
### <a name="to-display-the-properties-for-a-mining-model-column"></a>마이닝 모델 열의 속성을 표시하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 마이닝 모델의 이름이 포함된 열 머리글 또는 마이닝 알고리즘의 이름이 포함된 표의 행을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
     **속성** 창에 마이닝 모델과 연관된 모든 속성이 표시됩니다.  
  
2.  화면 왼쪽에 가까이 있는 **구조** 열에서 불연속화하려는 연속 숫자 데이터가 포함된 열을 클릭합니다.  
  
     **속성** 창에 선택한 열과 연관된 속성만 표시됩니다.  
  
### <a name="to-change-the-discretization-method"></a>분할 메서드를 변경하려면  
  
1.  에 **마이닝 속성** 창, 텍스트 상자 옆에 클릭 **콘텐츠**를 선택한 `Discretized` 드롭다운 목록에서.  
  
     이제 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 및 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 속성을 사용할 수 있습니다.  
  
2.  에 **속성** 창, 텍스트 상자 옆에 클릭 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 다음 값 중 하나를 선택 하 고: `Automatic`를 `EqualAreas`, 또는 `Cluster`합니다.  
  
    > [!NOTE]  
    >  열 사용법으로 설정 되어 있으면 `Ignore`는 **속성** 열 창은 비어 있습니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
3.  데이터 마이닝 디자이너의 **속성** 창에서 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 옆에 있는 입력란을 클릭하고 숫자 값을 입력합니다.  
  
    > [!NOTE]  
    >  이러한 속성을 변경하면 새 설정을 사용하려는 모든 모델과 함께 구조가 다시 처리되어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델 태스크 및 방법](mining-model-tasks-and-how-tos.md)  
  
  
