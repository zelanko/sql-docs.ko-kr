---
title: 파생 열 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.derivedcolumntrans.f1
- sql13.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 11848095ae04a257063601dc41aa8f146386775f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="derived-column-transformation"></a>파생 열 변환
  파생 열 변환은 변환 입력 열에 식을 적용하여 새로운 열 값을 만듭니다. 변환 입력의 변수, 함수, 연산자 및 열의 모든 조합이 식에 포함될 수 있습니다. 결과는 새 열로 추가하거나 기존 열에 대체 값으로 삽입할 수 있습니다. 파생 열 변환은 여러 개의 파생 열을 정의할 수 있으며 임의의 변수 또는 입력 열이 여러 개의 식에 사용될 수 있습니다.  
  
 이 변환을 사용하여 다음 태스크를 수행할 수 있습니다.  
  
-   여러 열의 데이터를 하나의 파생 열로 연결합니다. 예를 들어 식 **을 사용하여** FirstName **열과** LastName **열의 값을**FullName `FirstName + " " + LastName`이라는 단일 파생 열로 결합할 수 있습니다.  
  
-   SUBSTRING과 같은 함수를 사용하여 문자열 데이터에서 문자를 추출한 다음 결과를 파생 열에 저장합니다. 예를 들어 식 **을 사용하여** FirstName `SUBSTRING(FirstName,1,1)`열에서 특정인의 이니셜을 추출할 수 있습니다.  
  
-   숫자 데이터에 수치 연산 함수를 적용하고 계산 결과를 파생 열에 저장합니다. 예를 들어 식 **를 사용하여 숫자 열**SalesTax `ROUND(SalesTax, 2)`의 길이와 전체 자릿수를 소수 두 자리 수로 변경할 수 있습니다.  
  
-   입력 열과 변수를 비교하는 식을 만듭니다. 예를 들어 식 **을 사용하여 변수** Version **을**ProductVersion **열의 데이터와 비교하고 비교 결과에 따라** Version **또는**ProductVersion `ProductVersion == @Version? ProductVersion : @Version`중 하나의 값을 사용할 수 있습니다.  
  
-   datetime 값의 일부를 추출합니다. 예를 들어 식 `DATEPART("year",GETDATE())`를 사용하여 GETDATE 및 DATEPART 함수로 현재 연도를 추출할 수 있습니다.  
  
-   식을 사용하여 날짜 문자열을 특정 형식으로 변환합니다.  
  
## <a name="configuration-of-the-derived-column-transformation"></a>파생 열 변환 구성  
 다음과 같은 방법으로 파생 열 변환을 구성할 수 있습니다.  
  
-   변경될 각 입력 열이나 새 열에 대한 식을 제공합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
    > [!NOTE]  
    >  파생 열 변환에서 덮어쓰는 입력 열을 참조하는 식은 파생 값이 아닌 원래 열 값을 사용합니다.  
  
-   새 열에 결과를 추가하고 데이터 형식이 **string**인 경우 코드 페이지를 지정합니다. 자세한 내용은 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)을 참조하세요.  
  
 파생 열 변환에는 FriendlyExpression 사용자 지정 속성이 포함됩니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [패키지에서 속성 식 사용](../../../integration-services/expressions/use-property-expressions-in-packages.md)및 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 일반 출력 및 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [파생 열 변환을 사용하여 열 값 파생](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
## <a name="derived-column-transformation-editor"></a>파생 열 변환 편집기
  **파생 열 변환 편집기** 대화 상자를 사용하여 새 열 또는 대체 열을 채우는 식을 만들 수 있습니다.  
  
### <a name="options"></a>변수  
 **변수 및 열**  
 사용 가능한 변수 및 열 목록에서 아래 창의 기존 테이블 행이나 목록 아래쪽의 새 행으로 변수 또는 열을 끌어 변수 또는 입력 열을 사용하는 식을 작성합니다.  
  
 **함수 및 연산자**  
 목록에서 아래 창으로 함수와 연산자를 끌어 함수 또는 연산자를 사용하여 입력 데이터와 직접 출력 데이터를 계산하는 식을 작성합니다.  
  
 **파생 열 이름**  
 파생 열의 이름을 지정합니다. 기본값은 번호가 매겨진 파생 열 목록이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 **파생 열**  
 목록에서 파생 열을 선택합니다. 파생 열을 새 출력 열로 추가할지, 아니면 기존 열의 데이터를 바꿀지를 선택합니다.  
  
 **식**  
 식을 입력하거나 사용 가능한 열, 변수, 함수 및 연산자에 대한 이전 목록에서 끌어 식을 작성합니다.  
  
 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md), [연산자&#40;SSIS 식&#41;](../../../integration-services/expressions/operators-ssis-expression.md) 및 [함수&#40;SSIS 식&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **데이터 형식**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 식을 자동으로 계산하고 데이터 형식을 적절하게 설정합니다. 이 열의 값은 읽기 전용입니다. 자세한 내용은 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 **길이**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 식을 자동으로 계산하고 문자열 데이터의 열 길이를 설정합니다. 이 열의 값은 읽기 전용입니다.  
  
 **정밀도**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 데이터 형식을 기반으로 숫자 데이터의 전체 자릿수를 자동으로 설정합니다. 이 열의 값은 읽기 전용입니다.  
  
 **소수 자릿수**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 데이터 형식을 기반으로 숫자 데이터의 소수 자릿수를 자동으로 설정합니다. 이 열의 값은 읽기 전용입니다.  
  
 **코드 페이지**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 DT_STR 데이터 형식에 대한 코드 페이지를 자동으로 설정합니다. **코드 페이지**를 업데이트할 수 있습니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 대화 상자를 사용하여 오류 처리 방법을 지정합니다.  
  
## <a name="related-content"></a>관련 내용  
 social.technet.microsoft.com의 기술 문서 - [SSIS 식 예](http://go.microsoft.com/fwlink/?LinkId=220761)  
