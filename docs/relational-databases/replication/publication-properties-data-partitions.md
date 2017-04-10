---
title: "게시 속성, 데이터 파티션 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.datapartitions.f1"
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 게시 속성, 데이터 파티션
  **게시 속성** 대화 상자의 **데이터 파티션** 페이지를 사용하여 매개 변수가 있는 필터링을 사용하는 병합 게시를 위한 데이터 파티션을 정의할 수 있습니다. 파티션을 정의하고 나면 이들 파티션에 대한 스냅숏을 생성하여 구독자의 연결 속성(로그인 및/또는 컴퓨터 이름)을 기준으로 다양한 구독자에 대한 각기 다른 초기 데이터 집합을 제공할 수 있습니다. 또한 구독자가 처음 동기화할 때 파티션에 사용할 수 있는 스냅숏을 가지고 있지 않은 경우 스냅숏 배달 및 생성을 요청할 수 있도록 선택할 수 있습니다. 자세한 내용은 [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요.  
  
## 옵션  
 **추가**  
 클릭 **추가** 파티션을 정의할 수 있습니다. 에 **데이터 파티션 추가** 대화 상자에 대 한 값을 지정 **host_name ()** 및/또는 **suser_sname ()**, 스냅숏을 새로 고칠 일정을 정의 합니다.  
  
 **편집**  
 표에서 기존 파티션을 선택 하 고 클릭 **편집** 파티션을 편집 합니다.  
  
 **Delete**  
 표에서 기존 파티션을 선택 하 고 클릭 **삭제** 파티션을 삭제 합니다.  
  
 **선택한 스냅숏 지금 생성**  
 표에서 하나 이상의 파티션을 선택 하 고 클릭 **선택한 스냅숏 지금 생성** 이러한 파티션에 대 한 스냅숏을 생성할 수 있습니다.  
  
 **기존 스냅숏 정리**  
 표에서 하나 이상의 파티션을 선택 하 고 클릭 **기존 스냅숏 정리** 를 이러한 파티션에 대 한 스냅숏을 정리 합니다.  
  
 **새 구독자가 동기화할 때 필요한 경우 자동으로 파티션 정의 및 스냅숏 생성**  
 구독자가 스냅숏 생성 및 적용을 요청할 수 있도록 할 경우 이 옵션을 선택합니다. 구독자가 처음 동기화할 때 파티션에 사용할 수 있는 스냅숏을 가지고 있지 않은 경우 이 옵션이 필요할 수 있습니다.  
  
## 참고 항목  
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [매개 변수가 있는 필터를 사용하는 병합 게시의 스냅숏](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  