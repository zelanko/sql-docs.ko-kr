---
title: MSSQL_ENG002627 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG002627 error
ms.assetid: 7f4136ac-3784-4a41-a98c-8a02308e4883
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 787ad368e02cb2e8c2a39305aa186d5a04d8bd58
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049342"
---
# <a name="mssql_eng002627"></a>MSSQL_ENG002627
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2627|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름|해당 없음|  
|메시지 텍스트|%ls 제약 조건 '%.*ls'을(를) 위반했습니다. 개체 '%.\*ls'에 중복 키를 삽입할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 이 오류는 데이터베이스의 복제 여부에 관계없이 발생할 수 있는 일반 오류입니다. 복제된 데이터베이스에서 이 오류는 일반적으로 토폴로지 내에서 기본 키가 제대로 관리되지 않았기 때문에 발생합니다. 분산 환경에서는 둘 이상의 노드에서 기본 키 열 또는 다른 고유 열에 동일한 값이 삽입되지 않도록 해야 합니다. 가능한 원인은 다음과 같습니다.  
  
-   둘 이상의 노드에서 행 삽입 및 업데이트가 발생합니다. 병합 복제 및 트랜잭션 복제에 대한 업데이트할 수 있는 구독은 둘 다 충돌 감지 및 해결 기능을 제공하지만 한 노드에서만 특정 행을 삽입 또는 업데이트하는 것이 좋습니다. 피어 투 피어 트랜잭션은 충돌 감지 및 해결 기능을 제공하지 않으므로 삽입과 업데이트를 분할해야 합니다.  
  
-   읽기 전용이어야 하는 구독자에서 행이 삽입되었습니다. 업데이트할 수 있는 구독 또는 피어 투 피어 트랜잭션 복제를 사용하는 경우가 아니면 트랜잭션 게시에 대한 구독자와 마찬가지로 스냅샷 게시에 대한 구독자는 읽기 전용으로 취급되어야 합니다.  
  
-   ID 열이 있는 테이블이 사용되지만 해당 열이 적절히 관리되지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
 필요한 동작은 오류 발생 원인에 따라 다릅니다.  
  
-   둘 이상의 노드에서 행 삽입 및 업데이트가 발생합니다.  
  
     사용된 복제 유형에 관계없이 가능한 경우 삽입 및 업데이트를 분할하는 것이 좋습니다. 이렇게 하면 충돌 감지 및 해결 과정이 간편해집니다. 피어 투 피어 트랜잭션 복제의 경우 삽입과 업데이트를 분할해야 합니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
-   읽기 전용이어야 하는 구독자에서 행이 삽입되었습니다.  
  
     병합 복제, 업데이트할 수 있는 구독이 있는 트랜잭션 복제 또는 피어 투 피어 트랜잭션 복제를 사용하는 경우가 아니면 구독자에서 행을 삽입 또는 업데이트하지 마십시오.  
  
-   ID 열이 있는 테이블이 사용되지만 해당 열이 적절히 관리되지 않습니다.  
  
     병합 복제 및 업데이트할 수 있는 구독이 있는 트랜잭션 복제의 경우 ID 열은 복제에 의해 자동으로 관리됩니다. 피어 투 피어 트랜잭션 복제의 경우 ID 열을 수동으로 관리해야 합니다. 자세한 내용은 [ID 열 복제](publish/replicate-identity-columns.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)   
 [병합 복제](merge/merge-replication.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
