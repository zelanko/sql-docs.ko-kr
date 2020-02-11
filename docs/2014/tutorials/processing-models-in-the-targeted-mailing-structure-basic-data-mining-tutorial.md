---
title: 대상 메일 구조에서 모델 처리 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9d8233bb-117e-4563-9302-8a5a8ad1fae2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 605088d405cbd2dcfba92a2da5fa4e07c38d8f0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63188228"
---
# <a name="processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>대상 메일 구조에서 모델 처리(기본 데이터 마이닝 자습서)
  만든 마이닝 모델을 찾아보거나 사용하기 전에 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 배포하고 마이닝 구조 및 마이닝 모델을 처리해야 합니다.  
  
-   *배포* 하는 경우 프로젝트를 서버에 보내고 서버에 있는 해당 프로젝트에 개체를 만듭니다.  
  
-   *처리* 는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 관계형 데이터 원본의 데이터로 개체를 채웁니다.  
  
 모델은 배포 및 처리될 때까지 사용할 수 없습니다. 또한 새 데이터를 추가 하는 등 모델을 변경 하는 경우에는 모델을 다시 배포 하 고 다시 처리 해야 합니다.  
  
## <a name="ensuring-consistency-with-holdoutseed"></a>HoldoutSeed와의 일관성 확인  
 프로젝트를 배포 하 고 구조 및 모델을 처리 하는 경우 데이터 구조의 개별 행은 숫자 시드 값을 기반으로 학습 집합 또는 테스트 집합에 할당 됩니다. 기본적으로 숫자 초기값은 데이터 구조의 특성을 기반으로 계산 됩니다. 그러나 모델의 일부 측면을 변경 하는 경우 초기값이 변경 되어 약간 다른 결과를 초래 합니다. 따라서 결과가 여기에 설명 된 것과 동일 하도록 하기 위해의 `12`고정 *홀드 아웃 초기값* 을 임의로 할당 합니다. 홀드 아웃 초기값은 샘플링 알고리즘을 초기화 하는 데 사용 되 고 데이터는 모든 마이닝 구조 및 해당 모델에 대해 거의 동일한 방식으로 분할 됩니다.  
  
 이 값은 학습 집합의 사례 수에 영향을 주지 않습니다. 모델을 빌드할 때마다 동일한 분할 방법이 사용 되도록 합니다.  
  
 홀드 아웃 초기값에 대 한 자세한 내용은 [데이터 집합 학습 및 테스트](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md)를 참조 하세요.  
  
#### <a name="to-set-the-holdout-seed"></a>홀드아웃 초기값을 설정하려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]데이터 마이닝 디자이너에서 마이닝 **구조** 탭 이나 **마이닝 모델** 탭을 클릭 합니다.  
  
     **타겟 메일링 MiningStructure** 는 **속성** 창에 표시 됩니다.  
  
2.  **F4**키를 눌러 **속성** 창이 열려 있는지 확인 합니다.  
  
3.  **Cachemode** 가 **KeepTrainingCases**으로 설정 되어 있는지 확인 합니다.  
  
4.  HoldoutSeed `12` 에 **** 대해을 입력 합니다.  
  
## <a name="deploying-and-processing-the-models"></a>모델 배포 및 처리  
 데이터 마이닝 디자이너에서 모델에 대 한 변경 내용 또는 기본 데이터의 범위에 따라 처리할 개체를 결정할 수 있습니다.  
  
 이 태스크의 경우 데이터 및 모델이 새로운 것 이므로 구조와 모든 모델을 동시에 처리 합니다.  
  
#### <a name="to-deploy-the-project-and-process-all-the-mining-models"></a>프로젝트를 배포하고 모든 마이닝 모델을 처리하려면  
  
1.  **마이닝 모델** 메뉴에서 **마이닝 구조 및 모든 모델 처리**를 선택 합니다.  
  
     마이닝 구조를 변경한 경우 모델을 처리하기 전에 프로젝트를 빌드하고 배포할지 묻는 메시지가 표시됩니다. **예**를 클릭합니다.  
  
2.  **마이닝 구조 처리-대상 메일링** 대화 상자에서 **실행** 을 클릭 합니다.  
  
     
  **처리 진행률** 대화 상자가 열리고 모델 처리 세부 정보를 표시합니다. 컴퓨터에 따라 모델 처리에 시간이 걸릴 수 있습니다.  
  
3.  모델 처리가 완료되면 **처리 진행률** 대화 상자에서 **닫기** 를 클릭합니다.  
  
4.  **마이닝 구조 처리- \<구조>** 대화 상자에서 **닫기** 를 클릭 합니다.  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [&#40;기본 데이터 마이닝 자습서를 대상으로 지정 된 메일링 구조에 새 모델 추가&#41;](../../2014/tutorials/adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>다음 단원  
 [4 단원: 기본 데이터 마이닝 자습서 &#40;대상 메일링 모델 탐색&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝&#41;&#40;처리 요구 사항 및 고려 사항](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
