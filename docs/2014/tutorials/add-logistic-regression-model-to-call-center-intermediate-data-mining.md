---
title: 콜 센터 구조에 로지스틱 회귀 모델 추가 (중급 데이터 마이닝 자습서) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62823280"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>콜 센터 구조에 로지스틱 회귀 모델 추가(중급 데이터 마이닝 자습서)
  콜 센터 운영에 영향을 줄 수 있는 요인을 분석하는 것 외에 직원이 서비스 품질을 향상시킬 수 있는 방법에 대한 일부 특정 권장 사항을 제공할 것도 요청받았습니다. 이 작업에서는 탐색 모델을 작성하는 데 사용한 마이닝 구조를 그대로 사용하고 예측을 만드는 데 사용될 마이닝 모델을 추가합니다.  
  
 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 로지스틱 회귀 모델은 신경망 알고리즘을 기반으로 하므로 신경망 모델과 동일한 유연성과 강력한 기능을 제공합니다. 그러나 로지스틱 회귀는 이진 결과 예측에 특히 적합합니다.  
  
 이 시나리오에서는 신경망 모델에 사용한 것과 같은 마이닝 구조를 사용합니다. 다만 해당 비즈니스 질문에 맞게 새 모델을 사용자 지정합니다. 서비스 품질을 향상시키고 필요한 경력 전화 상담원 수를 결정하는 데 관심이 있으므로 그러한 값을 예측하도록 모델을 설정합니다.  
  
 콜 센터 데이터를 기반으로 한 전체 모델이 가능한 한 유사하도록 하려면 이전과 동일한 초기값을 사용합니다. 초기값 매개 변수를 설정하면 모델이 동일한 시작점에서 데이터를 처리하고 데이터의 아티팩트로 인해 발생한 변형을 최소화합니다.  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>콜 센터 마이닝 구조에 새 마이닝 모델을 추가하려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]솔루션 탐색기에서 마이닝 구조를 마우스 오른쪽 단추로 클릭 하 고 **호출 센터**를 클릭 한 다음 **디자이너 열기**를 선택 합니다.  
  
2.  데이터 마이닝 디자이너에서 **마이닝 모델** 탭을 클릭 합니다.  
  
3.  **관련 마이닝 모델 만들기를**클릭 합니다.  
  
4.  **새 마이닝 모델** 대화 상자의 **모델 이름**에을 입력 `Call Center - LR`합니다.  **알고리즘 이름**에 대해 **Microsoft 로지스틱 회귀**를 선택 합니다.  
  
5.  **확인**을 클릭합니다.  
  
     **마이닝** 모델 탭에 새 마이닝 모델이 표시 됩니다.  
  
### <a name="to-customize-the-logistic-regression-model"></a>로지스틱 회귀 모델을 사용자 지정하려면  
  
1.  새 마이닝 모델 `Call Center - LR`의 열에서 팩트 CALLCENTER ID를 키로 유지 합니다.  
  
2.  ServiceGrade 및 Level 2 연산자의 값을 **예측**으로 변경 합니다.  
  
     이러한 열은 입력 및 예측에 모두 사용됩니다. 기본적으로 동일한 데이터에서 두 개의 모델을 만듭니다. 하나는 연산자 수를 예측 하 고 다른 하나는 서비스 등급을 예측 합니다.  
  
3.  다른 모든 열을 **입력**으로 변경 합니다.  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>초기값을 지정하고 모델을 처리하려면  
  
1.  **마이닝 모델** 탭에서 Call CENTER-LR 이라는 모델의 열을 마우스 오른쪽 단추로 클릭 하 고 **알고리즘 매개 변수 설정**을 선택 합니다.  
  
2.  HOLDOUT_SEED 매개 변수에 대 한 행에서 **값**아래에 있는 빈 셀을 클릭 하 고 `1`을 입력 합니다. **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  모든 관련 모델에 대해 동일한 초기값을 사용하는 경우에는 초기값으로 선택한 값이 중요하지 않습니다.  
  
3.  **마이닝 모델** 메뉴에서 **마이닝 구조 및 모든 모델 처리**를 선택 합니다. 업데이트 된 데이터 마이닝 프로젝트를 서버에 배포 하려면 **예** 를 클릭 합니다.  
  
4.  **마이닝 모델 처리** 대화 상자에서 **실행**을 클릭 합니다.  
  
5.  **닫기** 를 클릭 하 여 **처리 진행률** 대화 상자를 닫은 다음 **마이닝 모델 처리** 대화 상자에서 **닫기** 를 다시 클릭 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [중급 데이터 마이닝 자습서 &#40;콜 센터 모델에 대 한 예측 만들기&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝&#41;&#40;처리 요구 사항 및 고려 사항](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
