---
title: 기본 멤버 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6899b40cd317db9d74a426038e7f0201223d9993
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263689"
---
# <a name="define-a-default-member"></a>기본 멤버 정의
  특성의 기본 멤버는 쿼리에 특성 계층이 포함되어 있지 않을 때 식을 평가하는 데 사용됩니다. 기본 멤버는 특성 계층이나 특성 계층의 원본이 되는 특성이 포함된 사용자 계층이 쿼리에 포함될 때마다 무시됩니다. 이는 쿼리에 지정된 멤버가 사용되기 때문입니다.  
  
 특성 계층에 대 한 기본 멤버는 특성 멤버를 지정 하 여 설정 됩니다는 `DefaultMember` 특성 계층에 대 한 속성 값입니다. 차원 디자이너의 차원 구조 탭에서 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 큐브 디자이너의 계산 탭에 있는 큐브의 계산 스크립트에서 이 속성을 설정할 수 있습니다. 또한 차원 보안을 정의할 때 차원 데이터 탭에서 차원에 설정된 기본 멤버를 재정의하는 보안 역할에 대해 `DefaultMember` 속성을 지정할 수 있습니다. 이름 확인 문제가 발생하지 않도록 하려면 큐브에서 두 번 이상 데이터베이스 차원을 참조하는 경우, 큐브의 차원에 데이터베이스의 차원과 다른 이름이 있는 경우 또는 큐브마다 서로 다른 기본 멤버를 보유하려는 경우 큐브의 MDX 스크립트에 기본 멤버를 정의합니다.  
  
 특성의 기본 멤버는 쿼리에 특성이 포함되어 있지 않을 때 식을 평가하는 데 사용됩니다. 지정 된 특성에 대 한 기본 멤버가 `DefaultMember` 속성입니다. 차원의 계층이 쿼리에 포함될 때는 항상 계층의 수준에 해당되는 특성의 모든 기본 멤버가 무시됩니다. 쿼리에 포함된 차원의 계층이 없으면 기본 멤버가 차원의 모든 특성에 사용됩니다.  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>지정된 기본 멤버가 없는 경우 기본 멤버 확인  
 특성 계층에 대해 지정 된 기본 멤버가 없고 특성 계층이 집계 가능 않은 경우 (합니다 `IsAggregatable` 특성에는 속성이로 설정 되어 `True`), (All) 멤버가 기본 멤버입니다. 지정 된 기본 멤버가 없고 특성 계층이 집계 가능 하지 않은 경우 (합니다 `IsAggregatable` 특성에는 속성이로 설정 되어 `False`), 특성 계층의 최상위 수준에서 기본 멤버가 선택 됩니다.  
  
## <a name="specifying-the-default-member"></a>기본 멤버 지정  
 차원의 모든 특성 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 사용 하 여 지정할 수 있는 기본 멤버에는 `DefaultMember` 특성의 속성입니다. 이 설정은 쿼리에 특성이 포함되지 않은 경우 식을 평가하는 데 사용됩니다. 쿼리에서 차원의 계층을 지정하는 경우 계층의 특성에 대한 기본 멤버는 무시됩니다. 쿼리 차원에서 계층을 지정 하지 않는 경우는 `DefaultMember` 차원 특성에 대 한 설정을 적용 합니다.  
  
 경우는 `DefaultMember` 설정은 특성은 빈 및 해당 `IsAggregatable` 속성이 `True`, 기본 멤버는 All 멤버입니다. 경우는 `IsAggregatable` 속성이 `False`, 기본 멤버는 표시 되는 첫 번째 수준의 첫 번째 멤버에 있습니다.  
  
 `DefaultMember` 설정은 특성이 참여 하는 모든 계층에 특성을 적용 합니다. 차원에서 다른 계층에 다른 설정을 사용할 수는 없습니다. 예를 들어 [1998] 멤버가 [Year] 특성에 대한 기본 멤버인 경우 이 설정은 차원의 모든 계층에 적용됩니다. `DefaultMember` 설정이 경우 일 수 없습니다 [1998] [1997] 하나의 계층에 다른 계층에서는 합니다.  
  
 자연적으로 집계되지 않는 계층의 특정 수준에 대한 기본 멤버를 정의하는 경우 계층에서 해당 수준 위의 모든 수준에 기본 멤버를 정의해야 합니다. 예를 들어 All-Countries-Climate 계층에서 Countries에 대한 기본 멤버를 정의하지 않고 Climate에 대한 기본 멤버를 정의할 수는 없습니다. 이렇게 정의하면 쿼리 시 오류가 발생합니다.  
  
 계층의 수준이 자연적으로 집계되는 경우 계층의 다른 특성과 관계없이 계층의 모든 특성에 대한 기본 멤버를 정의할 수 있습니다. 예를 들어 Country-Province-City 계층에서 State나 Country에 대한 기본 멤버를 정의하지 않고도 [City].[Montreal]과 같이 City에 대한 기본 멤버를 정의할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [구성 된 &#40;모든&#41; 특성 계층의 수준](database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
