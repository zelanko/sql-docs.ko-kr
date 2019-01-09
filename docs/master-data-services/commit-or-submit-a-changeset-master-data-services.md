---
title: 변경 집합 커밋 또는 제출(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a2953852ebc54099fa815af4399614a5c66825b4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821797"
---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>변경 집합 커밋 또는 제출(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  변경 집합은 마스터 데이터에 대해 보류 중인 변경 내용의 컬렉션입니다. 엔터티 변경 시 관리자의 승인이 필요하지 않으면 변경 집합을 커밋할 수 있습니다. 엔터티 변경 시 관리자의 승인이 필요하면 승인을 위해 변경 집합을 제출할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
-   엔터티 변경 시 관리자의 승인이 필요하지 않은 경우 자신이 소유한 열린 상태의 변경 집합만 커밋할 수 있습니다.  
  
-   엔터티 변경 시 관리자의 승인이 필요한 경우에는 자신이 소유한 열린 상태 또는 거부된 상태의 변경 집합만 승인을 위해 제출할 수 있습니다.  
  
## <a name="to-commit-a-local-changeset"></a>로컬 변경 집합을 커밋하려면  
 커밋 옵션은 엔터티 관리자가 승인 필요를 사용하도록 설정하지 않은 엔티티에 대한 로컬 변경 집합에만 사용할 수 있습니다.  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지에서 모델 및 버전을 선택하고 **탐색기**를 클릭합니다.  
  
2.  **엔터티** 메뉴에서 엔터티를 클릭합니다.  
  
3.  오른쪽 창에서 **변경 집합** 을 선택하고 커밋할 변경 집합을 두 번 클릭합니다.  
  
4.  **커밋**을 클릭합니다.  
  
## <a name="to-submit-a-changeset"></a>변경 집합을 제출하려면  
 제출 옵션은 엔터티 관리자가 승인 필요를 사용하도록 설정한 엔티티에 대한 변경 집합에만 사용할 수 있습니다.  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지에서 모델 및 버전을 선택하고 **탐색기**를 클릭합니다.  
  
2.  **엔터티** 메뉴에서 엔터티를 클릭합니다.  
  
3.  오른쪽 창에서 **변경 집합** 을 선택하고 제출할 변경 집합을 두 번 클릭합니다.  
  
4.  **제출**을 클릭합니다.  
  
## <a name="next-steps"></a>Next Steps  
 [변경 집합 승인 또는 거부&#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [변경 집합 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [변경 집합 적용 및 업데이트&#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [변경 집합 승인 또는 거부&#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
