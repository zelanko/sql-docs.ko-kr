---
title: "트랜잭션 게시에 대한 백업으로 초기화 설정(SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "수동 구독 초기화 [SQL Server 복제]"
  - "구독 [SQL Server 복제], 초기화"
  - "구독 초기화 [SQL Server 복제], 스냅숏 없음"
  - "트랜잭션 복제, 백업 및 복원"
  - "백업 [SQL Server 복제], 트랜잭션 복제"
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 트랜잭션 게시에 대한 백업으로 초기화 설정(SQL Server Management Studio)
  백업에서 트랜잭션 게시에 대한 구독을 초기화하려면 백업에서 초기화할 수 있도록 게시를 설정한 다음 구독을 만들 때 백업 정보를 지정합니다.  
  
-   게시를 사용 하도록 설정 된 **구독 옵션** 의 페이지는 **게시 속성-\< 게시>** 대화 상자. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
-   저장된 프로시저와 함께 백업 정보를 지정 [sp_addsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 필요한 매개 변수에 대 한 자세한 내용은 **sp_addsubscription**, 참조 [백업 & #40;에서 트랜잭션 구독 초기화 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/initialize a transactional subscription from a backup.md)합니다.  
  
### 백업으로 초기화를 설정하려면  
  
1.  에 **구독 옵션** 의 페이지는 **게시 속성-\< 게시>** 대화 상자에서 값 선택 **True** 에 대 한는 **백업 파일로 초기화 허용** 옵션입니다.  
  
## 참고 항목  
 [스냅숏 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  