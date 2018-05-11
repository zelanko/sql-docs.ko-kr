---
title: 컬렉션(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services]
- collections [Master Data Services], about collections
ms.assetid: 5aa1d1e0-b4e5-4897-8e74-01dcf418df73
caps.latest.revision: 14
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 55562a106650890b5fff491e00a5e23c62e878f0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="collections-master-data-services"></a>컬렉션(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  컬렉션은 단일 엔터티의 리프 멤버와 통합 멤버의 그룹입니다. 전체 계층이 필요 없고 보고나 분석을 위해 멤버의 다른 그룹을 보려는 경우 또는 분류를 만들어야 할 경우 컬렉션을 사용합니다.  
  
> [!NOTE]  
>  컬렉션은 더 이상 사용되지 않습니다.  
  
## <a name="what-collections-contain"></a>컬렉션에 포함되는 내용  
 컬렉션에는 포함할 수 있는 멤버의 개수나 유형에 대한 제한이 없습니다. 해당 멤버가 같은 엔터티 내에 있기만 하면 됩니다. 컬렉션은 여러 필수 및 필수가 아닌 명시적 계층의 리프 및 통합 멤버를 포함할 수 있습니다.  
  
 컬렉션을 만들 때 계층적 구조를 만들지 않고 멤버의 기본 목록을 만듭니다. 계층에서 노드를 선택하여 이를 컬렉션에 추가할 경우 선택한 통합 멤버만 컬렉션에 추가됩니다.  
  
 또한 컬렉션은 다른 컬렉션을 포함할 수도 있습니다. 컬렉션으로 구성된 컬렉션을 사용하여 분류를 만들 수 있습니다.  
  
 컬렉션을 만들면 사용자는 자동으로 소유자로 나열됩니다. 관리자인 경우 필요에 따라 자신의 컬렉션에 대한 다른 특성을 만들 수 있습니다.  
  
## <a name="subscription-views-for-collections"></a>컬렉션의 구독 뷰  
 컬렉션을 표시하는 두 가지 유형의 구독 뷰가 있습니다. **컬렉션 특성** 형식은 컬렉션 목록 및 컬렉션과 관련된 모든 특성(설명 또는 소유자 등)을 표시합니다. **컬렉션** 형식은 모든 컬렉션의 모든 멤버와 각 멤버의 가중치 및 정렬 순서를 표시합니다. 자세한 내용은 [개요: 데이터 내보내기&#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)를 참조하세요.  
  
 컬렉션의 특정 멤버에 대해 가중치를 설정하는 경우 이러한 값을 관련 구독 뷰에서 사용할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|새 컬렉션을 만듭니다.|[컬렉션 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-collection-master-data-services.md)|  
|기존 컬렉션에 멤버를 추가합니다.|[컬렉션에 멤버 추가&#40;Master Data Services&#41;](../master-data-services/add-members-to-a-collection-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [개요: 데이터 내보내기&#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)  
  
  
