---
title: "특성 그룹(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attribute groups [Master Data Services]
- attribute groups [Master Data Services], about attribute groups
ms.assetid: 648b3d0b-e15a-45f9-8292-3a54a072e62c
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 3762e429085613760b82709bd772313ed6ae667b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="attribute-groups-master-data-services"></a>특성 그룹(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 특성 그룹은 엔터티의 특성을 구성하는 데 유용합니다. 엔터티에 있는 특성이 여러 개인 경우 특성 그룹을 사용하면 엔터티가 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램에 표시되는 방식이 향상됩니다.  
  
## <a name="how-attribute-groups-change-the-display"></a>특성 그룹 표시를 변경하는 방법  
 특성 그룹은 **에서** 탐색기 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]기능 영역의 표 위에 탭으로 표시됩니다.  
  
 엔터티에 특성이 많이 있고 **탐색기**의 표에서 해당 엔터티를 볼 경우 모든 특성을 보려면 오른쪽으로 스크롤해야 합니다. 이렇게 스크롤하지 않고 모든 특성을 보려면 특성 그룹을 만듭니다.  
  
-   특성 그룹에는 Name 및 Code 특성이 항상 포함됩니다.  
  
-   엔터티의 각 특성은 하나 이상의 특성 그룹에 속할 수 있습니다.  
  
-   모든 특성은 **탐색기** 의 **모든 특성**탭에 자동으로 포함됩니다.  
  
-   **모든 특성** 탭을 숨길 수 있는 방법은 없습니다.  
  
 특성 그룹은 **의** 시스템 관리 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]기능 영역에서 관리됩니다.  
  
## <a name="show-or-hide-attribute-groups"></a>특성 그룹 표시 또는 숨기기  
 특성 그룹을 만들면 특성 그룹은 해당 그룹을 만든 사람을 제외한 모든 사용자로부터 자동으로 숨겨집니다. 그룹을 표시하는 방법에 대한 자세한 내용은 [특성 그룹을 사용자에게 표시되도록 설정&#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)기능 영역의 표 위에 탭으로 표시됩니다.  
  
 그룹 내의 특정 특성을 숨기려면 해당 특성에 **거부** 권한을 할당하면 됩니다. 자세한 내용은 [리프 권한&#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|새 특성 그룹을 만들고 이 그룹에 특성을 추가합니다.|[특성 그룹 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|특성 그룹을 사용자가 볼 수 있도록 활성화합니다.|[특성 그룹을 사용자에게 표시되도록 설정&#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)|  
|기존 특성 그룹의 이름을 변경합니다.|[특성 그룹 이름 변경&#40;Master Data Services&#41;](../master-data-services/change-an-attribute-group-name-master-data-services.md)|  
|기존 특성 그룹을 삭제합니다.|[특성 그룹 삭제&#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [특성&#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  

