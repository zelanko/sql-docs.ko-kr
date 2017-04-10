---
title: "게시 속성, 아티클 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.articles.f1"
ms.assetid: bdeea318-a153-44b8-9e51-9155f3bad18b
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# 게시 속성, 아티클
  **게시 속성** 대화 상자의 **아티클** 페이지에는 게시에 포함된 아티클에 대한 정보가 들어 있습니다. 이 페이지를 사용하여 기존 게시에 아티클을 추가하거나 기존 게시에서 아티클을 삭제할 수 있으며 아티클 속성 및 열 필터링을 변경할 수 있습니다.  
  
> [!NOTE]  
>  게시가 생성되면 일부 속성 변경으로 인해 새 스냅숏이 필요합니다. 게시에 구독이 있는 경우에는 이러한 변경 내용으로 인해 모든 구독도 다시 초기화해야 합니다. 자세한 내용은 참조 [변경 게시 및 아티클 속성](../../relational-databases/replication/publish/change-publication-and-article-properties.md) 및 [기사를 추가 하 고 기존 게시에서 아티클을 삭제할](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)합니다.  
  
 하나 이상의 다른 데이터베이스 개체에 종속된 데이터베이스 개체를 게시하는 경우 참조된 개체를 모두 게시해야 합니다. 예를 들어 테이블에 종속된 뷰를 게시하는 경우 테이블도 게시해야 합니다.  
  
 게시할 수 없는 개체는 옆에 빨간색 아이콘이 표시되며 마법사 페이지 아래쪽의 정보 패널에 설명이 표시됩니다. 다음 개체는 게시할 수 없습니다.  
  
-   암호화된 개체는 게시할 수 없습니다.  
  
-   NULL을 허용하는 열이 들어 있는 인덱싱된 뷰는 게시할 수 없습니다.  
  
-   기본 키가 없는 테이블은 트랜잭션 게시에 게시할 수 없습니다.  
  
-   지연 업데이트 구독이 설정된 트랜잭션 게시와 병합 게시에 테이블을 모두 게시할 수는 없습니다. 둘 이상의 게시에 아티클을 게시에 대 한 자세한 내용은 "게시 테이블에서 둘 이상의 게시" 섹션을 참조 하십시오. [게시 데이터 및 데이터베이스 개체](../../relational-databases/replication/publish/publish-data-and-database-objects.md)합니다.  
  
## Oracle 게시자  
 Oracle 게시자의 경우 다음 사항을 추가로 고려해야 합니다.  
  
-   Oracle에서 게시할 수 있는 개체 목록은 [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)을 참조하십시오. 게시할 수 없는 개체는 표시되지 않습니다.  
  
-   게시할 수 있는 데이터 형식 목록은 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하십시오. 게시할 수 없는 데이터 형식이 있는 열은 표시되지 않습니다.  
  
## 열 필터  
 테이블을 확장 하 여이 페이지에는 열을 필터링는 **게시할 개체** 창 한 다음 필요한 열만 선택 하 (에서 행을 필터링 할 수는 **테이블 행 필터** 이 마법사의 페이지). 열 필터링은 보안(예: 중요한 데이터의 복제 방지) 및 성능(예: 큰 BLOB(Binary Large Object) 열의 복제 방지)을 비롯하여 다양한 범위에서 유용하게 사용됩니다. 열 형식 필터링 할 수 없는, 목록 등 열 필터링 하는 방법에 대 한 자세한 내용은 참조 [데이터를 게시 하는 필터](../../relational-databases/replication/publish/filter-published-data.md)합니다.  
  
## 옵션  
 **게시할 개체** 창을 사용하여 다음 작업을 수행할 수 있습니다.  
  
-   복제에 사용 가능한 모든 개체를 봅니다.  
  
-   해당 개체 옆의 확인란을 선택하여 아티클을 게시에 추가합니다.  
  
-   해당 개체 옆의 확인란 선택을 취소하여 아티클을 게시에서 삭제합니다. 문서를 삭제할 수 있습니다 하는 방법에 대 한 정보를 참조 하십시오. [기사를 추가 하 고 기존 게시에서 아티클을 삭제할](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)합니다.  
  
-   특정 형식 (예: 테이블)의 모든 개체는 개체 유형 옆의 확인란을 선택 하 여 게시에 포함 (예: **테이블**).  
  
-   테이블 노드를 확장하여 테이블에 있는 열을 표시합니다.  
  
-   해당 열 옆의 확인란 선택을 취소하여 게시에서 테이블 열을 필터링하거나 확인란을 선택하여 게시되지 않은 열을 포함합니다.  
  
-   창에서 개체를 마우스 오른쪽 단추로 클릭하여 해당 개체의 명령 메뉴를 표시합니다.  
  
 **아티클 속성**  
 클릭 **아티클 속성** , 다음 중 하나를 클릭 합니다.  
  
-   클릭 **설정의 강조 표시 된 속성 \< ObjectType> 문서** 시작 하는 **아티클 속성-\< o b j>** 대화 상자, 속성이 대화 상자에서 변경한 내용을에 포함 된 개체 창에서 강조 표시 하는 개체에만 적용 됩니다는 **문서** 페이지입니다.  
  
-   클릭 **설정 속성의 모든 \< ObjectType> 문서**, 시작 하는 **모든 속성을 \< ObjectType> 문서** 대화 상자, 속성이 대화 상자에서 변경한 내용을에 개체 창에 있는 해당 유형의 모든 개체에 적용 되는 **문서** 게시에 대 한 선택 하지 않은 것을 포함 하 여 페이지.  
  
    > [!NOTE]  
    >  속성 변경 내용에서 **모든 속성을 \< ObjectType> 문서** 대화 상자에서 이전에 수행 된 모든 재정의 **아티클 속성-\< o b j>** 대화 상자. 예를 들어 특정 개체 유형의 모든 아티클에 대해 여러 기본값을 설정하고 개별 개체에 대해 일부 속성도 설정하려면 먼저 모든 아티클의 기본값을 설정합니다. 그런 다음 개별 개체에 대해 속성을 설정합니다.  
  
 **강조 표시된 테이블은 다운로드 전용**  
 병합 복제에 대해서만 사용할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 클라이언트 구독이 사용 중일 때는 구독자에서 변경 작업을 수행할 수 없게 지정하려면 선택합니다. 다운로드 전용 아티클은 구독자에서 업데이트할 수 없으므로 추적 메타데이터가 구독자로 전송되지 않습니다. 이로 인해 구독자의 저장소 용량 및 성능상 이점이 줄어들 수 있으며 특히 네트워크 연결 속도가 느릴 경우 더욱 그렇습니다. 이 옵션의 값에 해당 **구독자로 다운로드 전용 구독자 변경 금지** 옵션에 대 한 **동기화 방향** 에 **아티클 속성** 대화 상자입니다. 자세한 내용은 참조 [with Download-Only Articles 병합 복제 성능 최적화](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)합니다.  
  
 **선택 표시된 개체만 목록에 표시**  
 개체 창에서 선택한 아티클만 표시하려면 이 확인란을 선택합니다.  
  
## 참고 항목  
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [초기 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  