---
title: "구독자 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subscribers.f1"
helpviewer_keywords: 
  - "구독자 [SQL Server 복제]"
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 구독자
  지정 된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 비-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에는 선택한 게시에 대 한 구독을 받게 됩니다.  
  
## 옵션  
 **구독자**  
 해당 사용 하도록 설정 하려면 표에서 확인란을 선택 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 비-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에서 선택한 게시에 대 한 구독자는 **게시** 페이지입니다. 구독자가 나열되어 있지 않은 경우 **구독자 추가** 또는 **SQL Server 구독자 추가**를 클릭합니다.  
  
 **구독 데이터베이스**  
 정보에 표시 하 고이 열에서 사용할 수 있는 작업에 나열 된 구독자 유형에 따라 달라는 **구독자** 열:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자의 경우 **구독 데이터베이스** 목록에서 구독 데이터베이스를 선택하거나 동일한 목록에서 **새 데이터베이스** 명령을 선택하여 새 데이터베이스를 만듭니다.  
  
    > [!NOTE]  
    >  게시자를 구독자로 설정하는 경우 구독 데이터베이스가 게시 데이터베이스와 달라야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자의 경우 구독 데이터베이스가 표시되지 않습니다. 데이터베이스 및 기타 연결 정보를 지정 된 **데이터 원본 이름** 필드는 **비-SQL Server 추가** 대화 상자. 이 대화 상자를 클릭 하 여 사용할 수는 **구독자 추가** 클릭 한 다음 **비-SQL Server 구독자 추가**합니다.  
  
 **구독자 추가**  
 구독자로 설정할 수 있는 서버 목록에 서버를 추가합니다. 이 단추는 다음 조건이 모두 충족되는 경우 표시됩니다.  
  
-   선택한 게시가 구독 업데이트를 지원하지 않는 스냅숏 또는 트랜잭션 게시입니다.  
  
    > [!NOTE]  
    >  사용자가 구독하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독 및 게시가 있는 게시를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자가 사용할 수 없을 경우 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독을 추가할 수 없습니다.  
  
-   구독이 밀어넣기 구독입니다.  
  
-   선택한 게시의 게시자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전입니다.  
  
 클릭 하면 **구독자 추가** 선택할 수 있는 메뉴가 표시: **SQL Server 구독자 추가** 및 **비-SQL Server 구독자 추가**합니다. 클릭 **비-SQL Server 구독자 추가** Oracle 또는 IBM DB2 구독자를 추가 합니다.  
  
 **SQL Server 구독자 추가**  
 구독자로 설정할 수 있는 서버 목록에 서버를 추가합니다. 이 단추는 다음 조건 중 하나 이상이 충족되는 경우 표시됩니다.  
  
-   선택한 게시가 병합 게시이거나 구독 업데이트를 지원하는 스냅숏 또는 트랜잭션 게시입니다.  
  
-   구독이 끌어오기 구독입니다.  
  
-   선택한 게시의 게시자가 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]이전 버전입니다. 이전 버전의 경우 이 단추는 다음 조건 중 하나 이상이 충족되는 경우 표시됩니다.  
  
    -   사용자가 게시자에서 **sysadmin** 고정 서버 역할의 멤버입니다.  
  
    -   **게시자 속성** 대화 상자의 **구독자** 페이지에서 구독자가 추가되었습니다.  
  
    -   게시에서 익명 구독을 허용합니다.  
  
## 참고 항목  
 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)   
 [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)   
 [SQL Server 이외 구독자](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  