---
title: 멤버 수정 기록
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 113069c5-12e6-48ec-b443-b42e14f77308
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4bc3d2a084f7f1ec3abcf9e3d3bbcaf82e4749e8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729115"
---
# <a name="member-revision-history-master-data-services"></a>멤버 수정 기록(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  멤버 수정 기록은 엔터티 트랜잭션 로그 형식이 멤버인 경우 멤버가 변경될 때마다 기록됩니다.  
  
 트랜잭션 로그 유형에 대한 자세한 내용은 [엔터티 트랜잭션 로그 유형 변경&#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)을 참조하세요.  
  
 멤버 수정 기록은 다음 변경을 수행하면 기록됩니다.  
  
-   멤버를 생성, 삭제, 다시 활성화하거나 비우는 경우  
  
-   특성 값을 변경하는 경우  
  
-   계층이나 컬렉션에서 멤버를 이동하는 경우  
  
## <a name="view-and-manage-revision-history-by-entity"></a>엔터티별 수정 기록 보기 및 관리  
 탐색기 기능 영역에서 엔터티의 모든 멤버에 대한 수정 내용을 확인할 수 있습니다. 업데이트 권한이 있는 경우 멤버를 이전 수정으로 롤백할 수 있습니다.  
  
 **수정 기록을 보고 관리하려면**  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 모델 및 버전을 선택하고 **탐색기**를 클릭합니다.  
  
2.  **엔터티** 메뉴에서 엔터티를 선택합니다.  
  
3.  엔터티의 모든 기록 데이터를 확인하려면 **기록 보기** 를 클릭합니다.  
  
4.  데이터를 필터링하려면 **필터** 를 클릭합니다.  
  
5.  데이터를 정렬하려면 열 머리글을 클릭합니다.  
  
6.  업데이트 권한이 있는 경우 **멤버 되돌리기** 를 클릭하여 선택한 버전으로 롤백합니다.  
  
## <a name="view-and-manage-revision-history-by-member"></a>멤버별 수정 기록 보기 및 관리  
 멤버에 대한 읽기 권한이 있으면 탐색기 기능 영역에서 멤버의 수정 내용을 확인할 수 있습니다. 업데이트 권한이 있는 경우 멤버를 이전 수정으로 롤백하거나 수정에 주석을 추가할 수 있습니다.  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 모델 및 버전을 선택하고 **탐색기**를 클릭합니다.  
  
2.  **엔터티** 메뉴에서 엔터티를 선택합니다.  
  
3.  멤버를 선택합니다.  
  
4.  오른쪽 창에서 **기록 보기** 를 클릭합니다.  
  
## <a name="log-retention-setting"></a>로그 보존 설정  
 **데이터베이스에 대한 시스템 설정에서** 로그 보존 기간(일) [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 속성을 설정하고 모델을 만들거나 편집할 때 **로그 보존 기간(일)** 을 설정하면 기록 데이터를 보존할 기간을 구성할 수 있습니다.  
  
## <a name="related-task"></a>관련 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|멤버 수정 기록 롤백|[멤버 수정 기록 롤백&#40;Master Data Services&#41;](../master-data-services/rollback-member-revision-history-master-data-services.md)|  
  
## <a name="see-also"></a>참고 항목  
 [모델 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [시스템 설정&#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)  
  
  
