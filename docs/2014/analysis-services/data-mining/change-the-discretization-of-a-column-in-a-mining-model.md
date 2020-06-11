---
title: 마이닝 모델에서 열의 불연속화 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- mining structures [Analysis Services], how-to topics
- discretized columns [data mining]
- bucketing problems [Analysis Services]
ms.assetid: 3c49862b-595d-4fa4-b890-e2e1bde1d74f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 3f5dfbc1ab2481afc1b4f4b152c7748f9ac5a03a
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525069"
---
# <a name="change-the-discretization-of-a-column-in-a-mining-model"></a>마이닝 모델에서 열의 분할 변경
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]자동으로 값을 불연속화 합니다. 즉, 특정 시나리오에서 숫자 열의 데이터를 bin으로 표시 합니다. 예를 들어 데이터에 연속 숫자 데이터가 포함되고 있고 의사 결정 트리 모델을 만드는 경우 데이터의 배포에 따라 연속 데이터의 각 열이 자동으로 범주화됩니다. 데이터가 불연속화되는 방법을 제어하려면 모델에서 데이터가 사용되는 방법을 제어하는 마이닝 구조 열의 속성을 변경해야 합니다.  
  
 마이닝 모델의 속성을 설정하는 방법에 대한 일반적인 내용은 [마이닝 모델 열](mining-model-columns.md)을 참조하세요.  
  
### <a name="to-display-the-properties-for-a-mining-model-column"></a>마이닝 모델 열의 속성을 표시하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 마이닝 모델의 이름이 포함된 열 머리글 또는 마이닝 알고리즘의 이름이 포함된 표의 행을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
     **속성** 창에 마이닝 모델과 연관된 모든 속성이 표시됩니다.  
  
2.  화면 왼쪽에 가까이 있는 **구조** 열에서 불연속화하려는 연속 숫자 데이터가 포함된 열을 클릭합니다.  
  
     **속성** 창에 선택한 열과 연관된 속성만 표시됩니다.  
  
### <a name="to-change-the-discretization-method"></a>분할 메서드를 변경하려면  
  
1.  **마이닝 속성** 창에서 **내용**옆에 있는 입력란을 클릭 하 고 `Discretized` 드롭다운 목록에서를 선택 합니다.  
  
     이제 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 및 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 속성을 사용할 수 있습니다.  
  
2.  **속성** 창에서 옆의 텍스트 상자를 클릭 하 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 고, 또는 값 중 하나를 선택 `Automatic` `EqualAreas` `Cluster` 합니다.  
  
    > [!NOTE]  
    >  열 사용법을로 설정 하면 해당 `Ignore` 열에 대 한 **속성** 창이 비어 있습니다.  
  
     디자이너에서 다른 요소를 선택하면 새 값이 적용됩니다.  
  
3.  데이터 마이닝 디자이너의 **속성** 창에서 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 옆에 있는 입력란을 클릭하고 숫자 값을 입력합니다.  
  
    > [!NOTE]  
    >  이러한 속성을 변경하면 새 설정을 사용하려는 모든 모델과 함께 구조가 다시 처리되어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 모델 태스크 및 방법](mining-model-tasks-and-how-tos.md)  
  
  
