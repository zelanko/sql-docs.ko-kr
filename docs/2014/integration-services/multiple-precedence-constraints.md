---
title: 여러 선행 제약 조건 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c0b75b96f30d2fe7f104e8f59aa03d7de6202e6a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66057407"
---
# <a name="multiple-precedence-constraints"></a>여러 선행 제약 조건
  선행 제약 조건은 두 개의 태스크, 두 개의 컨테이너 또는 각 태스크와 컨테이너를 하나씩 선택하여 두 개의 실행 개체를 참조합니다. 선행 제약 조건을 선행 실행 개체 및 제약 조건이 지정된 실행 개체라고 합니다. 제약 조건이 지정된 실행 개체에는 여러 선행 제약 조건이 포함될 수 있습니다. 자세한 내용은 [Precedence Constraints](control-flow/precedence-constraints.md)을(를) 참조하세요.  
  
 제약 조건을 그룹화하여 복잡한 제약 조건 시나리오를 조합하면 패키지에 복잡한 제어 흐름을 구현할 수 있습니다. 예를 들어 다음 그림에서 태스크 D는 `Success` 제약 조건에 의해 태스크 A에 연결되며 태스크 D는 다시 `Failure` 제약 조건에 의해 태스크 B에 연결되고, 태스크 D는 `Success` 제약 조건에 의해 태스크 C에 연결됩니다. 태스크 D와 태스크 A 사이의 선행 제약 조건, 태스크 D와 태스크 B 사이의 선행 제약 조건 및 태스크 D와 태스크 C 사이의 선행 제약 조건은 논리적 *AND* 관계에 있습니다. 따라서 태스크 D를 실행하려면 태스크 A와 태스크 C는 성공적으로 실행되어야 하고 태스크 B는 실패해야 합니다.  
  
 ![선행 제약 조건으로 연결된 태스크](media/precedenceconstraints.gif "선행 제약 조건으로 연결된 태스크")  
  
## <a name="logicaland-property"></a>LogicalAnd 속성  
 태스크 또는 컨테이너에 여러 제약 조건이 있는 경우 `LogicalAnd` 속성은 선행 제약 조건이 그 자체로만 평가되는지 또는 다른 제약 조건과 함께 평가되는지 여부를 지정합니다.  
  
 디자이너 `LogicalAnd` [!INCLUDE[ssIS](../includes/ssis-md.md)] 에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] **선행 제약 조건 편집기** 를 사용 하거나에서 제공 하는 속성 창을 사용 하 여 속성을 설정할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [선행 제약 조건의 속성 설정](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  
