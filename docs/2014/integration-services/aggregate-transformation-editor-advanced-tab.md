---
title: 집계 변환 편집기 (고급 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregationtransformation.advanced.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: 186a9736-2554-40a0-9cb2-877a8db5fde8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 419a63f9a98e51b9601d7d38f70528ff4ae05970
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061587"
---
# <a name="aggregate-transformation-editor-advanced-tab"></a>집계 변환 편집기(고급 탭)
  **집계 변환 편집기** 대화 상자의 **고급** 탭을 사용하여 구성 요소 속성을 설정하고, 집계를 지정하고, 입력 및 출력 열의 속성을 설정할 수 있습니다.  
  
> [!NOTE]  
>  키 수, 키 배율, 고유 키 수, 고유 수 배율 옵션은 **고급** 탭에서 지정하면 구성 요소 수준에서 적용되고, **집계** 탭의 고급 디스플레이에서 지정하면 출력 수준에서 적용되고, **집계** 탭의 아래쪽에 있는 열 목록에서 지정하면 열 수준에서 적용됩니다.  
>   
>  집계 변환에서 **키** 및 **키 배율** 은 **Group by** 연산의 결과로 반환될 그룹 수를 나타냅니다. **고유 키 수** 및 **고유 수 배율** 은 **고유 카운트** 연산의 결과로 반환될 고유 값 수를 나타냅니다.  
  
 집계 변환에 대한 자세한 내용은 [Aggregate Transformation](data-flow/transformations/aggregate-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **키 배율**  
 필요에 따라 집계에 필요한 키 수를 대략적으로 지정합니다. 변환 시 이 정보를 사용하여 최초 캐시 크기를 최적화합니다. 이 옵션의 기본값은 **Unspecified**입니다. **키 배율** 과 **키 수** 를 모두 지정하면 **키 수** 가 우선 적용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|Unspecified|**키 배율** 속성이 사용되지 않습니다.|  
|낮음|집계에서 약 500,000개의 키를 쓸 수 있습니다.|  
|보통|집계에서 약 5,000,000개의 키를 쓸 수 있습니다.|  
|높음|집계에서 25,000,000개 이상의 키를 쓸 수 있습니다.|  
  
 **키 수**  
 필요에 따라 집계에 필요한 키 수를 정확하게 지정합니다. 변환 시 이 정보를 사용하여 최초 캐시 크기를 최적화합니다. **키 배율** 과 **키 수** 를 모두 지정하면 **키 수** 가 우선 적용됩니다.  
  
 **고유 수 배율**  
 필요에 따라 집계에서 쓸 수 있는 고유한 값의 수를 대략적으로 지정합니다. 이 옵션의 기본값은 **Unspecified**입니다. **고유 수 배율** 과 **고유 키 수** 를 모두 지정하면 **고유 키 수** 가 우선 적용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|Unspecified|CountDistinctScale 속성이 사용되지 않습니다.|  
|낮음|집계에서 약 500,000개의 고유한 값을 쓸 수 있습니다.|  
|보통|집계에서 약 5,000,000개의 고유한 값을 쓸 수 있습니다.|  
|높음|집계에서 25,000,000개 이상의 고유한 값을 쓸 수 있습니다.|  
  
 **고유 키 수**  
 필요에 따라 집계에서 쓸 수 있는 고유한 값의 수를 정확하게 지정합니다. **고유 수 배율** 과 **고유 키 수** 를 모두 지정하면 **고유 키 수** 가 우선 적용됩니다.  
  
 **자동 확장 비율**  
 1에서 100 사이의 값을 사용하여 집계 중에 메모리를 확장할 수 있는 비율을 지정합니다. 이 옵션의 기본값은 **25%** 입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [집계 변환 편집기&#40;집계 탭&#41;](../../2014/integration-services/aggregate-transformation-editor-aggregations-tab.md)   
 [집계 변환을 사용하여 데이터 세트의 값 집계](data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  
