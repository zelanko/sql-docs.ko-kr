---
title: 집계 변환 편집기 (집계 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregationtransformation.aggregations.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: a01cb124-ec79-4673-b1a1-bf4d60ee1b45
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 698e3757a32d9a2a9db95df495e33903dbdfed1f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061576"
---
# <a name="aggregate-transformation-editor-aggregations-tab"></a>집계 변환 편집기(집계 탭)
  **집계 변환 편집기** 대화 상자의 **집계** 탭을 사용하여 집계 및 집계 속성에 대한 열을 지정할 수 있습니다. 이때 여러 집계를 적용할 수 있습니다. 이 변환으로 인해 오류 출력이 생성되지는 않습니다.  
  
> [!NOTE]  
>  키 수, 키 배율, 고유 키 수, 고유 수 배율 옵션은 **고급** 탭에서 지정하면 구성 요소 수준에서 적용되고, **집계** 탭의 고급 디스플레이에서 지정하면 출력 수준에서 적용되고, **집계** 탭의 아래쪽에 있는 열 목록에서 지정하면 열 수준에서 적용됩니다.  
>   
>  집계 변환에서 **키** 및 **키 배율** 은 **Group by** 연산의 결과로 반환될 그룹 수를 나타냅니다. **고유 키 수** 및 **고유 수 배율** 은 **고유 카운트** 연산의 결과로 반환될 고유 값 수를 나타냅니다.  
  
 집계 변환에 대한 자세한 내용은 [Aggregate Transformation](data-flow/transformations/aggregate-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **고급/기본**  
 여러 개의 출력에 대한 여러 집계를 구성하는 옵션을 표시하거나 숨깁니다. 기본적으로 고급 옵션은 숨겨져 있습니다.  
  
 **집계 이름**  
 고급 디스플레이에서 집계의 이름을 입력합니다.  
  
 **Group By 열**  
 고급 디스플레이에서 아래에 설명된 **사용 가능한 입력 열** 목록을 사용하여 그룹화할 열을 선택합니다.  
  
 **키 배율**  
 고급 디스플레이에서 필요에 따라 집계가 쓸 수 있는 키의 수를 대략적으로 지정합니다. 이 옵션의 기본값은 **Unspecified**입니다. **키 배율** 과 **키** 속성을 모두 설정하면 **키** 의 값이 우선 적용됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|Unspecified|키 배율 속성을 사용하지 않습니다.|  
|낮음|집계에서 약 500,000개의 키를 쓸 수 있습니다.|  
|보통|집계에서 약 5,000,000개의 키를 쓸 수 있습니다.|  
|높음|집계에서 25,000,000개 이상의 키를 쓸 수 있습니다.|  
  
 **키**  
 고급 디스플레이에서 필요에 따라 집계가 쓸 수 있는 키의 수를 정확하게 지정합니다. **키 배율** 과 **키** 를 모두 지정하면 **키** 의 값이 우선 적용됩니다.  
  
 **사용 가능한 입력 열**  
 이 테이블의 확인란을 사용하여 사용 가능한 입력 열 목록에서 선택합니다.  
  
 **입력 열**  
 사용 가능한 입력 열 목록에서 선택합니다.  
  
 **출력 별칭**  
 각 열의 별칭을 입력합니다. 기본값은 입력 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 **연산**  
 다음 표를 참조하여 사용 가능한 연산 목록에서 선택합니다.  
  
|작업(Operation)|Description|  
|---------------|-----------------|  
|**Group By**|데이터 세트를 그룹으로 나눕니다. 모든 데이터 형식의 열을 그룹화할 수 있습니다. 자세한 내용은 GROUP BY를 참조하십시오.|  
|**총합**|열에 있는 값의 합계를 계산합니다. 숫자 데이터 형식의 열만 합계를 계산할 수 있습니다. 자세한 내용은 SUM을 참조하십시오.|  
|**평균**|열에 있는 열 값의 평균을 반환합니다. 숫자 데이터 형식의 열만 평균을 계산할 수 있습니다. 자세한 내용은 AVG를 참조하십시오.|  
|**Count**|그룹의 항목 개수를 반환합니다. 자세한 내용은 COUNT를 참조하십시오.|  
|**CountDistinct**|그룹에서 Null이 아닌 고유한 값의 개수를 반환합니다. 자세한 내용은 COUNT 및 DISTINCT를 참조하십시오.|  
|**최대**|그룹의 최소값을 반환합니다. 숫자 데이터 형식에서만 실행됩니다.|  
|**최대화**|그룹의 최대값을 반환합니다. 숫자 데이터 형식에서만 실행됩니다.|  
  
 **비교 플래그**  
 **Group By**를 선택하는 경우 확인란을 사용하여 변환이 비교를 수행하는 방법을 제어할 수 있습니다. 문자열 비교 옵션에 대한 자세한 내용은 [Comparing String Data](data-flow/comparing-string-data.md)를 참조하십시오.  
  
 **Count Distinct Scale**  
 필요에 따라 집계에서 쓸 수 있는 고유한 값의 수를 대략적으로 지정합니다. 이 옵션의 기본값은 **Unspecified**입니다. 및 CountDistinctKeys `CountDistinctScale` 가 **CountDistinctKeys** 모두 지정 된 경우 **CountDistinctKeys** 가 우선적으로 적용 됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|Unspecified|`CountDistinctScale` 속성을 사용하지 않습니다.|  
|낮음|집계에서 약 500,000개의 고유한 값을 쓸 수 있습니다.|  
|보통|집계에서 약 5,000,000개의 고유한 값을 쓸 수 있습니다.|  
|높음|집계에서 25,000,000개 이상의 고유한 값을 쓸 수 있습니다.|  
  
 **Count Distinct Keys**  
 필요에 따라 집계에서 쓸 수 있는 고유한 값의 수를 정확하게 지정합니다. 및 CountDistinctKeys `CountDistinctScale` 가 **CountDistinctKeys** 모두 지정 된 경우 **CountDistinctKeys** 가 우선적으로 적용 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [집계 변환 편집기 &#40;고급 탭&#41;](../../2014/integration-services/aggregate-transformation-editor-advanced-tab.md)   
 [집계 변환을 사용하여 데이터 세트의 값 집계](data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  
