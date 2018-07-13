---
title: 행 샘플링 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rowsamplingtrans.f1
helpviewer_keywords:
- sampling seeds [Integration Services]
- random seeds
- random sampling
- sample data sets [Integration Services]
- Row Sampling transformation
- packages [Integration Services], samples
- datasets [Integration Services], sample
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 07a8e8aefd414c04b1a7d6d3f0c3d6a5dcd51747
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37199703"
---
# <a name="row-sampling-transformation"></a>행 샘플링 변환
  행 샘플링 변환은 임의로 선택된 입력 데이터 집합의 하위 집합을 얻는 데 사용합니다. 출력 샘플의 정확한 크기와 난수 생성기의 초기값을 지정할 수 있습니다.  
  
 무작위 샘플링은 다양한 용도로 응용될 수 있습니다. 예를 들어 복권 당첨 경품을 받을 50명의 직원을 임의로 선택하려는 회사는 직원 데이터베이스에 대해 행 샘플링 변환을 사용하여 정확한 수의 당첨자를 생성할 수 있습니다.  
  
 행 샘플링 변환은 패키지 개발 중에 전체 데이터 집합을 대표하지만 크기가 작은 데이터 집합을 만드는 데에도 유용합니다. 유효한 대표 데이터를 사용하여 패키지 실행과 데이터 변환을 테스트할 수 있을 뿐만 아니라 전체 데이터 집합 대신 무작위 샘플링을 사용하기 때문에 시간이 훨씬 단축됩니다. 테스트 패키지에 사용되는 샘플 데이터 집합은 항상 크기가 같기 때문에 샘플 하위 집합을 사용하면 패키지의 성능 문제도 쉽게 식별할 수 있습니다.  
  
 이 변환은 입력 행의 비율을 선택하여 샘플 데이터 집합을 만드는 비율 샘플링 변환과 유사합니다. [Percentage Sampling Transformation](percentage-sampling-transformation.md)을 참조하세요.  
  
## <a name="configuring-the-row-sampling-transformation"></a>행 샘플링 변환 구성  
 행 샘플링 변환은 지정한 수의 변환 입력 행을 선택하여 샘플 데이터 집합을 만듭니다. 변환 입력에서 임의로 행이 선택되기 때문에 결과 샘플은 전체 입력을 대표합니다. 난수 생성기에 사용되는 초기값을 지정하여 변환의 행 선택 방법에 영향을 줄 수도 있습니다.  
  
 동일한 변환 입력에 대해 같은 임의 초기값을 사용하면 항상 동일한 샘플 출력이 만들어집니다. 초기값을 지정하지 않으면 변환에서 운영 체제의 틱 수를 사용하여 난수를 만듭니다. 따라서 패키지 개발 및 테스트 중에 변환 결과를 확인하기 위해 테스트 시에는 동일한 초기값을 사용한 다음 패키지를 프로덕션으로 이동할 때 임의 초기값으로 변경할 수도 있습니다.  
  
 행 샘플링 변환은 `SamplingValue` 사용자 지정 속성을 포함합니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](transformation-custom-properties.md)을 참조하세요.  
  
 이 변환에는 하나의 입력과 두 개의 출력이 있습니다. 오류 출력은 없습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **행 샘플링 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [행 샘플링 변환 편집기&#40;샘플링 페이지&#41;](../../row-sampling-transformation-editor-sampling-page.md)를 참조하세요.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [변환 사용자 지정 속성](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
  
