---
title: "웹 동기화를 위한 토폴로지 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "웹 동기화, 토폴로지"
  - "IIS 서버 구성 [SQL Server 복제]"
ms.assetid: 59444faf-bcb6-4421-a3df-8715753e453b
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# 웹 동기화를 위한 토폴로지
  다양한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 웹 동기화 복제 토폴로지를 선택할 수 있습니다. 웹 동기화를 구성하는 일반적인 방법은 다음과 같습니다.  
  
-   단일 서버  
  
-   두 대의 서버  
  
-   여러 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS) 시스템 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 재게시  
  
 웹 동기화를 구성 하는 방법에 대 한 정보를 참조 하십시오. [웹 동기화 구성](../../relational-databases/replication/configure-web-synchronization.md)합니다.  
  
## 단일 서버  
 가장 간단한 토폴로지에서 IIS, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자는 모두 단일 서버에 상주합니다. 구독자는 게시자의 IIS에 연결하여 동기화합니다. 게시자는 방화벽 뒤에 있습니다.  
  
> [!NOTE]  
>  이 구성은 인트라넷 시나리오에만 사용하는 것이 좋습니다. 다른 시나리오에서는 IIS 서버와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자/배포자를 별도의 컴퓨터에 두는 것이 좋습니다.  
  
 ![단일 서버를 사용한 웹 동기화](../../relational-databases/replication/media/web-sync02.gif "단일 서버를 사용한 웹 동기화")  
  
## 두 대의 서버  
 한 서버에는 IIS를 두고 다른 서버에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자와 배포자를 구성할 수 있습니다. IIS를 실행하는 서버는 방화벽에 의해 인터넷에서 격리될 수 있습니다. 구독자는 IIS에 연결하여 동기화합니다.  
  
 ![2대의 서버를 사용한 웹 동기화](../../relational-databases/replication/media/web-sync03.gif "2대의 서버를 사용한 웹 동기화")  
  
## 여러 IIS 시스템 및 SQL Server 재게시  
 동시에 동기화하는 많은 수의 구독자를 지원해야 하는 경우 IIS를 실행하는 여러 개의 컴퓨터에 작업을 분할할 수 있습니다.  
  
 ![여러 대의 IIS 서버를 사용한 웹 동기화](../../relational-databases/replication/media/web-sync04.gif "여러 대의 IIS 서버를 사용한 웹 동기화")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터에서 로드 균형 조정이 필요한 경우 여러 컴퓨터에 재게시 계층을 만들 수 있습니다. 최상위 게시자에서 데이터를 구독자에 게시하면 구독자에서는 데이터를 다시 게시하고 최상위 게시자에서는 구독자의 로드 균형 조정 요청을 게시합니다.  
  
> [!NOTE]  
>  구독자는 특정 게시자하고만 동기화될 수 있습니다. 예를 들어 재게시자 A의 구독자는 A를 사용할 수 없는 경우 재게시자 B와도 동기화될 수 없습니다.  
  
 ![다시 게시를 사용한 웹 동기화](../../relational-databases/replication/media/web-sync05.gif "다시 게시를 사용한 웹 동기화")  
  
## 참고 항목  
 [웹 동기화 구성](../../relational-databases/replication/configure-web-synchronization.md)   
 [병합 복제에 대한 웹 동기화](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  