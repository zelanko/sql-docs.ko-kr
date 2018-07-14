---
title: 타겟된 메일링 구조 (기본 데이터 마이닝 자습서)에서 모델 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9d8233bb-117e-4563-9302-8a5a8ad1fae2
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0682dc2cc2415e1f545b225206a4ecf10c250810
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274379"
---
# <a name="processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>대상 메일 구조에서 모델 처리(기본 데이터 마이닝 자습서)
  만든 마이닝 모델을 찾아보거나 사용하기 전에 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 배포하고 마이닝 구조 및 마이닝 모델을 처리해야 합니다.  
  
-   *배포* 서버로 전달 하 고 서버에서 해당 프로젝트의 모든 개체를 만듭니다.  
  
-   *처리* 채웁니다 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 관계형 데이터 원본에서 데이터를 사용 하 여 개체입니다.  
  
 모델은 배포 및 처리될 때까지 사용할 수 없습니다. 또한 모델에 새 데이터를 추가 하는 등 변경 하는 경우 다시 배포 하 고 모델을 다시 처리 해야 있습니다.  
  
## <a name="ensuring-consistency-with-holdoutseed"></a>HoldoutSeed와의 일관성 확인  
 프로젝트를 배포 하 고 구조 및 모델을 처리할 때 데이터 구조의 개별 행 집합 또는 테스트 집합을 숫자 시드 값을 기반으로 학습에 할당 됩니다. 기본적으로 숫자 초기값 데이터 구조의 특성을 기반으로 계산 됩니다. 그러나 모델의 일부 측면을 변경 하거나 초기값 약간 다른 결과를 선행 변경 됩니다. 따라서 결과 여기에 설명 된 대로 동일 위해서는 임의로 할당 고정 *홀드 아웃 초기값* 의 `12`합니다. 홀드 아웃 초기값을 샘플링 알고리즘을 초기화 하는 데 사용 됩니다 하 고 데이터와 거의 동일한 방식으로 모든 마이닝 구조 및 해당 모델에서 분할 되는 확인 합니다.  
  
 이 값은 학습 집합의 사례 수 영향을 주지 않습니다. 동일한 분할 메서드는 모델을 빌드할 때마다를 사용할 수는 단순히 확인 합니다.  
  
 홀드 아웃 초기값에 대 한 자세한 내용은 참조 하세요. [학습 및 테스트 데이터 집합](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md)합니다.  
  
#### <a name="to-set-the-holdout-seed"></a>홀드아웃 초기값을 설정하려면  
  
1.  클릭 합니다 **Mining Structure** 탭 또는 **마이닝 모델** 탭의 데이터 마이닝 디자이너에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]합니다.  
  
     **Targeted Mailing MiningStructure** 에 표시 합니다 **속성** 창입니다.  
  
2.  있는지 확인 합니다 **속성** 키를 눌러 창이 열려 **F4**합니다.  
  
3.  했는지 **CacheMode** 로 설정 된 **KeepTrainingCases**합니다.  
  
4.  입력 `12` 에 대 한 **HoldoutSeed**합니다.  
  
## <a name="deploying-and-processing-the-models"></a>모델 배포 및 처리  
 데이터 마이닝 디자이너에서 개체 모델 또는 기본 데이터에 대 한 변경의 범위에 따라 처리를 결정할 수 있습니다.  
  
 이 태스크에 대 한 데이터와 모델은 새 이므로 처리할 구조 및 모델이 모두 동시에 합니다.  
  
#### <a name="to-deploy-the-project-and-process-all-the-mining-models"></a>프로젝트를 배포하고 모든 마이닝 모델을 처리하려면  
  
1.  에 **마이닝 모델** 메뉴에서 **마이닝 구조 및 모든 모델 처리**합니다.  
  
     마이닝 구조를 변경한 경우 모델을 처리하기 전에 프로젝트를 빌드하고 배포할지 묻는 메시지가 표시됩니다. **예**를 클릭합니다.  
  
2.  클릭 **실행할** 에 **마이닝 구조 처리-Targeted Mailing** 대화 상자.  
  
     **처리 진행률** 대화 상자가 열리고 모델 처리 세부 정보를 표시합니다. 컴퓨터에 따라 모델 처리에 시간이 걸릴 수 있습니다.  
  
3.  모델 처리가 완료되면 **처리 진행률** 대화 상자에서 **닫기** 를 클릭합니다.  
  
4.  클릭 **닫습니다** 에 **마이닝 구조 처리- \<구조 >** 대화 상자.  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [대상된 메일 구조에 새 모델 추가 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>다음 단원  
 [4 단원: 타겟된 메일링 모델 탐색 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [처리 요구 사항 및 고려 사항 &#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
