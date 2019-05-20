---
title: 비율 샘플링 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.percentagesamplingtrans.f1
- sql13.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- testing mining models
- sampling seeds [Integration Services]
- data mining [Analysis Services], sample data sets
- Percentage Sampling transformation
- sample data sets [Integration Services]
- datasets [Integration Services], sample
- training mining models
ms.assetid: 59767e52-f732-4b3f-8602-be50d0a64ef2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 67fb4b94e777a974ff42c59d730a58bb1396f289
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725919"
---
# <a name="percentage-sampling-transformation"></a>비율 샘플링 변환

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  비율 샘플링 변환은 변환 입력 행의 비율을 선택하여 샘플 데이터 집합을 만듭니다. 샘플 데이터 집합은 입력을 대표하는 결과 샘플을 만들기 위해 변환 입력에서 임의로 선택한 행입니다.  
  
> [!NOTE]  
>  지정한 비율 외에도 비율 샘플링 변환은 특정 행을 샘플 출력에 포함할지를 결정하는 알고리즘을 사용합니다. 이는 샘플 출력의 행 수가 지정한 비율을 정확하게 반영하지 않을 수도 있다는 것을 의미합니다. 예를 들어 행 수가 25,000개인 입력 데이터 집합에 대해 10%를 지정해도 2,500개 행을 가진 샘플이 생성되지 않고 샘플에 포함된 행 수가 이보다 많거나 적을 수도 있습니다.  
  
 비율 샘플링 변환은 특히 데이터 마이닝에 유용합니다. 이 변환을 사용하면 하나의 데이터 집합을 임의로 두 개의 데이터 집합으로 나눌 수 있으며 하나는 데이터 마이닝 모델 학습에 사용되고 다른 하나는 모델 테스트에 사용됩니다.  
  
 비율 샘플링 변환은 패키지 개발을 위해 샘플 데이터 집합을 만드는 데에도 유용합니다. 비율 샘플링 변환을 데이터 흐름에 적용하면 데이터 특징을 유지하면서 데이터 집합의 크기를 균일하게 줄일 수 있습니다. 테스트 패키지는 전체 데이터 집합을 대표하지만 크기가 작은 데이터 집합을 사용하기 때문에 보다 신속하게 실행할 수 있습니다.  
  
## <a name="configuration-the-percentage-sampling-transformation"></a>비율 샘플링 변환 구성  
 샘플링 초기값을 지정하여 비율 샘플링 변환이 행 선택 시 사용하는 난수 생성기의 동작을 수정할 수 있습니다. 같은 샘플링 초기값을 사용하면 이 변환은 항상 동일한 샘플 출력을 만듭니다. 초기값을 지정하지 않으면 변환에서 운영 체제의 틱 수를 사용하여 난수를 만듭니다. 따라서 패키지 개발 및 테스트 중에 변환 결과를 확인하기 위해 표준 초기값을 사용하도록 선택한 다음 패키지를 프로덕션으로 이동할 때 임의 초기값을 사용하도록 변경할 수도 있습니다.  
  
 이 변환은 지정한 수의 입력 행을 선택하여 샘플 데이터 집합을 만드는 행 샘플링 변환과 유사합니다. 자세한 내용은 [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)을(를) 참조하세요.  
  
 비율 샘플링 변환은 **SamplingValue** 사용자 지정 속성을 포함합니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하세요.  
  
 이 변환에는 하나의 입력과 두 개의 출력이 있습니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="percentage-sampling-transformation-editor"></a>비율 샘플링 변환 편집기
  **비율 샘플링 변환 편집기** 대화 상자에서 지정한 행의 백분율을 사용하여 입력 부분을 샘플로 분할할 수 있습니다. 이 변환으로 인해 입력이 두 개의 별도 출력으로 나뉩니다.  
  
### <a name="options"></a>옵션  
 **행의 백분율**  
 입력에서 샘플로 사용할 행의 백분율을 지정합니다.  
  
 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
 **샘플 출력 이름**  
 샘플링한 행이 포함될 출력에 사용할 고유 이름을 제공합니다. 제공한 이름은 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **선택하지 않은 출력 이름**  
 샘플링에서 제외된 행이 포함될 출력에 사용할 고유 이름을 제공합니다. 제공한 이름은 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **다음과 같은 임의 초기값 사용**  
 변환에서 샘플을 만드는 데 사용하는 난수 생성기에 샘플링 초기값을 지정합니다. 이 옵션은 개발 및 테스트 용도로만 사용하는 것이 좋습니다. 임의 초기값을 지정하지 않으면 Microsoft Windows 틱 수가 사용됩니다.  
  
  
