---
title: 조건부 분할 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittrans.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dcfbbac9eacc96384a723088cf8f20cc939bdc48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900827"
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
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에는 입력 데이터를 평가하고 출력 데이터를 전달하는 식을 만들 때 사용할 수 있는 함수와 연산자가 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../expressions/integration-services-ssis-expressions.md)가 될 때까지 워크플로를 반복합니다.  
  
 조건부 분할 변환은 `FriendlyExpression` 사용자 지정 속성을 포함합니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [패키지에서 속성 식 사용](../../expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](transformation-custom-properties.md)을 참조하세요.  
  
 이 변환에는 하나의 입력, 여러 출력 및 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **조건부 분할 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Conditional Split Transformation Editor](../../conditional-split-transformation-editor.md)를 참조하십시오.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [변환 사용자 지정 속성](transformation-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [조건부 분할 변환을 사용하여 데이터 세트 분할](conditional-split-transformation.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [조건부 분할 변환을 사용하여 데이터 세트 분할](conditional-split-transformation.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 흐름](../data-flow.md)   
 [Integration Services 변환](integration-services-transformations.md)  
  
  
