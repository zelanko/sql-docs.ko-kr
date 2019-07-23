---
title: 업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드 전환 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, update modes
- subscriptions [SQL Server replication], updatable
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0b7ea891c0c4ee5dfbcd8301cff4e364dcd5cae7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909232"
---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드 전환
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 업데이트된 트랜잭션 구독에 대한 업데이트 모드를 전환하는 방법에 대해 설명합니다. 새 구독 마법사를 사용하여 업데이트할 수 있는 구독에 대한 모드를 지정합니다. 이 마법사를 사용할 때 모드를 설정하는 방법은 [끌어오기 구독 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 업데이트 가능한 트랜잭션 구독에 대한 업데이트 모드를 전환하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   언제든지 즉시 업데이트에서 지연 업데이트로 장애 조치할 수 있습니다. 그러나 장애 조치한 후에는 구독자와 게시자가 연결되고 큐 판독기 에이전트에서 큐의 보류 중인 모든 메시지를 게시자에 적용할 때까지는 즉시 업데이트로 되돌릴 수 없습니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   트랜잭션 게시에 대한 업데이트 구독이 한 업데이트 모드에서 다른 업데이트 모드로의 장애 조치를 지원하면 업데이트 모드를 프로그래밍 방식으로 전환하여 짧은 시간 동안 연결이 변경되는 경우를 처리할 수 있습니다. 업데이트 모드는 요청 시 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 설정할 수 있습니다. 자세한 내용은 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)에서 업데이트된 트랜잭션 구독에 대한 업데이트 모드를 전환하는 방법에 대해 설명합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
> [!NOTE]  
>  구독이 생성된 후에 업데이트 모드를 변경하려면 구독이 생성될 때 **update_mode** 속성을 즉시 업데이트에서 지연 업데이트로 전환할 수 있는 **failover** 또는 지연 업데이트에서 즉시 업데이트로 전환할 수 있는 **queued failover** 로 설정합니다. 이러한 속성은 새 구독 마법사에서 자동으로 설정됩니다.  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>밀어넣기 구독에 대한 업데이트 모드를 설정하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  업데이트 모드를 설정하려는 구독을 마우스 오른쪽 단추로 클릭한 다음 **업데이트 방법 설정**을 클릭합니다.  
  
4.  **업데이트 방법 설정 - \<Subscriber>: \<SubscriptionDatabase>** 대화 상자에서 **즉시 업데이트** 또는 **지연 업데이트**를 선택합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>끌어오기 구독에 대한 업데이트 모드를 설정하려면  
  
1.  **구독 속성 - \<Publisher>: \<PublicationDatabase>** 대화 상자에서 **구독자 업데이트 방법** 옵션에 대해 **즉시 변경 내용 복제** 또는 **변경 내용 대기** 중 하나를 선택합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **구독 속성 - \<Publisher>: \<PublicationDatabase>** 대화 상자에 액세스하는 방법에 대한 자세한 내용은 [끌어오기 구독 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-switch-between-update-modes"></a>업데이트 모드를 전환하려면  
  
1.  끌어오기 구독의 경우 [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) , 밀어넣기 구독의 경우 [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) 을 실행하여 구독에서 장애 조치가 지원되는지 확인합니다. 결과 집합의 **업데이트 모드** 값이 **3** 또는 **4**이면 장애 조치가 지원됩니다.  
  
2.  구독 데이터베이스의 구독자에서 [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)를 실행합니다. **@publisher** , **@publisher_db** , **@publication** 를 지정하고 **@failover_mode** 에 다음 값 중 하나를 지정합니다.  
  
    -   **queued** - 연결이 일시적으로 끊어진 경우 지연 업데이트로 장애 조치합니다.  
  
    -   **immediate** - 연결이 복원되었을 때 즉시 업데이트로 장애 초지합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
