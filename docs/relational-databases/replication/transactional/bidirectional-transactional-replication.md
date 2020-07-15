---
title: 양방향 트랜잭션 복제 | Microsoft 문서
description: 양방향 트랜잭션 복제로 두 서버가 변경 내용을 교환할 수 있습니다. 각 서버는 데이터를 게시하고 상대 서버의 게시를 구독합니다.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 903e92bd7eb306823189fdd80fd5968660f5c7e1
ms.sourcegitcommit: 19ff45e8a2f4193fe8827f39258d8040a88befc7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83807669"
---
# <a name="bidirectional-transactional-replication"></a>양방향 트랜잭션 복제
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  양방향 트랜잭션 복제는 두 개의 서버가 서로 변경 내용을 교환할 수 있는 특수 트랜잭션 복제 토폴로지입니다. 각 서버는 데이터를 게시한 다음 상대 서버에서 게시한 것과 동일한 데이터가 포함된 게시를 구독합니다. [sp_addsubscription&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)의 `@loopback_detection` 매개 변수를 TRUE로 설정하면 변경 내용이 구독자에게만 전송되고 게시자에게 다시 전송되지 않습니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서는 피어 투 피어 트랜잭션 복제에서도 이 토폴로지가 지원되지만 양방향 복제를 사용하면 성능이 향상될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
