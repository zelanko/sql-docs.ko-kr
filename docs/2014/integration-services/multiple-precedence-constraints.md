---
title: 여러 선행 제약 조건 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
caps.latest.revision: 44
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 60cd55a656849f3cb5eee9cac879a88d8d85ad4e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231467"
---
# <a name="multiple-precedence-constraints"></a>여러 선행 제약 조건
  선행 제약 조건은 두 개의 태스크, 두 개의 컨테이너 또는 각 태스크와 컨테이너를 하나씩 선택하여 두 개의 실행 개체를 참조합니다. 선행 제약 조건을 선행 실행 개체 및 제약 조건이 지정된 실행 개체라고 합니다. 제약 조건이 지정된 실행 개체에는 여러 선행 제약 조건이 포함될 수 있습니다. 자세한 내용은 [Precedence Constraints](control-flow/precedence-constraints.md)을 참조하세요.  
  
 제약 조건을 그룹화하여 복잡한 제약 조건 시나리오를 조합하면 패키지에 복잡한 제어 흐름을 구현할 수 있습니다. 예를 들어, 다음 그림에서 태스크 D는 태스크 A에 연결 하 여는 `Success` 의해 태스크 B에 연결 된 제약 조건, 태스크 D는 `Failure` 의해 태스크 C에 연결 된 제약 조건 및 태스크 D는 `Success` 제약 조건. 태스크 D와 태스크 A 사이의 선행 제약 조건, 태스크 D와 태스크 B 사이의 선행 제약 조건 및 태스크 D와 태스크 C 사이의 선행 제약 조건은 논리적 *AND* 관계에 있습니다. 따라서 태스크 D를 실행하려면 태스크 A와 태스크 C는 성공적으로 실행되어야 하고 태스크 B는 실패해야 합니다.  
  
 ![선행 제약 조건으로 연결된 태스크](media/precedenceconstraints.gif "선행 제약 조건으로 연결된 태스크")  
  
## <a name="logicaland-property"></a>LogicalAnd 속성  
 태스크 또는 컨테이너에 여러 제약 조건이 있는 경우 `LogicalAnd` 속성은 선행 제약 조건이 그 자체로만 평가되는지 또는 다른 제약 조건과 함께 평가되는지 여부를 지정합니다.  
  
 설정할 수 있습니다는 `LogicalAnd` 사용 하 여 속성을 **선행 제약 조건 편집기** 에서 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너 또는 속성 창에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 제공 합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [선행 제약 조건의 속성 설정](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  
