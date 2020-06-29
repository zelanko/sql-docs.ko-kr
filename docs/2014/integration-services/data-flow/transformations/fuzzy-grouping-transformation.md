---
title: 유사 항목 그룹화 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtrans.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- Fuzzy Grouping transformation
- temporary tables [Integration Services]
- grouping data
- standardizing data [Integration Services]
- columns [Integration Services], standardizing
- similarity thresholds [Integration Services]
- data cleaning [Integration Services]
- duplicate data [Integration Services]
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4937c4addfe8006bf09e390e0c204ab0ab64bf98
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430620"
---
# <a name="fuzzy-grouping-transformation"></a>유사 항목 그룹화 변환
  유사 항목 그룹화 변환에서는 중복되기 쉬운 데이터 행을 식별하고 데이터 표준화에 사용할 데이터의 중복 행을 선택하여 데이터 정리 태스크를 수행합니다.  
  
> [!NOTE]  
>  성능 및 메모리 제한 사항을 포함하여 유사 항목 그룹화 변환에 대한 자세한 내용은 [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604)(SQL Server Integration Services 2005에서 유사 항목 조회 및 유사 항목 그룹화) 백서를 참조하세요.  
  
 유사 항목 그룹화 변환에는 변환 알고리즘이 작업을 수행하는 데 필요한 임시 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블을 만들기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결이 필요합니다. 연결은 데이터베이스에 테이블을 만드는 권한을 가진 사용자로 확인되어야 합니다.  
  
 변환을 구성하려면 중복을 식별하는 데 사용할 입력 열을 선택하고 각 열에 대해 일치 유형으로 유사 항목 일치 또는 정확한 일치를 선택해야 합니다. 정확한 일치를 사용하면 해당 열에 동일한 값을 가진 행만 그룹화됩니다. DT_TEXT, DT_NTEXT 및 DT_IMAGE를 제외한 모든 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식의 열에 정확한 일치를 적용할 수 있습니다. 유사 항목 일치는 비슷한 값을 가진 행을 그룹화합니다. 데이터의 근사 일치 방식은 사용자 정의 유사성 점수에 기반합니다. DT_WSTR 및 DT_STR 데이터 형식을 가진 열만 유사 항목 일치에서 사용할 수 있습니다. 자세한 내용은 [Integration Services Data Types](../integration-services-data-types.md)을 참조하세요.  
  
 변환 출력에는 모든 입력 열, 표준화된 데이터를 가진 한 개 이상의 열 및 유사성 점수를 가진 열이 포함됩니다. 점수는 0과 1 사이의 10진수 값입니다. 정식 행의 점수는 1이며 유사 항목 그룹 내 다른 행의 점수는 정식 행과 일치하는 정도를 나타냅니다. 정식 행과 더 비슷하게 일치할수록 점수가 1에 가까워집니다. 유사 항목 그룹에 정식 행과 정확하게 중복되는 행이 포함된 경우 해당 행의 점수는 1입니다. 변환에서는 중복 행을 제거하지 않고 정식 행과 비슷한 행을 연결하는 키를 만들어 그룹화합니다.  
  
 변환에서는 각 입력 열당 다음 추가 열을 포함하여 한 개의 출력 행을 생성합니다.  
  
-   **_key_in**열, 각 행을 고유하게 식별합니다.  
  
-   **_key_out**열, 중복 행의 그룹을 식별합니다. **_key_out** 열은 정식 데이터 행에 **_key_in** 열 값을 가집니다. **_key_out** 에 동일한 값을 가진 행은 동일한 그룹의 일부입니다. 그룹의 **_key_out**값은 정식 데이터 행의 **_key_in** 값에 해당합니다.  
  
-   **_score**, 입력 행 및 정식 행 간의 유사성을 나타내는 0과 1 사이의 값입니다.  
  
 이것은 기본 열 이름이며 다른 이름을 사용하도록 유사 항목 그룹화 변환을 구성할 수 있습니다. 출력에서는 유사 항목 그룹화에 참여하는 각 열에 유사성 점수를 제공합니다.  
  
 유사 항목 그룹화 변환에는 수행할 그룹화를 사용자 지정하는 두 가지 기능인 토큰 구분 기호 및 유사성 임계값이 포함됩니다. 변환에서는 데이터를 토큰화하는 기본 구분 기호 집합을 제공하지만 새 구분 기호를 추가하여 데이터 토큰화 정도를 향상시킬 수 있습니다.  
  
 유사성 임계값은 변환에서 얼마나 엄격하게 중복을 식별하는지를 지정합니다. 유사성 임계값은 구성 요소 및 열 수준에서 설정할 수 있습니다. 열 수준 유사성 임계값은 유사 항목 일치를 수행하는 열에서만 사용할 수 있습니다. 유사성 범위는 0에서 1 사이입니다. 임계값이 1에 가까울수록 서로 유사한 행과 열이 중복된 것으로 간주되기 쉽습니다. 구성 요소 및 열 수준에서 MinSimilarity 속성을 설정하여 행 및 열 사이의 유사성 임계값을 지정하세요. 구성 요소 수준에서 지정된 유사성을 만족하려면 모든 행이 모든 열에 걸쳐 구성 요소 수준에서 지정된 유사성 임계값 보다 크거나 같은 유사성을 가져야 합니다.  
  
 유사 항목 그룹화 변환에서는 유사성 내부 측정값을 계산하고 MinSimilarity에 지정된 값보다 유사도가 떨어지는 행을 그룹화에서 제외합니다.  
  
 다른 최소 유사성 임계값을 사용하고 유사 항목 그룹화 변환을 여러 번 적용하여 데이터에 사용 중인 유사성 임계값을 확인할 수 있습니다. 변환 출력의 점수 열은 런타임에 그룹 내 각 행에 대한 유사성 점수를 포함합니다. 사용자의 데이터에 적절한 유사성 임계값을 알아내는 데 이 값을 사용할 수 있습니다. 유사성을 높이려면 점수 열의 값 보다 큰 값으로 MinSimilarity을 설정해야 합니다.  
  
 유사 항목 그룹화 변환 입력에 열 속성을 설정하여 변환에서 수행하는 그룹화를 사용자 지정할 수 있습니다. 예를 들어 FuzzyComparisonFlags 속성은 변환에서 열에 문자열 데이터를 비교하는 방법을 지정하며 ExactFuzzy 속성은 변환에서 유사 항목 일치를 수행하는지 또는 정확한 일치를 수행하는지를 지정합니다.  
  
 유사 항목 그룹화 변환에서 사용하는 메모리 양은 MaxMemoryUsage 사용자 지정 속성을 설정하여 구성할 수 있습니다. 크기(MB)를 지정하거나 값 0을 사용하여 변환에서 요구 사항 및 사용 가능한 실제 메모리를 기반으로 메모리를 동적으로 사용하도록 할 수 있습니다. MaxMemoryUsage 사용자 지정 속성은 패키지 로드 시 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](transformation-custom-properties.md)을 참조하세요.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
## <a name="row-comparison"></a>행 비교  
 유사 항목 그룹화 변환을 구성하는 경우 변환에서 변환 입력 내의 행을 비교하는 데 사용할 비교 알고리즘을 지정할 수 있습니다. 전체 속성을로 설정 하는 경우 `true` 변환에서는 입력의 모든 행을 입력의 다른 모든 행과 비교 합니다. 이 비교 알고리즘을 사용하면 더 정확한 결과를 얻을 수 있지만 입력 행의 수가 많으면 변환 성능이 느려집니다. 성능 문제를 방지 하려면 패키지를 개발 하는 동안에만 철저 한 속성을로 설정 하는 것이 좋습니다 `true` .  
  
## <a name="temporary-tables-and-indexes"></a>임시 테이블 및 인덱스  
 유사 항목 그룹화 변환에서는 런타임에 변환에서 연결하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 테이블 및 인덱스와 같은 크기가 큰 임시 개체를 만듭니다. 테이블 및 인덱스의 크기는 변환 입력 내 행의 수 및 유사 항목 그룹화 변환에서 만든 토큰의 수에 비례합니다.  
  
 변환은 또한 임시 테이블을 쿼리합니다. 따라서 프로덕션 서버에 사용 가능한 디스크 공간이 제한되는 경우 프로덕션 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 아닌 인스턴스로 유사 항목 그룹화 변환을 연결해야 합니다.  
  
 변환에서 사용하는 테이블 및 인덱스가 로컬 컴퓨터에 있는 경우 변환의 성능이 향상될 수 있습니다.  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>유사 항목 그룹화 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **유사 항목 그룹화 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [유사 항목 그룹화 변환 편집기&#40;연결 관리자 탭&#41;](../../fuzzy-grouping-transformation-editor-connection-manager-tab.md)  
  
-   [유사 항목 그룹화 변환 편집기&#40;열 탭&#41;](../../fuzzy-grouping-transformation-editor-columns-tab.md)  
  
-   [유사 항목 그룹화 변환 편집기&#40;고급 탭&#41;](../../fuzzy-grouping-transformation-editor-advanced-tab.md)  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 이 태스크의 속성 설정 방법에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [유사 항목 그룹화 변환을 사용하여 유사한 데이터 행 식별](fuzzy-grouping-transformation.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>참고 항목  
 [유사 항목 조회 변환](lookup-transformation.md)   
 [Integration Services 변환](integration-services-transformations.md)  
  
  
