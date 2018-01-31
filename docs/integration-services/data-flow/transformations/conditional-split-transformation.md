---
title: "조건부 분할 변환 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.conditionalsplittrans.f1
- sql13.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 751ca45d923265f7477aa7461cd24c87e3d0d41a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="conditional-split-transformation"></a>조건부 분할 변환
  조건부 분할 변환은 데이터 내용에 따라 각 데이터 행을 서로 다른 출력으로 라우팅할 수 있습니다. 조건부 분할 변환의 구현은 프로그래밍 언어의 CASE 의사 결정 구조와 유사합니다. 이 변환은 식을 평가한 후 평가 결과를 기준으로 데이터 행을 지정된 출력으로 보냅니다. 기본 출력도 제공되므로 일치하는 식이 없을 경우 행을 기본 출력으로 보냅니다.  
  
## <a name="configuration-of-the-conditional-split-transformation"></a>조건부 분할 변환 구성  
 다음과 같은 방법으로 조건부 분할 변환을 구성할 수 있습니다.  
  
-   변환에서 테스트할 각 조건에 대해 부울로 평가되는 식을 제공합니다.  
  
-   조건 평가 순서를 지정합니다. True가 되는 첫 번째 조건에 따라 행을 출력으로 보내기 때문에 순서가 중요합니다.  
  
-   변환에 기본 출력을 지정합니다. 이 변환은 기본 출력을 지정해야 합니다.  
  
 각 입력 행은 true가 되는 첫 번째 조건의 출력 한 개로만 보낼 수 있습니다. 예를 들어 다음 조건은 **A** 문자로 시작하는 *FirstName* 열의 모든 행을 특정 출력으로 보내고 *B* 문자로 시작하는 행을 다른 출력으로 보내고 다른 모든 행을 기본 출력으로 보냅니다.  
  
 출력 1  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 출력 2  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에는 입력 데이터를 평가하고 출력 데이터를 전달하는 식을 만들 때 사용할 수 있는 함수와 연산자가 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
 조건부 분할 변환은 **FriendlyExpression** 사용자 지정 속성을 포함합니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [패키지에서 속성 식 사용](../../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하세요.  
  
 이 변환에는 하나의 입력, 여러 출력 및 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [조건부 분할 변환을 사용하여 데이터 집합 분할](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [조건부 분할 변환을 사용하여 데이터 집합 분할](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
## <a name="conditional-split-transformation-editor"></a>조건부 분할 변환 편집기
  **조건부 분할 변환 편집기** 대화 상자를 사용하여 식을 만들고, 식을 평가하는 순서를 설정하고, 조건부 분할 출력의 이름을 지정할 수 있습니다. 이 대화 상자에는 식을 작성할 때 사용할 수 있는 수치 연산, 문자열 및 날짜/시간 함수와 연산자가 포함되어 있습니다. True로 평가하는 첫 번째 조건에 따라 행을 전송할 출력이 결정됩니다.  
  
> [!NOTE]  
>  조건부 분할 변환에서는 각 입력 행을 하나의 출력에만 전송합니다. 여러 조건을 입력하는 경우 조건부 분할 변환에서는 각 행을 조건이 True가 되는 첫 번째 출력으로 전송하고 해당 행에 대한 다른 조건은 무시합니다. 여러 조건을 연속적으로 평가해야 하는 경우 조건부 분할 변환을 데이터 흐름에서 연결해야 합니다.  
  
### <a name="options"></a>변수  
 **주문**  
 행을 선택하고 오른쪽의 화살표 키를 사용하여 식을 평가하는 순서를 변경합니다.  
  
 **출력 이름**  
 출력 이름을 입력합니다. 기본값은 번호가 매겨진 사례 목록이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 **조건**  
 식을 입력하거나 사용 가능한 열, 변수, 함수 및 연산자 목록에서 끌어 식을 작성합니다.  
  
 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md), [연산자&#40;SSIS 식&#41;](../../../integration-services/expressions/operators-ssis-expression.md) 및 [함수&#40;SSIS 식&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **기본 출력 이름**  
 기본 출력의 이름을 입력하거나 기본값을 사용합니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 대화 상자를 사용하여 오류 처리 방법을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
