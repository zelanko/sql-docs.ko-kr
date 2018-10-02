---
title: 병합 게시에 대한 충돌 정보 보기 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- sp_helpmergeconflictrows
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
- sp_helpmergearticleconflicts
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ed864c44fef3e5ca6305010fdc62a786331afe7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847381"
---
# <a name="view-conflict-information-for-merge-publications"></a>병합 게시에 대한 충돌 정보 보기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  병합 복제의 충돌을 해결하는 과정에서 무시되는 행의 데이터는 충돌 테이블에 기록됩니다. 복제 저장 프로시저를 사용하여 이 충돌 데이터를 프로그래밍 방식으로 볼 수 있습니다. 자세한 내용은 [고급 병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)을 참조하세요.  
  
### <a name="to-view-conflict-information-and-losing-row-data-for-all-types-of-conflicts"></a>충돌 정보와 모든 유형의 충돌에 대한 무시되는 열 데이터를 보려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)을 실행합니다. 결과 집합에서 다음 열의 값을 확인합니다.  
  
    -   **centralized_conflicts** - 1은 충돌 행이 게시자에 저장된다는 것을 의미하며, 0은 충돌 행이 게시자에 저장되지 않는다는 것을 의미합니다.  
  
    -   **decentralized_conflicts** - 1은 충돌 행이 구독자에 저장된다는 것을 의미하며, 0은 충돌 행이 구독자에 저장되지 않는다는 것을 의미합니다.  
  
        > [!NOTE]  
        >  병합 게시의 충돌 로깅 방식은 **@conflict_logging** 의 [@conflict_logging](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)을(를) 참조하세요. **@centralized_conflicts** 매개 변수는 사용되지 않습니다.  
  
     다음 표에서는 **@conflict_logging**을(를) 참조하세요.  
  
    |@conflict_logging 값|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**subscriber**|0|1|  
    |**both**|1|1|  
  
2.  게시 데이터베이스의 게시자나 구독 데이터베이스의 구독자에서 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)를 실행합니다. 특정 게시에 속한 아티클에 대한 충돌 정보만 반환하도록 하려면 **@publication** 의 값을 지정합니다. 이렇게 하면 충돌이 있는 아티클에 대한 충돌 테이블 정보가 반환됩니다. 정보를 보려는 아티클의 **conflict_table** 값을 확인합니다. 아티클에 대한 **conflict_table** 값이 NULL인 경우 이 아티클에 삭제 충돌만 발생한 것입니다.  
  
3.  필요에 따라 특정 아티클의 충돌 행을 검토합니다. 1단계에서 확인한 **centralized_conflicts** 및 **decentralized_conflicts** 값에 따라 다음 중 한 가지를 수행합니다.  
  
    -   게시 데이터베이스의 게시자에서 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)를 실행합니다. **@conflict_table**에 아티클에 대한 충돌 테이블(1단계에서 확인)을 지정합니다. 필요에 따라 **@publication** 의 값을 지정하여 반환되는 충돌 정보를 특정 게시로 제한합니다. 이렇게 하면 무시되는 행에 대한 행 데이터 및 기타 정보가 반환됩니다.  
  
    -   구독 데이터베이스의 구독자에서 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)를 실행합니다. **@conflict_table**에 아티클에 대한 충돌 테이블(1단계에서 확인)을 지정합니다. 이렇게 하면 무시되는 행에 대한 행 데이터 및 기타 정보가 반환됩니다.  
  
### <a name="to-view-information-only-on-conflicts-where-the-delete-failed"></a>삭제가 실패한 충돌에 대한 정보만 보려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)을 실행합니다. 결과 집합에서 다음 열의 값을 확인합니다.  
  
    -   **centralized_conflicts** - 1은 충돌 행이 게시자에 저장된다는 것을 의미하며, 0은 충돌 행이 게시자에 저장되지 않는다는 것을 의미합니다.  
  
    -   **decentralized_conflicts** - 1은 충돌 행이 구독자에 저장된다는 것을 의미하며, 0은 충돌 행이 구독자에 저장되지 않는다는 것을 의미합니다.  
  
        > [!NOTE]  
        >  병합 게시의 충돌 로깅 방식은 **@conflict_logging** 의 [@conflict_logging](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)을(를) 참조하세요. **@centralized_conflicts** 매개 변수는 사용되지 않습니다.  
  
2.  게시 데이터베이스의 게시자나 구독 데이터베이스의 구독자에서 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)를 실행합니다. 특정 게시에 속한 아티클에 대한 충돌 정보만 반환하도록 하려면 **@publication** 의 값을 지정합니다. 이렇게 하면 충돌이 있는 아티클에 대한 충돌 테이블 정보가 반환됩니다. 정보를 보려는 아티클의 **source_object** 값을 확인합니다. 아티클에 대한 **conflict_table** 값이 NULL인 경우 이 아티클에 삭제 충돌만 발생한 것입니다.  
  
3.  필요에 따라 삭제 충돌에 대한 충돌 정보를 검토합니다. 1단계에서 확인한 **centralized_conflicts** 및 **decentralized_conflicts** 값에 따라 다음 중 한 가지를 수행합니다.  
  
    -   게시 데이터베이스의 게시자에서 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)를 실행합니다. **@source_object**에는 충돌이 발생한 원본 테이블의 이름(1단계에서 확인)을 지정합니다. 필요에 따라 **@publication** 의 값을 지정하여 반환되는 충돌 정보를 특정 게시로 제한합니다. 이렇게 하면 게시자에 저장된 삭제 충돌 정보가 반환됩니다.  
  
    -   구독 데이터베이스의 구독자에서 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)를 실행합니다. **@source_object**에는 충돌이 발생한 원본 테이블의 이름(1단계에서 확인)을 지정합니다. 필요에 따라 **@publication** 의 값을 지정하여 반환되는 충돌 정보를 특정 게시로 제한합니다. 이렇게 하면 구독자에 저장된 삭제 충돌 정보가 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
