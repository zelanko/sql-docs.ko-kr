---
title: 엔터티 동기화 관계 편집 및 삭제(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9a5e37f3-352e-45a6-b4a0-6f98f83b4bd8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a3de4051ff43ebf0155571235890a28a28d24788
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65487573"
---
# <a name="edit-and-delete-an-entity-sync-relationship-master-data-services"></a>엔터티 동기화 관계 편집 및 삭제(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  엔터티 동기화는 엔터티 버전 간의 반복 가능한 단방향 동기화입니다. 이는 서로 다른 모델 간에 엔터티 데이터를 공유하는 방법을 제공합니다. 만든 동기화 관계를 편집하고 삭제할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 엔터티 동기화 관계를 편집하기 위한 필수 구성 요소  
  
-   시스템 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
-   대상 모델의 모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   최소한 원본 엔터티와 모든 엔터티 특성 및 멤버에 대한 읽기 권한이 있어야 합니다.  
  
 엔터티 동기화 관계를 삭제하기 위한 필수 구성 요소:  
  
-   시스템 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
-   대상 모델의 모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
 엔터티 동기화 관계를 편집할 때 다음을 고려하세요.  
  
-   원본 및 대상 엔터티는 서로 다른 모델에 있어야 합니다.  
  
-   대상 엔터티 버전 상태를 커밋하지 않아야 합니다.  
  
-   동기화 관계를 설정한 후 대상은 원본과 직접 동기화됩니다.  
  
-   대상 엔터티 버전은 다른 동기화 관계의 원본 엔터티 버전일 수 없습니다.  
  
 엔터티 동기화 관계를 실행할 때 다음을 고려하세요.  
  
-   리프 멤버만 복사됩니다.  
  
-   도메인 기반 특성은 복사되지 않습니다.  
  
-   일시 삭제된 멤버는 복사되지 않습니다.  
  
-   동기화는 대상 엔터티 트랜잭션/기록을 만들지 않습니다.  
  
 **엔터티 동기화 관계를 편집하려면**  
  
1.  마스터 데이터 관리자에서 **시스템 관리자**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **엔터티 동기화**를 클릭합니다.  
  
3.  **엔터티 동기화 유지 관리** 페이지의 표에서 동기화 관계를 선택합니다.  
  
4.  **편집**을 클릭합니다. 패널은 오른쪽에 표시됩니다.  
  
5.  **빈도**를 변경합니다. **필요 시 동기화**를 선택하거나 **자동 동기화** 를 선택하고 빈도를 설정합니다.  
  
6.  **저장**을 클릭합니다.  
  
 **엔터티 동기화 관계를 삭제하려면**  
  
1.  마스터 데이터 관리자에서 **시스템 관리자**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **엔터티 동기화**를 클릭합니다.  
  
3.  **엔터티 동기화 유지 관리** 페이지의 표에서 동기화 관계를 선택합니다.  
  
4.  **삭제**를 클릭합니다.  
  
5.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [엔터티 동기화 관계 만들기 및 실행&#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [엔터티 동기화 관계&#40;Master Data Services&#41;](../master-data-services/entity-sync-relationship-master-data-services.md)  
  
  
