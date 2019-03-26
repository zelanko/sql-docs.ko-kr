---
title: 정렬 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sorttrans.f1
- sql13.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 19bf7654a37d589877f806aaaa1d98fefac95b22
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270596"
---
# <a name="sort-transformation"></a>정렬 변환
  정렬 변환은 입력 데이터를 오름차순이나 내림차순으로 정렬하고 정렬된 데이터를 변환 출력에 복사합니다. 입력에 여러 가지 정렬을 적용할 수 있으며 각 정렬은 정렬 순서를 결정하는 숫자로 식별됩니다. 숫자가 가장 적은 열이 맨 먼저 정렬되고 그 다음 숫자의 정렬 열이 다음에 정렬됩니다. 예를 들어 **CountryRegion** 열이 정렬 순서 1이고 **City** 열이 정렬 순서 2인 경우 출력은 먼저 국가/지역별로 정렬된 다음 도시별로 정렬됩니다. 양수는 오름차순 정렬을 나타내고 음수는 내림차순 정렬을 나타냅니다. 정렬되지 않은 열의 정렬 순서는 0입니다. 정렬이 선택되지 않은 열은 정렬된 열과 함께 자동으로 변환 출력에 복사됩니다.  
  
 정렬 변환에는 변환에서 열의 문자열 데이터를 처리하는 방법을 정의하는 비교 옵션 집합이 포함되어 있습니다. 자세한 내용은 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)을 참조하세요.  
  
> [!NOTE]  
>  정렬 변환은 Transact-SQL에서 ORDER BY 절이 수행하는 것과 동일한 순서로 GUID를 정렬하지 않습니다. 정렬 변환은 0-9로 시작하는 GUID를 A-F로 시작하는 GUID보다 먼저 정렬하지만, [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]에 구현된 ORDER BY 절은 GUID를 다르게 정렬합니다. 자세한 내용은 [ORDER BY 절&#40;Transact-SQL&#41;](../../../t-sql/queries/select-order-by-clause-transact-sql.md)을 참조하세요.  
  
 정렬 변환은 정렬 중에 중복 행을 제거할 수도 있습니다. 중복 행은 동일한 정렬 키 값을 가진 행입니다. 정렬 키 값은 사용된 문자열 비교 옵션을 기반으로 생성되므로 서로 다른 리터럴 문자열이 동일한 정렬 키 값을 가질 수도 있습니다. 이 변환은 값이 다르지만 동일한 정렬 키를 가진 입력 열의 행을 중복 행으로 식별합니다.  
  
 정렬 변환은 패키지 로드 시 속성 식을 사용하여 업데이트할 수 있는 **MaximumThreads** 사용자 지정 속성을 포함합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하세요.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
## <a name="configuration-of-the-sort-transformation"></a>정렬 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 codeplex.com의 예제 - [SortDeDuplicateDelimitedString 사용자 지정 SSIS 구성 요소](https://go.microsoft.com/fwlink/?LinkId=220821)  
  
## <a name="sort-transformation-editor"></a>정렬 변환 편집기
  **정렬 변환 편집기** 대화 상자를 사용하여 정렬할 열을 선택하고, 정렬 순서를 설정하고, 중복을 제거할지 여부를 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 확인란을 사용하여 정렬할 열을 지정합니다.  
  
 **이름**  
 사용 가능한 각 입력 열 이름을 표시합니다.  
  
 **통과**  
 열을 정렬된 출력에 포함할지 여부를 나타냅니다.  
  
 **입력 열**  
 각 행에 대해 사용 가능한 입력 열 목록에서 선택합니다. 선택 내용에 따라 **사용 가능한 입력 열** 테이블의 확인란이 달라집니다.  
  
 **출력 별칭**  
 각 출력 열의 별칭을 입력합니다. 기본값은 입력 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 **정렬 형식**  
 오름차순으로 정렬할 것인지, 아니면 내림차순으로 정렬할 것인지를 나타냅니다.  
  
 **정렬 순서**  
 열을 정렬할 순서를 나타냅니다. 이 옵션은 각 열에 대해 수동으로 설정해야 합니다.  
  
 **비교 플래그**  
 문자열 비교 옵션에 대한 자세한 내용은 [문자열 데이터 비교](../../../integration-services/data-flow/comparing-string-data.md)를 참조하세요.  
  
 **중복되는 정렬 값이 있는 행 제거**  
 지정한 문자열 비교 옵션을 기반으로 변환에서 중복 행을 변환 출력에 복사할 것인지, 아니면 모든 중복에 대한 단일 항목을 만들 것인지를 나타냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
