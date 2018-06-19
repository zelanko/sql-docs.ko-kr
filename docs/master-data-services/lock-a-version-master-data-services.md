---
title: 버전 잠금(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- versions [Master Data Services], locking
- locking versions [Master Data Services]
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 5106c496b2b8ef81c8bd4754a764bc418408bcf3
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35328057"
---
# <a name="lock-a-version-master-data-services"></a>버전 잠금(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델의 멤버 및 특성이 변경되지 않도록 모델의 버전을 잠급니다.  
  
> [!NOTE]  
>  버전이 잠긴 경우 슈퍼 사용자 및 모델 관리자는 멤버를 계속 추가, 편집 및 제거할 수 있습니다. 모델에 대한 사용 권한이 있는 다른 사용자는 멤버를 볼 수만 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   버전의 상태가 **열림**이어야 합니다.  
  
-   버전 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
### <a name="to-lock-a-version"></a>버전을 잠그려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **버전 관리**를 클릭합니다.  
  
2.  **버전 관리** 페이지에서 잠그려는 버전의 행을 선택합니다.  
  
3.  **잠금**을 클릭합니다.  
  
4.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [버전 커밋&#40;Master Data Services&#41;](../master-data-services/commit-a-version-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [버전&#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [버전 잠금 해제&#40;Master Data Services&#41;](../master-data-services/unlock-a-version-master-data-services.md)  
  
  
