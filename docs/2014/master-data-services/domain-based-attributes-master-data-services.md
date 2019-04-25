---
title: 도메인 기반 특성(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], about domain-based attributes
- domain-based attributes [Master Data Services]
- attributes [Master Data Services], domain-based attributes
ms.assetid: df6f33ff-97f6-466c-af74-9780b2247473
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 28abd39a51a54747a1c93af2e0c36d4ff4100bd8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62765484"
---
# <a name="domain-based-attributes-master-data-services"></a>도메인 기반 특성(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 도메인 기반 특성은 다른 엔터티의 멤버로 값이 채워지는 특성입니다. 도메인 기반 특성은 제한된 목록으로 생각할 수 있습니다. 도메인 기반 특성을 사용하면 사용자가 유효하지 않은 특성 값을 입력하지 못하도록 할 수 있습니다. 특성 값을 선택하려면 사용자가 목록에서 선택해야 합니다.  
  
## <a name="domain-based-attribute-example"></a>도메인 기반 특성 예  
 다음 이미지의 Product 엔터티에는 Subcategory라는 도메인 기반 특성이 있습니다. Subcategory 특성은 Subcategory 엔터티의 값으로 채워집니다.  
  
 Subcategory 엔터티에는 Category라는 도메인 기반 특성이 있습니다. Category 특성은 Category 엔터티의 값으로 채워집니다.  
  
 ![엔터티의 도메인 기반 특성](../../2014/master-data-services/media/mds-conc-domain-based-attribute-conceptual.gif "엔터티의 도메인 기반 특성")  
  
## <a name="use-same-entity-for-multiple-domain-based-attributes"></a>여러 도메인 기반 특성에 동일한 엔터티 사용  
 동일한 엔터티를 여러 엔터티의 도메인 기반 특성으로 사용할 수 있습니다. 예를 들어, 멤버를 포함 하는 YesNoIndicator 라는 엔터티를 만들 수 있습니다. Yes, No 및 Maybe 합니다. 또한 InStock이라는 도메인 기반 특성을 만들고 YesNoIndicator 엔터티를 원본으로 사용할 수 있습니다. Approved라는 또 다른 도메인 기반 특성을 만들고 YesNoIndicator 엔터티를 원본으로 사용할 수도 있습니다. 사용자가 YesNoIndicator 엔터티의 멤버 목록에서 선택할 수 있도록 하려는 경우 엔터티를 도메인 기반 특성으로 사용할 수 있습니다.  
  
## <a name="domain-based-attributes-form-derived-hierarchies"></a>도메인 기반 특성으로 파생 계층 형성  
 도메인 기반 특성 관계는 파생 계층의 기반이 됩니다. 자세한 내용은 [파생 계층&#40;Master Data Services&#41;](derived-hierarchies-master-data-services.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|기존 엔터티를 원본으로 이용하여 새 도메인 기반 특성을 만듭니다.|[도메인 기반 특성 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|새 엔터티를 만듭니다.|[엔터티 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [파생 계층&#40;Master Data Services&#41;](derived-hierarchies-master-data-services.md)  
  
-   [특성&#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
-   [엔터티&#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)  
  
  
