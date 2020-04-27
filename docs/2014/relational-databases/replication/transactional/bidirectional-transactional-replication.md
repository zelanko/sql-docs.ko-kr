---
title: 양방향 트랜잭션 복제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2cf5fbf215338b273be0924e6930906c8698aff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63188598"
---
# <a name="bidirectional-transactional-replication"></a>양방향 트랜잭션 복제
  양방향 트랜잭션 복제는 두 개의 서버가 서로 변경 내용을 교환할 수 있는 특수 트랜잭션 복제 토폴로지입니다. 각 서버는 데이터를 게시한 다음 상대 서버에서 게시한 것과 동일한 데이터가 포함된 게시를 구독합니다. **@loopback_detection** [Sp_addsubscription &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) 매개 변수를 TRUE로 설정 하 여 변경 내용이 구독자에만 전송 되 고 변경 내용이 게시자로 다시 전송 되지 않도록 합니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서는 피어 투 피어 트랜잭션 복제에서도 이 토폴로지가 지원되지만 양방향 복제를 사용하면 성능이 향상될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [@loopback_detection](peer-to-peer-transactional-replication.md)  
  
  
