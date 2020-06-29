---
title: 선행 제약 조건 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- control flow [Integration Services], precedence constraints
- precedence constraints [Integration Services]
- constraints [Integration Services]
- sequence execution options [Integration Services]
- containers [Integration Services], precedence constraints
ms.assetid: c5ce5435-fd89-4156-a11f-68470a69aa9f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14fd00565c011b04c28345faca8ee5db5ae821f9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438200"
---
# <a name="precedence-constraints"></a>선행 제약 조건
  선행 제약 조건은 패키지에 있는 실행 개체, 컨테이너 및 태스크를 제어 흐름으로 연결하고 실행 개체의 실행 여부를 결정하는 조건을 지정합니다. 실행 개체는 For 루프, Foreach 루프 또는 시퀀스 컨테이너나 태스크 또는 이벤트 처리기일 수 있습니다. 또한 이벤트 처리기에서는 해당 실행 개체를 제어 흐름으로 연결하기 위해 선행 제약 조건이 사용됩니다.

 선행 제약 조건은 선행 실행 개체 및 제약 조건이 지정된 실행 개체의 두 실행 개체를 연결합니다. 선행 실행 개체는 제약 조건이 지정된 실행 개체 전에 실행되며, 선행 실행 개체의 실행 결과로 제약 조건이 지정된 실행 개체의 실행 여부가 결정될 수 있습니다. 다음 다이어그램에서는 선행 제약 조건으로 연결된 두 개의 실행 개체를 보여 줍니다.

 ![선행 제약 조건으로 연결된 실행 파일](../media/ssis-pcsimple.gif "선행 제약 조건으로 연결된 실행 파일")

 분기가 없는 선형 제어 흐름에서 선행 제약 조건은 태스크가 실행되는 시퀀스를 단독으로 제어합니다. 제어 흐름이 분기되는 경우 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 런타임 엔진은 해당 분기의 바로 다음에 오는 태스크 및 컨테이너에서의 실행 순서를 결정합니다. 런타임 엔진은 또한 제어 흐름에서 연결되지 않은 워크플로 사이의 실행 순서를 결정합니다.

 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 의 중첩된 컨테이너 아키텍처에서는 단일 태스크만 캡슐화하는 태스크 호스트를 제외한 모든 컨테이너에 다른 컨테이너가 포함될 수 있으며, 각 컨테이너에는 고유 제어 흐름이 포함됩니다. For 루프, Foreach 루프 및 시퀀스 컨테이너에는 여러 태스크와 다른 컨테이너가 포함될 수 있으며, 그 아래에도 다시 여러 태스크와 컨테이너가 포함될 수 있습니다. 예를 들어 스크립트 태스크와 시퀀스 컨테이너가 포함된 패키지에 해당 스크립트 태스크 및 시퀀스 컨테이너로 연결되는 선행 제약 조건이 있는 경우를 가정해 보십시오. 시퀀스 컨테이너에는 3개의 스크립트 태스크가 들어 있으며, 해당 선행 제약 조건은 이 3개의 스크립트 태스크를 하나의 제어 흐름으로 연결합니다. 다음 다이어그램에서는 두 개의 중첩 수준이 포함된 패키지의 선행 제약 조건을 보여 줍니다.

 ![패키지의 선행 제약 조건](../media/mw-dts-12.gif "패키지의 선행 제약 조건")

 패키지는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 컨테이너 계층에서 최상위에 있으므로 선행 제약 조건으로 여러 패키지를 연결할 수 없습니다. 하지만 패키지에 패키지 실행 태스크를 추가하고 다른 패키지를 제어 흐름에 간접적으로 연결할 수 있습니다.

 선행 제약 조건은 다음과 같은 방식으로 구성할 수 있습니다.

-   평가 작업을 지정합니다. 선행 제약 조건은 제약 조건 값이나 식 또는 둘을 모두 사용하여 제약 조건이 지정된 실행 개체가 실행되는지 여부를 결정합니다.

-   선행 제약 조건에서 실행 결과가 사용되는 경우 성공, 실패 또는 완료로 실행 결과를 지정할 수 있습니다.

-   선행 제약 조건에 계산 결과가 사용되는 경우 부울로 계산되는 식을 제공할 수 있습니다.

-   선행 제약 조건이 단독으로 계산되는지 아니면 제약 조건이 지정된 실행 개체에 적용되는 다른 제약 조건과 함께 계산되는지 여부를 지정합니다.

## <a name="evaluation-operations"></a>계산 작업
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 는 다음과 같은 계산 작업을 제공합니다.

-   제약 조건이 지정된 실행 개체가 실행되는지 여부를 확인하기 위해 선행 실행 개체의 실행 결과만 사용하는 제약 조건. 선행 실행 개체의 실행 결과는 완료, 성공 또는 실패일 수 있습니다. 이 작업이 기본 작업입니다.

-   제약 조건이 지정된 실행 개체가 실행되는지 여부를 확인하기 위해 계산되는 식. 식이 True로 계산되면 제약 조건이 지정된 실행 개체가 실행됩니다.

-   선행 실행 개체의 실행 결과에 대한 요구 사항과 식을 계산한 반환 결과를 조합하는 제약 조건과 식

-   선행 실행 개체의 실행 결과 또는 식을 계산한 반환 결과를 사용하는 제약 조건과 식

 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 색을 사용하여 선행 제약 조건의 유형을 확인합니다. Success 제약 조건은 녹색, Failure 제약 조건은 빨간색, Completion 제약 조건은 파란색입니다. [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에 제약 조건 유형을 나타내는 텍스트 레이블을 표시하려면 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너의 내게 필요한 옵션 기능을 구성해야 합니다.

 식은 유효한 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 식이어야 하며, 식에는 함수, 연산자, 시스템 변수 및 사용자 지정 변수가 포함될 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../expressions/integration-services-ssis-expressions.md) 및 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md)를 참조하세요.

## <a name="execution-results"></a>실행 결과
 선행 제약 조건에는 다음과 같은 식 결과만 단독으로 사용되거나 식이 함께 사용될 수 있습니다.

-   완료의 경우에는 출력 여부에 관계없이 선행 실행 개체가 완료되어야만 제약 조건이 지정된 실행 개체가 실행됩니다.

-   성공의 경우에는 선행 실행 개체가 성공적으로 완료되어야만 제약 조건이 지정된 실행 개체가 실행됩니다.

-   실패의 경우에는 선행 실행 개체가 실패해야만 제약 조건이 지정된 실행 개체가 실행됩니다.

> [!NOTE]
>  같은 `Precedence Constraint` 컬렉션의 멤버인 선행 제약 조건만 논리적 AND 조건으로 그룹화할 수 있습니다. 예를 들어 두 개의 Foreach 루프 컨테이너의 선행 제약 조건은 조합할 수 없습니다.

## <a name="configuration-of-the-precedence-constraint"></a>선행 제약 조건 구성
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.

 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [선행 제약 조건 편집기](../precedence-constraint-editor.md)를 참조하세요.

 이러한 속성을 프로그래밍 방식으로 설정하는 방법은 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>을 참조하세요.

## <a name="related-tasks"></a>관련 작업
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목 중 하나를 클릭하십시오.

-   [선행 제약 조건의 속성 설정](../set-the-properties-of-a-precedence-constraint.md)

-   [바로 가기 메뉴를 사용하여 선행 제약 조건 값 설정](../set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)

-   [기본 선행 제약 조건을 사용하여 태스크 및 컨테이너 연결](../connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)

     이 항목에서는 선행 제약 조건에 대한 기본 동작을 설정하는 방법과 기본 선행 제약 조건을 사용하여 실행 개체를 연결하는 방법에 대해 설명합니다.

## <a name="related-content"></a>관련 내용
 social.technet.microsoft.com의 기술 문서 - [SSIS 식 예](https://go.microsoft.com/fwlink/?LinkId=220761)

## <a name="see-also"></a>참고 항목
 [선행 제약 조건에](../add-expressions-to-precedence-constraints.md) [여러 선행 제약](../multiple-precedence-constraints.md) 조건에 식 추가


