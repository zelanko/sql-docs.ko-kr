---
title: "리프 멤버 (Master Data Services) 만들기 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- leaf members [Master Data Services], creating
- creating leaf members [Master Data Services]
- members [Master Data Services], creating leaf members
ms.assetid: 0499d3b3-d508-4d43-a740-19cf53ade9f1
caps.latest.revision: 14
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3745604313dde3eda55c3d0f5d8f634bf7187440
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-leaf-member-master-data-services"></a>리프 멤버 만들기(Master Data Services)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서는 시스템에 마스터 데이터를 추가하려는 경우 리프 멤버를 만듭니다. 데이터를 대량으로 추가하려는 경우에는 준비 테이블을 대신 사용합니다. 자세한 내용은 [테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md)를 참조하세요.  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 를 사용하여 데이터를 가져올 수도 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   멤버를 추가할 엔터티의 리프 모델 개체에 대한 **만들기** 또는 **업데이트** 이상의 권한이 있어야 합니다. 만들기 권한이 있으면 멤버를 만들고 코드 특성만 편집할 수 있습니다. 업데이트 권한이 있으면 다른 특성도 업데이트할 수 있습니다.  
  
     자세한 내용은 [보안&#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)을 참조하세요.  
  
### <a name="to-create-a-leaf-member"></a>리프 멤버를 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
2.  사용자의 경우는 **버전** 목록에서 열린 버전을 선택합니다. 관리자의 경우는 **버전** 목록에서 열린 상태 또는 잠긴 상태의 버전을 선택합니다.  
  
3.  **탐색기**를 클릭합니다.  
  
4.  메뉴 모음에서 **엔터티** 를 가리키고 멤버를 추가하려는 엔터티의 이름을 클릭합니다.  
  
5.  **멤버 추가**를 클릭합니다.  
  
6.  **세부 정보** 창의 필드에 입력합니다.  
  
     특성이 도메인을 기반으로 하며 필터가 특성에 적용된 경우에는 필터 부모 특성에 의해 특성 값 목록이 제한됩니다.  
  
     필터 부모 특성 및 도메인 기반 특성에 대한 자세한 내용은 [도메인 기반 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)를 참조하세요.  
  
7.  (선택 사항) **주석** 상자에 멤버를 추가한 이유에 대한 주석을 입력합니다. 멤버에 액세스할 수 있는 모든 사용자가 주석을 볼 수 있습니다.  
  
8.  **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [통합 멤버 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)   
 [멤버 &#40; Master Data services&#41;](../master-data-services/members-master-data-services.md)  
  
  
