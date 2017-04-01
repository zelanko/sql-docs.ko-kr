---
title: "병합 테이블 아티클에 대한 처리 순서 지정(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
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
  - "아티클 [SQL Server 복제], 처리 순서"
  - "병합 복제 [SQL Server 복제], 아티클 처리 순서"
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 병합 테이블 아티클에 대한 처리 순서 지정(복제 Transact-SQL 프로그래밍)
  병합 복제를 사용하면 동기화 프로세스 중에 병합 에이전트에서 아티클을 처리하는 순서를 지정할 수 있습니다. 아티클을 작성할 때 복제 저장 프로시저를 사용하여 각 아티클 순서를 프로그래밍 방식으로 할당할 수 있습니다. 아티클은 최하위에서 최상위의 순서로 처리됩니다. 두 아티클의 값이 같으면 동시에 처리됩니다. 자세한 내용은 참조 [는 처리 순서의 병합 아티클을 지정](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)합니다.  
  
### 새 병합 아티클의 처리 순서를 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle & #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. 아티클 처리 순서를 나타내는 정수 값을 지정 **@processing_order**합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
    > [!NOTE]  
    >  정렬된 아티클을 만들려면 아티클 순서 값 사이에 간격을 두어야 합니다. 그러면 나중에 새 값을 쉽게 설정할 수 있습니다. 예를 들어 3 개 아티클의 고정된 처리 순서를 지정 해야 하는 경우 설정의 값 **@processing_order** 10, 20, 및 30 보다는 1, 2 및 3을 각각.  
  
### 병합 아티클의 처리 순서를 변경하려면  
  
1.  아티클의 처리 순서를 확인 하려면 실행 [sp_helpmergearticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) 값을 확인 하 고 **processing_order** 결과 집합에 있습니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 값을 지정 **processing_order** 에 대 한 **@property** 와 처리 순서를 나타내는 정수 값 **@value**합니다.  
  
## 참고 항목  
 [병합 아티클의 처리 순서 지정](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)  
  
  