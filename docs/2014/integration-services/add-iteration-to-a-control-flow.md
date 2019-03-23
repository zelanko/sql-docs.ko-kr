---
title: 제어 흐름에 반복 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- repeating workflows
- adding iterations
- control flow [Integration Services], iterations
- expressions [Integration Services], control flow
- iterations [Integration Services]
- For Loop containers
ms.assetid: eb3a7494-88ae-4165-9d0f-58715eb1734a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 26c555b22ae219eeec9e0b1670f407c2504ac7f7
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389251"
---
# <a name="add-iteration-to-a-control-flow"></a>제어 흐름에 반복 추가
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에는 패키지의 제어 흐름에서 조건에 따라 반복되는 루프를 간단하게 포함시킬 수 있는 제어 흐름 요소인 For 루프 컨테이너가 포함됩니다. 자세한 내용은 [For 루프 컨테이너](control-flow/for-loop-container.md)가 될 때까지 워크플로를 반복합니다.  
  
 For 루프 컨테이너는 루프가 반복될 때마다 조건을 평가하고 조건이 False이면 중지합니다. For 루프 컨테이너에는 루프를 초기화하고, 반복되는 제어 흐름의 실행을 중지하는 평가 조건을 지정하고, 평가 조건을 비교할 값을 업데이트하는 식에 값을 대입하는 식이 포함됩니다. 평가 조건은 필수 항목이지만 초기화 및 대입 식은 선택 항목입니다.  
  
 For 루프 컨테이너는 기능을 제공하는 것이 아니고 반복할 수 있는 제어 흐름을 만드는 구조만 제공합니다. 컨테이너 기능을 제공하려면 적어도 하나 이상의 태스크를 For 루프 컨테이너에 포함시켜야 합니다. 자세한 내용은 [Integration Services Tasks](control-flow/integration-services-tasks.md)를 참조하세요.  
  
 For 루프 컨테이너에는 여러 태스크가 포함된 제어 흐름과 다른 컨테이너가 포함될 수 있습니다. For 루프 컨테이너에 태스크 및 컨테이너를 추가하는 방법은 패키지에 추가하는 방법과 비슷하며, 태스크 및 컨테이너를 패키지가 아닌 For 루프 컨테이너로 끌어 온다는 점만 다릅니다. For 루프 컨테이너에 두 개 이상의 태스크 또는 컨테이너가 포함된 경우 패키지에서와 같은 방식으로 선행 제약 조건을 사용하여 이를 연결할 수 있습니다. 자세한 내용은 [Precedence Constraints](control-flow/precedence-constraints.md)을(를) 참조하세요.  
  
## <a name="using-expressions-in-for-loop-configuration"></a>For 루프 구성에서 식 사용  
 평가 조건, 초기화 값 또는 대입 식을 지정하여 For 루프 컨테이너를 구성할 때는 문자 또는 식을 사용할 수 있습니다.  
  
 식에는 변수가 포함될 수 있습니다. 변수를 사용하면 런타임 시 값을 업데이트하여 패키지를 보다 유연하고 쉽게 관리할 수 있습니다. 식의 최대 길이는 4000자입니다.  
  
 식에서 변수를 지정할 때는 변수 이름 앞에 @ 기호를 사용해야 합니다. 명명 된 변수에 대 한 예를 들어 `Counter`, 입력 @Counter For 루프 컨테이너를 사용 하는 식에 있습니다. 변수에 네임스페이스 속성을 포함시키려면 변수와 네임스페이스를 괄호로 묶어야 합니다. 예를 `Counter` 변수를 `MyNamespace` 네임 스페이스, 형식 [@MyNamespace::Counter].  
  
 For 루프 컨테이너에서 사용되는 변수는 For 루프 컨테이너의 범위 또는 패키지 컨테이너 계층에서 높은 수준의 컨테이너 범위에 정의되어 있어야 합니다. 예를 들어 For 루프 컨테이너는 자체 범위에 정의된 변수와 패키지 범위에 정의된 변수를 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../../2014/integration-services/use-variables-in-packages.md)을 참조하세요.  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 식 문법에는 평가, 초기화 및 대입에 사용되는 복잡한 식을 구현할 수 있는 완벽한 연산자 및 함수가 제공됩니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md)가 될 때까지 워크플로를 반복합니다.  
  
### <a name="to-implement-a-for-loop-container-in-a-control-flow"></a>제어 흐름에서 For 루프 컨테이너를 구현하려면  
  
1.  패키지에 For 루프 컨테이너를 추가합니다. 자세한 내용은 참조 하세요. [작업 또는 제어 흐름 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  의 동일한 원격 인스턴스에 있는 경우 master 데이터베이스는 여러 보조 데이터베이스를 사용할 수 있습니다.  
  
2.  For 루프 컨테이너에 태스크 및 컨테이너를 추가합니다. 자세한 내용은 참조 하세요. [작업 또는 제어 흐름 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  의 동일한 원격 인스턴스에 있는 경우 master 데이터베이스는 여러 보조 데이터베이스를 사용할 수 있습니다.  
  
3.  선행 제약 조건을 사용하여 For 루프 컨테이너에 있는 태스크 및 컨테이너를 연결합니다. 자세한 내용은 [기본 선행 제약 조건을 사용하여 태스크 및 컨테이너 연결](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)을 참조하세요.  
  
4.  For 루프 컨테이너를 구성합니다. 자세한 내용은 [For 루프 컨테이너 구성](../../2014/integration-services/configure-a-for-loop-container.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [그룹 또는 그룹 해제 구성 요소](group-or-ungroup-components.md)   
 [기본 선행 제약 조건을 사용하여 태스크 및 컨테이너 연결](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [제어 흐름에 열거 추가](../../2014/integration-services/add-enumeration-to-a-control-flow.md)   
 [제어 흐름](control-flow/control-flow.md)  
  
  
