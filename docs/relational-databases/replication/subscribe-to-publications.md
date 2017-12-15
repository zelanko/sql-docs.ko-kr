---
title: "게시 구독 | Microsoft 문서"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.conc.subtopubs.f1
helpviewer_keywords:
- subscriptions [SQL Server replication], about subscriptions
- pull subscriptions [SQL Server replication]
- subscriptions [SQL Server replication]
- push subscriptions [SQL Server replication], about push subscriptions
- merge replication subscribing [SQL Server replication]
- merge replication subscribing [SQL Server replication], about subscribing
- publications [SQL Server replication], subscribing
- push subscriptions [SQL Server replication]
- pull subscriptions [SQL Server replication], about pull subscriptions
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 088ee30a-05ab-47c4-92ed-316b93e12445
caps.latest.revision: "44"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4613a7ee6306ba86b5748377f20c1cf48117815
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="subscribe-to-publications"></a>게시 구독
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] 구독은 게시에 있는 데이터 및 데이터베이스 개체 복사본에 대한 요청입니다. 구독은 어떤 게시를 언제 어디서 받을 것인지를 정의합니다. 구독을 계획하는 경우 에이전트 처리를 수행할 위치를 고려합니다. 선택한 구독 유형에 따라 에이전트가 실행되는 위치가 결정됩니다. 밀어넣기 구독을 사용하면 병합 에이전트 또는 배포 에이전트가 배포자에서 실행되고 끌어오기 구독을 사용하면 에이전트가 구독자에서 실행됩니다. 구독을 만든 후에는 해당 유형을 변경할 수 없습니다.  
  
|구독|특징|사용 시기|  
|------------------|---------------------|--------------|  
|밀어넣기 구독|밀어넣기 구독의 경우 게시자는 구독자의 요청 없이 변경 내용을 구독자로 전파합니다. 변경 내용은 요청 시나 계속적으로 또는 일정에 따라 구독자로 전달됩니다. 배포 에이전트 또는 병합 에이전트는 배포자에서 실행됩니다.|데이터가 일반적으로 계속 또는 정기적으로 자주 동기화되는 경우<br /><br /> 게시가 실시간에 가까운 데이터 이동을 요구하는 경우<br /><br /> 배포자에서 프로세서 오버헤드가 증가해도 성능에 영향을 주지 않는 경우<br /><br /> 스냅숏과 트랜잭션 복제에 가장 많이 사용되는 경우|  
|끌어오기 구독|끌어오기 구독의 경우 구독자는 게시자의 변경 내용을 요청합니다. 끌어오기 구독을 사용하면 구독자에 있는 사용자가 데이터 변경 내용의 동기화 시기를 지정할 수 있습니다. 배포 에이전트 또는 병합 에이전트는 구독자에서 실행됩니다.|데이터는 일반적으로 계속 동기화되지 않고 요청 시 또는 일정에 따라 동기화되는 경우<br /><br /> 게시에 많은 구독자가 있으며 배포자에서 모든 에이전트를 실행하는 데 너무 많은 리소스가 필요한 경우<br /><br /> 구독자가 자치적이거나, 연결이 끊어졌거나 이동 중인 경우. 구독자는 언제 연결하여 변경 내용을 동기화할 것인지를 결정합니다.<br /><br /> 병합 복제에 가장 많이 사용되는 경우|  
  
## <a name="merge-replication-subscription-types"></a>병합 복제 구독 유형  
 모든 복제 유형은 밀어넣기 및 끌어오기 구독을 허용합니다. 병합 복제는 클라이언트 구독과 서버 구독이라는 두 개의 추가 용어를 사용하여 구독을 구분합니다. 클라이언트 구독 유형과 서버 구독 유형은 모두 밀어넣기 및 끌어오기 구독에 사용할 수 있습니다. 클라이언트 구독은 대부분의 구독자에 적합한 반면 서버 구독은 일반적으로 데이터를 다른 구독자에게 다시 게시하는 구독자에 사용됩니다. 선택한 구독 유형은 충돌 해결에도 영향을 줍니다.  
  
## <a name="non-sql-server-subscribers"></a>SQL Server 이외 구독자  
 Oracle 및 IBM DB2는 밀어넣기 구독을 사용하여 스냅숏 및 트랜잭션 게시를 구독할 수 있습니다. 자세한 내용은 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)을(를) 참조하세요.  
  
## <a name="creating-subscriptions"></a>구독 만들기  
 구독을 만들려면 다음 정보를 제공하십시오.  
  
-   게시의 이름입니다.  
  
-   구독자 및 구독 데이터베이스 이름  
  
-   배포 에이전트 또는 병합 에이전트가 배포자 또는 구독자에서 실행되는지의 여부  
  
-   배포 에이전트 또는 병합 에이전트가 계속 실행되는지, 일정에 따라 또는 요청 시에만 실행되는지의 여부  
  
-   스냅숏 에이전트에서 구독에 대한 초기 스냅숏을 만들어야 하는지, 배포 에이전트 또는 병합 에이전트가 해당 스냅숏을 구독자에서 적용해야 하는지의 여부  
  
-   배포 에이전트 또는 병합 에이전트가 실행될 계정  
  
-   병합 복제의 경우 구독 유형은 서버 및 클라이언트입니다.  
  
 **밀어넣기 구독을 만들려면**  
  
 [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)  
  
 **밀어넣기 구독 속성을 보거나 수정하려면**  
  
 [밀어넣기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
 **밀어넣기 구독을 삭제하려면**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [밀어넣기 구독 삭제](../../relational-databases/replication/delete-a-push-subscription.md)  
  
> [!NOTE]  
>  구독을 삭제해도 게시된 개체가 구독자에서 제거되지 않습니다.  
  
 **끌어오기 구독을 만들려면**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)  
  
 **끌어오기 구독 속성을 보거나 수정하려면**  
  
 [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
 **끌어오기 구독을 삭제하려면**  
  
 [끌어오기 구독 삭제](../../relational-databases/replication/delete-a-pull-subscription.md)  
  
## <a name="see-also"></a>관련 항목:  
 [구독자 보안 설정](../../relational-databases/replication/security/secure-the-subscriber.md)   
 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
