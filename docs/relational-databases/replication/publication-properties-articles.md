---
title: "게시 속성, 아티클 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.pubproperties.articles.f1
ms.assetid: bdeea318-a153-44b8-9e51-9155f3bad18b
caps.latest.revision: "29"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c0f2c87e7f36b1c1952b9126f43a0be8d04ea4d7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="publication-properties-articles"></a>게시 속성, 아티클
  **게시 속성** 대화 상자의 **아티클** 페이지에는 게시에 포함된 아티클에 대한 정보가 들어 있습니다. 이 페이지를 사용하여 기존 게시에 아티클을 추가하거나 기존 게시에서 아티클을 삭제할 수 있으며 아티클 속성 및 열 필터링을 변경할 수 있습니다.  
  
> [!NOTE]  
>  게시가 생성되면 일부 속성 변경으로 인해 새 스냅숏이 필요합니다. 게시에 구독이 있는 경우에는 이러한 변경 내용으로 인해 모든 구독도 다시 초기화해야 합니다. 자세한 내용은 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md) 및 [기존 게시에 대한 아티클 추가 및 삭제](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
 하나 이상의 다른 데이터베이스 개체에 종속된 데이터베이스 개체를 게시하는 경우 참조된 개체를 모두 게시해야 합니다. 예를 들어 테이블에 종속된 뷰를 게시하는 경우 테이블도 게시해야 합니다.  
  
 게시할 수 없는 개체는 옆에 빨간색 아이콘이 표시되며 마법사 페이지 아래쪽의 정보 패널에 설명이 표시됩니다. 다음 개체는 게시할 수 없습니다.  
  
-   암호화된 개체는 게시할 수 없습니다.  
  
-   NULL을 허용하는 열이 들어 있는 인덱싱된 뷰는 게시할 수 없습니다.  
  
-   기본 키가 없는 테이블은 트랜잭션 게시에 게시할 수 없습니다.  
  
-   지연 업데이트 구독이 설정된 트랜잭션 게시와 병합 게시에 테이블을 모두 게시할 수는 없습니다. 둘 이상의 게시에 아티클을 게시하는 방법은 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)의 "둘 이상의 게시에 테이블 게시" 섹션을 참조하세요.  
  
## <a name="oracle-publishers"></a>Oracle 게시자  
 Oracle 게시자의 경우 다음 사항을 추가로 고려해야 합니다.  
  
-   Oracle에서 게시할 수 있는 개체 목록은 [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)을 참조하십시오. 게시할 수 없는 개체는 표시되지 않습니다.  
  
-   게시할 수 있는 데이터 형식 목록은 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하십시오. 게시할 수 없는 데이터 형식이 있는 열은 표시되지 않습니다.  
  
## <a name="column-filters"></a>열 필터  
 이 페이지의 **게시할 개체** 창에서 테이블을 확장한 다음 필요한 열만 선택하여 열을 필터링할 수 있습니다. 이 마법사의 **테이블 행 필터** 페이지에서는 행을 필터링할 수 있습니다. 열 필터링은 보안(예: 중요한 데이터의 복제 방지) 및 성능(예: 큰 BLOB(Binary Large Object) 열의 복제 방지)을 비롯하여 다양한 범위에서 유용하게 사용됩니다. 필터링할 수 없는 열 유형 목록 등 열 필터링에 대한 자세한 내용은 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **게시할 개체** 창을 사용하여 다음 작업을 수행할 수 있습니다.  
  
-   복제에 사용 가능한 모든 개체를 봅니다.  
  
-   해당 개체 옆의 확인란을 선택하여 아티클을 게시에 추가합니다.  
  
-   해당 개체 옆의 확인란 선택을 취소하여 아티클을 게시에서 삭제합니다. 아티클을 삭제할 수 있는 경우에 대한 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
-   개체 유형(예: **테이블**) 옆의 확인란을 선택하여 특정 유형(예: 테이블)의 개체를 모두 게시에 포함합니다.  
  
-   테이블 노드를 확장하여 테이블에 있는 열을 표시합니다.  
  
-   해당 열 옆의 확인란 선택을 취소하여 게시에서 테이블 열을 필터링하거나 확인란을 선택하여 게시되지 않은 열을 포함합니다.  
  
-   창에서 개체를 마우스 오른쪽 단추로 클릭하여 해당 개체의 명령 메뉴를 표시합니다.  
  
 **아티클 속성**  
 **아티클 속성** 을 클릭한 후 다음 중 하나를 클릭합니다.  
  
-   **선택한 \<ObjectType> 아티클 속성 설정**을 클릭하여 **아티클 속성 - \<ObjectName>** 대화 상자를 엽니다. 이 대화 상자에서 변경한 속성은 **아티클** 페이지의 개체 창에 강조 표시된 개체에만 적용됩니다.  
  
-   **모든 \<ObjectType> 아티클 속성 설정**을 클릭하여 **모든 \<ObjectType> 아티클의 속성** 대화 상자를 엽니다. 이 대화 상자에서 변경한 속성은 게시용으로 아직 선택하지 않은 개체를 비롯하여 **아티클** 페이지의 개체 창에서 해당 형식을 갖는 모든 개체에 적용됩니다.  
  
    > [!NOTE]  
    >  **모든 \<ObjectType> 아티클의 속성** 대화 상자에서 변경한 속성은 이전에 **아티클 속성 - \<ObjectName>** 대화 상자에서 지정한 내용을 재정의합니다. 예를 들어 특정 개체 유형의 모든 아티클에 대해 여러 기본값을 설정하고 개별 개체에 대해 일부 속성도 설정하려면 먼저 모든 아티클의 기본값을 설정합니다. 그런 다음 개별 개체에 대해 속성을 설정합니다.  
  
 **강조 표시된 테이블은 다운로드 전용**  
 병합 복제에 대해서만 사용할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 클라이언트 구독이 사용 중일 때는 구독자에서 변경 작업을 수행할 수 없게 지정하려면 선택합니다. 다운로드 전용 아티클은 구독자에서 업데이트할 수 없으므로 추적 메타데이터가 구독자로 전송되지 않습니다. 이로 인해 구독자의 저장소 용량 및 성능상 이점이 줄어들 수 있으며 특히 네트워크 연결 속도가 느릴 경우 더욱 그렇습니다. 이 옵션은 **아티클 속성** 대화 상자에 있는 **동기화 방향** 옵션의 **구독자로 다운로드 전용, 구독자 변경 금지** 값과 동일합니다. 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.  
  
 **선택 표시된 개체만 목록에 표시**  
 개체 창에서 선택한 아티클만 표시하려면 이 확인란을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [초기 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
