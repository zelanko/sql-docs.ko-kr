---
title: "버전 (Master Data Services) 잠금 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- versions [Master Data Services], locking
- locking versions [Master Data Services]
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8edd7ce020ad20917c4bdc76c636b8cf7a06fadd
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="lock-a-version-master-data-services"></a>버전 잠금(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델의 멤버 및 특성이 변경되지 않도록 모델의 버전을 잠급니다.  
  
> [!NOTE]  
>  버전이 잠긴 경우 슈퍼 사용자 및 모델 관리자는 멤버를 계속 추가, 편집 및 제거할 수 있습니다. 모델에 대한 사용 권한이 있는 다른 사용자는 멤버를 볼 수만 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   버전의 상태가 **열림**이어야 합니다.  
  
-   버전 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
### <a name="to-lock-a-version"></a>버전을 잠그려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **버전 관리**를 클릭합니다.  
  
2.  **버전 관리** 페이지에서 잠그려는 버전의 행을 선택합니다.  
  
3.  **잠금**을 클릭합니다.  
  
4.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [비즈니스 규칙 &#40;에 대해 버전 유효성 검사 Master Data services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [버전 &#40; 커밋 Master Data services&#41;](../master-data-services/commit-a-version-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [버전 &#40; Master Data services&#41;](../master-data-services/versions-master-data-services.md)   
 [버전 &#40; 잠금 해제 Master Data services&#41;](../master-data-services/unlock-a-version-master-data-services.md)  
  
  
