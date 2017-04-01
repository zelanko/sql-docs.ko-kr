---
title: "새 피어 초기화(피어 투 피어 복제) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.p2pwizard.init.f1"
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 새 피어 초기화(피어 투 피어 복제)
  **새 피어 초기화** 페이지를 사용하여 피어 데이터베이스가 초기화된 방법을 지정할 수 있습니다. 이 마법사를 완료하기 전에 피어를 초기화해야 합니다. 피어는 수동으로 초기화되거나 트랜잭션 복제에서 제공하는 **initialize with backup** 기능을 사용하여 초기화됩니다. 피어 투 피어 트랜잭션 복제는 스냅숏을 사용한 피어 초기화를 지원하지 않습니다. 여러 피어를 각각 다른 방법을 사용하여 초기화해야 하는 경우에는 이 마법사를 두 번 수행하여 피어를 개별적으로 추가해야 합니다.  
  
## 옵션  
 **새 피어 데이터베이스가 초기화된 방법을 지정하십시오.**  
 게시된 모든 개체의 스키마와 데이터가 각 피어에 있어야 합니다. 다음 옵션 중 하나를 선택합니다.  
  
-   게시된 개체의 스키마를 수동으로 만들었거나 백업을 복원했으며 백업이 만들어진 이후 첫 번째 게시 데이터베이스에서 데이터가 변경되지 않은 경우 첫 번째 옵션을 선택합니다. 스키마를 수동으로 만든 경우 필요한 모든 데이터가 각 피어에 있는지 확인해야 합니다. 이 옵션의 값에 해당 **복제 지원 전용** 구독 속성에 대 한 **sync_type**합니다.  
  
-   백업을 복원했으며 백업이 수행된 후 첫 번째 게시 데이터베이스에서 데이터가 변경된 경우 두 번째 옵션을 선택합니다. 이제 복제에서 백업에 포함되지 않은 첫 번째 게시 데이터베이스의 변경 내용을 배달합니다. 이 옵션의 값에 해당 **백업으로 초기화** 구독 속성에 대 한 **sync_type**합니다.  
  
     피어 투 피어 복제는 게시를 활성화 하는 경우는 **allow_initialize_from_backup** 게시 속성을 설정 합니다. 복제에서 즉시 첫 번째 게시 데이터베이스의 변경 내용을 추적하기 시작하므로 **initialize with backup** 옵션을 선택하면 하나 이상의 피어에 있는 복원된 데이터베이스에 변경 내용이 배달될 수 있습니다. 클릭는 **찾아보기** 를 사용 하는, 백업 찾습니다 및 복제 백업에서 로그 시퀀스 번호 (LSN)를 읽고 됩니다. 첫 번째 게시 데이터베이스에서 LSN이 높은 모든 변경 내용이 각 피어로 배달됩니다.  
  
     [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]가 포함된 토폴로지를 만들거나 해당 토폴로지에 추가할 경우 이 옵션을 사용하지 못할 수 있습니다. 다음 표에서는 기존 토폴로지에 노드를 추가할 때 이 옵션을 사용할 수 있는지 여부를 보여 줍니다.  
  
    |새 노드|첫 번째 노드|추가 노드|옵션|  
    |--------------|----------------|----------------------|------------|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|사용 안 함|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|없음|사용 안 함|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|사용 안 함|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|없음|설정|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|없음|설정|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|설정|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|없음|사용|  
  
## 참고 항목  
 [피어 투 피어 토폴로지 & #40; 관리 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [피어 투 피어 트랜잭션 복제](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  