---
title: "MSSQL_ENG020598 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG020598 error
ms.assetid: 1c3032f2-23d1-4ead-94ee-16ac4d75cd0c
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 46ca28952a628032fc98fe0fb78f603c4101f726
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="mssqleng020598"></a>MSSQL_ENG020598
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|20598|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|복제된 명령을 적용하는 동안 구독자에서 행을 찾을 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 배포 에이전트가 구독자에서 행을 업데이트하려고 하지만 해당 행이 삭제되었거나 해당 행의 기본 키가 변경된 경우 트랜잭션 복제에서 이 오류가 발생합니다. 기본적으로 변경 내용은 게시자로 다시 전파되지 않기 때문에 트랜잭션 게시에 대한 구독자는 읽기 전용으로 취급됩니다. 트랜잭션 복제의 경우 업데이트할 수 있는 구독이나 피어 투 피어 복제를 사용하는 경우에만 사용자가 구독자에서 변경해야 합니다. 이러한 옵션에 대한 자세한 내용은 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md) 및 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)를 참조하십시오.  
  
## <a name="user-action"></a>사용자 동작  
 **이 문제를 해결하려면**  
  
1.  오류 원인을 식별하는 동안 복제가 계속되어야 하는 경우 배포 에이전트에 매개 변수 **-SkipErrors 20598** 을 지정합니다. 이렇게 하면 에이전트는 오류 20598이 발생한 변경 내용을 건너뛰고 다른 변경 내용을 복제할 수 있습니다.  
  
2.  구독자에서 삭제되었거나 기본 키가 게시자의 해당 행과 일치하지 않는 행을 식별합니다. [tablediff Utility](../../tools/tablediff-utility.md) 를 사용하여 게시 및 구독 데이터베이스에서 일치하지 않는 행을 확인할 수 있습니다. 복제된 데이터베이스에서 이 유틸리티를 사용하는 방법은 [복제된 테이블의 차이점 비교&#40;복제 프로그래밍&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)를 참조하세요.  
  
3.  **tablediff** 유틸리티나 다른 방법을 사용하여 구독자에서 행을 수정합니다.  
  
4.  (선택 사항) **-SkipErrors** 매개 변수를 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
