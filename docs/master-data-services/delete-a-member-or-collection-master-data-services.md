---
title: 멤버 또는 컬렉션 삭제(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53005e9b2bec6b4f1e3a5a80f8dbbcad83a1ab31
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="delete-a-member-or-collection-master-data-services"></a>멤버 또는 컬렉션 삭제(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서는 멤버나 컬렉션이 더 이상 필요하지 않으면 삭제할 수 있습니다. 멤버를 대량으로 삭제하려면 준비 테이블을 대신 사용합니다. 자세한 내용은 [테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md)를 참조하세요.  
  
> [!NOTE]  
>  다른 멤버의 도메인 기반 특성 값으로 사용되는 멤버는 삭제할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   멤버의 경우 멤버를 삭제할 리프 모델 개체에 대한 **삭제** 이상의 권한이 있어야 합니다.  
  
-   컬렉션의 경우 컬렉션을 삭제할 리프 컬렉션 모델 개체에 대한 **업데이트** 이상의 권한이 있어야 합니다.  
  
### <a name="to-delete-a-member-or-collection"></a>멤버 또는 컬렉션을 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
2.  **버전** 목록에서 버전을 선택합니다.  
  
3.  **탐색기**를 클릭합니다.  
  
4.  삭제하려면  
  
    -   리프 멤버를 삭제하려면 메뉴 모음에서 **엔터티** 를 가리키고 멤버가 포함된 엔터티의 이름을 클릭합니다.  
  
    -   통합 멤버를 삭제하려면 메뉴 모음에서 **계층** 을 가리키고 멤버가 포함된 계층의 이름을 클릭합니다. 그런 다음 멤버를 포함하고 있는 계층에서 노드를 클릭합니다.  
  
    -   컬렉션을 삭제하려면 메뉴 모음에서 **컬렉션** 을 가리키고 컬렉션이 포함된 엔터티의 이름을 클릭합니다.  
  
5.  표에서 삭제할 멤버 또는 컬렉션의 행을 선택합니다.  
  
6.  **멤버 삭제**또는 **삭제**또는 **컬렉션 삭제**를 클릭합니다.  
  
7.  엔터티 관리자도 엔터티 버전의 일시 삭제된 모든 멤버를 삭제(영구 삭제)에 대한 메뉴 옵션이 나타납니다.  
  
8.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [멤버 또는 컬렉션 다시 활성화&#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [멤버&#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [컬렉션&#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  
