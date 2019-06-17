---
title: 측정값 속성 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- additivity [Analysis Services]
- ID property
- ErrorConfiguration property
- AggregateFunction property
- DisplayFolder property
- IgnoreUnrelatedDimensions property
- FormatString property
- Description property
- semiadditive
- properties [Analysis Services], measure groups
- aggregate functions [Analysis Services]
- DataType property
- ProcessingMode property
- MeasureExpression property
- AggregationPrefix property
- Visible property
- properties [Analysis Services], measures
- StorageLocation property
- StorageMode property
- formats [Analysis Services], measures
- Source property
- aggregations [Analysis Services], measures
- measures [Analysis Services], properties
- nonadditive [Analysis Services]
- Name property
- measures [Analysis Services], display formats
- ProcessingPriority property
- measure groups [Analysis Services], properties
- Type property
- ProactiveCaching property
ms.assetid: e9031078-c4f5-4986-b0c9-4d064b622ab7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b1acd9e33865f1f60c1d1134e3173af4e4a562b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076613"
---
# <a name="configure-measure-properties"></a>측정값 속성 구성
  측정값에는 해당 측정값의 작동 방법을 정의하고 측정값의 표시 방법을 제어하는 데 사용할 수 있는 속성이 있습니다.  
  
 큐브 또는 측정값을 만들거나 편집할 때 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 속성을 설정할 수 있습니다. 또한 MDX 또는 AMO를 사용하여 프로그래밍 방식으로 속성을 설정할 수 있습니다. 자세한 내용은 [다차원 모델의 측정값 및 측정값 그룹 만들기](create-measures-and-measure-groups-in-multidimensional-models.md), [CREATE MEMBER 문&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member) 또는 [AMO OLAP 기본 개체 프로그래밍](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects)을 참조하세요.  
  
## <a name="measure-properties"></a>측정값 속성  
 측정값은 해당 속성이 측정값 수준에서 무시되는 경우를 제외하고 자신이 속한 측정값 그룹에서 특정 속성을 상속합니다. 측정값 속성은 측정값이 집계되는 방법, 측정값의 데이터 형식, 사용자에게 표시되는 이름, 측정값이 나타날 표시 폴더, 측정값의 형식 문자열, 측정값 식, 기본 원본 열 및 사용자에 대한 표시 유형을 결정합니다.  
  
|속성|정의|  
|--------------|----------------|  
|`AggregateFunction`|필수 사항입니다. 측정값이 집계되는 방법을 결정합니다. `Sum`이 기본 집계입니다. 자세한 내용은 각 함수 설명의 [Use Aggregate Functions](use-aggregate-functions.md) 을 참조하세요.|  
|`DataType`|필수 사항입니다. 측정값이 바인딩되는 기본 팩트 테이블 열의 데이터 형식을 지정합니다. 이 값은 기본적으로 원본 열에서 상속됩니다.|  
|`Description`|클라이언트 애플리케이션에 노출될 수 있는 측정값에 대한 설명을 제공합니다.|  
|`DisplayFolder`|사용자가 큐브에 연결할 때 측정값이 표시되는 폴더를 지정합니다. 큐브에 많은 측정값이 있을 때 표시 폴더를 사용하여 측정값을 분류하고 사용자 검색 환경을 개선할 수 있습니다.|  
|`FormatString`|측정값의 `FormatString` 속성을 사용하여 사용자에게 측정값을 표시하는 데 사용되는 형식을 선택할 수 있습니다.<br /><br /> [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 표시 형식 목록이 제공되지만 목록에 없는 여러 가지 추가 형식을 지정할 수 있습니다. Microsoft Visual Basic에서 유효한 사용자 정의 형식이나 명명된 형식을 지정할 수 있습니다.|  
|`ID`|필수 사항입니다. 측정값의 고유 ID를 표시합니다. 이 속성은 읽기 전용입니다.|  
|`MeasureExpression`|측정값을 정의하는 제한된 MDX 식을 지정합니다. 식은 집계되기 전에 리프 수준에서 평가되고 값의 가중치 적용을 허용합니다. 예를 들어 통화 변환에서 판매액은 환율에 따라 가중치가 적용됩니다.|  
|`Name`|필수 사항입니다. 측정값의 이름을 지정합니다.|  
|`Source`|필수 사항입니다. 측정값이 바인딩되는 데이터 원본 뷰의 열을 지정합니다. [데이터 원본 및 바인딩&#40;SSAS 다차원&#41;](data-sources-and-bindings-ssas-multidimensional.md)을 참조하세요.|  
|`Visible`|클라이언트 애플리케이션에서 측정값의 표시 유형을 결정합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [측정값 그룹 속성 구성](configure-measure-group-properties.md)   
 [측정값 수정](../lesson-3-1-modifying-measures.md)  
  
  
