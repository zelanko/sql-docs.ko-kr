---
title: "사용자 정의 계층 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 28210f8ed93af087c1eb4bdf20c54fbdf842139e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="user-defined-hierarchies---create"></a>사용자 정의 계층-만들기
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 사용자 정의 계층 구조를 만들 수 있습니다. 계층은 특성을 기반으로 하는 수준 모음입니다. 예를 들어 시간 계층에는 년, 분기, 월, 주 및 일 수준이 포함될 수 있습니다. 각 멤버 특성이 상위 멤버 특성을 고유하게 내재하고 있는 계층도 있는데 이를 자연 계층이라고 합니다. 최종 사용자가 계층을 사용하여 큐브 데이터를 검색할 수 있습니다. 계층은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 차원 디자이너의 계층 창을 사용하여 정의합니다.  
  
 사용자 정의 계층 구조를 만들 때 *비정형*계층 구조가 될 수 있습니다. 비정형 계층에서는 최소한 한 멤버의 논리적 부모 멤버가 해당 멤버 바로 위 수준에 있지 않습니다. 비정형 계층일 경우 누락된 멤버 표시 여부와 누락된 멤버 표시 방법을 제어하는 설정이 있습니다. 자세한 내용은 [비정형 계층 구조](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md)를 참조하세요.  
  
> [!NOTE]  
>  사용자 정의 계층 구조의 디자인 및 구성과 관련된 성능 문제에 대한 자세한 내용은 [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(SQL Server 2005 Analysis Services 성능 가이드)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 계층 속성](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [수준 속성-사용자 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [부모-자식 차원](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  
