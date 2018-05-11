---
title: 버전 플래그 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
- creating version flags [Master Data Services]
- version flags [Master Data Services], creating
- versions [Master Data Services], creating flags
ms.assetid: 3067e1e3-05b7-4f11-9206-c612ef4e7e42
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 85b834edea995f957383df84ff3bcd7c35eb1677
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-version-flag-master-data-services"></a>버전 플래그 만들기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 버전에 할당할 버전 플래그를 만듭니다. 플래그는 사용자나 구독 시스템에서 사용해야 하는 버전을 나타낼 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **버전 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   버전 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
### <a name="to-create-a-version-flag"></a>버전 플래그를 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **버전 관리**를 클릭합니다.  
  
2.  **버전 관리** 페이지의 메뉴 모음에서 **관리** 를 가리킨 다음 **플래그**를 클릭합니다.  
  
3.  **버전 플래그 관리** 페이지의 **모델** 필드에서 플래그를 만들 모델을 선택합니다.  
  
4.  **추가**를 클릭합니다.  
  
5.  **이름** 상자에 이름을 입력합니다.  
  
6.  **설명** 상자에 설명을 입력합니다.  
  
7.  상태가 **커밋됨** 인 버전에만 플래그를 할당할 수 있도록 지정하려면 **커밋된 버전만** 필드에서 **True** 를 선택합니다. 모든 상태의 버전에 플래그를 할당할 수 있도록 지정하려면 **False** 를 선택합니다.  
  
8.  **저장**을 클릭합니다.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [버전에 플래그 할당&#40;Master Data Services&#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [버전&#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [버전 플래그 이름 변경&#40;Master Data Services&#41;](../master-data-services/change-a-version-flag-name-master-data-services.md)  
  
  
