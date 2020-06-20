---
title: 제어 흐름에 열거 추가 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding enumerations
- Foreach Loop containers
- control flow [Integration Services], enumerations
- repeating workflows
- enumerations [Integration Services]
ms.assetid: f212b5fb-3cc4-422e-9b7c-89eb769a812a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bff127798f7c36340a85fa72cebfdc9a012c0676
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84926104"
---
# <a name="add-enumeration-to-a-control-flow"></a>제어 흐름에 열거 추가
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에는 패키지의 제어 흐름에 파일 및 개체를 열거하는 루핑 구성을 간단하게 포함시킬 수 있는 제어 흐름 요소인 Foreach 루프 컨테이너가 포함됩니다. 자세한 내용은 [Foreach 루프 컨테이너](control-flow/foreach-loop-container.md)을 참조하십시오.  
  
 Foreach 루프 컨테이너는 특정 기능을 제공하는 것이 아니라 반복 가능한 제어 흐름을 작성하고, 열거자 유형을 지정하고, 열거자를 구성할 수 있는 구조만 제공합니다. 컨테이너 기능을 제공하려면 적어도 하나 이상의 태스크를 Foreach 루프 컨테이너에 포함시켜야 합니다. 자세한 내용은 [Integration Services Tasks](control-flow/integration-services-tasks.md)을(를) 참조하세요.  
  
 Foreach 루프 컨테이너에는 여러 태스크가 포함된 제어 흐름과 다른 컨테이너가 포함될 수 있습니다. Foreach 루프 컨테이너에 태스크 및 컨테이너를 추가하는 방법은 패키지에 추가하는 방법과 비슷하며, 태스크 및 컨테이너를 패키지가 아닌 Foreach 루프 컨테이너로 끌어 온다는 점만 다릅니다. Foreach 루프 컨테이너에 두 개 이상의 태스크 또는 컨테이너가 포함된 경우 패키지에서와 같은 방식으로 선행 제약 조건을 사용하여 이를 연결할 수 있습니다. 자세한 내용은 [Precedence Constraints](control-flow/precedence-constraints.md)을(를) 참조하세요.  
  
### <a name="to-implement-a-foreach-loop-container-in-a-control-flow"></a>제어 흐름에서 Foreach 루프 컨테이너를 구현하려면  
  
1.  패키지에 Foreach 루프 컨테이너를 추가합니다. 자세한 내용은 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md) 를 참조 하세요.  
  .  
  
2.  Foreach 루프 컨테이너에 태스크 및 컨테이너를 추가합니다. 자세한 내용은 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md) 를 참조 하세요.  
  .  
  
3.  선행 제약 조건을 사용하여 Foreach 루프 컨테이너에 있는 태스크 및 컨테이너를 연결합니다. 자세한 내용은 [기본 선행 제약 조건을 사용하여 태스크 및 컨테이너 연결](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)을 참조하세요.  
  
4.  Foreach 루프 컨테이너를 구성합니다. 자세한 내용은 [Foreach 루프 컨테이너 구성](../../2014/integration-services/configure-a-foreach-loop-container.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [구성 요소 그룹화 또는 그룹 해제](group-or-ungroup-components.md)   
 [선행 제약 조건](control-flow/precedence-constraints.md)   
 [제어 흐름에 반복 추가](add-iteration-to-a-control-flow.md)   
 [제어 흐름](control-flow/control-flow.md)  
  
  
