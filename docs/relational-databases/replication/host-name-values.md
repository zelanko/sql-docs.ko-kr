---
title: "HOST_NAME 값 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.hostnamevalue.f1"
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# HOST_NAME 값
  매개 변수가 있는 필터가 포함된 병합 게시는 SUSER_SNAME() 함수 및/또는 HOST_NAME() 함수를 사용하여 데이터를 필터링합니다. 함수는 새 게시 마법사 또는 **게시 속성** 대화 상자에서 지정합니다.  
  
 기본적으로 HOST_NAME() 함수는 게시자에 연결하는 컴퓨터 이름을 반환합니다. 매개 변수가 있는 필터를 사용할 경우 이 마법사 페이지에서 값을 입력하여 이 값을 재정의하는 것이 일반적입니다. 그러면 HOST_NAME() 함수는 컴퓨터 이름 대신 사용자가 지정한 값을 반환합니다. 자세한 내용은의 "host_name () 값 재정의" 섹션을 참조 하십시오. [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
> [!NOTE]  
>  HOST_NAME()을 재정의할 경우 HOST_NAME() 함수에 대한 모든 호출은 사용자가 지정한 값을 반환합니다. 다른 응용 프로그램이 컴퓨터 이름을 반환하는 HOST_NAME()에 종속되지 않아야 합니다.  
  
## 옵션  
 **구독 속성**  
 각 구독자에 대 한 값을 입력 하면 **HOST_NAME 값** 열 하거나 구독자 컴퓨터의 이름인 기본값을 그대로.  
  
## 참고 항목  
 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)   
 [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)   
 [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [밀어넣기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME & #40. SQL 트랜잭션 & #41.](../../t-sql/functions/host-name-transact-sql.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  