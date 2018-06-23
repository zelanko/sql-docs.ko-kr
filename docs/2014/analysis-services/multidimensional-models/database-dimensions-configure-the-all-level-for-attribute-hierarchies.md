---
title: 특성 계층에 대해 (All) 수준 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- All members
- IsAggregatable property
- topmost levels [Analysis Services]
- (All) levels
- AttributeAllMemberName property
- levels [Analysis Services]
- members [Analysis Services], All
- AllMemberName property
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e61b7606ab4a7c2418294133ad7c4f3b03672df1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186181"
---
# <a name="configure-the-all-level-for-attribute-hierarchies"></a>특성 계층에 대해 (All) 수준 구성
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 (All) 수준은 선택적인 시스템 생성 수준입니다. 이 수준에는 바로 아래 종속되는 수준의 모든 멤버 값의 집계를 값으로 갖는 멤버 하나만 포함됩니다. 이 멤버를 All 멤버라고 합니다. All 멤버는 차원 테이블에 포함되지 않은 시스템 생성 멤버입니다. (All) 수준의 멤버는 계층의 맨 위에 있기 때문에 이 멤버의 값은 해당 계층의 모든 멤버 값을 통합하여 집계한 값입니다. All 멤버는 대개 계층의 기본 멤버 역할을 합니다.  
  
 특성 계층의 (All) 수준의 존재 여부에 따라 달라 집니다는 `IsAggregatable` 특성 및 사용자 정의 계층에 (All) 수준이 있는지 여부에 대 한 속성 설정에 따라 달라 집니다는 `IsAggregatable` 의 최상위 수준에서 특성의 속성 사용자 정의 계층입니다. `IsAggregatable` 속성이 `True`로 설정되어 있으면 (All) 수준이 존재합니다. `IsAggregatable` 속성이 `False`로 설정되어 있으면 계층에 (All) 수준이 없습니다.  
  
## <a name="establishing-the-topmost-level"></a>최상위 수준 설정  
 계층에서 수준의 원본 특성에 `IsAggregatable` 속성이 `False`로 설정되어 있으면 계층에서 해당 수준 위에 집계할 수 있는 수준이 나타나지 않습니다. 집계할 수 없는 수준은 계층의 최상위 수준이어야 합니다. 또는 해당 수준 위의 모든 수준에 대한 원본 특성의 `IsAggregatable` 속성이 `False`로 설정되어야 합니다.  
  
## <a name="all-member-and-all-level"></a>All 멤버 및 (All) 수준  
 (All) 수준의 단일 멤버를 All 멤버라고 합니다. `AttributeAllMemberName`차원에 속성 차원의 특성에 대 한 All 멤버의 이름을 지정 합니다. 계층의 `AllMemberName` 속성은 계층에 대한 All 멤버의 이름을 지정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [기본 멤버 정의](attribute-properties-define-a-default-member.md)  
  
  