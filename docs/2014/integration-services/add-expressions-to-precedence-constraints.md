---
title: 선행 제약 조건에 식을 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence executables [Integration Services]
- precedence constraints [Integration Services], adding expressions
- adding expressions
- constrained executables [Integration Services]
- combining constraints
- expressions [Integration Services], constraints
ms.assetid: 5574d89a-a68e-4b84-80ea-da93305e5ca1
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fee423c1000d2be7ebc70f2cfb40e3d83ba24150
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370985"
---
# <a name="add-expressions-to-precedence-constraints"></a>선행 제약 조건에 식 추가
  선행 제약 조건에서는 식을 사용하여 선행 실행 개체 및 제약 조건이 지정된 실행 개체 간의 제약 조건을 정의할 수 있습니다. 실행 개체는 태스크 또는 컨테이너일 수 있습니다. 식은 단독으로 사용되거나 선행 실행 개체의 실행 결과와 함께 사용될 수 있습니다. 실행 개체의 실행 결과는 성공 또는 실패입니다. 선행 제약 조건의 실행 결과를 구성할 경우 `Success`, `Failure` 또는 `Completion`으로 실행 결과를 지정할 수 있습니다. `Success`로 설정하려면 선행 실행 개체가 성공해야 하며, `Failure`는 선행 실행 개체가 실패해야 하며, `Completion`은 선행 태스크의 성공 또는 실패 여부에 관계없이 제약 조건이 지정된 실행 개체가 실행되어야 함을 나타냅니다.  자세한 내용은 [Precedence Constraints](control-flow/precedence-constraints.md)을(를) 참조하세요.  
  
 식은 `True` 또는 `False`로 계산되어야 하며 유효한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 식이어야 합니다. 식에서는 문자, 시스템 및 사용자 지정 변수와 [!INCLUDE[ssIS](../includes/ssis-md.md)] 식 문법에서 제공하는 함수와 연산자를 사용할 수 있습니다. 예를 들어 `@Count == SQRT(144) + 10` 식에서는 `Count` 변수, SQRT 함수 및 등호(==)와 더하기(+) 연산자가 사용되었습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md)가 될 때까지 워크플로를 반복합니다.  
  
 다음 그림에서 태스크 A와 태스크 B는 실행 결과와 식을 사용하는 선행 제약 조건으로 연결되어 있습니다. 제약 조건 값은 `Success`로 설정되었으며 식은 `@X >== @Z`입니다. 제약 조건이 지정된 태스크 B는 태스크 A가 성공적으로 완료되고 변수 `X`의 값이 변수 `Z`의 값보다 크거나 같은 경우에만 실행됩니다.  
  
 ![두 태스크 간 선행 제약 조건](media/mw-dts-03.gif "두 태스크 간 선행 제약 조건")  
  
 실행 개체는 또한 여러 식이 포함된 여러 선행 제약 조건을 사용하여 연결될 수 있습니다. 예를 들어 다음 그림에서 태스크 B와 C는 실행 결과와 식을 사용하는 선행 제약 조건에 의해 태스크 A에 연결됩니다. 두 제약 조건 값은 모두 `Success.`로 설정됩니다. 하나의 선행 제약 조건에는 식 `@X >== @Z`가 포함되고 다른 선행 제약 조건에는 식 `@X < @Z`가 포함됩니다. 변수 `X`와 변수 `Z`의 값에 따라 태스크 C 또는 태스크 B가 실행됩니다.  
  
 ![선행 제약 조건의 식](media/mw-dts-04.gif "선행 제약 조건의 식")  
  
 **디자이너에서** 선행 제약 조건 편집기 [!INCLUDE[ssIS](../includes/ssis-md.md)] 를 사용하거나 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서 제공하는 속성 창을 사용하여 식을 추가하거나 수정할 수 있습니다. 하지만 속성 창에는 식 구문에 대한 검사 기능이 제공되지 않습니다.  
  
 선행 제약 조건에 식이 포함되는 경우 **제어 흐름** 탭의 디자인 화면에서 선행 제약 조건 옆에 아이콘이 표시되고 아이콘의 도구 설명에 해당 식이 표시됩니다.  
  
## <a name="combining-execution-values-and-expressions"></a>실행 값과 식 조합  
 다음 표에서는 선행 제약 조건에서 실행 값 제약 조건과 식을 조합한 결과에 대해 설명합니다.  
  
|평가 작업|제약 조건 계산 결과|식 계산 결과|제약 조건이 지정된 실행 개체 실행|  
|--------------------------|-----------------------------|-----------------------------|---------------------------------|  
|제약 조건|True|해당 사항 없음|True|  
|제약 조건|False|해당 사항 없음|False|  
|식|해당 사항 없음|True|True|  
|식|해당 사항 없음|False|False|  
|제약 조건 및 식|True|True|True|  
|제약 조건 및 식|True|False|False|  
|제약 조건 및 식|False|True|False|  
|제약 조건 및 식|False|False|False|  
|제약 조건 또는 식|True|True|True|  
|제약 조건 또는 식|True|False|True|  
|제약 조건 또는 식|False|True|True|  
|제약 조건 또는 식|False|False|False|  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>선행 제약 조건에 식을 추가하려면  
  
-   [선행 제약 조건에서 식 사용](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
-   [선행 제약 조건의 속성 설정](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
## <a name="external-resources"></a>외부 리소스  
 social.technet.microsoft.com의 기술 문서 - [SSIS 식 예](https://go.microsoft.com/fwlink/?LinkId=220761)  
  
## <a name="see-also"></a>관련 항목:  
 [여러 선행 제약 조건](../../2014/integration-services/multiple-precedence-constraints.md)   
 [선행 제약 조건](control-flow/precedence-constraints.md)  
  
  
