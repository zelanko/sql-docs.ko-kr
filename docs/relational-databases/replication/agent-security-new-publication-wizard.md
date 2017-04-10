---
title: "에이전트 보안(새 게시 마법사) | Microsoft Docs"
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
  - "sql13.rep.agentsecurity.articles.f1"
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 에이전트 보안(새 게시 마법사)
   **에이전트 보안** 페이지를 사용 하는 다음 에이전트 실행 하 고 복제 토폴로지의 컴퓨터에 대 한 연결을 확인 하는 계정을 지정할 수 있습니다.  
  
-   모든 게시에 대한 스냅숏 에이전트입니다.  
  
-   모든 트랜잭션 게시에 대한 로그 판독기 에이전트입니다.  
  
-   업데이트할 수 있는 구독을 허용하는 트랜잭션 게시에 대한 큐 판독기 에이전트입니다.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정한 경우이 에이전트에 대 한 에이전트 작업이 생성 됩니다 **업데이트할 수 있는 구독이 있는 트랜잭션 게시** 에 **게시 유형** 사용 하면 업데이트할 수 있는 구독 유형에 관계 없이 페이지입니다. 업데이트할 수 있는 구독에 대한 자세한 내용은 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)을 참조하십시오.  
  
 에이전트 및 복제 보안을 위한 모범 사례에 필요한 사용 권한에 대 한 정보를 참조 하십시오. [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md) 및 [복제 보안에 대 한 유용한 정보](../../relational-databases/replication/security/replication-security-best-practices.md)합니다.  
  
## 옵션  
 **스냅숏 에이전트**  
 모든 게시에 대해 표시됩니다. 클릭 **보안 설정을** 의 보안 설정을 지정 하는 **스냅숏 에이전트 보안** 대화 상자입니다.  
  
 클릭 **도움말** 에 **스냅숏 에이전트 보안** 스냅숏 에이전트에 의해 사용 되는 계정에 필요한 권한에 대 한 자세한 내용은 대화 상자입니다.  
  
 **로그 판독기 에이전트**  
 모든 트랜잭션 게시에 대해 표시됩니다. 클릭 **보안 설정을** 의 보안 설정을 지정 하는 **로그 판독기 에이전트 보안** 대화 상자입니다.  
  
 클릭 **도움말** 에 **로그 판독기 에이전트 보안** 로그 판독기 에이전트에서 사용 되는 계정에 필요한 권한에 대 한 자세한 내용은 대화 상자입니다.  
  
> [!NOTE]  
>  트랜잭션 복제를 사용하여 게시된 각 데이터베이스에 대해 하나의 로그 판독기 에이전트가 있습니다. 데이터베이스에 트랜잭션 게시가 이미 있으면 보안 설정은 읽기 전용입니다. 설정을 변경할 수는 **게시 속성** 변경 내용은 제외 하 고 대화 상자, 데이터베이스의 모든 트랜잭션 게시에 영향을 줍니다.  
  
 **큐 판독기 에이전트**  
 업데이트할 수 있는 구독을 허용하는 트랜잭션 게시에 대해 표시됩니다. 클릭 **보안 설정을** 의 보안 설정을 지정 하는 **큐 판독기 에이전트 보안** 대화 상자입니다. 이 마법사를 완료하면 큐 판독기 에이전트 작업이 생성됩니다. 지연 업데이트 구독의 생성 여부와는 관계가 없습니다. 지연 업데이트 구독을 만들지 않으려면 이 작업을 해제할 수 있습니다. 작업을 마우스 오른쪽 단추로 클릭 (이름의 형식은: *[\< 게시자>]. \< 정수>*.)에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 **작업** 폴더를 마우스 클릭 한 다음 **사용 하지 않도록**합니다.  
  
 클릭 **도움말** 에 **큐 판독기 에이전트 보안** 큐 판독기 에이전트에서 사용 되는 계정에 필요한 권한에 대 한 자세한 내용은 대화 상자입니다.  
  
> [!NOTE]  
>  각 배포 데이터베이스 및 이 데이터베이스에서 처리하는 모든 게시자에 대해 하나의 큐 판독기 에이전트가 있습니다. 지정된 배포 데이터베이스를 사용하는 게시자에 지연 업데이트 구독을 허용하는 트랜잭션 게시가 이미 있으면 보안 설정은 읽기 전용입니다. 큐 판독기 에이전트를 실행 및 연결할 계정을 변경할 수 있습니다는 **배포자 속성** 변경 내용은 제외 하 고 대화 상자에서 배포 데이터베이스를 사용 하는 모든 게시자에서 게시에 영향을 줍니다.  
  
## 관련 항목:  
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](https://msdn.microsoft.com/library/mt740635.aspx)   
 [게시자 및 배포자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [복제의 로그인 및 암호 관리](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  