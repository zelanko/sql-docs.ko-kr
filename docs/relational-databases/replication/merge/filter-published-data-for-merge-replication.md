---
title: "병합 복제의 게시된 데이터 필터링 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "병합 복제 [SQL Server 복제], 게시된 데이터 필터링"
  - "복제 [SQL Server], 게시된 데이터 필터링"
ms.assetid: 46c5023d-7a3b-4455-becc-e159fcb5d6c4
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 병합 복제의 게시된 데이터 필터링
  다른 복제 유형으로 정의할 수 있는 정적 행 필터와 열 필터 이외에 병합 복제는 매개 변수가 있는 행 필터 및 조인 필터를 제공합니다. 정적 행 필터와 열 필터에 대 한 자세한 내용은 참조 [데이터를 게시 하는 필터](../../../relational-databases/replication/publish/filter-published-data.md)합니다.  
  
 병합 복제는 모바일 사용자를 지원하는 여러 응용 프로그램에서 사용됩니다. 이러한 응용 프로그램에는 대개 많은 구독이 있으며 각 구독은 고유한 데이터 집합을 받습니다. 매개 변수가 있는 필터를 조인 필터와 함께 사용하면 관리자는 하나의 게시 또는 적은 수의 게시를 설정한 다음에도 다양한 데이터 집합을 사용자에게 제공할 수 있으므로 여러 게시를 만들 때 발생하는 관리 오버헤드를 줄일 수 있습니다.  
  
-   매개 변수가 있는 필터를 사용하면 게시를 여러 개 만들지 않아도 데이터의 다른 파티션을 다른 구독자에게 보낼 수 있습니다. 예를 들어 지정된 판매 담당자의 데이터가 해당 담당자에게만 복제되도록 테이블을 필터링할 수 있습니다. 매개 변수가 있는 필터의 다양한 옵션을 활용하여 성능을 최적화하고 데이터 및 응용 프로그램 요구 사항에 가장 적합한 필터링을 만들 수 있습니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)을 참조하세요.  
  
-   조인 필터는 일반적으로 필터를 관련 테이블로 확장하기 위해 매개 변수가 있는 필터와 함께 사용되며 정적 필터와 함께 사용할 수도 있습니다. 예를 들어 판매 담당자는 일반적으로 고객 테이블 및 주문 테이블과 같은 다른 테이블에 데이터를 저장합니다. 판매 담당자가 자신의 고객 및 고객의 주문에 대한 정보만을 받을 수 있도록 이러한 정보를 필터링할 수 있습니다. 자세한 내용은 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)을(를) 참조하세요.  
  
 필터는 행 식별을 위해 복제에 사용된 **rowguidcol** 을 포함하지 않아야 합니다. 기본적으로 이 열은 병합 복제를 설정할 때 추가된 열이며 이름은 **rowguid**입니다.  
  
## 참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  