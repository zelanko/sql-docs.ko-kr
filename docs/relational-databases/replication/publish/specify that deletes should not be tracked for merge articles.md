---
title: "병합 아티클에 대해 삭제가 추적되지 않도록 지정(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
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
  - "조건부 삭제 추적 [SQL Server 복제]"
  - "병합 복제 [SQL Server 복제], 조건부 삭제 추적"
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 병합 아티클에 대해 삭제가 추적되지 않도록 지정(복제 Transact-SQL 프로그래밍)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 기본적으로 병합 복제는 게시자와 구독자 간에 DELETE 명령을 동기화합니다. 병합 복제에서는 행을 게시에서 삭제한 경우에도 구독 데이터베이스에는 그대로 유지할 수 있으며 반대의 경우도 마찬가지입니다. 새 아티클을 만들 때 DELETE 명령을 무시할지 여부를 프로그래밍 방식으로 지정할 수 있으며 복제 저장 프로시저를 사용하여 이 기능을 나중에 활성화할 수도 있습니다.  
  
> [!IMPORTANT]  
>  이 기능을 활성화하면 불일치가 발생합니다. 이는 구독자에 있는 데이터가 게시자에 있는 데이터를 정확하게 반영하지 않음을 의미합니다. 이 경우 삭제된 행을 수동으로 제거하기 위한 메커니즘을 직접 구현해야 합니다.  
  
### 새 병합 아티클에 대해 삭제가 무시되도록 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle & #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. 값을 지정 **false** 에 대 한 **@delete_tracking**합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
    > [!NOTE]  
    >  아티클의 원본 테이블이 이미 다른 게시의 값에 게시 된 경우 **delete_tracking** 두 아티클에 대해 동일 해야 합니다.  
  
### 기존 병합 아티클에 대해 삭제가 무시되도록 지정하려면  
  
1.  아티클에 대 한 오류 보정을 사용할 수 있는지를 확인 하려면 실행 [sp_helpmergearticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) 값을 확인 하 고 **delete_tracking** 결과 집합에 있습니다. 이 값이 **0**이면 삭제가 이미 무시되고 있는 것입니다.  
  
2.  1 단계에서 값이 **1**, 실행 [sp_changemergearticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 게시 데이터베이스의 게시자입니다. 값을 지정 **delete_tracking** 에 대 한 **@property**, 및의 값 **false** 에 대 한 **@value**합니다.  
  
    > [!NOTE]  
    >  아티클의 원본 테이블이 이미 다른 게시의 값에 게시 된 경우 **delete_tracking** 두 아티클에 대해 동일 해야 합니다.  
  
## 참고 항목  
 [조건부 삭제 추적으로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  