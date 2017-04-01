---
title: "구독에 대한 만료 기간 설정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "구독 [SQL Server 복제], 만료"
  - "만료 [SQL Server 복제]"
  - "보존 기간 [SQL Server 복제]"
  - "구독 비활성화"
ms.assetid: 542f0613-5817-42d0-b841-fb2c94010665
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 구독에 대한 만료 기간 설정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 구독 만료 기간을 설정하는 방법에 대해 설명합니다. 구독 만료 기간은 구독이 만료되어 제거되기 전까지 유효한 기간을 나타냅니다. 자세한 내용은 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 구독에 대한 만료 기간을 설정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   구독 만료 기간을 *게시 보존 기간*이라고도 합니다. 병합 복제 메타데이터의 정리는 다음과 같이 이 설정의 영향을 받습니다.  
  
    -   보존 기간에 도달하기 전까지는 복제 작업을 통해 게시 및 구독 데이터베이스의 메타데이터를 정리할 수 없습니다. 보존 기간을 너무 길게 설정하면 복제 성능이 저하될 수 있으므로 주의해야 합니다. 보존 기간 내에 모든 구독자가 정기적으로 동기화될 가능성이 있으면 보존 기간을 낮은 값으로 설정하는 것이 좋습니다.  
  
         병합 게시의 보존 기간은 다양한 표준 시간대의 구독자를 수용하기 위해 24시간의 유예 기간을 갖습니다. 예를 들어 보존 기간을 하루로 설정한 경우 실제 보존 기간은 48시간이 됩니다.  
  
    -   구독이 만료되지 않도록 지정할 수 있지만 이 경우 메타데이터를 정리할 수 없으므로 이 값은 사용하지 않도록 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 구독에 대 한 만료 기간을 설정 된 **일반** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### 구독에 대한 만료 기간을 설정하려면  
  
1.  에 **구독 만료** 섹션에 **일반** 의 페이지는 **게시 속성-\< 게시>** 대화 상자 여부를 지정 합니다.  
  
2.  구독이 만료되어야 하는 경우 만료 기간을 지정합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 게시를 만들 때 이 값을 설정하거나 나중에 이 값을 수정할 수 있습니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 구독 만료 기간을 설정하려면  
  
1.  게시자에서 실행 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)합니다. 이때 **@retention**에 원하는 구독 만료 기간(시간)을 지정합니다. 기본 만료 기간은 336시간입니다. 자세한 내용은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
#### 병합 게시에 대한 구독 만료 기간을 설정하려면  
  
1.  게시자에서 실행 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다. 이때 **@retention**에 원하는 구독 만료 기간 값을 지정하고 에 대 한 만료 기간을 표시 하는 단위 지정 **@retention_period_unit**, 다음 중 하나일 수 있습니다.  
  
    -   **1** = 주  
  
    -   **2** = 월  
  
    -   **3** = 년  
  
     기본 만료 기간은 14일입니다. 자세한 내용은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
#### 스냅숏 또는 트랜잭션 게시에 대한 구독 만료 기간을 변경하려면  
  
1.  게시자에서 실행 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)합니다. 이때 **@property** 에 **retention** , **@value**에 새 구독 만료 기간(시간)을 지정합니다.  
  
#### 병합 게시에 대한 구독의 만료 기간을 변경하려면  
  
1.  게시자에서 실행 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), 로 지정 하 여 **@publication** 및 **@publisher**합니다. 값을 확인 **retention_period_unit** 에서 결과 집합은 다음 중 하나일 수 있습니다.  
  
    -   **0** = 일  
  
    -   **1** = 주  
  
    -   **2** = 월  
  
    -   **3** = 년  
  
2.  게시자에서 실행 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)합니다. 이때 **@property** 에 **retention** 을 지정하고 **@value**에 1단계에서 만든 보존 기간 단위에 따라 텍스트로 새 구독 만료 기간을 지정합니다.  
  
3.  (선택 사항) 게시자에서 실행 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)합니다. 지정 **retention_period_unit** 에 대 한 **@property** 및에 대 한 구독 만료 기간에 대 한 새 단위 **@value**합니다.  
  
## 참고 항목  
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [구독 만료 및 비활성화](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  