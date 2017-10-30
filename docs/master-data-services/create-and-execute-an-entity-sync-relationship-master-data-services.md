---
title: "엔터티 동기화 관계(Master Data Services) 만들기 및 실행 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0ddceab4-d2b3-4bc1-bd9c-6b852200b414
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 14bc03c2c8c462895102d6c34c62cf23724c706f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="create-and-execute-an-entity-sync-relationship-master-data-services"></a>엔터티 동기화 관계(Master Data Services) 만들기 및 실행
  엔터티 동기화는 엔터티 버전 간의 반복 가능한 단방향 동기화입니다. 이는 서로 다른 모델 간에 엔터티 데이터를 공유하는 방법을 제공합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 엔터티 동기화 관계를 만들기 위한 필수 구성 요소:  
  
-   시스템 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
-   대상 모델의 모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   최소한 원본 엔터티와 모든 엔터티 특성 및 멤버에 대한 읽기 권한이 있어야 합니다.  
  
 엔터티 동기화 관계를 만들기 위한 필수 구성 요소:  
  
-   시스템 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
-   대상 모델의 모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
 엔터티 동기화 관계를 만들 때 다음을 고려하십시오.  
  
-   원본 및 대상 엔터티는 서로 다른 모델에 있어야 합니다.  
  
-   대상 엔터티 버전 상태를 커밋하지 않아야 합니다.  
  
-   동기화 관계를 설정한 후 대상은 원본과 직접 동기화됩니다.  
  
-   대상 엔터티 버전은 다른 동기화 관계의 원본 엔터티 버전일 수 없습니다.  
  
 엔터티 동기화 관계를 실행할 때 다음을 고려하십시오.  
  
-   리프 멤버만 복사됨  
  
-   도메인 기반 특성은 복사되지 않습니다.  
  
-   일시 삭제된 멤버는 복사되지 않습니다.  
  
-   동기화는 대상 엔터티 트랜잭션/기록을 만들지 않습니다.  
  
 **엔터티 동기화 관계를 만들려면**  
  
1.  마스터 데이터 관리자에서 **시스템 관리자**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **엔터티 동기화**를 클릭합니다.  
  
3.  **엔터티 동기화 유지 관리** 페이지에서 **추가**를 클릭합니다. 패널은 오른쪽에 표시됩니다.  
  
4.  원본 **모델** 목록에서 모델을 선택합니다.  
  
5.  원본 **버전** 목록에서 버전을 선택합니다.  
  
6.  원본 **엔터티** 목록에서 엔터티를 선택합니다.  
  
7.  대상 **모델** 목록에서 모델을 선택합니다.  
  
8.  대상 **버전** 목록에서 버전을 선택합니다.  
  
9. **기존 엔터티** 를 선택하고 기존 엔터티를 동기화하려는 경우 엔터티 목록에서 엔터티를 선택하거나 **새 엔터티** 에 동기화하려는 경우 대상 엔터티 이름을 입력합니다.  
  
10. **필요 시 동기화**를 선택하거나 **자동 동기화** 를 선택하고 빈도를 설정합니다.  
  
11. **저장**을 클릭합니다.  
  
 **엔터티 동기화 관계를 만들려면**  
  
1.  마스터 데이터 관리자에서 **시스템 관리자**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **엔터티 동기화**를 클릭합니다.  
  
3.  **엔터티 동기화 유지 관리** 페이지의 표에서 동기화 관계를 선택합니다.  
  
4.  **실행**을 클릭합니다.  
  
## <a name="sync-relationship-information"></a>동기화 관계 정보  
 각 만들어진 동기화 관계에 대해 열이 열 개인 행 하나가 표에 추가됩니다. 다음 표에서는 열을 설명합니다.  
  
|열|Description|  
|------------|-----------------|  
|상태|동기화 관계 상태입니다.<br /><br /> **저장** 을 클릭하거나 동기화 관계를 실행하는 경우 동기화 관계가 업데이트되고 있음을 나타내는 ![업데이트 상태 아이콘](../master-data-services/media/mds-statusicon-updating.png "업데이트 상태 아이콘") 이미지가 표시됩니다.<br /><br /> 동기화 관계를 생성, 편집 또는 실행할 때 오류가 발생하면 ![오류 상태 아이콘](../master-data-services/media/mds-statusicon-error.png "오류 상태 아이콘") 이미지가 표시됩니다.<br /><br /> 그렇지 않으면 상태가 정상이고 ![정상 상태 아이콘](../master-data-services/media/mds-statusicon-ok.png "정상 상태 아이콘")이미지가 표시됩니다.|  
|원본 모델|원본 모델 이름입니다.|  
|원본 버전|원본 버전 이름입니다.|  
|원본 엔터티|원본 엔터티 이름입니다.|  
|대상 모델|대상 모델 이름입니다.|  
|대상 버전|대상 버전 이름입니다.|  
|대상 엔터티|대상 엔터티 이름입니다.|  
|빈도|동기화 관계의 빈도를 지정합니다.|  
|마지막 시도 시간|마지막 동기화 시도가 발생한 시간을 표시합니다.|  
|마지막으로 성공한 시간|마지막으로 성공한 동기화 시도가 발생한 시간을 표시합니다.|  
  
 인덱스를 클릭하면 다음 정보가 표시됩니다.  
  
-   **마지막 시도 오류**: 마지막 동기화 시도에 관한 오류 정보를 표시합니다.  
  
-   **만든 사람**: 동기화를 만든 사용자의 이름입니다.  
  
-   **시기**: 동기화가 만들어진 날짜와 시간입니다.  
  
-   **업데이트한 사람**: 동기화를 마지막 업데이트한 사용자의 이름입니다.  
  
-   **시기**: 동기화를 마지막 업데이트한 날짜 및 시간입니다.  
  
## <a name="next-steps"></a>다음 단계  
 [엔터티 동기화 관계 편집 및 삭제&#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  

