---
title: 테스트 집합 만들기 (데이터 마이닝 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.holdout.f1
ms.assetid: d0a44b59-ffbd-45fc-baa8-6b8046b1a2f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f0e4d1a384995c0c49c346102f8fddbcdf47f68
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086785"
---
# <a name="create-testing-set-data-mining-wizard"></a>테스트 집합 만들기(데이터 마이닝 마법사)
  
  **테스트 집합 만들기** 페이지를 사용하여 학습에 사용할 데이터 양과 테스트 집합으로 사용하기 위해 예약할 양을 지정할 수 있습니다. 마이닝 구조를 만들 때 학습 집합과 테스트 집합으로 데이터를 분리하면 나중에 만드는 마이닝 모델의 정확도를 보다 편리하게 평가할 수 있습니다.  
  
 테스트 데이터 양을 비율로 지정하거나 테스트에 사용되는 사례 수를 제한하는 수를 지정할 수 있습니다. 테스트에 사용할 사례의 최대 수와 비율을 모두 지정하면 두 설정이 모두 사용되어 테스트 데이터 집합에 적은 수의 사례가 포함됩니다. 기본적으로 데이터의 30%는 테스트에 사용되고 70%는 학습에 사용되며 테스트 사례의 최대 수는 없습니다.  
  
 기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 분할을 시작할 때 사용되는 숫자 시드를 생성합니다. 이 시드는 마이닝 구조의 이름을 기반으로 합니다. 마이닝 구조의 이름이 변경된 후에도 파티션을 동일하게 유지하려면 마이닝 구조의 HoldoutSeed 속성을 설정하여 시드의 값을 지정하면 됩니다. 홀드아웃 시드를 변경하면 구조를 다시 처리해야 합니다.  
  
 나중에 테스트 또는 학습 데이터의 양을 변경 하려면 **속성** 창을 사용 하 여 데이터 마이닝 구조 `HoldoutMaxCases` 에서 `HoldoutMaxPercent` 및 속성을 수정할 수 있습니다. 그러나 변경 후에는 마이닝 구조 및 연결된 모든 마이닝 모델을 다시 처리해야 합니다. 또한 다음과 같은 제한 사항이 적용됩니다.  
  
-   데이터 마이닝 구조의 분할은 데이터 마이닝 구조가 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에 저장된 경우에만 지원됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 마이닝 구조에 대 한 파티션 정보의 캐싱을 지원 하지 않습니다.  
  
-   마이닝 구조에 시계열 마이닝 모델에 필요한 Key Time 열이 포함된 경우 마이닝 구조를 분할할 수 없습니다.  
  
-   중첩 테이블에 저장되는 값을 예측하려는 경우 데이터를 분할할 수 없습니다.  
  
 **자세한 내용:** [데이터 마이닝&#41;&#40;테스트 및 유효성 검사 ](data-mining/testing-and-validation-data-mining.md), [관계형 마이닝 구조 만들기](data-mining/create-a-relational-mining-structure.md), [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
## <a name="options"></a>옵션  
 **테스트용 데이터 비율**  
 위쪽/아래쪽 화살표를 클릭하여 학습 집합으로 사용할 데이터 비율을 늘이거나 줄입니다. 또는 입력란에 0에서 100 사이의 값을 입력합니다.  
  
 **테스트 데이터 집합의 최대 사례 수**  
 테스트에 사용할 수 있는 사례 수를 제한하려면 원하는 수를 입력합니다.  
  
 데이터의 실제 사례 수보다 더 큰 수를 지정하면 모든 사례가 사용됩니다.  
  
 기본값은 NULL입니다. 이 값은 제한이 없음을 의미합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 마법사 F1 도움말 &#40;Analysis Services 데이터 마이닝&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [데이터 마이닝 마법사 &#40;관련 열 제안&#41;](suggest-related-columns-data-mining-wizard.md)   
 [데이터 마이닝 마법사 &#40;테이블 형식을 지정&#41;](specify-table-types-data-mining-wizard.md)   
 [열 내용 및 데이터 형식 &#40;데이터 마이닝 마법사를 지정&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
