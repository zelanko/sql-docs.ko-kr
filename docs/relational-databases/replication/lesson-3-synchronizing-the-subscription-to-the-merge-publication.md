---
title: '3단원: 병합 게시에 구독 동기화 | Microsoft 문서'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79b8774de74316a4595d7ebd028b9f2e853882bd
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
# <a name="lesson-3-synchronizing-the-subscription-to-the-merge-publication"></a>3단원: 병합 게시에 구독 동기화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 단원에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 병합 에이전트를 시작하여 구독을 초기화합니다. 또한 이 절차를 사용하여 게시자와 동기화합니다. 이 단원을 수행하려면 이전 단원인 [2단원: 병합 게시에 대한 구독 만들기](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md)를 완료해야 합니다.  
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>동기화를 시작하고 구독을 초기화하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구독자에 연결하고 해당 서버 노드를 확장한 다음 **복제** 폴더를 확장합니다.  
  
2.  **로컬 구독** 폴더에서 **SalesOrdersReplica** 데이터베이스의 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기**를 클릭합니다.  
  
3.  **시작** 을 클릭하여 구독을 초기화합니다.  
  
## <a name="next-steps"></a>Next Steps  
병합 에이전트를 실행하여 동기화를 시작하고 구독을 초기화했습니다. 또한 게시자나 구독자에 있는 **SalesOrderHeader** 나 **SalesOrderDetail** 테이블에서 데이터를 삽입, 업데이트 또는 삭제할 수 있고 네트워크가 연결되어 있을 때 이 절차를 반복하여 게시자와 구독자 사이의 데이터를 동기화한 다음 다른 서버에 있는 **SalesOrderHeader** 나 **SalesOrderDetail** 테이블을 쿼리하여 복제된 변경 내용을 볼 수 있습니다.  
  
이로써 모바일 클라이언트와의 데이터 복제 자습서를 마쳤습니다. 트랜잭션 복제를 사용하는 유사한 자습서를 보려면 [Tutorial: Replicating Data Between Continuously Connected Servers](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
[스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[데이터 동기화](../../relational-databases/replication/synchronize-data.md)  
[끌어오기 구독 동기화](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
