---
title: "보기 또는 변경 알고리즘 매개 변수 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- algorithms [data mining]
- mining models [Analysis Services], algorithms
ms.assetid: 151b899b-c27a-4a09-bcf5-5c9f0ec24168
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5bd20ff4beddb94831f634304f1a9628f21025a3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="view-or-change-algorithm-parameters"></a>알고리즘 매개 변수 확인 또는 변경
  데이터 마이닝 모델을 작성하여 모델 결과를 사용자 지정하는 데 사용하는 알고리즘과 함께 제공되는 매개 변수를 변경할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 알고리즘 매개 변수는 모델에 대한 속성보다 훨씬 더 많으며, 이 매개 변수는 데이터의 처리, 그룹화 및 표시 방법을 근본적으로 변경하는 데 사용할 수 있습니다. 예를 들어 알고리즘 매개 변수를 사용하여 다음을 수행할 수 있습니다.  
  
-   클러스터링 메서드와 같은 분석 방법을 변경합니다.  
  
-   기능 선택 동작을 제어합니다.  
  
-   항목 집합 크기 또는 규칙 확률을 지정합니다.  
  
-   의사 결정 트리의 분기와 깊이를 제어합니다.  
  
-   모델 생성에 사용되는 내부 홀드아웃 집합의 크기 또는 초기값을 지정합니다.  
  
 각 알고리즘마다 제공되는 매개 변수는 크게 다릅니다. 각 알고리즘에 대해 설정할 수 있는 매개 변수 목록은 이 섹션의 기술 참조 항목 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)을 참조하세요.  
  
### <a name="change-an-algorithm-parameter"></a>알고리즘 매개 변수 변경  
  
1.  **의 데이터 마이닝 디자이너에 있는** 마이닝 모델 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭에서 알고리즘을 조정할 마이닝 모델의 알고리즘 유형을 마우스 오른쪽 단추로 클릭하고 **알고리즘 매개 변수 설정**을 선택합니다.  
  
     **알고리즘 매개 변수** 대화 상자가 열립니다.  
  
2.  **값** 열에서 변경할 알고리즘의 새 값을 설정합니다.  
  
     **값** 열에 값을 입력하지 않으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 기본 매개 변수 값이 사용됩니다. **범위** 열에서 입력할 수 있는 값을 확인할 수 있습니다.  
  
3.  **확인**을 클릭합니다.  
  
     알고리즘 매개 변수가 새 값으로 설정됩니다. 모델을 다시 처리해야 매개 변수 변경 내용이 마이닝 모델에 적용됩니다.  
  
### <a name="view-the-parameters-used-in-an-existing-model"></a>기존 모델에 사용되는 매개 변수 보기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 DMX 쿼리 창을 엽니다.  
  
2.  다음과 같은 쿼리를 입력합니다.  
  
    ```  
    select MINING_PARAMETERS   
    from $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = '<model name>'  
  
    ```  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 태스크 및 방법](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
