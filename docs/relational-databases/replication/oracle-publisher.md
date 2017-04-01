---
title: "Oracle 게시자 | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.selectoraclepublisher.f1"
ms.assetid: 019b7c49-dcca-445d-8969-5982a8ccbc1a
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Oracle 게시자
  부터는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅숏 및 트랜잭션 복제를 사용 하 여 Oracle 데이터베이스에서 데이터를 게시할 수 있습니다. 자세한 내용은 참조 [Oracle 게시 개요](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)합니다.  
  
 Oracle 게시자는 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자를 사용해야 합니다. 이 마법사는 필요한 Oracle 네트워킹 소프트웨어를 설치 및 테스트한 후 해당 서버에서 실행해야 합니다. 자세한 내용은 참조 [Oracle 게시자를 구성](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
> [!IMPORTANT]  
>  하는 경우 다른 관리자가 구성 된 Oracle 데이터베이스를 게시자로 클릭 한 후 **다음** Oracle 데이터베이스에 연결 하는 데 사용 하는 복제 로그인에 대 한 암호를 입력 하 라는 메시지가 표시 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle 데이터베이스에 연결 된 서버 연결과 사용자 로그인 간에 매핑을 만듭니다. 이후에 Oracle 데이터베이스에 연결할 때는 암호를 입력할 필요가 없습니다.  
  
## 옵션  
 **Oracle 게시자**  
 목록에서 Oracle 게시자를 선택합니다. 이 목록에는 마법사가 실행 중인 서버를 배포자로 사용하도록 이전에 구성된 Oracle 게시자가 포함되어 있습니다. 목록이 비어 또는 Oracle 게시자 하려는 경우 사용 하 여 목록에 없는, 클릭 **Oracle 게시자 추가**합니다.  
  
 **Oracle 게시자 추가**  
 시작 하려면 클릭은 **배포자 속성** 대화 상자입니다. 이 대화 상자에서 클릭 **추가**, 를 클릭 하 고 **Oracle 게시자 추가**합니다. 에 **서버에 연결** 대화 상자를 Oracle 서버 이름 및 로그인 및 복제 관리 사용자 스키마에 대 한 암호를 지정 합니다. 자세한 내용은 참조 [연결할 서버 & #40; Oracle & #41; 로그인](../../relational-databases/replication/connect-to-server-oracle-login.md)합니다.  
  
> [!NOTE]  
>  마법사가 실행 중인 서버가 배포자로 구성되어 있지 않으면 지금 배포자로 구성하라는 메시지가 표시됩니다.  
  
## 참고 항목  
 [Oracle 데이터베이스에서 게시 만들기](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)   
 [속성 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  