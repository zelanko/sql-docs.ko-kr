---
title: "업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드 전환 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "트랜잭션 복제, 업데이트 가능 구독"
  - "업데이트 가능 구독, 업데이트 모드"
  - "구독 [SQL Server 복제], 업데이트 가능"
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드 전환
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 업데이트된 트랜잭션 구독에 대한 업데이트 모드를 전환하는 방법에 대해 설명합니다. 새 구독 마법사를 사용하여 업데이트할 수 있는 구독에 대한 모드를 지정합니다. 이 마법사를 사용 하는 경우 모드를 설정 하는 방법에 대 한 정보를 참조 하십시오. [뷰와 끌어오기 구독 속성을 수정](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드를 전환하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   언제든지 즉시 업데이트에서 지연 업데이트로 장애 조치할 수 있습니다. 그러나 장애 조치한 후에는 구독자와 게시자가 연결되고 큐 판독기 에이전트에서 큐의 보류 중인 모든 메시지를 게시자에 적용할 때까지는 즉시 업데이트로 되돌릴 수 없습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   트랜잭션 게시에 대한 업데이트 구독이 한 업데이트 모드에서 다른 업데이트 모드로의 장애 조치를 지원하면 업데이트 모드를 프로그래밍 방식으로 전환하여 짧은 시간 동안 연결이 변경되는 경우를 처리할 수 있습니다. 업데이트 모드는 요청 시 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 설정할 수 있습니다. 자세한 내용은 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)를 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
> [!NOTE]  
>  구독을 만든 후 업데이트 모드를 변경 하는 **update_mode** 속성으로 설정 되어 있어야 **장애 조치** (즉시 업데이트에서 스위치를 허용 하는 지연 업데이트) 또는 **장애 조치 대기** (지연 업데이트 하는 즉시 업데이트에서 전환할 수)는는 구독을 만들 때. 이러한 속성은 새 구독 마법사에서 자동으로 설정됩니다.  
  
#### 밀어넣기 구독에 대한 업데이트 모드를 설정하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  업데이트 모드를 설정 하 고 클릭 한 다음 구독을 마우스 오른쪽 단추로 클릭 **업데이트 방법 설정**합니다.  
  
4.  에 **업데이트 방법 설정-\< 구독자>: \< SubscriptionDatabase>** 대화 상자에서 **즉시 업데이트** 또는 **지연 업데이트**합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 끌어오기 구독에 대한 업데이트 모드를 설정하려면  
  
1.  에 **구독 속성-\< 게시자>: \< PublicationDatabase>** 대화 상자에서 값 선택 **즉시 변경 내용 복제** 또는 **변경 내용 대기** 에 대 한는 **구독자 업데이트 방법** 옵션입니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 에 액세스 하는 방법에 대 한 자세한 내용은 **구독 속성-\< 게시자>: \< PublicationDatabase>** 대화 상자, 참조 [뷰와 끌어오기 구독 속성을 수정](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### 업데이트 모드를 전환하려면  
  
1.  구독을 실행 하 여 장애 조치를 지원 하는지 확인 [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) 끌어오기 구독에 대 한 또는 [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) 밀어넣기 구독에 대 한 합니다. 결과 집합의 **업데이트 모드** 값이 **3** 또는 **4**이면 장애 조치가 지원됩니다.  
  
2.  구독 데이터베이스의 구독자에서 실행 [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)합니다. 지정 **@publisher**, **@publisher_db**, **@publication**, 는 다음 값 중 하나에 대 한 고 **@failover_mode**:  
  
    -   **큐에 대기** -연결이 일시적으로 끊긴 경우 지연 업데이트로 장애 조치 합니다.  
  
    -   **즉시** -연결이 복원 되 면 즉시 업데이트로 장애 조치 합니다.  
  
## 참고 항목  
 [트랜잭션 복제를 위한 업데이트 가능 구독](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  