---
title: 행 샘플링 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rowsamplingtrans.f1
- sql13.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql13.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- sampling seeds [Integration Services]
- random seeds
- random sampling
- sample data sets [Integration Services]
- Row Sampling transformation
- packages [Integration Services], samples
- datasets [Integration Services], sample
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 432c461f90f89eb625e923af342f7c96f323709c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297825"
---
# <a name="row-sampling-transformation"></a>행 샘플링 변환

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  행 샘플링 변환은 임의로 선택된 입력 데이터 세트의 하위 세트를 얻는 데 사용합니다. 출력 샘플의 정확한 크기와 난수 생성기의 초기값을 지정할 수 있습니다.  
  
 무작위 샘플링은 다양한 용도로 응용될 수 있습니다. 예를 들어 복권 당첨 경품을 받을 50명의 직원을 임의로 선택하려는 회사는 직원 데이터베이스에 대해 행 샘플링 변환을 사용하여 정확한 수의 당첨자를 생성할 수 있습니다.  
  
 행 샘플링 변환은 패키지 개발 중에 전체 데이터 세트를 대표하지만 크기가 작은 데이터 세트를 만드는 데에도 유용합니다. 유효한 대표 데이터를 사용하여 패키지 실행과 데이터 변환을 테스트할 수 있을 뿐만 아니라 전체 데이터 세트 대신 무작위 샘플링을 사용하기 때문에 시간이 훨씬 단축됩니다. 테스트 패키지에 사용되는 샘플 데이터 세트는 항상 크기가 같기 때문에 샘플 하위 집합을 사용하면 패키지의 성능 문제도 쉽게 식별할 수 있습니다.  
  
 이 변환은 입력 행의 비율을 선택하여 샘플 데이터 세트를 만드는 비율 샘플링 변환과 유사합니다. [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)을 참조하세요.  
  
## <a name="configuring-the-row-sampling-transformation"></a>행 샘플링 변환 구성  
 행 샘플링 변환은 지정한 수의 변환 입력 행을 선택하여 샘플 데이터 세트를 만듭니다. 변환 입력에서 임의로 행이 선택되기 때문에 결과 샘플은 전체 입력을 대표합니다. 난수 생성기에 사용되는 초기값을 지정하여 변환의 행 선택 방법에 영향을 줄 수도 있습니다.  
  
 동일한 변환 입력에 대해 같은 임의 초기값을 사용하면 항상 동일한 샘플 출력이 만들어집니다. 초기값을 지정하지 않으면 변환에서 운영 체제의 틱 수를 사용하여 난수를 만듭니다. 따라서 패키지 개발 및 테스트 중에 변환 결과를 확인하기 위해 테스트 시에는 동일한 초기값을 사용한 다음 패키지를 프로덕션으로 이동할 때 임의 초기값으로 변경할 수도 있습니다.  
  
 행 샘플링 변환은 **SamplingValue** 사용자 지정 속성을 포함합니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하세요.  
  
 이 변환에는 하나의 입력과 두 개의 출력이 있습니다. 오류 출력은 없습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성을 설정하는 방법은 다음을 참조하십시오.  
  
## <a name="row-sampling-transformation-editor-sampling-page"></a>행 샘플링 변환 편집기(샘플링 페이지)
  **행 샘플링 변환 편집기** 대화 상자를 사용하여 입력의 일부분을 지정된 행 수를 사용하는 샘플로 분할할 수 있습니다. 이 변환으로 인해 입력이 두 개의 별도 출력으로 나뉩니다.  
  
### <a name="options"></a>옵션  
 **행 수**  
 입력에서 샘플로 사용할 행 수를 지정합니다.  
  
 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
 **샘플 출력 이름**  
 샘플링한 행이 포함될 출력에 사용할 고유 이름을 제공합니다. 제공한 이름은 SSIS 디자이너에 표시됩니다.  
  
 **선택하지 않은 출력 이름**  
 샘플링에서 제외된 행이 포함될 출력에 사용할 고유 이름을 제공합니다. 제공한 이름은 SSIS 디자이너에 표시됩니다.  
  
 **다음과 같은 임의 초기값 사용**  
 변환에서 샘플을 만드는 데 사용하는 난수 생성기에 샘플링 초기값을 지정합니다. 이 옵션은 개발 및 테스트 용도로만 사용하는 것이 좋습니다. 임의 초기값을 지정하지 않으면 변환에서 Microsoft Windows 틱 수를 초기값으로 사용합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
  
