---
title: "병합 게시에 대한 충돌 정보 보기(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "병합 복제 충돌 해결 [SQL Server 복제], 충돌 보기"
  - "sp_helpmergeconflictrows"
  - "충돌 정보 보기"
  - "충돌 해결 [SQL Server 복제], 병합 복제"
  - "sp_helpmergearticleconflicts"
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 병합 게시에 대한 충돌 정보 보기(복제 Transact-SQL 프로그래밍)
  병합 복제의 충돌을 해결하는 과정에서 무시되는 행의 데이터는 충돌 테이블에 기록됩니다. 복제 저장 프로시저를 사용하여 이 충돌 데이터를 프로그래밍 방식으로 볼 수 있습니다. 자세한 내용은 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)을 참조하세요.  
  
### 충돌 정보와 모든 유형의 충돌에 대한 무시되는 열 데이터를 보려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)합니다. 결과 집합에서 다음 열의 값을 확인합니다.  
  
    -   **centralized_conflicts** -1은 게시자에서 충돌 행을 저장 하 고 0은 충돌 행은 게시자에 저장 되지 않은 나타냅니다.  
  
    -   **decentralized_conflicts** -1은 구독자에서 충돌 행을 저장 하 고 0은 충돌 행은 구독자에 저장 되지 않는다는 나타냅니다.  
  
        > [!NOTE]  
        >  사용 하 여 병합 게시의 충돌 로깅 동작이 설정 되어는 **@conflict_logging** 의 매개 변수 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다. 사용 하 여는 **@centralized_conflicts** 매개 변수는 사용 되지 않습니다.  
  
     다음 표에서 지정 된 값에 따라 이러한 열의 값을 설명 **@conflict_logging**합니다.  
  
    |@conflict_logging 값|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**subscriber**|0|1|  
    |**both**|1|1|  
  
2.  게시 데이터베이스의 게시자 또는 구독 데이터베이스의 구독자에서 실행 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)합니다. 특정 게시에 속한 아티클에 대한 충돌 정보만 반환하도록 하려면 **@publication** 의 값을 지정합니다. 이렇게 하면 충돌이 있는 아티클에 대한 충돌 테이블 정보가 반환됩니다. 값을 확인 **conflict_table** 관심 있는 모든 기사에 대 한 합니다. 하는 경우의 값 **conflict_table** 삭제 충돌만이 문서에서 발생 한 아티클을 NULL입니다.  
  
3.  필요에 따라 특정 아티클의 충돌 행을 검토합니다. 값에 따라 **centralized_conflicts** 및 **decentralized_conflicts** 1 단계에서 다음 중 하나를 수행 합니다.  
  
    -   게시 데이터베이스의 게시자에서 실행 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)합니다. (1 단계)에서 문서에 대 한 충돌 테이블을 지정 **@conflict_table**합니다. (선택 사항) 값을 지정 **@publication** 특정 게시에 반환 된 충돌 정보를 제한할 수 있습니다. 이렇게 하면 무시되는 행에 대한 행 데이터 및 기타 정보가 반환됩니다.  
  
    -   구독 데이터베이스의 구독자에서 실행 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)합니다. (1 단계)에서 문서에 대 한 충돌 테이블을 지정 **@conflict_table**합니다. 이렇게 하면 무시되는 행에 대한 행 데이터 및 기타 정보가 반환됩니다.  
  
### 삭제가 실패한 충돌에 대한 정보만 보려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)합니다. 결과 집합에서 다음 열의 값을 확인합니다.  
  
    -   **centralized_conflicts** -1은 게시자에서 충돌 행을 저장 하 고 0은 충돌 행은 게시자에 저장 되지 않은 나타냅니다.  
  
    -   **decentralized_conflicts** -1은 구독자에서 충돌 행을 저장 하 고 0은 충돌 행은 구독자에 저장 되지 않는다는 나타냅니다.  
  
        > [!NOTE]  
        >  병합 게시의 충돌 로깅 동작이 사용 하 여 설정 되는 **@conflict_logging** 의 매개 변수 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다. 사용 하 여는 **@centralized_conflicts** 매개 변수는 사용 되지 않습니다.  
  
2.  게시 데이터베이스의 게시자 또는 구독 데이터베이스의 구독자에서 실행 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)합니다. 특정 게시에 속한 아티클에 대한 충돌 테이블 정보만 반환하도록 **@publication** 의 값을 지정합니다. 이렇게 하면 충돌이 있는 아티클에 대한 충돌 테이블 정보가 반환됩니다. 값을 확인 **source_object** 관심 있는 모든 기사에 대 한 합니다. 하는 경우의 값 **conflict_table** 삭제 충돌만이 문서에서 발생 한 아티클을 NULL입니다.  
  
3.  필요에 따라 삭제 충돌에 대한 충돌 정보를 검토합니다. 값에 따라 **centralized_conflicts** 및 **decentralized_conflicts** 1 단계에서 다음 중 하나를 수행 합니다.  
  
    -   게시 데이터베이스의 게시자에서 실행 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)합니다. 에 대 한 발생 한 충돌 (1 단계)에서 원본 테이블의 이름을 지정 **@source_object**합니다. (선택 사항) 값을 지정 **@publication** 특정 게시에 반환 된 충돌 정보를 제한할 수 있습니다. 이렇게 하면 게시자에 저장된 삭제 충돌 정보가 반환됩니다.  
  
    -   구독 데이터베이스의 구독자에서 실행 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)합니다. 에 대 한 발생 한 충돌 (1 단계)에서 원본 테이블의 이름을 지정 **@source_object**합니다. (선택 사항) 값을 지정 **@publication** 특정 게시에 반환 된 충돌 정보를 제한할 수 있습니다. 이렇게 하면 구독자에 저장된 삭제 충돌 정보가 반환됩니다.  
  
## 참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  