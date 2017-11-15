---
title: "명시적 캡이 포함된 파생 계층(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [Master Data Services], derived hierarchies with explicit caps
- explicit hierarchies, derived hierarchies with explicit caps
- derived hierarchies, derived hierarchies with explicit caps
ms.assetid: 6a82ff66-c137-4757-99bb-787d189b4295
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e8487b1131fb71a543f0f65b592904599893b03
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="derived-hierarchies-with-explicit-caps-master-data-services"></a>명시적 캡이 포함된 파생 계층(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 명시적 계층의 수준이 파생 계층의 최상위 수준으로 사용되는 경우 이를 명시적 캡이 포함된 파생 계층이라고 합니다.  
  
 명시적 계층은 파생 계층의 최상위 엔터티와 동일한 엔터티를 기반으로 해야 합니다.  
  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] UI(사용자 인터페이스)에서는 명시적 계층을 파생 계층의 맨 위로 끌어와서 이 유형의 계층을 만듭니다.  
  
 ![mds_conc_explicit_cap_UI_structure](../master-data-services/media/mds-conc-explicit-cap-ui-structure.gif "mds_conc_explicit_cap_UI_structure")  
  
## <a name="derived-hierarchy-with-explicit-cap-example"></a>명시적 캡이 포함된 파생 계층 예제  
 이 예에서는 명시적 계층의 멤버를 Subcategory 엔터티에서 가져옵니다. 파생 계층의 최상위 멤버 역시 Subcategory 엔터티에서 가져옵니다.  
  
 ![mds_conc_explicit_cap_UI_example](../master-data-services/media/mds-conc-explicit-cap-ui-example.gif "mds_conc_explicit_cap_UI_example")  
  
 파생 계층의 맨 위에 명시적 계층을 사용하므로 파생 계층이 비정형 계층이 됩니다.  
  
## <a name="rules"></a>규칙  
  
-   명시적 캡을 포함한 파생 계층에 두 개 이상의 명시적 계층이 있을 수 없습니다.  
  
-   여러 파생 계층에 Cap과 동일한 명시적 계층을 사용할 수 있습니다.  
  
-   명시적 캡이 포함된 파생 계층에 계층 멤버 권한을 할당할 수 없습니다. 명시적 계층이나 파생 계층에 개별적으로 사용 권한을 할당할 경우 해당 권한이 두 계층에 모두 적용됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|파생 계층을 만듭니다.|[파생 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|명시적 계층을 만듭니다.|[명시적 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|기존 파생 계층을 삭제합니다.|[파생 계층 삭제&#40;Master Data Services&#41;](../master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
|||  
  
## <a name="related-content"></a>관련 내용  
  
-   [파생 계층&#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
-   [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
