---
title: For 루프 컨테이너 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.forloopcontainerdetails.f1
helpviewer_keywords:
- repeating control flow
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: 44cf7355-992b-4bbf-a28c-bfb012de06f6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ec872407dbec3885f72c4300b90cb3e11d1bcf92
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433040"
---
# <a name="for-loop-container"></a>For 루프 컨테이너
  For 루프 컨테이너는 패키지의 반복 제어 흐름을 정의합니다. 루프 구현은 프로그래밍 언어에서의 **For** 루프 구조와 유사합니다. For 루프 컨테이너는 각 루프를 반복할 때마다 식을 계산하고 식이 `False`가 될 때까지 워크플로를 반복합니다.  
  
 For 루프 컨테이너는 다음 요소를 사용하여 루프를 정의합니다.  
  
-   루프 카운터에 값을 할당하는 초기화 식(옵션)  
  
-   루프를 중지 또는 계속할지를 테스트하는 식이 포함된 계산 식  
  
-   루프 카운터를 증가 또는 감소시키는 반복 식(옵션)  
  
 다음 다이어그램에서는 메일 보내기 태스크를 사용한 For 루프 컨테이너를 보여 줍니다. 초기화 식이 `@Counter = 0`이고 계산 식이 `@Counter < 4`이고 반복 식이 `@Counter = @Counter + 1`이면 루프가 4번 반복되어 4개의 전자 메일 메시지를 보냅니다.  
  
 ![한 태스크를 4번 반복하는 For 루프 컨테이너](../media/ssis-forloop.gif "한 태스크를 4번 반복하는 For 루프 컨테이너")  
  
 식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 유효한 식이어야 합니다.  
  
 초기화 식과 대입 식을 만들려면 대입 연산자(=)를 사용할 수 있습니다. 이 연산자는 Integration Services 식 문법에서 다른 용도로 지원되지 않으며 For 루프 컨테이너의 초기화 및 대입 식 유형에만 사용할 수 있습니다. 대입 연산자를 사용 하는 식에는 구문이 있어야 합니다 `@Var = <expression>` . 여기서 **Var** 은 런타임 변수이 고 \<expression> 은 식 구문의 규칙을 따르는 식입니다 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] . 식은 변수, 리터럴 및 SSIS 식 문법에서 지원하는 모든 연산자와 함수를 포함할 수 있습니다. 변수의 데이터 형식으로 캐스팅할 수 있는 데이터 형식으로 식이 계산되어야 합니다.  
  
 For 루프 컨테이너는 하나의 계산 식만 포함할 수 있습니다. 따라서 For 루프 컨테이너는 모든 제어 흐름 요소를 동일한 횟수만큼 실행합니다. For 루프 컨테이너에 다른 For 루프 컨테이너가 포함될 수 있으므로 중첩 루프를 만들고 패키지에 복잡한 루프를 구현할 수 있습니다.  
  
 For 루프 컨테이너의 트랜잭션 속성을 설정하여 패키지 제어 흐름의 하위 집합에 대해 트랜잭션을 정의할 수 있습니다. 이러한 방식으로 보다 세부적으로 트랜잭션을 관리할 수 있습니다. 예를 들어 For 루프 컨테이너가 테이블의 데이터를 업데이트하는 제어 흐름을 여러 번 반복하는 경우 For 루프와 해당 제어 흐름에서 트랜잭션을 사용하여 모든 데이터가 성공적으로 업데이트되지 않으면 데이터가 업데이트되지 않도록 구성할 수 있습니다. 자세한 내용은 [Integration Services 트랜잭션](../integration-services-transactions.md)을 참조하세요.  
  
## <a name="configuration-of-the-for-loop-container"></a>For 루프 컨테이너 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [For 루프 편집기](../for-loop-editor.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 프로그래밍 방식으로 이러한 속성을 설정하는 방법은 개발자 가이드에서 **T:Microsoft.SqlServer.Dts.Runtime.ForLoop** 클래스에 대한 설명서를 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
 For 루프 컨테이너를 구성하는 방법은 다음 항목을 참조하십시오.  
  
-   [For 루프 컨테이너 구성](for-loop-container.md)  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>참고 항목  
 [제어 흐름](control-flow.md)   
 [Integration Services&#40;SSIS&#41; 식](../expressions/integration-services-ssis-expressions.md)  
  
  
