---
title: 콜 센터 구조 (중급 데이터 마이닝 자습서)에 로지스틱 회귀 모델 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 32e66a84dea20964c11c7de0aa568530aa8c28c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823280"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>콜 센터 구조에 로지스틱 회귀 모델 추가(중급 데이터 마이닝 자습서)
  콜 센터 운영에 영향을 줄 수 있는 요인을 분석하는 것 외에 직원이 서비스 품질을 향상시킬 수 있는 방법에 대한 일부 특정 권장 사항을 제공할 것도 요청받았습니다. 이 작업에서는 탐색 모델을 작성하는 데 사용한 마이닝 구조를 그대로 사용하고 예측을 만드는 데 사용될 마이닝 모델을 추가합니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 로지스틱 회귀 모델은 신경망 알고리즘을 기반으로 하므로 신경망 모델과 동일한 유연성과 강력한 기능을 제공합니다. 그러나 로지스틱 회귀는 이진 결과 예측에 특히 적합합니다.  
  
 이 시나리오에서는 신경망 모델에 사용한 것과 같은 마이닝 구조를 사용합니다. 다만 해당 비즈니스 질문에 맞게 새 모델을 사용자 지정합니다. 서비스 품질을 향상시키고 필요한 경력 전화 상담원 수를 결정하는 데 관심이 있으므로 그러한 값을 예측하도록 모델을 설정합니다.  
  
 콜 센터 데이터를 기반으로 한 전체 모델이 가능한 한 유사하도록 하려면 이전과 동일한 초기값을 사용합니다. 초기값 매개 변수를 설정하면 모델이 동일한 시작점에서 데이터를 처리하고 데이터의 아티팩트로 인해 발생한 변형을 최소화합니다.  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>콜 센터 마이닝 구조에 새 마이닝 모델을 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], 솔루션 탐색기에서 마이닝 구조를 마우스 오른쪽 단추로 클릭 **Call Center Binned**를 선택 하 고 **디자이너 열기**합니다.  
  
2.  데이터 마이닝 디자이너에서을 클릭 합니다 **마이닝 모델** 탭 합니다.  
  
3.  클릭 **관련된 마이닝 모델을 만드는**합니다.  
  
4.  에 **새 마이닝 모델** 대화 상자에 대 한 **모델 이름**, 형식 `Call Center - LR`합니다.  에 대 한 **알고리즘 이름**를 선택 **Microsoft 로지스틱 회귀**합니다.  
  
5.  **확인**을 클릭합니다.  
  
     새 마이닝 모델에 표시 되는 **마이닝 모델** 탭 합니다.  
  
### <a name="to-customize-the-logistic-regression-model"></a>로지스틱 회귀 모델을 사용자 지정하려면  
  
1.  새 마이닝 모델 열에서 `Call Center - LR`에서 Fact CallCenter ID 키로 그대로 둡니다.  
  
2.  ServiceGrade 및 Level Two Operators에 값을 변경 **Predict**합니다.  
  
     이러한 열은 입력 및 예측에 모두 사용됩니다. 기본적으로 모델을 만드는 두 가지 별도 동일한 데이터에서: 연산자의 수를 예측 하는 하나 및 서비스 등급을 예측 하는 것입니다.  
  
3.  다른 모든 열을 변경 **입력**합니다.  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>초기값을 지정하고 모델을 처리하려면  
  
1.  에 **마이닝 모델** 탭, 명명 된 Call Center-LR을 모델에 대 한 열을 마우스 오른쪽 단추로 **알고리즘 매개 변수 설정**합니다.  
  
2.  HOLDOUT_SEED 매개 변수의 행에서 아래의 빈 셀을 클릭 **값**, 및 형식 `1`합니다. **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  모든 관련 모델에 대해 동일한 초기값을 사용하는 경우에는 초기값으로 선택한 값이 중요하지 않습니다.  
  
3.  에 **마이닝 모델** 메뉴에서 **마이닝 구조 및 모든 모델 처리**합니다. 클릭 **예** 서버에 업데이트 된 데이터 마이닝 프로젝트를 배포 합니다.  
  
4.  에 **마이닝 모델 처리** 대화 상자, 클릭 **실행**합니다.  
  
5.  클릭 **닫습니다** 를 닫습니다 합니다 **처리 진행률** 대화 상자에서을 클릭 한 다음 **닫습니다** 다시 합니다 **마이닝 모델 처리** 대화 상자.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [콜 센터 모델에 대 한 예측을 만드는 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [처리 요구 사항 및 고려 사항 & #40; 데이터 마이닝 & #41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
