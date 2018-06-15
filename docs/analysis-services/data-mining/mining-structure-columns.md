---
title: 마이닝 구조 열 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1cbdcd14127cdf45eb35dd7a24652be4f7c4d613
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34015160"
---
# <a name="mining-structure-columns"></a>마이닝 구조 열
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  마이닝 구조를 만들 때 외부 데이터 열을 선택한 다음 데이터가 모델링에 사용되는 방법을 지정하여 마이닝 구조의 열을 정의합니다. 따라서 마이닝 구조 열이 데이터 원본의 데이터 복사본보다 많으며 마이닝 구조 열에 따라 원본 데이터가 마이닝 모델에 사용되는 방법이 정의됩니다. 데이터를 분할하는 방법을 결정하는 속성과 데이터 값을 분산하는 방법을 설명하는 속성을 할당할 수 있습니다.  
  
 마이닝 모델 작성 시 사용하는 각 알고리즘이 구조의 여러 열을 사용하여 데이터를 해석할 수 있기 때문에 마이닝 구조 열은 유연성이 있고 확장 가능합니다. 각 모델에 대해 하나의 데이터 집합을 포함하는 대신 단일 마이닝 구조를 사용하고 해당 구조의 열을 사용하여 데이터를 각 모델에 맞게 사용자 지정할 수 있습니다.  
  
## <a name="defining-mining-structure-columns"></a>마이닝 구조 열 정의  
 구조 열을 정의하는 기본 데이터 형식과 내용 유형은 구조 생성 시 사용하는 데이터 원본에서 파생됩니다. 마이닝 구조 내에서 이러한 설정을 변경할 수 있으며 연속 열에 대해 분포를 설정하고 모델링 플래그를 설정할 수도 있습니다.  
  
 마이닝 구조 열의 정의에는 다음 정보가 포함되어야 합니다.  
  
-   **ID**: 열의 고유 이름이며 이름과 동일한 경우가 많습니다. 마이닝 구조를 만든 후 이름은 변경할 수 있지만 ID는 변경할 수 없습니다.  
  
-   **이름**: 열의 이름 또는 별칭입니다.  
  
-   **콘텐츠**: 데이터가 불연속형인지 연속형인지 여부를 설명하는 열거형입니다.  
  
-   **형식**: 일반 데이터 형식을 나타내는 열거형입니다.  
  
-   **분포**: 예상 분포 값을 설명하는 열거형입니다. 열이 연속인 경우 분포가 포함됩니다.  
  
-   **모델링 플래그**: 누락 값 등을 처리하는 방법을 나타내는 열거형입니다. 마이닝 모델에 대해 모델링 플래그를 정의할 수도 있지만 모델 플래그는 구조 열에 사용되는 플래그와 다릅니다.  
  
-   **바인딩**: 원본 데이터를 지정하는 속성입니다.  
  
 타사 알고리즘은 마이닝 구조 열에 대해 정의할 수 있는 사용자 지정 속성을 포함할 수도 있습니다.  
  
 데이터 마이닝 구조와 데이터 마이닝 모델에 대한 자세한 내용은 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 마이닝 구조 열을 정의하고 사용하는 방법은 다음 항목을 참조하십시오.  
  
|항목|링크|  
|-----------|-----------|  
|마이닝 구조 열을 정의하는 데 사용할 수 있는 데이터 형식에 대해 설명합니다.|[데이터 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/data-types-data-mining.md)|  
|마이닝 구조 열에 포함되어 있는 각 데이터 형식에 사용할 수 있는 내용 유형에 대해 설명합니다. 내용 유형은 데이터 형식에 따라 달라집니다. 내용 유형은 모델 수준에서 할당되며 모델에 열 데이터가 사용되는 방법을 결정합니다.|[콘텐츠 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/content-types-data-mining.md)|  
|중첩 테이블의 개념을 도입하고, 중첩 테이블을 데이터 원본에 마이닝 구조 열로 추가하는 방법에 대해 설명합니다.|[분류된 열&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/classified-columns-data-mining.md)|  
|열의 예상 분포 값을 지정하기 위해 마이닝 구조 열에 대해 설정할 수 있는 분포 속성을 나열하고 설명합니다.|[열 배포&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md)|  
|*범주화*라고도 하는 불연속화의 개념을 설명하고 Analysis Services에서 연속 숫자 데이터 불연속화를 위해 제공하는 메서드에 대해 설명합니다.|[분할 메서드&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/discretization-methods-data-mining.md)|  
|마이닝 구조 열에 대해 설정할 수 있는 모델링 플래그에 대해 설명합니다.|[모델링 플래그&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)|  
|한 마이닝 구조 열을 다른 마이닝 구조 열과 연결하는 데 사용할 수 있는 특수한 유형의 열인 분류된 열에 대해 설명합니다.|[분류된 열&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/classified-columns-data-mining.md)|  
|마이닝 구조 열을 추가하고 수정하는 방법에 대해 알아봅니다.|[마이닝 구조 태스크 및 방법](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 구조 & #40; Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [마이닝 모델 열](../../analysis-services/data-mining/mining-model-columns.md)  
  
  
