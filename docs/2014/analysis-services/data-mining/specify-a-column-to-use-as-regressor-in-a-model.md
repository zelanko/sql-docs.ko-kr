---
title: 모델에서 회귀 변수로 사용할 열을 지정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d8e0cb8e-302a-4166-9ed0-e2d9e2919b0a
author: minewiskan
ms.author: owend
ms.openlocfilehash: f3ce5a339275c834673afedcbbec50078407acdd
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84520411"
---
# <a name="specify-a-column-to-use-as-regressor-in-a-model"></a>모델에서 회귀 변수로 사용할 열 지정
  선형 회귀 모델은 데이터를 예상 회귀선에 가능한 한 근접하게 맞추는 방식으로 입력을 조합하는 수식의 결과로 예측 가능한 특성 값을 나타냅니다. 알고리즘은 숫자 값만 입력으로 받으며 가장 적합한 입력을 자동으로 검색합니다.  
  
 그러나 FORCE_REGRESSOR 매개 변수를 모델에 추가하고 사용할 회귀 변수를 지정하여 열을 회귀 변수로 포함하도록 지정할 수 있습니다. 효과가 너무 작아 모델에서 검색할 수 없어도 특성이 의미를 가지는 경우 또는 특성을 수식에 포함해야 할 경우 이 작업을 원할 수 있습니다.  
  
 다음 절차에서는 [신경망 자습서](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)에 사용된 것과 동일한 예제 데이터를 사용하여 간단한 선형 회귀 모델을 만드는 방법을 설명합니다. 모델은 견고할 필요는 없지만 데이터 마이닝 디자이너를 사용하여 선형 회귀 모델을 사용자 지정하는 방법을 보여 줍니다.  
  
### <a name="how-to-create-a-simple-linear-regression-model"></a>단순 선형 회귀 모델을 만드는 방법  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **솔루션 탐색기**에서 **마이닝 구조**를 확장합니다.  
  
2.  Call Center.dmm을 두 번 클릭하여 디자이너에서 엽니다.  
  
3.  **마이닝 모델** 메뉴에서 **새 마이닝 모델**을 선택합니다.  
  
4.  알고리즘에 대해 **Microsoft 선형 회귀**를 선택합니다. 이름에 대해 **Call Center Regression**을 입력합니다.  
  
5.  **마이닝 모델** 탭에서 열 사용법을 다음과 같이 변경합니다. 다음 목록에 없는 열은 모두 **Ignore**로 설정(이미 설정되어 있지 않은 경우)해야 합니다.  
  
     FactCallCenterID**Key**  
  
     ServiceGrade**PredictOnly**  
  
     Total Operators**Input**  
  
     AverageTimePerIssue**Input**  
  
6.  **마이닝 모델** 메뉴에서 **모델 매개 변수 설정**을 선택합니다.  
  
7.  매개 변수 FORCE_REGRESSOR의 경우 **값** 열에서 다음과 같이 괄호로 묶고 쉼표로 구분한 열 이름을 입력합니다.  
  
    ```  
    [Average Time Per Issue],[Total Operators]  
    ```  
  
    > [!NOTE]  
    >  알고리즘이 자동으로 최상의 회귀 변수인 열을 검색합니다. 열을 최종 수식에 포함하려는 경우 회귀 변수를 적용하기만 하면 됩니다.  
  
8.  **마이닝 모델** 메뉴에서 **모델 처리**를 선택합니다.  
  
     뷰어에서 모델은 회귀 수식을 포함하는 단일 노드로 나타납니다. **마이닝 범례**에서 수식을 보거나 쿼리를 사용하여 수식에 대한 계수를 추출할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft 선형 회귀 알고리즘](microsoft-linear-regression-algorithm.md)   
 [데이터 마이닝 쿼리](data-mining-queries.md)   
 [Microsoft 선형 회귀 알고리즘 기술 참조](microsoft-linear-regression-algorithm-technical-reference.md)   
 [선형 회귀 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
