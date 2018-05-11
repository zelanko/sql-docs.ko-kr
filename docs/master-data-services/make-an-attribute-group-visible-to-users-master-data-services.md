---
title: 특성 그룹을 사용자에게 표시되도록 설정(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c68a17800113f6f413daa8534a61f296f96e9494
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>특성 그룹을 사용자에게 표시되도록 설정(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 특성 그룹이 사용자나 그룹에 표시되도록 설정하여 **탐색기** 기능 영역의 표 위에 탭이 나타나도록 할 수 있습니다.  
  
 특성 그룹을 만들면 특성 그룹은 해당 그룹을 만든 사람을 제외한 모든 사용자로부터 자동으로 숨겨집니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   하나 이상의 특성 그룹이 있어야 합니다. 자세한 내용은 [특성 그룹 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)를 참조하세요.  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>특성 그룹이 사용자에게 표시되도록 설정하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지의 표에서 특성 그룹을 편집하려는 엔터티에 대한 행을 선택합니다.  
  
4.  **특성 그룹**을 클릭합니다.  
  
5.  **특성 그룹 관리** 페이지에 있는 **멤버 유형** 드롭다운 목록 상자에서 멤버 유형을 선택하여 표시하려는 그룹의 형식에 따라 **리프**, **통합** 또는 **컬렉션**을 확장합니다.  
  
6.  표에서 편집할 특성 그룹을 선택하고 **편집**을 클릭합니다.  
  
7.  **사용 가능** 상자에서 사용자나 그룹을 클릭하고 **추가** 화살표를 클릭합니다. 모두 추가하려면 **모두 추가** 화살표를 클릭합니다.  
  
8.  **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [특성 그룹&#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [특성 그룹 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
