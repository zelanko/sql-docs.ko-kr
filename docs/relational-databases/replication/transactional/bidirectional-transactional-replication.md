---
title: "양방향 트랜잭션 복제 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: "27"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa0124b90d473d3960891b67901c972aa0f51b81
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="bidirectional-transactional-replication"></a>양방향 트랜잭션 복제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 양방향 트랜잭션 복제는 두 개의 서버가 서로 변경 내용을 교환할 수 있는 특수 트랜잭션 복제 토폴로지입니다. 각 서버는 데이터를 게시한 다음 상대 서버에서 게시한 것과 동일한 데이터가 포함된 게시를 구독합니다. [sp_addsubscription&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)의 **@loopback_detection** 매개 변수를 TRUE로 설정하면 변경 내용이 구독자에게만 전송되고 다시 게시자에게 전송되지 않습니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서는 피어 투 피어 트랜잭션 복제에서도 이 토폴로지가 지원되지만 양방향 복제를 사용하면 성능이 향상될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
