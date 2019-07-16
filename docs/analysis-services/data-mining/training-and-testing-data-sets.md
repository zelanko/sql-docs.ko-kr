---
title: 학습 및 테스트 데이터 집합 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 15ee82c04372528d29289a3ed6c5c55271acf5fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209598"
---
# <a name="training-and-testing-data-sets"></a>데이터 집합 학습 및 테스트
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  데이터를 학습 집합과 테스트 집합으로 분할하는 작업은 데이터 마이닝 모델 평가의 중요한 부분입니다. 데이터 집합을 학습 집합과 테스트 집합으로 분리할 경우 일반적으로 대부분의 데이터가 학습에 사용되고 나머지 데이터가 테스트에 사용되지만, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 테스트 및 학습 집합의 크기가 비슷하게 되도록 데이터를 무작위로 샘플링합니다. 학습 및 테스트에 유사한 데이터를 사용하면 데이터 불일치의 영향을 최소화하고 모델의 특징을 보다 잘 이해할 수 있습니다.  
  
 학습 집합을 사용하여 모델을 처리한 후에는 테스트 집합에 대한 예측을 만들어 모델을 테스트합니다. 테스트 집합의 데이터에는 예측할 특성의 알려진 값이 이미 포함되어 있으므로 모델의 예측이 올바른지 여부를 쉽게 확인할 수 있습니다.  
  
## <a name="creating-test-and-training-sets-for-data-mining-structures"></a>데이터 마이닝 구조에 대한 테스트 및 학습 집합 만들기  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 마이닝 구조의 수준에서 원래 데이터 집합을 분할합니다. 학습 및 테스트 데이터 집합의 크기와 각 집합에 포함되는 행에 대한 정보가 구조와 함께 저장되며, 이 구조를 기반으로 하는 모든 모델이 학습 및 테스트에 해당 집합을 사용할 수 있습니다.  
  
 다음과 같은 방법으로 마이닝 구조에 테스트 데이터 집합을 정의할 수 있습니다.  
  
-   마이닝 구조를 만들 때 데이터 마이닝 마법사를 사용하여 마이닝 구조를 분할합니다.  
  
-   데이터 마이닝 디자이너의 **마이닝 구조** 탭에서 구조 속성을 수정합니다.  
  
-   AMO(Analysis Management Objects) 또는 XML DDL(데이터 정의 언어)을 사용하여 프로그래밍 방식으로 구조를 생성하고 수정합니다.  
  
### <a name="using-the-data-mining-wizard-to-divide-a-mining-structure"></a>데이터 마이닝 마법사를 사용하여 마이닝 구조 분할  
 기본적으로 사용자가 마이닝 구조의 데이터 원본을 정의하면 데이터 마이닝 마법사에서 데이터를 두 가지 집합으로 분할합니다. 원본 데이터의 70%는 모델 학습을 위한 집합에, 나머지 30%는 모델 테스트를 위한 집합에 할당합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 데이터 마이닝에서 일반적으로 사용되는 이 70:30의 기본 비율 대신, 사용자의 필요에 따라 다른 비율로 변경할 수 있습니다.  
  
 마법사를 구성하여 최대 학습 사례 수를 설정하거나 여러 제한을 조합하여 지정한 최대 사례 수까지 최대 사례 비율을 허용할 수도 있습니다. 최대 사례 비율과 최대 사례 수를 모두 지정하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 두 제한 중 보다 작은 값을 테스트 집합의 크기로 사용합니다. 예를 들어 테스트 사례에 대해 30%의 홀드아웃을 지정하고 최대 테스트 사례 수를 1000으로 지정하는 경우 테스트 집합의 크기는 1000개의 사례를 초과하지 않습니다. 이는 보다 많은 학습 데이터가 모델에 추가되더라도 테스트 집합의 크기를 일관되게 유지하려는 경우 유용할 수 있습니다.  
  
 다른 마이닝 구조에 대해 같은 데이터 원본 뷰를 사용하고 데이터가 모든 마이닝 구조 및 해당 모델에 대해 대략 같은 방식으로 분할되도록 하려면 무작위 샘플링을 초기화하는 데 사용되는 초기값을 지정해야 합니다. **HoldoutSeed**의 값을 지정하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 해당 값을 사용하여 샘플링을 시작합니다. 그렇지 않으면 샘플링은 마이닝 구조의 이름에 해시 알고리즘을 사용하여 초기값을 만듭니다.  
  
> [!NOTE]  
>  **EXPORT** 및 **IMPORT** 문을 사용하여 마이닝 구조의 복사본을 만들면 내보내기 프로세스에서 새 ID를 만들지만 같은 이름을 사용하므로 새 마이닝 구조가 같은 학습 및 테스트 데이터 집합을 갖게 됩니다. 그러나 두 마이닝 구조가 같은 기본 데이터 원본을 사용하지만 이름이 다를 경우에는 각 마이닝 구조에 대해 생성되는 집합이 달라집니다.  
  
### <a name="modifying-structure-properties-to-create-a-test-data-set"></a>테스트 데이터 집합을 만들기 위한 구조 속성 수정  
 마이닝 구조를 만들고 처리한 다음 나중에 테스트 데이터 집합을 새로 만들려는 경우 마이닝 구조의 속성을 수정할 수 있습니다. 데이터가 분할되는 방식을 변경하려면 다음 속성을 편집합니다.  
  
|속성|설명|  
|--------------|-----------------|  
|**HoldoutMaxCases**|테스트 집합에 포함할 최대 사례 수를 지정합니다.|  
|**HoldoutMaxPercent**|테스트 집합에 포함할 사례 수를 전체 데이터 집합의 비율로 지정합니다. 데이터 집합을 갖지 않으려면 0을 지정합니다.|  
|**HoldoutSeed**|파티션에 대한 데이터를 무작위로 선택할 때 초기값으로 사용할 정수 값을 지정합니다. 이 값은 학습 집합의 사례 수에 영향을 주는 대신 파티션이 반복될 수 있도록 합니다.|  
  
 테스트 데이터 집합을 기존 구조에 추가하거나 변경하는 경우 구조 및 모든 관련 모델을 다시 처리해야 합니다. 또한 원본 데이터를 분할하면 데이터의 다른 하위 집합에서 모델이 학습되므로 모델의 다른 결과를 확인할 수 있습니다.  
  
### <a name="specifying-holdout-programmatically"></a>프로그래밍 방식으로 홀드아웃 지정  
 DMX 문, AMO 또는 XML DDL을 사용하여 마이닝 구조에서 테스트 및 학습 데이터 집합을 정의할 수 있습니다. ALTER MINING STRUCTURE 문은 홀드아웃 매개 변수의 사용을 지원하지 않습니다.  
  
-   **DMX** DMX(Data Mining Extensions) 언어에서 CREATE MINING STRUCTURE 문은 WITH HOLDOUT 절을 포함하도록 확장되었습니다.  
  
-   **ASSL** ASSL( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language)을 사용하여 새 마이닝 구조를 만들거나 기존 마이닝 구조에 테스트 데이터 집합을 추가할 수 있습니다.  
  
-   **AMO** AMO를 사용하여 홀드아웃 데이터 집합을 보고 수정할 수도 있습니다.  
  
 데이터 마이닝 스키마 행 집합을 쿼리하여 기존 마이닝 구조의 홀드아웃 데이터 집합에 대한 정보를 볼 수 있습니다. 이렇게 하려면 DISCOVER ROWSET을 호출하거나 DMX 쿼리를 사용하면 됩니다.  
  
## <a name="retrieving-information-about-holdout-data"></a>홀드아웃 데이터에 대한 정보 검색  
 기본적으로 학습 및 테스트 데이터 집합에 대한 모든 정보는 기존 데이터를 사용하여 새 모델을 학습하고 테스트할 수 있도록 캐시됩니다. 또한 데이터의 하위 집합에서 모델을 평가할 수 있도록 사용자가 캐시된 홀드아웃 데이터에 적용할 필터를 정의할 수도 있습니다.  
  
 사례가 학습 및 테스트 데이터 집합으로 분할되는 방법은 사용자가 홀드아웃을 구성하는 방법과 사용자가 제공한 데이터에 따라 달라집니다. 학습 또는 테스트에 사용된 사례 수를 확인하거나 학습 및 테스트 집합에 포함된 사례에 대한 추가 세부 정보를 찾으려는 경우 DMX 쿼리를 만들어 모델 구조를 쿼리할 수 있습니다. 예를 들어 다음 쿼리는 모델의 학습 집합에 사용된 사례를 반환합니다.  
  
```  
SELECT * from <structure>.CASES WHERE IsTrainingCase()  
```  
  
 테스트 사례만 검색하고 테스트 사례를 마이닝 구조의 열 중 하나에서 추가로 필터링하려면 다음 구문을 사용합니다.  
  
```  
SELECT * from <structure>.CASES WHERE IsTestCase() AND <structure column name> = '<value>'  
```  
  
## <a name="limitations-on-the-use-of-holdout-data"></a>홀드아웃 데이터 사용의 제한 사항  
  
-   홀드아웃을 사용하려면 마이닝 구조의 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 속성을 기본값인 **KeepTrainingCases**로 설정해야 합니다. **CacheMode** 속성을 **ClearAfterProcessing**으로 변경한 다음 마이닝 구조를 다시 처리하면 파티션이 손실됩니다.  
  
-   시계열 모델에서는 데이터를 제거할 수 없으므로 원본 데이터를 학습 및 테스트 집합으로 분리할 수 없습니다. 마이닝 구조와 모델을 만들 때 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시계열 알고리즘을 사용하도록 선택하면 홀드아웃 데이터 집합을 만들 수 없습니다. 마이닝 구조의 사례 테이블 또는 중첩 테이블 수준에 KEY TIME 열이 포함되어 있어도 홀드아웃 데이터를 사용할 수 없습니다.  
  
-   실수로 테스트에 전체 데이터 집합이 사용되고 학습에는 데이터 집합이 전혀 사용되지 않도록 홀드아웃 데이터 집합을 구성할 수 있습니다. 그러나 이렇게 구성하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 오류가 발생하여 문제를 수정하도록 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 경고를 표시합니다.  
  
-   대부분의 사례에서 기본 홀드아웃 값인 30을 사용하면 학습 데이터와 테스트 데이터 간에 균형이 맞춰집니다. 충분한 학습을 제공하기 위해 데이터 집합이 얼마나 커야 하는지, 또는 과도한 적합화(overfitting)를 방지하기 위해 학습 집합이 얼마나 작아도 되는지를 결정할 수 있는 간단한 방법은 없습니다. 그러나 모델을 작성한 후에는 교차 유효성 검사를 사용하여 특정 모델과 관련된 데이터 집합을 평가할 수 있습니다.  
  
-   AMO 및 XML DDL에서는 앞의 표에 나열된 속성 외에 읽기 전용 속성인 **HoldoutActualSize**가 제공됩니다. 그러나 구조를 처리할 때까지 파티션의 실제 크기를 정확하게 확인할 수 없으므로 **HoldoutActualSize** 속성의 값을 검색하기 전에 모델이 처리되었는지 여부를 확인해야 합니다.  
  
## <a name="related-content"></a>관련 내용  
  
|항목|링크|  
|------------|-----------|  
|모델의 필터가 학습 및 테스트 데이터 집합과 상호 작용하는 방법에 대해 설명합니다.|[마이닝 모델에 대한 필터&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)|  
|학습 및 테스트 데이터를 사용하는 방법에 따라 교차 유효성 검사에 미치는 영향에 대해 설명합니다.|[교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|마이닝 구조에서 학습 및 테스트 집합을 사용하는 프로그래밍 인터페이스에 대한 정보를 제공합니다.|[AMO 개념 및 개체 모델](https://docs.microsoft.com/bi-reference/amo/amo-concepts-and-object-model)<br /><br /> [MiningStructure 요소&#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/objects/miningstructure-element-assl)|  
|홀드아웃 집합을 만들기 위한 DMX 구문을 제공합니다.|[CREATE MINING STRUCTURE&#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md)|  
|학습 및 테스트 집합에서 사례에 대한 정보를 검색합니다.|[데이터 마이닝 스키마 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets)<br /><br /> [데이터 마이닝 스키마 행 집합&#40;SSAs&#41;](../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 도구](../../analysis-services/data-mining/data-mining-tools.md)   
 [데이터 마이닝 개념](../../analysis-services/data-mining/data-mining-concepts.md)   
 [데이터 마이닝 솔루션](../../analysis-services/data-mining/data-mining-solutions.md)   
 [테스트 및 유효성 검사&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
